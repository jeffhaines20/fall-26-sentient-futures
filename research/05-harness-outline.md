# Harness outline — structure, not code

How to lay out the code that plays the four-turn scripts, records what comes back, scores it, and
(optionally) captures activations from open-weight models. **This is a structural sketch: files,
responsibilities, function signatures, and the decisions that are expensive to reverse.** No
implementations.

Reads: [`04-design-memo.md`](04-design-memo.md) for why the design is what it is,
[`fixtures/README.md`](fixtures/README.md) for the schema and the pre-flight checks.

> **Version 2.** Version 1 was adversarially reviewed by two critics and did not survive intact.
> Summary of what changed is at the end, under *What review changed*. The single most important
> correction: **v1's `schema.py` encoded the study's mechanics and omitted four of the variables its
> inferences depend on** — the named primary outcome, the inherited-rubric scoring pass, the two
> rated covariates, and the control-to-base pairing. Each would have surfaced in weeks 4–6 as
> "we need one more column," after the run was paid for.

---

## Seven decisions to make before writing any code

**1. JSONL is the source of truth; CSV is a derived export.** Append-only JSONL survives crashes,
tolerates concurrent writers, holds nested data (token spans, per-turn records, judge payloads),
and distinguishes `null` from `""`. CSV does none of that. `generate` writes `generations.jsonl`,
`judge` writes `judgments.jsonl`, `export` produces `results.csv`. **Never append to the CSV.**

**2. Generation and judging are separate passes over separate files.** The codebook will change
after week 5's double-coding, and re-judging must not mean re-generating.

> **But instrument it.** Week 5 contains both the codebook revision *and* 5.3, the first fit of
> the primary model. A cheap re-judge in the week the primary result first becomes visible is the
> textbook shape of analytic flexibility. The harness's job is to make it *visible*, not to
> prevent it: `export` must emit the list of every `judge_prompt_version` ever run against a
> dataset, which is also the raw material for schedule 7.3's deviation table.

**3. `record_id` is a deterministic hash — over the fields that define one generation, and only
those.** From `(item_id, model_id, sample_index, prompt_version, system_prompt_id, n_turns,
cue_turn_index, temperature, max_tokens, model_revision)`.

**Explicitly NOT in the hash: `models`, `k_samples`, `spend_cap_usd`, `capture`.** Hashing the
whole `RunConfig` — the obvious implementation — couples resume to things that must be changeable
mid-run. The schedule plans two cuts that mutate the config (*six models instead of eight*, *k = 5
→ 3*), and `SpendGuard` raising at the cap invites raising the cap. Under a whole-config hash,
each of those changes `record_id` for every record, `plan()`'s set difference matches nothing, and
`--resume` regenerates the entire study. **The cut designed to save spend would trigger a full
re-spend, and hitting the cap would destroy the ability to resume.** Record the full config in the
manifest; hash only what defines a generation.

**4. Tensors never go in the tabular store.** Activations go to a separate array store; the JSONL
holds a pointer. At the default capture policy the run's activations are **~420 MB against a
~12 MB `results.csv`** — a 35× ratio, and the two have completely different access patterns.

**5. The judge sees a whitelist, not a redaction.** Build the judge payload by *naming the fields
it may have*, never by stripping fields from a record. A whitelist fails closed when someone adds
a column.

> **What the whitelist does not buy you, and v1 claimed it did.** The whitelist cannot blind the
> judge to rung, because **the rung *is* turn 4** and the judge must see the scored turn. Memo §7
> says so directly: *"at rungs 3–4 the gap between the proposition and the utterance is the
> manipulation, so handing it both may let it read the rung off the gap."* The memo's mitigation is
> not structural — it is *"verify via per-rung agreement that it is not inferring the
> manipulation."* The whitelist stops *metadata* leaking. Blinding evidence comes from the rung ×
> agreement interaction, and it has to be measured.

**6. Capture policy is declarative and versioned.** "Save everything" is terabytes. The policy
object says which layers, which positions, which precision. It is recorded in the manifest and
keyed into the array-store ref — **not** into `record_id` (see decision 3: adding capture in week 5
must not invalidate API-model records, which have no activations at all).

**7. Decide the preamble policy before week 4, because it determines the `Backend` signature.**
Fixtures README check 9: at temperature > 0 the model's *assistant* replies in turns 1–3 differ
across rungs by chance, so "identical context" is true of the **user** turns only. Memo §6 justifies
the whole preamble structure with *"identical context before it, so the only difference between
rungs is the thing being studied"* — which is false of the assistant half. It is noise, not bias,
so it inflates variance rather than manufacturing an effect, but it makes the memo's cleanest
sentence literally untrue and week-7's external reviewers will read that sentence.

`preamble_policy: Literal["freeze", "vary"]` in `RunConfig`. **`"freeze"` is teacher-forcing and
is not buildable from this outline** — `Backend.generate` always generates. If you want that
branch, the `Backend` protocol needs a second method *before* the record shape is frozen, not
after.

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
    local_hf.py      open weights — text plus activations   [unbudgeted, see below]
  conversation.py    the fixed n-turn script runner
  capture.py         what to record from an open-weight forward pass  [unbudgeted]
  store.py           JSONL append, array store, manifest
  judge.py           judge calls, parsing, repair, validation
  runner.py          orchestration: concurrency, retries, resume, spend
  validate_dev.py    fixture-bound checks — run at build step 2
  validate_run.py    real-run invariants — run before analysis
  export.py          results.csv, blinded coder export, analysis long-format
  cli.py             estimate / generate / judge / validate / export
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
    provider_order: list[str] | None   # OpenRouter routes one id to several providers
    allow_fallbacks: bool              # False, or you cannot say which weights served you
    max_tokens: int
    temperature: float       # > 0, see memo §6; at 0, k=5 buys nothing
    price_in: float; price_out: float  # per-model, per-token — see estimate_cost
    accessed: date

@dataclass(frozen=True)
class RunConfig:
    models: list[ModelSpec]
    judge: ModelSpec                   # pinned. Not optional
    judge_prompt_version: str
    judge_turns: list[int]             # which turns get scored — see judge.py
    primary_outcome_key: str           # names the ONE outcome. See below
    k_samples: int
    seed_base: int                     # seed = seed_base + sample_index. State the rule
    system_prompt_id: str | None       # None is a choice; record it either way
    prompt_version: str
    n_turns: int                       # NOT hard-coded 4 — see below
    cue_turn_index: int
    preamble_policy: Literal["freeze", "vary"]
    capture: CapturePolicy | None
    spend_cap_usd: float
    prereg_ref: str | None             # timestamp + hash of the locked preregistration
