# Eight-week schedule — *Disentangling Epistemic Sycophancy from Affective Support*

**Window:** Mon 14 Sep – Sun 8 Nov 2026. **Program deadline:** Fri 13 Nov. **Buffer: 5 days.**
**Design decisions behind this plan:** [`04-design-memo.md`](04-design-memo.md). Read that first
if you disagree with the item count or the analysis — the arguments are there, not here.

> **Version 2.** Version 1 was reviewed by two adversarial critics and did not survive: it
> summed hours globally while defining roles that make hours non-fungible, it claimed a cut
> that saved 51 hours and actually saved 5, and it scheduled a gate whose stimuli it never
> wrote. What changed is listed at the end.

---

## Can your team actually run this?

**This plan allocates 199 task-hours, plus ~30 hours of standing overhead** (weekly standups,
status lines, onboarding reading) that version 1 left out entirely. **Call it ~230 hours.**

**Size against the busiest person, not the total.** Roles here are not interchangeable —
"Stimuli" needs no programming, "Harness" needs Python and API keys. Hours cannot be moved
between them freely, so an aggregate comparison is meaningless.

| Role | Total | Busiest week |
|---|---|---|
| **Lead** | 38.1 h | 7.0 h (w1, w7) |
| **Stimuli A** | 41.6 h | 7.0 h (w1, w2, w3) |
| **Stimuli B** | 39.6 h | 7.0 h (w2, w3) |
| **Harness** | 38.6 h | 7.0 h (w1, w4) |
| **Analysis** | 41.1 h | 7.0 h (w5, w6) |

**No role exceeds 7 h in any week.** That is the constraint that shaped this plan, and it is
the number to size against — not the total.

| Team | Capacity at 7 h/week | Verdict against ~230 h |
|---|---|---|
| **5 people** | 280 h | **Works.** One role each, with genuine slack |
| **4 people** | 224 h | **Just misses.** Take the item cut on day one (saves ~11 h → ~219 h) and pair **Analysis + Harness**, which share few weeks. Never pair Stimuli A with Stimuli B |
| **3 people** | 168 h | **Does not fit, even with every cut.** All four cuts together bring this to ~213 h. Three people cannot run this study as designed — reduce to two rungs (explicit vs purely implied), which is a different and smaller paper |

**This is the honest arithmetic, and it says the study wants five people.** Version 1 fudged
the same question by comparing a global total against a global capacity.

**Target output:** an empirical workshop paper (4–8 pages + appendix). **Confirm your venue
deadline in week 1.** If it lands before 13 Nov, the fallback is arXiv plus a later venue —
decide that rather than compressing weeks 1–4.

---

## What this plan builds

**9 propositions × 4 rungs = 36 base items, plus 18 controls = 54 items.**

Version 1 said 48 base items. The cut is deliberate and is explained in the design memo, but
the short version: at an honest writing rate 48 base items plus 24 controls is ~36 hours of
writing, which does not fit any team in range. 36 + 18 does.

**The unit is the *proposition*, not the scenario.** Each proposition is one delusional
belief, written down explicitly, then expressed at all four rungs. That pairing is what makes
the rung effect a within-proposition contrast and roughly doubles the power. **If writers own
whole rungs or whole domains instead of whole propositions, the pairing does not exist in the
data and the analysis in week 6 cannot be run.**

**The need domain is a stratification variable, not a crossed factor.** Three propositions
from each of autonomy / belonging / safety, so the stimulus set spans the space — but the
4×3 interaction is not tested. It was never powered, and both reviewers said so.

---

## The gates

Five gates, four of them in week 1. Each has a **pass threshold written before it runs** and
a fail branch that is actually costed.

| | Gate | Passes if | If it fails |
|---|---|---|---|
| **G0** | The framing statistics are real | All four public-health numbers trace to a primary source | Strike the unsourced ones now. Changes what the paper may claim, not whether it runs |
| **G1** | The ladder carries the belief | ≥ 6 of 8 raters recover an *external-agency attribution* from rung 4, on ≥ 3 of 4 ladders | See the design memo — the fix is to change the outcome, not the stimuli |
| **G2** | The ladder is ordered | Mean Spearman ρ against the assumed order ≥ 0.5, Kendall's *W* significant | Ladder becomes 4 unordered levels; re-run the power sketch at 3 df; contribution claim changes |
| **G3** | Domains are distinguishable | Fleiss' κ ≥ 0.6 across three domains | Drop domain from the stratification and draw all 9 propositions freely. Costs nothing downstream |
| **G4** | There is signal to measure | Explicit-rung primary-outcome rate between 0.15 and 0.85 | Add the 3-turn preamble condition and re-run — cheap in week 4, impossible in week 6 |

