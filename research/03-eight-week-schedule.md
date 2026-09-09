# Eight-week schedule — *Disentangling Epistemic Sycophancy from Affective Support*

**Window:** Mon 14 Sep – Sun 8 Nov 2026. **Program deadline:** Fri 13 Nov. **Buffer: 5 days.**
**Capacity assumed:** 3–5 mentees at 5–7 h/week = **120–280 person-hours**.

**This plan allocates 216 hours, and you should check that against your real headcount before
week 1.**

| Team | Capacity at 5–7 h/week | Verdict against 216 h |
|---|---|---|
| **3 people** | 120–168 h | **Does not fit.** Take cut 3 below (collapse to 4×1) from the start, which brings the plan to roughly 165 h — don't discover this in week 5 |
| **4 people** | 160–224 h | **Fits only at the top of the range.** Viable at 7 h/week with no slippage |
| **5 people** | 200–280 h | Comfortable |

**Week 2 is the crunch at 38 hours** — nearly all of it scenario writing, which is hard to
compress and hard to parallelise beyond two writers. If any week is going to slip, it is that
one. Plan for it now rather than absorbing it later.

**Target output:** an empirical workshop paper (4–8 pages + appendix). **Confirm your actual
venue deadline in week 1** — if it falls before 13 Nov, compress weeks 7–8, not weeks 1–3.

---

## The shape of the plan, and why

Two things drive the ordering.

**Stimulus writing is the critical path, and it cannot be parallelised late.** Everything
downstream — the run, the analysis, the paper — is blocked on 48 scenarios plus controls that a
clinician has signed off. So weeks 1–3 are almost entirely design and writing, and the API run
does not start until week 4.

**Three design questions must be settled before the 48 are written, not after.** Each is a
cheap pilot and each can force a rewrite. They are week 1, deliberately, because discovering
any of them in week 5 costs the semester. They are gates **G1–G3** below.

| | Gate | Fails if | Cost if missed until week 5 |
|---|---|---|---|
| **G1** | The ladder holds the belief constant | A blind reader cannot recover the same belief from rung 4 as from rung 1 | The whole ladder is rewritten; ~3 weeks lost |
| **G2** | The ladder is actually ordered | Blind raters don't rank hedged > metaphorical > implied for directness | The primary analysis has no ordered factor |
| **G3** | The three need domains are separable | Blind coders can't assign scenarios to domains above chance | The 4×3 becomes a 4×1; half the design evaporates |

---

## Roles

Adapt to your team. One person can hold two roles; nobody should hold three.

| Role | Owns | Skills |
|---|---|---|
| **Lead** | The paper, the schedule, the clinician relationship, the preregistration | Writing, coordination |
| **Stimuli A / B** | The 48 scenarios + controls, the codebook, human double-coding | Careful writing, clinical reading. **No programming required** |
| **Harness** | API pipeline, judge implementation, data collection, reproducibility | Python, API keys |
| **Analysis** | Power, mixed-effects models, figures, reliability statistics | R or Python stats |

---

## Week 1 — Mon 14 Sep · Gates, and the pilot that could rewrite the ladder
**~28 h.** The highest-leverage week in the project. Do not let it slip.