```

**`primary_outcome_key` exists because the memo names one and the harness otherwise cannot.**
Memo §1 makes **elicited introduction** primary and spends a whole section arguing why, not
endorsement; memo §8 and schedule 3.5 both say *"name one primary outcome."* If the primary
outcome is only an unnamed string key in a `scores` dict whose meaning lives in a judge prompt,
then **G4 has no referent** — G4 passes if *"explicit-rung primary-outcome rate is between 0.15
and 0.85"*, and the harness cannot compute a quantity it does not name. Put the key in the config,
hash it into `record_id`'s `prompt_version` lineage, and give `export` one function that emits
that rate per rung. That function *is* G4's number.

**`n_turns` is configurable because G4's own fail branch changes it.** G4 fails → *"extend to
6 turns (two constant-rung pressing turns after the cue) and re-run that week."* Memo §6's stretch
goal is the same two turns. Both are documented as same-week repairs; with `4` hard-coded into
`schema.py` — "the contract between every other module" — neither is. Changing the turn count also
moves token spans and the capture policy's `turn_index`.

**`prereg_ref` is the binding.** Week 3 locks the preregistration; week 4 runs. Nothing in v1
stopped `harness generate` pointing at the real `stimuli.csv` in week 2. Rule: **`generate`
refuses non-fixture stimuli when `prereg_ref` is `None`.** That is the team's one hard constraint,
enforced in one place.

`system_prompt_id` being `None` must be *recorded*, not merely absent — psychosis-bench sends no
system prompt at all (see *Inherited-code facts* below), and if you match that, you should be able
to prove it later.

---

## `schema.py`

One place where the record shape is defined. Everything else imports from here.

```python
@dataclass
class Item:                       # one row of stimuli.csv
    item_id: str
    proposition_id: str           # the pairing unit; the random-effect grouping factor
    rung: str | None              # label only — never sort on this
    rung_index: int | None        # 1-4 — THE analysis variable
    matched_rung_index: int | None  # which base rung a control arm pairs against
    condition: str                # base | ungrounded_neutral | grounded_distress
    domain: str
    proposition: str
    rated_directness: float | None          # from the G2 blind rater pass
    rated_distress_intensity: float | None  # from the same pass
    do_not_send_canary: str
    turns: list[str]              # len == cfg.n_turns, validated not commented
```

Four of these fields were missing in v1, and each one silently removes an analysis the memo
mandates:

| Field | What its absence costs |
|---|---|
| `matched_rung_index` | **RQ2 cannot be joined.** Memo §5 makes the ungrounded-neutral arm *"RQ2's actual contrast"* and a *paired* one — control vs. the same proposition's base item at a specific rung. In the fixtures, control rows have empty `rung` and `rung_index` (verified). Without this field the harness records *that* a row is a control but not *what it controls for* |
| `rated_directness` | Memo §8: regressing on *rated* directness rather than rung membership is *"the best available defence against the reviewer question 'did you find a boundary, or do your items just vary in difficulty?'"* Schedule 6.2 budgets it |
| `rated_distress_intensity` | Memo §5: rung 4 is *defined* as maximal distress, so distress is correlated with rung across the whole base set — *"the very thing RQ2 exists to separate."* The memo requires reporting the ladder effect **with and without** it. This is the study's one acknowledged unremovable confound, and v1 left it unmeasured |
| `do_not_send_canary` | The leak detector the fixtures require. v1 never loaded it, so the check that greps for it could not fail |

```python
@dataclass
class TurnRecord:
    turn_index: int
    user_text: str
    assistant_text: str | None
    finish_reason: str | None
    prompt_tokens: int; completion_tokens: int
    token_spans: dict[str, tuple[int, int]] | None   # see capture.py
    activation_ref: str | None
    latency_ms: int
    error: str | None

@dataclass
class GenerationRecord:
    record_id: str
    item_id: str; proposition_id: str; rung_index: int | None
    matched_rung_index: int | None; condition: str; domain: str
    model_id: str; provider: str | None; sample_index: int; seed: int
    temperature: float; system_prompt_id: str | None
    prompt_version: str; preamble_policy: str
    turns: list[TurnRecord]
    complete: bool                # see runner.py — resume keys on this
    started_at: datetime; completed_at: datetime
    cost_usd: float | None

@dataclass
class Judgment:
    judgment_id: str              # REQUIRED — see below
    record_id: str; turn_index: int
    judge_model: str; judge_prompt_version: str
    judge_pass: Literal["epistemic", "affective", "dcs_inherited"]
    rubric_version: str
    judge_replicate_index: int    # memo §7 runs the judge three times
    scores: dict[str, int | None]
    response_class: Literal["answered","refusal_policy","inability","empty","error"]
    raw_judge_prompt: str         # REQUIRED — the canary check has nothing to read without it
    raw_judge_output: str
    parse_status: Literal["ok","repaired","failed"]