**G1 and G2 use different rater pools.** Version 1 reused them, which primes the second task
with the first task's propositions.

---

## Roles

| Role | Owns | Skills |
|---|---|---|
| **Lead** | Coordination, external relationships (clinician, venue, ethics, budget), preregistration, Introduction and Discussion | Writing, chasing people |
| **Stimuli A / B** | Propositions, items, controls, codebook, human coding | Careful writing, clinical reading. **No programming** |
| **Harness** | API pipeline, judge, the run, reproducibility, Method section | Python, API access |
| **Analysis** | Power, models, reliability statistics, Results | R or Python stats |

---

## Week 1 — Mon 14 Sep · Procurement, gates, and the smoke test
**33 h.** Four external dependencies start here because they are the only things you cannot
compress later.

| # | Task | Owner | h |
|---|---|---|---|
| 1.1 | **Procurement.** Open and fund the API account (the inherited harness is OpenRouter-based), name who pays, get reimbursement in writing, set a hard spend cap | Lead | 3 |
| 1.2 | **External bookings.** Clinician: agree scope and book **two** slots (w2 and w3). Confirm venue and deadline. Recruit **two external reviewers** for week 7 | Lead | 2 |
| 1.3 | **G0 — source the framing statistics.** The 0.07% figure, 265 documented cases, 43.8%, 36% of psychologists. Primary sources or they come out. This is a library task with no dependencies, and it decides what the Introduction may claim | Analysis | 3 |
| 1.4 | **Write 12 pilot items** — 3 domains × 1 proposition × 4 rungs. Write each proposition down *first*, then the four utterances expressing it. **Record actual minutes per item** | Stimuli A+B | 8 |
| 1.5 | **G1 — attribution-recovery test.** 8 raters, shuffled unlabelled rungs. Ask: *"Does this person think something outside them is acting on them? Yes / No / Unclear — and if yes, what?"* Score against the threshold above | Stimuli A | 3 |
| 1.6 | **G2 — ordering test**, **separate rater pool**. Rank the 4 rungs by *"how clearly does this state a belief that something external is acting on this person?"* | Stimuli B | 2 |
| 1.7 | **G3 — domain assignment.** The 12 pilot items, blind coders assign to autonomy / belonging / safety. Fleiss' κ | Lead | 2 |
| 1.8 | **Smoke test.** Run psychosis-bench's public code on its own 16 cases, 2 models. **Set the judge explicitly to `openai/gpt-4o-mini` — the repo's default is `openai/o4-mini`, which is not what the paper used and is itself one of the eight tested models.** Diff against the published run in `outputs/` | Harness | 3 |
| 1.9 | **Harness skeleton and model pinning.** 6–8 models, exact snapshot IDs and access dates, check each resolves. One prompt in, one JSON record out, k samples, everything logged incl. temperature | Harness | 4 |
| 1.10 | **Power sketch with a stated MDES.** N for the ladder contrast is **9 propositions × 8 models**, not 1,440 responses. Report the minimum detectable *adjacent-rung* difference, not just the endpoint one | Analysis | 3 |

**Deliverable:** a one-page gate report with the raters' actual answers, and a funded API key.
**Done when:** G0–G3 have recorded verdicts against their written thresholds.

> **Ethics.** G1/G2/G3 show simulated delusional content to people outside the team. Get a
> written not-human-subjects determination or exemption in 1.1's slot if your institution has
> one. **If there is no pathway, use team members and record it as a limitation** — that costs
> the gates their independence, and it should be a decision, not a discovery.

---

## Week 2 — Mon 21 Sep · Write the ladder
**28 h.** The critical path starts here and cannot be parallelised past two writers.

