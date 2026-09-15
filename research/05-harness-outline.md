# Harness outline — structure, not code

How to lay out the code that plays the four-turn scripts, records what comes back, scores it, and
captures activations from open-weight models. **This is a structural sketch: files,
responsibilities, function signatures, and the decisions that are expensive to reverse.** No
implementations.

Reads: [`04-design-memo.md`](04-design-memo.md) for why the design is what it is,
[`fixtures/README.md`](fixtures/README.md) for the schema and the nine pre-flight checks.

---

## Six decisions to make before writing any code

**1. JSONL is the source of truth; CSV is a derived export.** Append-only JSONL survives crashes,
tolerates concurrent writers, holds nested data (token spans, per-turn records, judge payloads),
and distinguishes `null` from `""`. CSV does none of that. Write `records.jsonl`, generate
`results.csv` from it with a script anyone can re-run. **Never append to the CSV.**

**2. Generation and judging are separate passes over separate files.** The codebook will change
after week 5's double-coding, and re-judging must not mean re-generating — it is the difference
between an afternoon and a re-spend. `generate` writes `generations.jsonl`; `judge` reads it and
writes `judgments.jsonl`; `export` joins them.

**3. `record_id` is a deterministic hash, not a counter.** From
`(item_id, model_id, sample_index, prompt_version, run_config_hash)`. Resumability, idempotent
writes and duplicate detection all fall out of this for free, and a re-run with unchanged config
is a no-op rather than a second copy.

**4. Tensors never go in the tabular store.** Activations go to a separate array store keyed by
`record_id`; the JSONL holds a pointer. A single residual-stream capture is ~264 KB — three of
those exceed a whole CSV of text.

**5. The judge sees a whitelist, not a redaction.** Build the judge payload by *naming the fields
it may have*, never by stripping fields from a record. Memo §7 requires the judge to get the
proposition and never the rung; a whitelist fails closed when someone adds a column.

**6. Capture policy is declarative and versioned.** "Save everything" is terabytes. The policy
object says which layers, which positions, which precision — and it is hashed into
`run_config_hash` so two runs with different capture policies never collide.

---

## Layout

```
harness/
  config.py          settings, model registry, capture policy
  schema.py          typed records — the contract between every other module
  stimuli.py         load and validate stimuli.csv
  backends/
    base.py          the Backend protocol both implementations satisfy
    openrouter.py    API models — text only
    local_hf.py      open weights — text plus activations
  conversation.py    the fixed four-turn script runner
  capture.py         what to record from an open-weight forward pass
  store.py           JSONL append, array store, manifest
  judge.py           judge calls, parsing, repair, validation
  runner.py          orchestration: concurrency, retries, resume, spend
  validate.py        invariants that must hold or the run is void
  export.py          results.csv, blinded coder export, analysis long-format
  cli.py             generate / judge / export / validate / estimate
tests/
scripts/
```

---

## `config.py`

Everything that must appear in the Method section lives here, and nothing else.

```python
@dataclass(frozen=True)
class ModelSpec:
    model_id: str            # exact snapshot, e.g. "openai/gpt-4o-mini-2024-07-18"
    backend: Literal["openrouter", "local_hf"]
    revision: str | None     # HF commit SHA — "main" is not a version
    max_tokens: int
    temperature: float       # > 0, see memo §6; at 0, k=5 buys nothing
    accessed: date

@dataclass(frozen=True)
class CapturePolicy:
    layers: Literal["all"] | list[int]
    positions: list[PositionSpec]      # see capture.py
    dtype: Literal["float16", "float32"]
    top_k_logits: int                  # 0 disables
    full_logits_at: list[PositionSpec] # expensive — usually just first generated token
    attention: AttentionPolicy | None  # usually None; see the sizing table

@dataclass(frozen=True)
class RunConfig:
    models: list[ModelSpec]
    k_samples: int
    seed_base: int
    system_prompt_id: str | None       # None is a choice; record it either way
    prompt_version: str
    capture: CapturePolicy | None
    spend_cap_usd: float

def run_config_hash(cfg: RunConfig) -> str: ...
def load_config(path: Path) -> RunConfig: ...
```

`system_prompt_id` being `None` must be *recorded*, not merely absent. psychosis-bench sends no
system prompt at all (`_prepare_request` builds `{model, messages}` and nothing else), and if you
match that you should be able to prove it later.

---

## `schema.py`

One place where the record shape is defined. Everything else imports from here.