```

**`judgment_id = hash(record_id, turn_index, judge_pass, judge_model, judge_prompt_version,
judge_replicate_index)`.** Without it, three things break at once, all of them in the pass that
decision 2 exists to protect:

- **Memo §7's judge self-consistency — *"run it three times on the same responses and report its
  agreement with itself"* (schedule 6.4) — produces three rows identical on every field.** They
  cannot be told apart, and decision 3's dedup logic treats replicates 2 and 3 as duplicate writes.
- **Judging cannot resume.** `JsonlStore.read_ids()` has nothing to read; a crash partway through
  ~17,280 judge calls leaves re-spend or duplicates with no way to tell which.
- **The export join fans out.** There are always ≥2 judgments per turn (epistemic and affective),
  so a join on `(record_id, turn_index)` doubles N — and with self-consistency, sextuples it —
  without erroring. `to_results_csv` must be a **pivot on `judge_pass`**, not a join.

**`judge_pass` has three members, because the positive control needs the third.** Memo §9 makes
the control two steps, and step 2 — *"your own explicit-rung items, scored with the inherited
rubric, must land near the published band"* — is the one the memo calls **"the one that can fail
informatively."** Schedule 4.1 names it explicitly: *"score your own explicit-rung items with
psychosis-bench's inherited DCS rubric."* `02`'s do-not-cut list names it too. The inherited rubric
is DCS/HES/SIS; **v1's `judge_pass` was a two-member Literal with no DCS pass and no
`rubric_version`, so the positive control had nowhere to run.** If the ladder comes back flat — a
live outcome the memo pre-commits to — the team could not have distinguished *"implicitness doesn't
matter"* from *"our stimuli are weaker than theirs."* The generations are the same; only the
scoring pass differs.

**`response_class` is one field with five values, not a boolean.** `refusal_policy` and `inability`
must be distinguishable — *"I won't"* and *"I can't tell from this"* are different behaviours, and
inability replies will be commoner at the implied end, so merging them manufactures a rung effect.

**But it must be a judge output, not a keyword function.** v1 specified
`classify_response(assistant_text, finish_reason)` — a deterministic function of text. Distinguishing
*"I won't"* from *"I can't tell"* is a semantic judgement no keyword classifier makes reliably, and
memo §8 makes refusal rate a **reported result** (*"report refusal rate per rung as a result in its
own right"*). A biased classifier then produces exactly the ladder pattern the study is testing for
— and because the classifier also stratifies the human-coder sample, the reliability draw
under-represents the cells where it is wrong. Circular. Keep `classify_response` for `empty` and
`error` only, which is all `finish_reason` can honestly support; get the rest from the judge, and
put it on the human coding sheet so it earns an agreement statistic like every other reported
measure.

---

## `stimuli.py`

```python
def load_stimuli(path: Path, cfg: RunConfig) -> list[Item]: ...
def validate_stimuli(items, cfg) -> list[Violation]: ...
```

**Hard failures** (refuse to proceed):

- Every proposition has exactly four rungs plus its control arms.
- **Turns 1–`cue_turn_index - 1` byte-identical across all rows sharing a `proposition_id`,
  controls included.** The central invariant of the design. (Fixtures README rule 3 says
  *"all rungs **and controls**"*; v1's wording said "all rungs", which let a control preamble drift.)
- `len(turns) == cfg.n_turns`.
- `rung_index` populated for every `condition == "base"` row; `matched_rung_index` populated for
  every row where `condition != "base"`.
- `rated_directness` and `rated_distress_intensity` populated before the main run. They come from
  week 1's G2 pass, so this is enforceable.
- Turn-4 length matched within ±3 words across a proposition's four rungs.
- No hypothesis vocabulary in any loader-visible column.

**Warning, not a hard failure — and this is a correction:** the presupposition check. v1 specified
it as a token grep for bare anaphora (`those`, `they`, `that`), acknowledgements (`thanks`,
`great`), and answer tokens (`yeah`, `no`), as a hard refusal, and told you to run it against the
fixtures on day one of the build order. **Run literally, it flags 9 of the 30 shipped fixtures** —
all six `P-DEV-03` rows on *"six flats, no concierge"*, plus `E-DEV-01`, `E-DEV-05`, and
**`E-DEV-08`, the context-accumulation canary**, on ordinary relative-pronoun *"that"*. Day one
would have ended in a hard refusal on the file it was told to validate, and the obvious fix —
delete the offending rows — deletes the canary, after which `check_context_accumulation` can never
run.

The rule that was actually applied to fixtures v2 is narrower: **bare anaphora and answer tokens
in *response position*** (*"a couple of those"*, *"They were fine"*, *"Yeah —"*), not any occurrence
of the substring. State it as a positional rule — sentence-initial answer token; anaphor with no
in-turn antecedent — and make the token grep a warning a human clears.

---

## `backends/`

```python
class Backend(Protocol):
    def generate(self, messages, spec: ModelSpec, seed: int,
                 capture: CapturePolicy | None) -> Completion: ...
    def supports_capture(self) -> bool: ...
    def estimate_cost(self, spec: ModelSpec, prompt_tokens: int,
                      completion_tokens: int) -> float | None: ...
```

**`estimate_cost` takes the `spec`.** OpenRouter prices per model and one client serves 6–8 of
them; without it you can only return a blended rate, and both `harness estimate` and the spend cap
are computed at the wrong price — in a study whose schedule warns the token spend is *"roughly
8–10×"* a single-turn design. Project at `spec.max_tokens`, not at an expected completion length:
completion tokens are not knowable before the call, and an expected-length projection
under-projects systematically, which is how caps get crossed.

**`openrouter.py`** — `supports_capture() -> False`. Auth, retry with exponential backoff and
jitter, *retryable* (429, 5xx, timeout) vs *fatal* (401, 400, content filter), and surfaces
`finish_reason` rather than swallowing it. Sends `temperature` and `seed` explicitly, and pins
`provider_order` / `allow_fallbacks=False` so the manifest can answer "which weights served this?"

**On seeds, state the truth in the Method rather than the aspiration.** `seed = seed_base +
sample_index` — say the rule, because if `seed` is constant across `k`, any provider that honours
it collapses the five draws toward identical strings and destroys the very variance the k samples
exist to supply. And: OpenAI documents `seed` as *best-effort*, the Anthropic Messages API has no
`seed` parameter at all, and OpenRouter forwards it only to providers that support it. **Seeded
reproducibility will be available for part of the model set and not the rest**, and the Method
cannot claim it uniformly.

> Related, and it belongs in `fixtures/README.md` rather than here: the pre-flight check *"run one
> fixture at k=5 at temperature 0 — must give 5 identical strings; if not, your temperature isn't
> being sent"* will report false failures on correct code. Temperature 0 does not guarantee
> identical API outputs (batching non-determinism, MoE routing). Scope that check to the local
> backend, or relax it to ≥4 of 5.

**`local_hf.py`** — `supports_capture() -> True`. Pinned `revision`, `apply_chat_template`,
generation with hooks registered per `CapturePolicy`.

```python
def load_model(spec: ModelSpec) -> tuple[Model, Tokenizer]: ...
def build_prompt(messages, tokenizer) -> tuple[str, dict[str, tuple[int,int]]]:
    """Returns the templated string AND the turn -> token-span map."""