| # | Task | Owner | h |
|---|---|---|---|
| 2.1 | **Freeze the template**, using week 1's recorded timings. Fields: proposition, domain, rung, harm flag, length band, forbidden keywords. **If week 1 came in over 30 min/item, take the item cut now** — not in week 5 | Stimuli A+B | 2 |
| 2.2 | **Write the remaining 24 base items** (9 propositions × 4 rungs = 36 total; 12 exist from week 1). **Each writer owns whole propositions across all four rungs**, then swaps for cross-review. Counterbalance who writes which rung first | Stimuli A+B | 12 |
| 2.3 | **Clinician round 1** — send the 9 propositions and one worked ladder only. 30 minutes of their time, and it catches class-level problems *before* 54 items exist | Lead | 2 |
| 2.4 | **Batch runner.** Full item set in, structured records out, resumable, rate-limit aware, temperature explicit | Harness | 5 |
| 2.5 | **Draft the codebook.** Every check: definition, 2 positive examples, 2 negative, 1 edge case. **Blinding rule: coders see the response and the proposition, never the rung** | Lead + Analysis | 4 |
| 2.6 | **Mine `01` for related work.** It covers ~150 papers; start there, not from scratch | Analysis | 3 |

**Deliverable:** 36 base items, every proposition present at all four rungs.
**Done when:** a reader who has never seen the project can recover each item's proposition from
the file's own `proposition` column.

---

## Week 3 — Mon 28 Sep · Controls, codebook, judge, prereg
**28 h.**

| # | Task | Owner | h |
|---|---|---|---|
| 3.1 | **Write 18 controls.** 9 *ungrounded-neutral* (same proposition, distress stripped) and 9 *grounded-distress* (same need and distress, no ungrounded belief). **These carry RQ2** — see the memo for which rungs they match | Stimuli A+B | 9 |
| 3.2 | **Clinician round 2** — the full 54-item set. Revise on their notes. **If they reject a class of item, take the item cut immediately; do not rewrite in week 4** | Lead + Stimuli A | 5 |
| 3.3 | **Freeze the outcome scales.** Epistemic axis as an ordinal (see memo); affective axis separate; refusal as its own code. This must be settled before 3.5 | Stimuli B + Analysis | 5 |
| 3.4 | **Implement the judge — two separate calls**, one epistemic, one affective, so the judge's errors across the two axes are not correlated by construction. Pin the judge model and version | Harness | 5 |
| 3.5 | **Preregister**, now that the instrument exists. Name **one** primary outcome, the three planned adjacent-rung contrasts, the correction, and what is exploratory. Declare the pilot as instrument-development data | Lead + Analysis | 4 |

**Deliverable:** frozen codebook, frozen scales, working judge, timestamped preregistration.
**Done when:** nothing about the measurement can change without a logged deviation.

---

## Week 4 — Mon 5 Oct · The run, the positive control, and the signal gate
**21 h.**

| # | Task | Owner | h |
|---|---|---|---|
| 4.1 | **The positive control.** Score your own *explicit-rung* items with psychosis-bench's inherited DCS rubric and check they land near its published band. **This is the one test that can fail informatively** — it is the only thing distinguishing "implicitness doesn't matter" from "our stimuli are weak." Diagnose in order: judge drift → model-version drift → your stimuli | Harness + Analysis | 4 |
| 4.2 | **Main run.** 54 items × k = 5 × 6–8 models ≈ 1,600–2,200 generations, plus judging. **Temperature above 0** — at 0, k = 5 returns five identical strings and buys nothing | Harness | 3 |
| 4.3 | **G4 — signal gate.** Is the explicit-rung primary-outcome rate between 0.15 and 0.85? Is rung 1 ≠ rung 4 in the expected direction? **Fail → add the 3-turn preamble condition and re-run this week** | Analysis | 2 |
| 4.4 | **Integrity and refusal pass.** No truncations, no missing cells. **Code refusals as their own category** and report the refusal rate per rung — it is a result, and if it is not coded it manufactures a ladder effect | Harness + Stimuli B | 4 |
| 4.5 | **Draw the reliability sample** from the *main run*, stratified by rung × item-type × judge-label, oversampling judge-positive cases on the rare checks. Strip all rung labels | Stimuli A | 3 |
| 4.6 | **Draft the Method section** while the decisions are fresh | Lead + Stimuli A | 5 |

**Deliverable:** the full scored dataset, a positive-control verdict, and a G4 verdict.
**Done when:** you know whether there is an effect to write about.

---

## Week 5 — Mon 12 Oct · Reliability
**22 h.** The week that separates this from the benchmark it builds on.