```python
@dataclass
class Item:                       # one row of stimuli.csv
    item_id: str
    proposition_id: str
    rung: str | None              # label only
    rung_index: int | None        # 1-4 — THE analysis variable
    condition: str                # base | ungrounded_neutral | grounded_distress
    domain: str
    proposition: str
    turns: list[str]              # exactly 4

@dataclass
class TurnRecord:
    turn_index: int               # 1-4
    user_text: str
    assistant_text: str | None
    finish_reason: str | None
    prompt_tokens: int
    completion_tokens: int
    token_spans: dict[str, tuple[int, int]] | None   # see capture.py — load-bearing
    activation_ref: str | None    # key into the array store
    latency_ms: int
    error: str | None

@dataclass
class GenerationRecord:
    record_id: str
    item_id: str; proposition_id: str; rung_index: int | None; condition: str
    model_id: str; sample_index: int; seed: int
    temperature: float; system_prompt_id: str | None
    prompt_version: str; run_config_hash: str
    turns: list[TurnRecord]
    started_at: datetime; completed_at: datetime
    cost_usd: float | None

@dataclass
class Judgment:
    record_id: str; turn_index: int
    judge_model: str; judge_prompt_version: str; judge_pass: Literal["epistemic","affective"]
    scores: dict[str, int | None]
    response_class: Literal["answered","refusal_policy","inability","empty","error"]
    raw_judge_output: str
    parse_status: Literal["ok","repaired","failed"]
```

**`response_class` is one field with five values, not a boolean.** `refusal_policy` and
`inability` must be distinguishable — *"I won't"* and *"I can't tell from this"* are different
behaviours, and inability replies will be commoner at the implied end, so merging them
manufactures a rung effect. `empty` covers a null or whitespace completion, which is neither.

---

## `stimuli.py`

```python
def load_stimuli(path: Path) -> list[Item]: ...
def validate_stimuli(items: list[Item]) -> list[Violation]: ...
```

`validate_stimuli` runs the checks the study depends on, and **refuses to proceed rather than
warning**:

- Every proposition has exactly four rungs plus its control arms.
- **Turns 1–3 are byte-identical across all rows sharing a `proposition_id`.** The central
  invariant of the design.
- **No preamble turn contains a presupposition token** — bare anaphora (`those`, `they`, `that`),
  acknowledgements (`thanks`, `that's helpful`, `great`), answer tokens (`yeah`, `no`). This is a
  grep, and it caught twelve rows in the fixtures' first version.
- `rung_index` populated for every `condition == "base"` row.
- Turn-4 length matched within ±3 words across a proposition's four rungs.
- No row carries hypothesis vocabulary in any loader-visible column.

---

## `backends/`

```python
class Backend(Protocol):
    def generate(self, messages: list[Message], spec: ModelSpec, seed: int,
                 capture: CapturePolicy | None) -> Completion: ...
    def supports_capture(self) -> bool: ...
    def estimate_cost(self, prompt_tokens: int, completion_tokens: int) -> float | None: ...
```

**`openrouter.py`** — `supports_capture() -> False`. Handles auth, retry with exponential backoff
and jitter, distinguishes *retryable* (429, 5xx, timeout) from *fatal* (401, 400, content filter),
and surfaces `finish_reason` rather than swallowing it. Sends `temperature` and `seed` explicitly;
the inherited psychosis-bench client sends neither, which is why its published numbers are single
draws at provider defaults.

**`local_hf.py`** — `supports_capture() -> True`. Loads with a pinned `revision`, applies
`tokenizer.apply_chat_template`, runs generation with hooks registered per `CapturePolicy`.

```python
def load_model(spec: ModelSpec) -> tuple[Model, Tokenizer]: ...
def build_prompt(messages, tokenizer) -> tuple[str, dict[str, tuple[int,int]]]:
    """Returns the templated string AND the turn -> token-span map."""
```

**`build_prompt` returning token spans is the most important function in the file.** Without a map
from turn index to token positions, every activation you store is unusable — you cannot say which
tensor corresponds to "the last token of the turn-4 cue." Spans are model-specific because
tokenizers differ, so they are stored per record, not computed once.

Record the **chat template hash** too. A template change alters tokenization and therefore every
stored position.

---

## `capture.py`

```python
@dataclass(frozen=True)
class PositionSpec:
    anchor: Literal["last_prompt_token", "turn_end", "first_generated",
                    "all_generated", "generated_stride"]
    turn_index: int | None = None
    stride: int | None = None

def resolve_positions(spec: PositionSpec, spans, generated_len) -> list[int]: ...
def register_hooks(model, policy) -> HookHandles: ...
def collect(model_out, policy, spans) -> CaptureBundle: ...
```

**What to capture, in priority order:**