```

**Without a map from turn index to token positions, every activation you store is unusable** — you
cannot say which tensor corresponds to the last token of the cue. Spans are model-specific because
tokenizers differ, so they are stored per record.

Two traps that silently corrupt every capture:

- **Double BOS.** `apply_chat_template(..., tokenize=False)` returns a string that already contains
  `<|begin_of_text|>`. Re-tokenizing it with the default `add_special_tokens=True` prepends a
  *second* BOS and shifts every span by one. Use `add_special_tokens=False` and assert the ids
  match `apply_chat_template(..., tokenize=True)`. An off-by-one here is invisible in the logs and
  passes a "spans within sequence length" check.
- **`return_offsets_mapping` is fast-tokenizer only** — slow tokenizers raise. Pin fast tokenizers
  explicitly; it is not safe as a blanket assumption across three open models.

Record the **chat-template hash** and tokenizer revision. A template change alters tokenization and
therefore every stored position.

---

## `capture.py`

```python
@dataclass(frozen=True)
class PositionSpec:
    anchor: Literal["turn_end", "last_prompt_token", "first_generated",
                    "all_generated", "generated_stride"]
    turn_index: int | None = None
    stride: int | None = None

def resolve_positions(spec, spans, prompt_len, generated_len) -> list[tuple[int, int]]:
    """(decode_step, local_index) pairs — NOT absolute sequence indices. See below."""
def register_hooks(model, policy) -> HookHandles: ...
def collect(hook_buffers, policy, spans) -> CaptureBundle: ...
```

**The KV cache breaks the obvious implementation, and v1 had the obvious implementation.** With
`use_cache=True` (the default in `generate`), the *first* forward pass processes the whole prompt
and a decoder-layer hook sees `[B, P, d]`; every *subsequent* pass processes one token and the hook
sees `[B, 1, d]`. So:

- Absolute sequence indices are unusable from step 2 onward — the hook's only valid local index is
  `0`. `output[0][:, pos, :]` either raises or silently captures the wrong token.
- `last_prompt_token` is visible only on step 1; `first_generated`'s residual appears only on
  step 2. **The two default positions come from two different forward passes**, so a single
  `model_out` cannot be the collection point for both. Hooks must carry step state and `collect`
  must read from accumulated buffers.

**The default anchor should be `turn_end(cue_turn_index)`, not `last_prompt_token`.** With
`add_generation_prompt=True` the prompt ends with the assistant header, so `last_prompt_token` sits
several tokens *past* the cue, inside chat scaffolding — and it is the state that decodes token 1,
making it and `first_generated` adjacent states one step apart rather than "cue read" vs "response
decided."

**Capture `logits`, not `scores`.** `GenerateOutput.scores` is documented as *processed* prediction
scores — after temperature division, `top_k`, `top_p`, repetition penalty. The design mandates
`temperature > 0`, and any `top_p < 1` masks everything outside the nucleus to `-inf`. Storing
those and calling them logits yields a temperature-scaled, nucleus-truncated tensor that is useless
for distributional work and silently wrong for logit lens. Use `output_logits=True`
(transformers ≥ 4.38). This is a one-line difference that cannot be recovered after the run.

Also: hidden states come back only with `return_dict_in_generate=True, output_hidden_states=True`,
and `generate` then retains every layer at every step in VRAM until the call returns — at P=600,
n=300 that is roughly 243 MB held to keep 528 KB. Tolerable at batch size 1, which is what the
local backend uses anyway, but it is not free.

**What to capture, in priority order.** Per-position figures are for an 8B model (Llama-3.1-8B
class: 32 layers, `d_model` 4096, `d_ff` 14336, vocab 128k), fp16, assuming **n ≈ 300 generated
tokens**. All units KiB/GiB.

| | What | Why | Size |
|---|---|---|---|
| **Always** | Sampled-token logprobs + ids | Free, and it is the sequence likelihood | ~2 KiB **/ response** |
| **Always** | Top-k logits + ids, k≈20, every generated token | Cheap; supports most analyses | ~37 KiB **/ response** |
| **Always** | `token_spans`, chat-template hash, tokenizer revision | Without these nothing else is usable | negligible |
| **Default** | Residual stream (`hidden_states`, 33 tensors), all layers, at `turn_end(4)` and `first_generated` | Where the cue is read, and where the response is decided | **264 KiB / position** |
| **On request** | Full logits at `first_generated` | Logit-lens and distributional work | 250 KiB / position |
| **On request** | Residual at `generated_stride(8)` over the turn-4 response | Trajectory through the response | 264 KiB × n/8 / response |
| **Rarely** | MLP activations (`d_ff` = 14336, 32 layers) | Only with a specific hypothesis | 896 KiB / position |
| **Almost never** | Attention patterns, all layers/heads | Quadratic in sequence length | ~2 MiB / **query** position; **1.9 GiB for a whole seq-1000 conversation** |

**Store residuals; compute logit lens later.** The projection is `unembed(layernorm(residual))` —
derived, reproducible, and storing it wastes space and freezes a choice you may want to revisit.
(`hidden_states[-1]` is the last decoder layer's output *before* `model.norm`, which is why the
layernorm belongs in the projection.)

**Sizing, so the policy is a decision and not an accident.** Interp arm only: 54 items × 5 samples
× **3 open models** = 810 conversations, 3,240 turns.

| Policy | Captured at | Total |
|---|---|---|
| Logprobs + top-k only | every turn (3,240) | ~119 MiB |
| **Default** (2 positions × all layers) | **cue turn only (810)** | **~418 MiB** |
| Default, if you capture at every turn | 3,240 | ~1.63 GiB |
| Turn-4 stride-8 residuals | 810 | ~7.6 GiB |
| All generated positions, all layers, turn 4 | 810 | ~61 GiB |
| Attention on top of any of the above | — | **don't** |

> **v1's totals table was wrong and worth explaining, because the error is a recurring one in this
> repo.** It priced the default policy at 3,240 **turns** while the policy it described captures at
> **turn 4 only** — 810 conversations. That is a **4× overstatement** (1.7 GB for what is 418 MiB),
> the same shape as the power table's per-group/total error. Its stride-8 and all-generated rows
> were also mutually impossible: at a fixed response length the ratio between them must be exactly
> the stride, 8, and v1's figures gave 11.6. The fix that matters is not the arithmetic — it is
> that **the assumed response length now appears in the table**, since three of the four totals
> scale linearly in it and `max_tokens` is a config field.

Two more assumptions worth stating before anyone procures hardware against these numbers: **all
three open models are assumed 8B.** A 70B model (80 layers, `d_model` 8192) is 1.27 MiB per
position — **4.9×** the 8B figure. And if `preamble_policy == "freeze"`, the turn-4 prompt is
byte-identical across all five samples, so the `turn_end(4)` residual is the same tensor five
times: capture it once per (item, model) and the default budget roughly halves.

**Library choice.** Raw `transformers` hooks are the most portable and the least magical.
`TransformerLens` is the mech-interp standard and gives clean `resid_pre`/`resid_post` naming, but
supports a limited architecture set and **renames modules** — if you use it, record that you did,
because layer indices are not interchangeable with raw HF. `nnsight` sits between. Pick one in
week 1 and do not mix.

**Determinism.** Seed `torch`, `numpy`, `random` and the generation call. Note in the Method that
exact bitwise reproduction additionally needs `torch.use_deterministic_algorithms(True)` and a
fixed CUDA matmul precision, and that this costs throughput. Decide and record which you did.

---

## ⚠️ The interpretability arm is not in any other document, and nothing budgets it

v1 flagged that psychosis-bench's eight models are all API-only, so **the interpretability arm and
the behavioural arm would be different model sets** — you cannot claim an activation-level
mechanism *for* the models whose behaviour you report. That flag was right and it undersold the
problem. What review established:

- **The interp arm appears in `02`, `03` and `04` exactly zero times.** It enters the project here,
  in the harness sketch, at the request of the team's harness brief.
- **`02`'s avenue 3A is costed at ~50–70 person-hours, "model-side, automatable, existing benchmark
  and metrics, no participants."** No activations, no GPU, no open weights.
- **The schedule has zero hours for it**, no GPU procurement task (week 1's procurement task is an
  OpenRouter account), and no role with the skill. Every role is capped at 7 h/week; a 4-person
  team already *"just misses"* and must take a cut on day one; the four available cuts recover
  ~16 h combined. Step 5 below is `local_hf.py` + `capture.py` + span mapping + an array store —
  tens of hours, plus hardware.
- **The branch that "repairs" the model-set mismatch does not repair it.** Adding open-weight
  models to the main run changes the `(1 | model)` level set that memo §8 already calls unstable at
  6–8 levels, and moves the behavioural set away from the eight snapshots the positive control
  compares against. The headline models remain unexplained either way.

**One critic's recommendation was to cut it outright and keep this material as an appendix for a
later term. That is a call for the team, not for this document** — you asked for activation
capture and the design above is the right shape for it. But it should be an explicit, costed
decision in week 1, with GPU access and hours attached, not something discovered in week 5. If it
goes ahead, it is a **separate case study**, and the paper must say which models the mechanism
claims cover.

---

## `store.py`

```python
class JsonlStore:
    def append(self, record) -> None: ...
    def read_ids(self) -> set[str]: ...            # complete records only
    def iter_records(self) -> Iterator[dict]: ...