| # | Task | Owner | h |
|---|---|---|---|
| 1.1 | **Write 6 pilot scenarios** — 2 need domains × the full 4-rung ladder, holding one delusional proposition fixed per ladder. Write the proposition down explicitly first, then the four utterances that express it | Stimuli A+B | 6 |
| 1.2 | **G1 — belief-recovery test.** Give the 4 rungs, shuffled and unlabelled, to 3 people outside the project. Ask: *"What does this person believe is happening to them?"* Score whether rung 4 yields the same proposition as rung 1 | Stimuli A | 3 |
| 1.3 | **G2 — ordering test.** Same raters, new task: rank the 4 rungs by *"how clearly does this state a belief that something external is acting on this person?"* Check the ranking matches the assumed order | Stimuli B | 2 |
| 1.4 | **G3 — domain separability.** 12 scenarios (4 per domain), blind coders assign each to autonomy / belonging / safety. Compute agreement | Stimuli B | 2 |
| 1.5 | **Contact a clinician.** Longest lead time in the project. Agree scope (review stimuli for realism and harm), and book the week-3 review slot now | Lead | 2 |
| 1.6 | **Confirm venue + deadline**, and read the workshop's format and page limit | Lead | 1 |
| 1.7 | **Model selection.** Pick 6–8 models; record exact snapshot IDs and access dates. Check each still resolves. Note which, if any, overlap psychosis-bench's Sept-2025 set | Harness | 3 |
| 1.8 | **Skeleton harness.** One prompt in, one JSON record out, k samples per prompt, everything logged with model ID, timestamp, temperature, seed | Harness | 6 |
| 1.9 | **Power sketch.** For the ladder main effect at the observed psychosis-bench effect size, how many scenarios per rung per model do you need? Write down what the design *cannot* detect | Analysis | 3 |

**Deliverable:** a one-page gate report — G1/G2/G3 pass or fail, with the raters' actual answers.
**Done when:** the team has decided, in writing, whether the ladder as proposed survives.

> **If G1 fails** — the likeliest outcome, and the reason this is week 1 — rewrite rung 4 so the
> delusional belief is still *recoverable* rather than replaced by generic distress, and re-run
> the test before week 2 ends. See the note on this in the design memo.
>
> **If G2 fails**, treat the ladder as 4 unordered conditions rather than an ordered factor. The
> paper survives; the "degradation curve" framing does not.
>
> **If G3 fails**, drop to a 4×1 design with more scenarios per rung. This is a *better* study
> than a 4×3 with an uninterpretable second factor.

---

## Week 2 — Mon 21 Sep · Write the stimulus set
**~38 h — the heaviest week in the plan.** Almost all of it is scenario writing, which is the
critical path and resists parallelising past two writers. Protect it.

| # | Task | Owner | h |
|---|---|---|---|
| 2.1 | **Freeze the scenario template**: ground-truth proposition, need domain, harm code, 4 rung utterances, target length band, forbidden keywords | Stimuli A | 3 |
| 2.2 | **Write the 48** — 12 cells × 4 scenarios. Split by domain so each writer owns whole cells, then swap for cross-review | Stimuli A+B | 16 |
| 2.3 | **Write the controls.** These are not optional extras — **RQ2 is unanswerable without them.** Minimum 24: 12 *grounded-distress* (same need, same distress, no ungrounded belief) and 12 *ungrounded-neutral* (same belief, no distress framing). Add 6 *benign-metaphor* if time allows | Stimuli A+B | 8 |
| 2.4 | **Code the harm covariate** on all items as written: present/absent, and target (self / other / none). Do **not** cross it into the design — see the design memo | Stimuli B | 2 |
| 2.5 | **Preregister.** OSF, free. Hypotheses, primary analysis, what is exploratory, stopping rule | Lead + Analysis | 4 |
| 2.6 | **Harness: batch runner.** Full item set in, structured records out, resumable, rate-limit aware | Harness | 5 |

**Deliverable:** `stimuli.csv` — 48 base + ≥24 control items, every field populated.
**Done when:** a reader who has never seen the project can tell, from the file alone, what the
believed proposition is for every item.

---

## Week 3 — Mon 28 Sep · Clinician review, and build the judge
**~26 h.** The two things that decide whether anyone believes your numbers.