| | What | Why | Size per position (8B model, fp16) |
|---|---|---|---|
| **Always** | Sampled-token logprobs | Free, and it is the sequence likelihood | ~2 KB / response |
| **Always** | Top-k logits + ids, k≈20, every generated token | Cheap; supports most analyses | ~36 KB / response |
| **Always** | `token_spans`, chat-template hash, tokenizer revision | Without these nothing else is usable | negligible |
| **Default** | Residual stream (`hidden_states`), all layers, at `last_prompt_token` of turn 4 and `first_generated` | The two positions where the cue is read and the response is decided | **~264 KB** |
| **On request** | Full logits at `first_generated` | Logit-lens and distributional work | ~250 KB |
| **On request** | Residual at `generated_stride(8)` over turn 4 | Trajectory through the response | 264 KB × n/8 |
| **Rarely** | MLP activations (`d_ff` = 14336) | Only with a specific hypothesis | ~917 KB |
| **Almost never** | Attention patterns, all layers/heads | Quadratic in sequence length | **~2 GB at seq 1000** |

**Store residuals; compute logit lens later.** A logit lens projection is
`unembed(layernorm(residual))` — derived, reproducible, and storing it wastes space and freezes a
choice you may want to revisit.

**Sizing, so the policy is a decision and not an accident** (54 items × 5 samples × 3 open models
= 810 conversations, 3,240 turns):

| Policy | Total |
|---|---|
| Logprobs + top-k only | ~120 MB |
| **Default** (2 positions × all layers) | **~1.7 GB** |
| Turn-4 stride-8 residuals | ~25 GB |
| All generated positions, all layers | ~290 GB |
| Attention on top of any of the above | **don't** |

**Library choice.** Raw `transformers` hooks are the most portable and the least magical.
`TransformerLens` is the mech-interp standard and gives clean `resid_pre`/`resid_post` naming, but
supports a limited architecture set and **renames modules**, which matters for reproducibility —
if you use it, record that you did, because layer indices are not interchangeable with raw HF.
`nnsight` sits between. Pick one in week 1 and do not mix.

**Determinism.** Seed `torch`, `numpy`, `random` and the generation call. Note in the Method that
exact bitwise reproduction additionally needs `torch.use_deterministic_algorithms(True)` and a
fixed CUDA matmul precision, and that this costs throughput. Decide and record which you did.

> **The design consequence nobody will raise until week 6:** every model psychosis-bench tested is
> API-only, so **the interpretability arm and the behavioural arm are different model sets.** You
> cannot claim an activation-level mechanism *for* the models whose behaviour you report. Decide in
> week 1 whether open-weight models join the main run as additional behavioural subjects — which
> makes the mech-interp claims about the same systems — or whether interp is a separate case study
> on models the headline never mentions.

---

## `store.py`

```python
class JsonlStore:
    def append(self, record) -> None: ...
    def read_ids(self) -> set[str]: ...            # for resume
    def iter_records(self) -> Iterator[dict]: ...

class ArrayStore:
    """safetensors shards keyed by record_id. One file per shard, not per record —
    3,240 tiny files is a filesystem problem."""
    def put(self, record_id: str, bundle: CaptureBundle) -> str: ...
    def get(self, ref: str) -> CaptureBundle: ...
    def manifest(self) -> pd.DataFrame: ...        # ref -> shapes, dtypes, bytes

def write_manifest(run_dir: Path, cfg: RunConfig) -> None:
    """config, git SHA, package versions, GPU, start time, spend. The Method section
    is generated from this, not written from memory."""
```

`safetensors` over pickle (no arbitrary code on load) and over HDF5 (fewer install problems,
better mmap). Shard at ~1 GB.

---

## `judge.py`

```python
def build_judge_payload(rec: GenerationRecord, turn_index: int,
                        pass_name: Literal["epistemic","affective"]) -> dict:
    """WHITELIST. Returns exactly: the conversation up to and including the turn,
    and — epistemic pass only — the proposition. Never rung, rung_index, condition,
    proposition_id, domain, or any notes field."""

def score_turn(payload, judge_spec, prompt_version) -> Judgment: ...
def parse_judge_output(raw: str) -> tuple[dict | None, ParseStatus]: ...
def classify_response(assistant_text, finish_reason) -> ResponseClass: ...
```

**Two passes, separate calls.** One invocation emitting all five checks correlates its errors
across them by construction — a judge that reads a reply as warm marks both "acknowledged
distress" and "validated the belief." RQ3 cross-tabulates exactly those two axes, so a single call
would measure the judge's halo rather than the model's behaviour.

**`parse_judge_output` must handle, without crashing:** markdown-fenced JSON, prose instead of
JSON, trailing commas, missing keys, out-of-range values, two concatenated objects, nulls. All
twelve cases are in `fixtures/harness-dev-responses.jsonl`. Return `ParseStatus` rather than
raising — a failed parse is data, and the failure rate per model is worth reporting.

**Judge pinning.** The paper used `openai/gpt-4o-mini`; the released psychosis-bench code defaults
to `openai/o4-mini`, which is also one of the eight *tested* models. Set it explicitly.

---

## `runner.py`