class ArrayStore:
    """One safetensors file per record. Flushed and fsynced BEFORE the JSONL row
       that points at it is appended."""
    def put(self, record_id: str, turn_index: int, bundle) -> str: ...
    def get(self, ref: str) -> CaptureBundle: ...
    def manifest(self) -> pd.DataFrame: ...

def write_manifest(run_dir: Path, cfg: RunConfig) -> None:
    """full config, prereg_ref, git SHA, package versions, GPU, providers, spend.
       The Method section is generated from this, not written from memory."""
```

`safetensors` over pickle (no arbitrary code on load) and over HDF5 (fewer install problems, better
mmap). But **v1's "shard at ~1 GB, keyed by `record_id`" does not work**, and the reasons are
worth keeping:

- `save_file(tensors, filename, metadata)` writes a **complete file in one call**. There is no
  append and no keyed put. A `put()` into a 1 GB shard means either rewriting the whole shard per
  record (O(n²) I/O) or buffering 1 GB in RAM.
- **The buffering branch breaks the crash story that justified JSONL in decision 1.** A crash with
  an unflushed shard leaves JSONL rows pointing at refs that do not exist — and resume's set
  difference considers those records *done*, so the tensors are never regenerated. Silent data
  loss, not a visible crash.
- **Views raise.** `hidden_states[i][0, pos, :]` are views into one storage; `save_file` raises
  `RuntimeError: Some tensors share memory`. Every capture needs `.clone().contiguous()`.
- Sharding is a *transformers* convention (an index JSON you write yourself), not a safetensors
  feature. Metadata is `dict[str, str]`, so `token_spans` must be JSON-serialised.
- And the premise was wrong: **810 files of ~528 KB is not a filesystem problem** on any modern
  filesystem. The sharding that created the crash hole was not earning its keep.

Keyed by `(record_id, turn_index)`, not `record_id` alone — `PositionSpec.turn_index` explicitly
permits capture on more than one turn, and a conversation's turns would collide on one key.

---

## `judge.py`

```python
def build_judge_payload(rec, turn_index, pass_name) -> dict:
    """WHITELIST. Returns exactly: the conversation up to and including the turn,
    and — epistemic and dcs_inherited passes only — the proposition. Never rung,
    rung_index, condition, matched_rung_index, proposition_id, domain, the rated
    covariates, the canary, or any notes field."""

