# Harness development fixtures

**19 four-turn conversations, 76 user utterances, no delusional content.**

`harness-dev-fixtures.csv` — primary, open it in Sheets or import as UTF-8.
`harness-dev-fixtures.json` — same content, for the harness to load directly.

## What these are for

The Harness role can build and exercise the full pipeline — batching, context accumulation,
logging, the judge, refusal coding, storage — **before any real stimulus exists**, and without
generating anything that could inform the preregistration.

> **Results from these are pipeline diagnostics, not study data.** Nothing here bears on the
> hypothesis. Do not read model behaviour on these as a preview of anything, and do not let
> them reach the preregistration.

**Do not reuse these as study items.** If a phrasing is useful as a control template, rewrite
it fresh under the real template.

## Structure — deliberately identical to the real items

Four turns. **Turns 1–3 are a benign preamble, shared byte-identically across all four rungs of
a proposition; turn 4 carries the manipulation.** That is the design agreed for the study, so
the code path you build here is the code path you will run.

Three mundane "propositions" — a workload complaint, a recent house move, an insecure building —
one per need-domain analogue, each expressed at four levels of directness. The content is
ordinary and grounded. The *shape* is the study's.

| | |
|---|---|
| **Ladder fixtures** | 12 (3 propositions × 4 rungs) |
| **Edge cases** | 7 |
| **Longest single turn** | 401 words |

## What each edge case is for

| Fixture | Exercises |
|---|---|
| **E-DEV-01** | Unicode — curly quotes, em-dashes, accents, emoji, Japanese. Catches encoding bugs before real data hits them |
| **E-DEV-02** | A ~400-word turn. Token accounting, context limits, silent truncation |
| **E-DEV-03** | Near-empty turns. Short-input handling, and any length assumption baked into the judge prompt |
| **E-DEV-04** | Sleep trouble plus an existing prescription — usually elicits a "talk to a pharmacist" reply, so the **resource-redirection check** fires on benign content |
| **E-DEV-05** | The "we only use 10% of our brains" myth — usually elicits a correction, so the **grounding check** fires and the epistemic scale lands at *challenged*. **See the caveat below** |
| **E-DEV-06** | A pet's death — grounded distress with nothing to endorse. The **emotional-reflection check** should fire *and* the epistemic scale should return "no stance" without erroring |
| **E-DEV-07** | Asking the model to guess a postcode — usually declined. **This is the fixture that proves your refusal category is wired up** |

**E-DEV-05 is the only fixture containing any ungrounded claim.** It is a folk myth, not a
delusional belief, and nothing in the study hypothesis concerns folk myths — but it is the one
item that touches "model validates vs. corrects an untrue statement." If you want the dev set
to contain zero ungrounded claims, drop it; you lose a test of the *challenged* end of the
epistemic scale and nothing else.

## Five things to verify before the real stimuli arrive

1. **All four rungs of a proposition log byte-identical turns 1–3.** If they don't, the
   manipulation is contaminated and nothing downstream is interpretable.
2. **E-DEV-02 is not silently truncated.** Compare logged input tokens against what you sent.
3. **E-DEV-01 round-trips through storage unchanged** — no mojibake, no escaped-quote damage.
4. **E-DEV-07 is coded as a refusal, not as zeros on every check.** Refusals scored as zero
   manufacture a ladder effect, because safety-tuned models refuse more at the explicit end.
5. **E-DEV-06 returns a valid "no epistemic stance" rather than an error.** That state will be
   the modal response at the top rungs of the real ladder.

## Schema

The CSV columns are the fields the real `stimuli.csv` will carry, so the loader you write here
should not need changing.

| Column | Notes |
|---|---|
| `fixture_id` | unique |
| `fixture_type` | `ladder` / `edge_case` |
| `proposition_id` | **the pairing unit** — the study's random-effect grouping factor. Four rows share one |
| `domain_analogue` | `autonomy` / `belonging` / `safety` — mundane analogue only |
| `rung` | `explicit` / `hedged` / `metaphorical` / `implied` |
| `item_type` | `base` / `dev_fixture` |
| `proposition` | the mundane statement the four rungs express |
| `turn_1`–`turn_4` | played in order. Model replies accumulate in context but **never** change the next turn |
| `contains_ungrounded_claim` | `true` for E-DEV-05 only |
| `purpose`, `check` | what the fixture exercises, and what to verify — pipeline behaviour, not expected scores |

Deliberately absent: any expected score. These fixtures say what the *pipeline* should do, never
what a model should answer.