| # | Task | Owner | h |
|---|---|---|---|
| 5.1 | **Human double-coding.** **Three coders, at least one from outside the stimulus team**, all blind to rung, item order randomised. **120 responses, each coded by all three**, at a realistic 2.5 min per response — 5 h per coder. Two coders cannot form a majority; three can | Stimuli A+B + Lead | 15 |
| 5.2 | **Agreement statistics.** κ **and** raw agreement **and** prevalence, per check. On rare checks κ collapses toward zero even at 95% agreement — report a prevalence-adjusted statistic (Gwet's AC1 or PABAK) and judge the check on that | Analysis | 4 |
| 5.3 | **First fit of the primary model** on the frozen data | Analysis | 3 |

**Deliverable:** a reliability table, and a first look at the primary result.

> **If a check has poor agreement**, it does not carry a primary claim — but say so in the
> paper rather than dropping it silently. A well-reported low-agreement measure is a finding
> about the construct's difficulty.

---

## Week 6 — Mon 19 Oct · Analysis and figures
**22 h.**

| # | Task | Owner | h |
|---|---|---|---|
| 6.1 | **Primary model.** `outcome ~ rung + (1 \| proposition) + (1 \| model) + (1 \| proposition:model)`, with **model as a fixed factor** if the variance component is unstable at 6–8 levels. Sum-to-zero contrasts. **Three planned adjacent-rung contrasts with Holm correction**, plus a monotonicity test. Report the MDES alongside every null | Analysis | 5 |
| 6.2 | **The rated-directness model.** Regress the outcome on G2's *continuous* directness ratings rather than rung membership. This roughly doubles the usable information and is the best defence against "you found a boundary" vs "your items varied in difficulty" | Analysis | 2 |
| 6.3 | **RQ2 and RQ3 tables.** RQ2 from the controls. RQ3 as a **2 × 4**, not a 2 × 2 — "no epistemic stance" is the modal response at the top rungs and collapsing it misstates the result | Harness | 3 |
| 6.4 | **Judge validation and self-consistency.** Judge vs human majority, **per rung**, with a test of the rung × agreement interaction. Plus the judge run 3× on the same responses, agreeing with itself. Both are cheap and neither has been done for this benchmark | Harness | 3 |
| 6.5 | **Figures — three, maximum.** Ladder curve with CIs, the affective × epistemic table, the reliability table | Stimuli B | 4 |
| 6.6 | **Results draft** | Lead + Stimuli A | 5 |

**Deliverable:** every number the paper reports, regenerable from one script.

---

## Week 7 — Mon 26 Oct · Full draft, then adversarial review
**22 h.**

| # | Task | Owner | h |
|---|---|---|---|
| 7.1 | **Introduction and contributions.** Claim what you measured. **"Maps the exact mathematical degradation curve" is not what this design does** — locate where behaviour changes most sharply, and state the MDES | Lead | 5 |
| 7.2 | **Discussion, and what this does not show** | Lead + Analysis | 4 |
| 7.3 | **Limitations, written honestly**, plus the **preregistration deviation table**. Turn structure; the judge; 9 propositions; authored stimuli | Analysis + Stimuli A | 4 |
| 7.4 | **Appendix**: full stimulus set, codebook, prompts, model IDs, spend | Stimuli B + Harness | 4 |
| 7.5 | **Two external reviewers** (booked in week 1), briefed to assume the authors are overconfident. One on citations and numbers, one on reasoning. Hand them the data, collect the reviews | Stimuli A | 2 |
| 7.6 | **Ethics and release statement**, with **clinician sign-off on anything raw**. Budget their time here, not in week 8 | Stimuli B + Harness | 3 |

**Deliverable:** a complete draft plus two reviews.

---

## Week 8 — Mon 2 Nov · Fix, polish, submit
**23 h.** Ends Sun 8 Nov, five days before the deadline.

| # | Task | Owner | h |
|---|---|---|---|
| 8.1 | **Fix what the reviewers found.** Log what changed | Lead + Analysis | 6 |
| 8.2 | **Reproducibility check** — someone who did not build the harness regenerates the results from the repo | Stimuli B + Harness | 3 |
| 8.3 | Format to the venue template; check the page limit | Stimuli A | 3 |
| 8.4 | Abstract, written last | Lead | 2 |
| 8.5 | Figure pass: legible at print size, readable in greyscale | Stimuli B | 3 |
| 8.6 | **Release the artifact**: stimuli, codebook, prompts, analysis scripts, model IDs — minus whatever the ethics statement withholds | Harness | 3 |
| 8.7 | Full read-through by every author, then **submit by Fri 6 Nov** | All | 3 |

---

## Standing rules

**Pin everything.** Model snapshots, judge model *and* version, temperature, dates, prompt
versions. The judge point is not pedantry: **the paper says `gpt-4o-mini` and the released code
defaults to `o4-mini`.** Whichever you use, say which.

**Never sum the five checks.** Checks 1–2 measure harm, 3–5 measure safety. A total is
meaningless. (The epistemic ordinal in 3.3 combines checks 1 and 2 deliberately — that is a
scale, not a total.)

**One 30-minute standup a week**, plus a written status line per role. This is ~30 h of
standing overhead across the project and it is counted in the ~196 h, not hidden.

**Two checkpoints owned by the Lead**, in the calendar now:
- **Fri 25 Sep (end of week 2):** are the 36 base items written? If not, take the item cut.
- **Fri 9 Oct (end of week 4):** is the dataset scored and does G4 pass? If not, take the model
  and k cuts and descope RQ3.

---

## If you fall behind

Version 1's cut list saved 5 hours of 216 and claimed 51. These are recomputed from the task
table, and the first one is the only one that matters.

| Cut | Saves | Costs |
|---|---|---|
| **1. Item cut: 6 propositions × 4 rungs = 24 base + 12 controls** | **~11 h**, from 2.2, 3.1, 3.2, 5.1 | The random-effect estimate on 6 propositions is thin; report proposition as fixed. **This is the cut a 3-person team takes on day one** |
| **2. Drop the domain stratification** | ~4 h, from 1.7 and template bookkeeping | Weaker generalisability claim. Nothing downstream breaks |
| **3. Six models instead of eight** | ~1 h of orchestration, plus API spend | Marginally weaker "models in general" claim |
| **4. k = 5 → 3** | ~0 h, some API spend | Real power loss. **Cut models before you cut k** — version 1 had this backwards |

**Do not cut:** the clinician review, the human double-coding, the controls, or the positive
control (4.1). Those four are what make the result believable, and they are the first thing a
reviewer checks.

**If a null:** the paper is still there. Pre-commit to it in week 3's preregistration — *"we
built the first graded implicitness ladder, validated the scoring instrument against human
coders (which the benchmark we build on never did), and found the boundary is not where the
field assumed, within ±X points."* Framing that in week 3 costs nothing and rescues week 6.

---

## What changed from version 1

| Change | Why |
|---|---|
| **Per-role hours published; every role capped at 7 h/week** | v1 summed 216 h globally against a global capacity. Per role, the Lead alone needed 57 h — more than one person's entire eight weeks — and every role busted its weekly ceiling |
| **Week 5 and 6 levelled** | v1 put 21 h on one person in week 5 and 19 h on the Lead in week 6, with two people at zero. v1 also named week 2 as the crunch; it was not |
| **Standing overhead counted (~30 h)** | Standups and onboarding were not in the 216, which alone broke the 4-person verdict |
| **36 base + 18 controls, not 48 + 24** | At v1's own week-1 writing rate, its week 2 was 68 h, not 38 |
| **The unit is the proposition; writers own propositions, not cells** | v1's `(1 \| scenario)` discarded the pairing the ladder exists to create, and "each writer owns whole cells" confounded writer with domain |
| **Domain demoted to stratification** | The 4×3 interaction was never powered |
| **G1 asks for attribution recovery, not proposition recovery** | v1's G1 could only be passed by destroying the manipulation. See the memo |
| **G0 and G4 added; all gates given numeric thresholds and separate rater pools** | v1 had no thresholds, used 3 raters, reused them across G1 and G2, and scheduled G3 with stimuli it never wrote |
| **The positive control restored** | `02` specifies a two-step falsification. v1 contained neither step — "positive control" appeared zero times |
| **Procurement, ethics and statistic-sourcing moved to week 1** | v1 had no API-key task at all while requiring API calls in weeks 1 and 3, and sourced the Introduction's statistics in week 7, after week 6 wrote around them |
| **Preregistration moved to week 3** | v1 preregistered in week 2 and changed the outcome scale in week 3 |
| **Main run before double-coding; 3 blinded coders** | v1 coded pilot data, changed the codebook afterwards, and used 2 unblinded stimulus authors — so the reported κ described an instrument that produced none of the paper's numbers |
| **Analysis plan rebuilt** | Planned adjacent contrasts with correction, a named primary outcome, refusal coding, MDES reporting, the rated-directness model, RQ3 as 2×4 |
| **Cut list recomputed with real hours** | v1's headline cut saved 5 h and claimed 51 |
| **The design memo actually written** | v1 pointed at it twice; it did not exist |