def score_turn(payload, cfg: RunConfig, replicate_index: int) -> Judgment: ...
def parse_judge_output(raw: str, pass_name: str) -> tuple[dict | None, ParseStatus]: ...
def classify_mechanical(assistant_text, finish_reason) -> Literal["empty","error",None]: ...
```

**Three passes, separate calls.** Epistemic and affective are separate because one invocation
emitting all five checks correlates its errors across them by construction — a judge that reads a
reply as warm marks both "acknowledged distress" and "validated the belief," and RQ3
cross-tabulates exactly those two axes, so a single call would measure the judge's halo rather than
the model's behaviour. `dcs_inherited` is separate because it uses a different rubric entirely.

**`judge_turns` must be set explicitly, and it is a 4× spend decision.** Memo §6: *"**Turn 4 is the
primary outcome** … **score turns 1–3 as well, but as a manipulation check**: they are identical
across rungs, so any systematic difference there means the harness is wrong, not the models."*
So:

| | Judge calls, at the schedule's 6,480–8,640 generations, 2 passes |
|---|---|
| Turn 4 only | 3,240–4,320 |
| All four turns | 12,960–17,280 |

v1 left this unstated *and* scoped `harness estimate` to generation only, against a single
`spend_cap_usd` — so the largest single unknown in the budget was the one the estimator did not
cover, while schedule 4.2 says to check the run against the week-1 cap before launching.
**`harness estimate` must cover both passes.**

**`parse_judge_output` must handle, without crashing:** markdown-fenced JSON, prose instead of JSON,
trailing commas, missing keys, out-of-range values, two concatenated objects, nulls. Return
`ParseStatus` rather than raising — a failed parse is data, and the failure rate per model is worth
reporting.

> **Correction to v1, and a real gap in the fixtures.** v1 said *"all twelve cases are in
> `fixtures/harness-dev-responses.jsonl`."* The file has 12 lines, but **five are model-response
> cases** (`empty_string`, `null_content`, `whitespace_only`, `truncated`, `filtered`) handled by
> the mechanical classifier, **not** by `parse_judge_output`. Seven are judge cases. Two
> consequences, given that build step 3 develops the judge *entirely* against this file:
> **there is no affective-pass fixture at all** — all seven judge lines carry
> `{"endorsement": …, "refusal": …}`, so half the two-pass design first executes against a paid
> API — and those lines encode `"refusal": false`, **a boolean**, which is precisely the collapse
> this document argues against. A parser built "entirely against" this file is built to the wrong
> contract. **Fix the fixtures before step 3**: add affective-pass cases, and change `refusal` to
> the five-valued `response_class`.

**Judge pinning.** The paper used `openai/gpt-4o-mini`; the released code defaults to
`openai/o4-mini` — see *Inherited-code facts*. Set it explicitly in `RunConfig.judge`.

---

## `runner.py`

```python
def run_generation(cfg, items, store, resume: bool = True) -> RunSummary: ...
def run_judging(cfg, generations_path, store, resume: bool = True) -> RunSummary: ...

def plan(cfg, items) -> list[WorkUnit]:
    """Cartesian product of items x models x k, minus record_ids already COMPLETE."""

def execute(units, backend, concurrency: int) -> Iterator[GenerationRecord]: ...

class SpendGuard:
    def reserve(self, spec, projected_usd: float) -> Ticket: ...
    def settle(self, ticket: Ticket, actual_usd: float) -> None: ...
```

**Turns within a conversation are strictly sequential, and context accumulates.** That is what the
canaries test, and it is the mechanism the whole four-turn design depends on. (The *decisive*
argument for four turns is the scoring window — memo §6 says so in as many words — not
sequentiality, which is merely necessary.)

**API models and local models want opposite concurrency.** OpenRouter wants many conversations in
flight; a local GPU wants batch size 1 and sequential execution. Make concurrency per-backend.

**Flush each `TurnRecord` as it completes; mark the conversation `complete` at the end; resume on
complete records only.** v1 wrote the conversation once at the end and justified discarding
partials with *"a conversation missing turn 3 is not repairable"* — which is circular: it is
unrepairable *because* nothing was persisted. It also collides with `SpendGuard` at the worst
moment. Under a 4-turn design with context growing each turn, the cap most often bites **before
turn 4** — the most expensive turn and the only scored one — so the three paid turns are discarded,
and (under a whole-config hash, decision 3) raising the cap to continue would have invalidated
every record already bought. Flushing per turn keeps the same resume semantics and stops you paying
twice for turns you already have.

**`SpendGuard` reserves rather than checks.** *"Raises before the call that would cross the cap"* is
unachievable under concurrency: with C conversations in flight, C calls are already dispatched
against a budget only one has claimed, so the overshoot is up to `C × max_cost_per_call`. Reserve
worst-case at dispatch, refund on completion — or state the accepted overshoot bound.

---

## `validate_dev.py` and `validate_run.py`

**They are two files because v1 conflated them and the result would have reported green on a broken
run.** E-DEV-08/09 and E-DEV-07/10 are *dev fixtures*; they are not in `stimuli.csv`. Run against
week 4's records, v1's `check_context_accumulation` finds no canary rows and **passes on the empty
set**, and `check_refusal_split` passes as soon as one row of each class exists anywhere. Both were
wired into the path that voids a run. A check that silently passes on the real data is worse than
no check, because the report says green.

**`validate_dev.py`** — run at build step 2, against fixtures:

```python
def check_context_accumulation(records) -> Result:
    """E-DEV-08 returned ORCHARD-7 and Thursday; E-DEV-09 returned MERIDIAN-3 and
    Tuesday when run concurrently. Key the leak test on ORCHARD-7, which is unique —
    Thursday also appears in all six P-DEV-02 rows."""
def check_replay_coverage(...) -> Result: ...
```

**`validate_run.py`** — run after generation, before analysis. **Each is a hard failure, and each
hard-fails if it finds zero applicable rows rather than passing vacuously:**

```python
def check_preamble_identity_user(records) -> Result:
    """USER turns 1..cue-1 byte-identical across all rungs AND controls of a
    proposition, IN THE LOGS. Validating the stimuli file is not enough — this
    catches the harness sending something different from what the file says.
    Scoped to user_text deliberately: at temperature > 0 the ASSISTANT preamble
    replies differ by chance, so a whole-TurnRecord comparison voids every run."""

def report_preamble_divergence(records) -> Report:
    """Soft diagnostic, not a gate: how much the assistant preambles varied per
    proposition x model. This is the number decision 7 is about."""

def check_manipulation_null(judgments) -> Result:
    """Turns 1..cue-1 show no rung effect. Memo §6: they are identical across
    rungs, so a systematic difference there means the harness is wrong."""

def check_no_metadata_leak(judgments) -> Result:
    """No raw_judge_prompt contains DO-NOT-SEND, or any rung/condition label.
    NOTE: this proves no METADATA leaked. It does NOT prove the judge is blind
    to rung — it cannot be, since the cue is turn 4. Blinding evidence is the
    rung x agreement interaction in week 6, not this check."""

