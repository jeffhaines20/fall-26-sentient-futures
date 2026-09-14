# Harness development fixtures

**Version 2.** Version 1 was adversarially reviewed and did not survive — see *What v1 got
wrong* at the end. Most importantly, **every v1 preamble broke the response-agnostic rule that
the design memo states and that these fixtures are supposed to demonstrate.**

| File | |
|---|---|
| `harness-dev-fixtures.csv` | **Primary.** 30 rows. Open in Sheets, or import as UTF-8 |
| `harness-dev-fixtures.json` | Same content for the harness to load directly |
| `harness-dev-responses.jsonl` | **Canned model/judge responses.** No user-turn fixture can produce an empty, null, filtered, truncated or malformed-JSON response — point the harness at this instead of the API to test those paths |
| `fixture-notes.md` | What each fixture is for. **Deliberately not in the CSV or JSON** — see rule 3 below |

## What these are for

Build and exercise the whole pipeline — batching, context accumulation, logging, the judge,
refusal coding, storage — **before any real stimulus exists**, without generating anything that
could inform the preregistration.

> Results here are **pipeline diagnostics, not study data.** Nothing bears on the hypothesis.
> Do not reuse these as study items.

## Three rules these fixtures exist to demonstrate

**1. Every preamble turn is a standalone declarative.** No turn reacts to, thanks, agrees with,
or answers the model. No bare anaphora (*those*, *they*, *that*), no acknowledgements (*thanks*,
*that's helpful*, *great*), no answer tokens (*yeah*, *no*).

This is the memo's rule and it is the criticism the memo levels at psychosis-bench, whose
scripts thank a model at turn 12 for validation it refused at turn 3. **v1 of these fixtures
broke it in all 12 ladder rows.** When you write the real preambles, grep for those tokens —
it should be a CI check on `stimuli.csv`.

**2. The preamble sets the domain without asserting the proposition.** v1's P-DEV-01 turn 3 —
*"things get added or swapped in by other people rather than by me"* — **was the proposition**,
stated plainly, in the context every rung inherited. The implied rung was therefore not implied,
and rung range would have collapsed toward zero.

Test it on the real set: **a blind rater given only turns 1–3 must not be able to state the
proposition.** That is one extra column in the same rater pass as G2.

**3. No row a loader reads carries hypothesis vocabulary or condition labels.** `purpose` and
`check` moved to `fixture-notes.md` because a row gets dumped into debug prompts, `to_dict()`ed
into judge templates, and pasted into chat windows. Memo §7 requires the judge to see the
proposition but **not** the rung.

Every row carries `do_not_send_canary = DO-NOT-SEND-TO-JUDGE`. **Grep your logged judge prompts
for `DO-NOT-SEND`. Any hit means you are leaking condition labels into the judge.**

## Structure

Four turns. Turns 1–3 are a benign preamble shared byte-identically across a proposition's four
rungs **and its two control arms**; turn 4 carries the manipulation.

| | |
|---|---|
| Ladder rows | 12 (3 propositions × 4 rungs) |
| Control-arm rows | 6 (ungrounded-neutral and grounded-distress per proposition) |
| Edge cases | 12 |
| **Total** | **30 rows, 120 user turns** |

Turn-4 utterances are **length-matched within ±3 words across a proposition's four rungs**.
v1's implied rungs were 33% shorter than its hedged rungs, which builds an alternative
explanation for any rung effect straight into the stimulus set. Carry that constraint into the
real spec.

## `rung_index` is the analysis variable

`rung` is a **label only**. Sorted alphabetically it gives
`explicit, hedged, implied, metaphorical` — **rungs 3 and 4 swapped.** Any default categorical
ordering (`pd.Categorical` without `categories=`, R's `factor()`, a `groupby`, a plot legend)
silently permutes them, and the planned adjacent contrasts would be computed as 1→2, 2→**4**,
**4**→3. Use `rung_index` (1–4) everywhere.

## Nine things to verify before the real stimuli arrive

1. **E-DEV-08 returns `ORCHARD-7` and `Thursday`.** This is the **context-accumulation canary**
   and the only fixture that fails deterministically. If either token is missing, the harness is
   not accumulating context — **fail the run.** A silent context bug is otherwise invisible
   through dev and indistinguishable in the results from "the rung effect is small."
2. **Run E-DEV-08 and E-DEV-09 concurrently.** If E-DEV-09 returns `ORCHARD-7` or `Thursday`,
   your batch runner is sharing state between conversations.
3. **All rungs *and controls* of a proposition log byte-identical turns 1–3.**
4. **E-DEV-10 is coded `refusal_policy`; E-DEV-07 is coded `inability`** — and they are
   different categories. "I can't determine that" is not a policy refusal, and merging them
   contaminates the refusal rate with item difficulty, which will be higher at the implied end.
5. **E-DEV-01 round-trips byte-identical**, and its `=SUM(...)` field is not evaluated as a
   formula on import.
6. **E-DEV-11 is not truncated mid-character.** Compare byte length *and* codepoint count
   against the source.
7. **E-DEV-12's judge output is not influenced by the JSON in the user turn.**
8. **Every case in `harness-dev-responses.jsonl` is handled** without crashing and without
   silently scoring zero.
9. **Log the assistant turns 1–3, not just the user turns.** At temperature > 0 the model's
   preamble replies differ across rungs by chance, so "identical context" is true of the *user*
   turns only. **Decide before week 4** whether to freeze preamble replies per
   proposition × model or let them vary, and record which.

Also worth running once: kill the runner mid-set and restart — you should get exactly 30 records,
no duplicates, no gaps. And run one fixture at k=5 at temperature 0 (must give 5 identical
strings; if not, your temperature isn't being sent) and at your chosen temperature (must give
≥2 distinct strings under distinct sample indices).

## Schema

These columns are a **subset** of what the real `stimuli.csv` will carry. `domain_analogue`
becomes `domain`; `rated_directness` and `rated_distress_intensity` are present but empty so the
loader tolerates them from day one.

| Column | Notes |
|---|---|
| `fixture_id` | unique |
| `fixture_type` | `ladder` / `edge_case` |
| `proposition_id` | **the pairing unit** — the study's random-effect grouping factor |
| `domain_analogue` | `autonomy` / `belonging` / `safety` — mundane analogue only |
| `rung` | label only — **do not sort or order on this** |
| `rung_index` | **1–4. The analysis variable** |
| `condition` | `base` / `ungrounded_neutral` / `grounded_distress` |
| `proposition` | the mundane statement the four rungs express |
| `turn_1`–`turn_4` | played in order; model replies accumulate in context but never change the next turn |
| `contains_ungrounded_claim` | `true` for E-DEV-05 only |
| `rated_directness`, `rated_distress_intensity` | empty — populated from the rater pass on the real set |
| `do_not_send_canary` | leak detector, see rule 3 |

**Coerce types on load.** `contains_ungrounded_claim` is the string `"false"` in CSV and a real
boolean in JSON — and `bool("false")` is `True`. Empty fields are `""` in CSV and `null` in
JSON. Suggested: `pd.read_csv(path, keep_default_na=False, dtype=str)` then explicit casts.

No expected scores anywhere. These say what the **pipeline** should do, never what a model
should answer.

## What v1 got wrong

| | |
|---|---|
| **Every ladder preamble presupposed a model reply** — *"That's helpful"*, *"Yeah —"*, *"a couple of those"*, *"They were fine"* | The rule these fixtures exist to demonstrate, broken in the file the schedule calls "the worked pattern" |
| **The shared preamble asserted the proposition** | The implied rung wasn't implied. Rung range would have collapsed |
| **No context canary** | All 19 turn-4s were answerable cold. A silent context bug would have survived dev and corrupted the whole week-4 run |
| **No `rung_index`**, and alphabetical sort permutes rungs 3 and 4 | A wrong-but-publishable-looking number |
| **E-DEV-07 would not have produced a refusal** | No city named, so the honest reply is inability, not a policy decline. The refusal branch would never have executed |
| **`hedged` was inconsistent** — a hedged assertion in one item, embedded questions in two | Rung confounded with proposition, in a design whose whole point is the within-proposition contrast |
| **Content drifted across rungs** — an implied *memory* claim, an explicit rung stronger than its own proposition, a distress clause at one rung only | The manipulation was not "the same belief, four ways" |
| **P-DEV-01's metaphor was a passivity figure** — *"someone else's hand is moving the pieces"* | The standard figure for a delusion of control, in a file promising no delusional content |
| **Turn-4 length tracked rung** (implied 33% shorter than hedged) | A built-in alternative explanation for any rung effect |
| **No coverage** for empty/null/filtered/truncated responses or malformed judge JSON | Added as `harness-dev-responses.jsonl` |
| **Hypothesis vocabulary in loader-visible columns** | Moved to `fixture-notes.md` |
| README **forbade expected scores, then stated two** | Both rewritten as pipeline statements |
| CSV claimed the long turn was ~600 words | It is 401 |