| # | Task | Owner | h |
|---|---|---|---|
| 3.1 | **Clinician review** of all stimuli: realism, clinical plausibility, and anything that should not be written down at all. Revise on their notes | Lead + Stimuli | 6 |
| 3.2 | **Write the scoring codebook.** Every check gets a definition, two positive examples, two negative, and one hard edge case. Checks 3 and 4 need the most work — they are the judgement calls | Stimuli A + Lead | 6 |
| 3.3 | **Restructure the epistemic axis as ordinal** (0 = challenged, 1 = neutral/deflected, 2 = validated, 3 = validated + confabulated) rather than two correlated binaries. Keeps comparability with psychosis-bench's 0–2 DCS | Analysis | 2 |
| 3.4 | **Implement the LLM judge** against the codebook. Pin its model and version | Harness | 5 |
| 3.5 | **Pilot run**: 12 items × all models × k samples. Sanity-check the pipeline end to end | Harness | 3 |
| 3.6 | **Draft the paper's Method section now**, while decisions are fresh | Lead | 4 |

**Deliverable:** a frozen codebook, a working judge, and a clean pilot dataset.
**Done when:** two people applying the codebook to the same 20 pilot responses agree often enough
to proceed (see 4.1).

---

## Week 4 — Mon 5 Oct · Reliability, then the main run
**~24 h.** The week that separates this from psychosis-bench.

| # | Task | Owner | h |
|---|---|---|---|
| 4.1 | **Human double-coding.** Two coders independently score a stratified sample of **120–150 responses**. Compute **Cohen's κ per check** | Stimuli A+B | 8 |
| 4.2 | **Judge validation.** Agreement between the LLM judge and the human majority, per check. **psychosis-bench never did this — reporting it is a genuine methodological contribution, and it is cheap** | Analysis | 3 |
| 4.3 | **Adjudicate disagreements**, refine codebook wording, re-run the judge if the prompt changed | Stimuli + Harness | 3 |
| 4.4 | **Main run.** All items × all models × **k = 5 samples**, temperature fixed and recorded. ~78 items × 5 × 8 models ≈ 3,100 calls — trivial cost, and it gives you within-item variance instead of one stochastic draw | Harness | 4 |
| 4.5 | **Data integrity pass**: no truncations, no refusals miscoded as scores, no missing cells | Harness + Analysis | 3 |
| 4.6 | Draft Related Work | Lead | 3 |

**Deliverable:** the full scored dataset, plus a reliability table.
**Done when:** κ is reported for all five checks and the team has decided which checks are solid
enough to carry a headline claim.

> **If κ is poor on a check** (say below ~0.6), that check does not carry a primary result. Say
> so in the paper rather than quietly reporting it anyway. A well-reported low-κ measure is a
> finding about the difficulty of the construct.

---

## Week 5 — Mon 12 Oct · Analysis
**~24 h.**

| # | Task | Owner | h |
|---|---|---|---|
| 5.1 | **Primary model.** Mixed-effects logistic (or ordinal) regression: outcome ~ ladder rung × need domain, random intercepts for **scenario** and for **model**. Ladder is the main effect you are powered for | Analysis | 8 |
| 5.2 | **RQ2 via the controls** — distress-wrapped vs ungrounded-neutral, on the same proposition | Analysis | 3 |
| 5.3 | **RQ3, the most novel result.** Cross-tabulate affective support × epistemic outcome. The cell that matters is *"validated the emotion, challenged the belief"* — the DBT-correct response. Report the rate per model per rung. **Do not sum the five checks into one score**; checks 1–2 are harmful and 3–5 are good, so a total is meaningless | Analysis | 4 |
| 5.4 | **Exploratory, and labelled as such**: ladder × domain interaction, harm covariate, per-model differences | Analysis | 3 |
| 5.5 | **Figures.** Three, maximum: the ladder curve, the affective×epistemic 2×2, the reliability table | Analysis + Lead | 6 |

**Deliverable:** every number the paper will report, in a script that regenerates them.
**Done when:** re-running one script reproduces every figure and table from raw data.

---

## Week 6 — Mon 19 Oct · Write the full draft
**~30 h.** Method and Related Work already exist from weeks 3–4.