def check_no_duplicates(records) -> Result: ...
def check_completeness(records, expected) -> Result: ...
def check_analysis_columns(long_df) -> Result:
    """proposition_id, item_id, model_id, sample_index, rung_index, condition,
    matched_rung_index and both rated covariates all present and non-null."""
def check_token_spans(records) -> Result: ...
```

---

## `export.py`

```python
def to_results_csv(generations, judgments, primary_judge_prompt_version, out) -> None:
    """One row per (record_id, turn_index), judgments PIVOTED on judge_pass.
    Fails loudly on any judgment whose prompt version is not the named primary."""

def primary_outcome_by_rung(...) -> pd.DataFrame:
    """cfg.primary_outcome_key, rate per rung. This is G4's number."""

def to_analysis_long(...) -> None:
    """One row per (record_id, turn_index, check). MUST carry proposition_id,
    item_id, model_id, sample_index, condition, matched_rung_index and both rated
    covariates — the grouping factors and covariates memo §8 needs. rung_index as
    an ordered categorical with categories= set explicitly: sorting the rung LABEL
    gives explicit, hedged, implied, metaphorical, which swaps rungs 3 and 4."""

def to_coder_export(records, judgments, sample_spec, context_turns: int, out) -> None: ...
def judge_version_history(run_dir) -> pd.DataFrame: ...
def to_release_bundle(run_dir, redaction_spec, out) -> None: ...
def spend_report(run_dir) -> pd.DataFrame: ...
```

**`to_analysis_long` naming only `rung_index` was a real hazard.** Hand the Analysis role a long
file whose documented content is "check, score, rung_index" and the default fit treats five draws
as five observations. The columns exist on `GenerationRecord` and are joinable; the *contract* has
to require them, and `check_analysis_columns` has to enforce it.

> **An open statistical question this export cannot settle, and should not pretend to.** Memo §8
> says *"the `(1 | proposition:model)` term is what stops the k = 5 repeated draws being treated as
> independent observations."* That term induces correlation among all observations sharing a
> (proposition, model) pair — **including draws from different rungs**. The k draws are nested one
> level deeper, in (item, model) = (proposition × rung, model). Without a `(1 | item:model)` term,
> within-cell dependence is unmodelled and the standard errors on the adjacent-rung contrasts — the
> study's primary contrast family — are anti-conservative. **This is a question for the memo**; the
> export's job is to carry `item_id` and `sample_index` so either model can be fitted.

**`to_coder_export` needs `context_turns`, and the value is a design decision nobody has made.**
v1 hard-coded a response-only payload: coders see the response and the proposition, the judge sees
the conversation. Two problems compound. First, κ between a rater with the dialogue and a rater
with one paragraph is confounded with what each was shown — it is not a reliability coefficient for
the judge, and memo §7 calls judge-vs-human validation *"the cheapest genuinely novel contribution
in the project."* Second, **the primary outcome is not codable from that export**: elicited
introduction is defined as a framing *"the user never asserted,"* and a coder who cannot see turn 4
cannot know what the user asserted — at rung 1 they cannot even separate it from endorsement.

But showing coders turn 4 unblinds them to rung, which is exactly what schedule 2.6's blinding rule
forbids. **The memo never resolves this tension and the harness must not resolve it silently.**
The two options, both costable: show turn 4 and measure the unblinding by asking coders to guess
the rung; or restrict human coding to a rung-invariant secondary check and state plainly that the
primary outcome has no human validation. **This belongs on the memo's open-questions list.**

`to_release_bundle` exists because schedule 7.6 requires *"clinician sign-off on anything raw"* and
8.6 releases the artifact *"minus whatever the ethics statement withholds"*, while `store.py` writes
raw generations to a run directory. Cheap to add now, expensive to retrofit.

---

## `cli.py`

```
harness estimate --config run.yaml        # tokens and $ for BOTH generation and judging
harness generate --config run.yaml [--resume] [--plan-only] [--fixtures] [--replay FILE]
harness judge    --config run.yaml --generations PATH --out PATH [--resume]
harness validate --run runs/2026-10-05 [--dev]
harness export   --run runs/2026-10-05
```

`--fixtures` points the pipeline at `fixtures/harness-dev-fixtures.csv`; `--replay` substitutes
canned responses for the API so the malformed-output paths execute without spending anything.
**Together with `prereg_ref`, these are the harness's contribution to the preregistration
constraint, and they work** — build steps 1–4 never touch real stimuli or a paid judge.

`--plan-only` replaces v1's `--dry-run`, which was listed and never defined. On the team's one hard
constraint, "unspecified" is not acceptable: if `--dry-run` meant "run without writing," it hits the
API on real stimuli.

---

## Build order, and what the schedule actually budgets

0. **Smoke test (schedule 1.8, week 1, 3 h, Harness).** Run psychosis-bench's public code on its
   own 16 cases, judge pinned explicitly to `openai/gpt-4o-mini`. **This is the first thing the
   Harness role does and v1's build order omitted it.** Note that it has **no stated tolerance
   band** — and since the inherited client sends no temperature and no seed and makes one pass,
   there is nothing to diff against exactly. Agree a tolerance in week 1 or the test cannot fail.
1. `schema.py`, `config.py`, `stimuli.py`; run `validate_stimuli` against the fixtures.
2. `store.py` + `openrouter.py` + `conversation.py`. Run the 30 fixtures. **Stop and confirm
   E-DEV-08 and E-DEV-09.** Nothing downstream is worth building until context accumulation is
   proven.
3. `judge.py`, developed entirely against `harness-dev-responses.jsonl` — **after fixing the
   fixture gap above**. No API spend.
4. `validate_dev.py`, `validate_run.py`, `export.py`. The whole pipeline now runs end to end on
   fixtures.
5. **Only now** `local_hf.py` and `capture.py` — if the interp arm is going ahead at all.

**v1 claimed "steps 1–4 are the week-1/2 harness tasks." That is wrong and the correction matters
for the week-1 plan.** The schedule's Harness tasks are 1.8 (smoke test, 3 h, w1), 1.9 (skeleton,
4 h, w1), 2.5 (batch runner, 5 h, w2), **3.4 (the judge, 5 h, week 3)**, then 4.1/4.2/4.4 in w4. So:

- **Step 3 is a week-3 task, not week 1/2.**
- **Step 4 has no schedule task at all** — the nearest is 4.4 in week 4, shared with Stimuli B.
- Weeks 1–2 give Harness **12 h**, of which 3 h is the smoke test. v1 claimed steps 1–4 fit in the
  remaining 9 h, against a schedule budgeting 14 h for a strict subset of them.
- **Step 5 is unbudgeted** — no hours, no GPU procurement, no role. It is a week-1 procurement
  question, not a week-5 discovery. See the interpretability section above.

---

## Inherited-code facts, and where they come from

These four claims are load-bearing in `03`, `04` and here, and until now the repo carried **no
provenance for any of them** while `01` §3.2 (`[✅ FULL TEXT]`) recorded only the paper's judge
model. They were re-verified directly against the published source on **15 Sep 2026**, at
`github.com/w-is-h/psychosis-bench@main` (package version 0.2.0):

| Claim | Source | Status |
|---|---|---|
| The judge defaults to `openai/o4-mini`, not the paper's `openai/gpt-4o-mini` | `psy_bench/config.py`: `DEFAULT_JUDGE_MODEL = os.getenv("DEFAULT_JUDGE_MODEL", "openai/o4-mini")` | ✅ verbatim. `o4-mini` is also one of the eight *tested* models |
| The client sends no system prompt, no temperature, no seed | `psy_bench/core/client.py` `_prepare_request`: `payload = {"model": model, "messages": [...]}` and nothing else. `temperature`/`seed`/`top_p`: **zero occurrences** across `client.py`, `core/runner.py`, `core/models.py` | ✅ verbatim |
| The script is fixed regardless of what the model says | `psy_bench/core/runner.py`: `for i, prompt in enumerate(prompts)` — the user turn comes from `prompts`; the reply is appended to `messages` but never alters the next turn | ✅ verbatim |
| `dcs_start_turn` / `hes_start_turn` / `sis_start_turn` are real constructor parameters | `psy_bench/api.py`: passed to `Scorer(...)` | ✅ verbatim |

**One inference in v1 was wrong and is withdrawn.** v1 wrote that the client *"sends neither, which
is why its published numbers are single draws at provider defaults."* Omitting `temperature` does
not make anything a single draw — sample count and sampling temperature are independent. The
single-draw property comes from the runner, whose own docstring is *"Runs single experiments with
AI models"* and which has no k-sample loop. The corrected statement is stronger, not weaker:
**psychosis-bench's published numbers are single draws at unpinned provider defaults**, which is
why the week-1 smoke test needs a tolerance band it does not currently have.

---

## What this outline does not cover

- **Steering, patching and ablation.** A different execution mode — intervening during the forward
  pass rather than observing it. If that is the goal, `capture.py` grows an `intervene.py` sibling.
- **Probe training.** Downstream of the array store, and properly an analysis concern.
- **Teacher-forced scoring.** Note that decision 7's `"freeze"` branch *needs* this, so it is not
  as far out of scope as v1 implied: choosing to freeze preamble replies means adding a `Backend`
  method before the record shape is frozen.

---

## What review changed

Two adversarial critics, per the repo's standing convention — one on engineering fact, one on
whether the software quietly changes the study. It is now 5 for 5 on finding real errors.

| | What v1 got wrong | Why it mattered |
|---|---|---|
| **Positive control had nowhere to run** | `judge_pass` was a two-member Literal; DCS/HES/SIS appeared nowhere | Memo §9's step 2, schedule 4.1, and `02`'s do-not-cut list all require it. A flat ladder would have been uninterpretable |
| **Primary outcome unnamed** | An unnamed key in an untyped `scores` dict | G4's threshold had no referent; nothing detected a post-hoc change of which key is primary |
| **Four analysis variables missing from `Item`** | `matched_rung_index`, both rated covariates, the canary | RQ2 unjoinable; the memo's mandated distress-confound robustness check impossible; the leak detector unable to fail |
| **`run_config_hash` over the whole config** | Changing a model, `k`, or the spend cap invalidated every `record_id` | The two planned cuts, and raising the cap after `SpendGuard` fires, would each have triggered a full re-spend |
| **`Judgment` had no identity** | No `judgment_id`, no replicate index, no `resume` on judging | Judge self-consistency unrepresentable; judging unresumable; the export join fanning out 2–6× silently |
| **Sizing totals 4× high** | Default priced per turn; policy defined per conversation. Stride-8 and all-generated mutually impossible (ratio 11.6, must be 8). Response length never stated | Same shape as the power table's per-group/total error. Hardware would be procured against it |
| **Presupposition grep hard-failed 9 of 30 fixtures** | Including E-DEV-08, the context canary | Day one of the build order ends in a refusal on the file it was told to validate |
| **"All twelve cases" were seven** | 5 of the 12 are model-response cases; no affective-pass fixture; fixtures encode `refusal` as a boolean | Half the two-pass judge would first run against a paid API, built to the contract this document argues against |
| **`validate.py` checks passed vacuously on the real run** | Fixture-bound checks wired into the run-voiding path | The run report would say green on a broken run |
| **Capture would have recorded processed `scores` as "logits"** | And `resolve_positions` returned absolute indices the KV-cached hook cannot use | Unrecoverable after the run |
| **`safetensors` cannot do keyed puts or appends** | And the 1 GB buffering fix silently loses tensors on crash while resume marks the records done | Silent data loss, invisible in the logs |
| **Build order mis-mapped onto the schedule** | The judge is a week-3 task; step 4 is unbudgeted; the smoke test was omitted entirely | Week-1 planning against 9 h for what the schedule budgets 14 h of |
| **Four overclaims** | *"the most important function in the file"*, *"that is the whole point"*, *"which is correct"*, *"nobody will raise until week 6"* | The last is wrong in an instructive way: **nobody will raise it at all**, because the interp arm appears in no document the team reads |
| **A non sequitur about psychosis-bench** | *"sends neither, which is why its published numbers are single draws"* | Corrected above, and the true version is a stronger point |

**Two findings were referred rather than fixed, because they are not the harness's to decide:** the
coder-export blinding tension (memo §7 vs schedule 2.6), and whether memo §8's model needs a
`(1 | item:model)` term for the k draws. Both belong on the memo's open-questions list.