```python
def run_generation(cfg: RunConfig, items: list[Item], store, resume: bool = True) -> RunSummary: ...
def run_judging(cfg, generations_path, store) -> RunSummary: ...

def plan(cfg, items) -> list[WorkUnit]:
    """Cartesian product of items x models x k, minus record_ids already present."""

def execute(units, backend, concurrency: int) -> Iterator[GenerationRecord]:
    """Conversations are the unit of concurrency. The four turns WITHIN a
    conversation are strictly sequential — that is the whole point."""

class SpendGuard:
    def check(self, projected_usd: float) -> None:
        """Raises before the call that would cross the cap, not after."""
```

**API models and local models want opposite concurrency.** OpenRouter wants many conversations in
flight; a local GPU wants batch size 1 and sequential execution. Make concurrency per-backend, not
global.

**Resume works by set difference on `record_id`.** A conversation is written once, complete, at
the end — never partially. A half-written conversation on crash is discarded and redone, which is
correct: a conversation missing turn 3 is not repairable.

---

## `validate.py`

Run after generation, before analysis. **Each returns a hard failure, not a warning.**

```python
def check_preamble_identity(records) -> Result:
    """Turns 1-3 byte-identical across all rungs of a proposition IN THE LOGS.
    Validating the stimuli file is not enough — this catches the harness sending
    something different from what the file says."""

def check_context_accumulation(records) -> Result:
    """E-DEV-08 returned ORCHARD-7 and Thursday; E-DEV-09 returned MERIDIAN-3 and
    Tuesday when run concurrently. If either fails, the run is void."""

def check_canary_not_leaked(judge_prompts) -> Result:
    """No logged judge prompt contains DO-NOT-SEND. A hit means condition labels
    are reaching the judge."""

def check_no_duplicates(records) -> Result: ...
def check_completeness(records, expected) -> Result: ...
def check_refusal_split(judgments) -> Result:
    """refusal_policy and inability both non-empty. If inability is zero, they have
    been merged."""
def check_token_spans(records) -> Result:
    """Every activation_ref has spans, and spans are within sequence length."""
```

---

## `export.py`

```python
def to_results_csv(generations, judgments, out: Path) -> None:
    """One row per (record_id, turn_index). The team-facing artifact."""

def to_analysis_long(...) -> None:
    """One row per (record_id, turn_index, check). rung_index as an ordered
    categorical with categories= set explicitly — sorting the rung LABEL gives
    explicit, hedged, implied, metaphorical, which swaps rungs 3 and 4."""

def to_coder_export(records, sample_spec, out: Path) -> None:
    """Blinded export for the three human coders: response text, proposition,
    shuffled order. No rung, no rung_index, no condition, no model_id.
    Stratified by rung x response_class x judge label."""

def spend_report(run_dir) -> pd.DataFrame: ...
```

---

## `cli.py`

```
harness estimate --config run.yaml       # tokens and $ before spending anything
harness generate --config run.yaml [--resume] [--dry-run] [--fixtures]
harness judge    --config run.yaml --generations runs/2026-10-05/generations.jsonl
harness validate --run runs/2026-10-05
harness export   --run runs/2026-10-05
```

`--fixtures` points the whole pipeline at `fixtures/harness-dev-fixtures.csv`, and
`--replay fixtures/harness-dev-responses.jsonl` substitutes canned responses for the API so the
malformed-output paths execute without spending anything.

---

## Build order

1. `schema.py`, `config.py`, `stimuli.py` — then run `validate_stimuli` against the fixtures.
2. `store.py` + `openrouter.py` + `conversation.py`. Run the 30 fixtures. **Stop and confirm
   E-DEV-08 and E-DEV-09.** Nothing downstream is worth building until context accumulation is
   proven.
3. `judge.py`, developed entirely against `harness-dev-responses.jsonl`. No API spend.
4. `validate.py` and `export.py`. Now the whole pipeline runs end to end on fixtures.
5. **Only now** `local_hf.py` and `capture.py`. The interp path is the one place where a wrong
   decision costs a re-run of everything, and by this point the record shape is settled.

Steps 1–4 are the week-1/2 harness tasks in the schedule. Step 5 is not budgeted there — **if the
interpretability arm is going ahead, it needs its own hours and its own GPU access, and that is a
week-1 procurement question, not a week-5 discovery.**

---

## What this outline does not cover

- **Steering, patching and ablation.** A different execution mode — intervening during the
  forward pass rather than observing it. If that is the goal, `capture.py` grows an
  `intervene.py` sibling and the run config grows an intervention spec. Out of scope here.
- **Probe training.** Downstream of the array store, and properly an analysis concern.
- **Teacher-forced scoring.** Scoring a fixed continuation rather than a sampled one is often
  what you want for interp. It is a separate `Backend` method, not a flag on `generate`.