| # | Task | Owner | h |
|---|---|---|---|
| 6.1 | Results | Lead + Analysis | 8 |
| 6.2 | Introduction and contributions — **claim what you measured, not the strongest available framing** | Lead | 6 |
| 6.3 | Discussion, including what this does *not* show | Lead | 5 |
| 6.4 | **Limitations, written honestly and early.** Single-turn if you stayed single-turn; the judge; scenario count; the fact that stimuli are authored, not naturalistic | Lead | 3 |
| 6.5 | **Ethics and release statement.** What you release, what you withhold, why. **Do not publish raw generated delusional dialogue without clinician review** | Lead + Stimuli | 3 |
| 6.6 | Appendix: full stimulus set, codebook, prompts, model IDs | Stimuli + Harness | 5 |

**Deliverable:** a complete draft, every section present, no placeholders.

---

## Week 7 — Mon 26 Oct · Adversarial review, then fix
**~26 h.** This repo's four review rounds each caught real errors. Do the same to the paper.

| # | Task | Owner | h |
|---|---|---|---|
| 7.1 | **Two independent reviewers**, briefed to assume the authors are overconfident. One checks every citation and number against its source; one attacks the reasoning and whether the conclusions follow. Give them the raw data | 2 × team, or external | 8 |
| 7.2 | **Verify every statistic in the framing sections.** The proposal's real-world numbers (the 0.07% figure, 265 documented cases, 43.8%, 36% of psychologists) currently have no primary sources in the draft. **Every one needs a citable source or it comes out** | Lead | 5 |
| 7.3 | Fix what the reviewers find. Log what changed | All | 8 |
| 7.4 | Reproducibility check — a teammate who did not build the harness regenerates the results from the repo | Harness + one other | 3 |
| 7.5 | Read the paper aloud once, start to finish | Lead | 2 |

**Deliverable:** a revised draft plus a short record of what review changed.

---

## Week 8 — Mon 2 Nov · Polish and submit
**~20 h.** Ends Sun 8 Nov, five days before the deadline. **That gap is the plan, not slack to spend.**

| # | Task | Owner | h |
|---|---|---|---|
| 8.1 | Format to the venue template; check page limit | Lead | 4 |
| 8.2 | Abstract — written last, deliberately | Lead | 2 |
| 8.3 | Final figure pass: legible at print size, readable in greyscale | Analysis | 3 |
| 8.4 | Release the artifact: stimuli, codebook, prompts, analysis scripts, model IDs. Withhold what the ethics statement says you withhold | Harness | 4 |
| 8.5 | Full read-through by every author | All | 4 |
| 8.6 | **Submit by Fri 6 Nov if the venue allows.** Do not aim at the 13th | Lead | 1 |
| 8.7 | Write the handoff: what you would do next, what broke, what you would redo | All | 2 |

---

## Standing rules for the whole eight weeks

**Pin and record everything.** Model snapshot IDs, judge model, temperature, dates, prompt
versions. A boundary can move under you when an endpoint updates mid-semester, and the models
psychosis-bench used are already a year old.

**Never sum the five checks.** Checks 1–2 measure harm, 3–5 measure safety. A "score out of 5"
would be meaningless and a reviewer will say so.

**Controls are part of the design, not extras.** RQ2 has no comparison class without them.

**One weekly 30-minute standup**, with a written status line per role. Blockers go to the Lead
the day they appear, not at standup.

**Two decisions need a named owner and a date, this week:** the clinician, and the venue. Both
have external lead times and neither is under your control.

---

## What to cut if you fall behind

In this order. Cut early and deliberately rather than running out of time in week 7.

1. **The benign-metaphor controls** (6 items). Costs you one robustness check.
2. **Two models.** Six is enough for a workshop paper; eight is nicer.
3. **The need-domain factor** — collapse to 4×1 with 48 scenarios across four rungs. **This is
   a genuinely good paper on its own** and is the cut that preserves the most value per hour
   saved. It also removes the analysis you were least powered for.
4. **k = 5 samples → k = 3.** Costs precision, not validity.

**Do not cut:** the clinician review, the human double-coding and κ, or the controls. Those
three are what make the result believable, and they are the parts a reviewer will check first.
