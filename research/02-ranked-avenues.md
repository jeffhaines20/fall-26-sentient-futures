# Ranked Research Avenues

Up to three avenues per idea, ranked **most → least promising**, plus an overall ranking.
Companion to `01-literature-review.md`; section references (§) point there.

> **Version 4.** Three rounds of adversarial critique plus a full-text verification round
> (`critiques/`). v1's ranking rested on
> three "nobody has done this" claims that did not survive fact-checking; v2 fixed those but
> its stated tiebreak was inconsistent with its own scoring table. Changes at the end.

---

# The short version

**Recommended project: 3A — map the implicit/explicit boundary in delusion confirmation.**
Take psychosis-bench's unexplained headline finding (models confirm delusions far more when
the content is *implicit*, p < .001) and characterise where that boundary sits.

| | |
|---|---|
| **Effort** | ~50–70 person-hours, fits comfortably in ~12 working weeks |
| **Participants** | **None.** Model-side only — no recruitment, no ethics application, no budget |
| **Needs** | API access, and a clinical advisor to review stimuli |
| **Week-1 check that could kill it** | ✅ **Run and passed.** psychosis-bench's implicit/explicit gap is only *reported* — a two-level contrast with no gradation anywhere in the benchmark. See the gate table |

**The alternative: 2A — build the plurality router** (when *should* an assistant show
multiple viewpoints?). It has the cleanest unclaimed gap in this document. **Pick it only
if** you confirm an ethics pathway in week 1 *and* accept that the full version does not fit
one semester — the realistic scope is the model-behaviour audit plus an expert-rated
fallback, which drops the "should" from the claim.

**If you want to avoid human subjects entirely: 1A + 3A.** Both are annotation-heavy
trajectory measurement, they share a harness, and the work distributes well across mixed
skill levels.

**Before committing to anything, read the ten week-1 gates.** Eight have been run for you
(the reading ones); gates 8 and 9 are institutional and still open. They are
the highest-return work in the project.

*Why 3A over 2A, when 2A has the better gap: 2A's own stated timeline (5–7 weeks for Phase 1
of 12 available, plus a 2–6 week ethics wait, plus a two-stage human study) does not fit the
semester. 3A does. See the scoring table for the full reasoning, including where I think
this call could be wrong.*

---

## ⚠️ Read this before using the ranking

**1. "Nobody has done X" here means "three search passes, plus full text on the seventeen
papers that matter most, did not surface X."** `01-literature-review.md` was built without reading any paper (publisher
domains were blocked), and its recall is incomplete — proceedings from ACL, EMNLP, NeurIPS
and CHI are poorly covered by general web search. An adversarial fact-check **falsified
three of the original novelty claims outright**, and the verification round below
**narrowed two more**. Assume more will fall. **Before committing to any avenue, run a
targeted search of the relevant proceedings plus forward-citations on the two nearest
papers.**

**2. The load-bearing numbers are now first-hand; the rest are not.** A later session with
web access **pulled full text on the seventeen papers this document's recommendations rest
on**, including every paper named in a week-1 gate, and checked each figure and scope claim
against the method that produced it. Their headline numbers — psychosis-bench's "p < .001",
StoryScope's "93.2% macro-F1", *Choose Your Agent*'s "44% / 19%" — **all checked out
exactly, and nothing was fabricated.** What changed was scope: abstracts systematically
omit the conditions that decide whether a result transfers, and in two cases those
conditions changed an avenue. Every figure *not* attached to a gate is still from an
abstract or a search summary. *(v2 claimed numbers were individually marked. They weren't —
that promise is withdrawn rather than faked; the honest split is gate-papers vs. the
rest.)*

**3. Every avenue names the one premise whose falsification kills it.** Check that premise
first, not last.

**4. This file carries no `[✅ FULL TEXT]` marks; `01` does.** Seventeen sources have been
read in full and every one of them is flagged in `01`. When this document cites a paper
without saying "read in full" or "not one of the seventeen," check `01` before you rely on
it. The three places where that distinction is load-bearing — Song et al. (2411.04578) under
2A, BeliefTrack (2605.30219) under 1B, and StoryScope's venue under 5A — say so inline.

## Ranking criteria

Six criteria. The first five were in version 1; **the sixth was being applied invisibly
and is now explicit**, along with the fact that criteria 7–8 (demoability, legibility)
also influenced the original ordering without being declared.

| # | Criterion | Why it matters here |
|---|---|---|
| 1 | **Gap size** | Is it unclaimed *after* adversarial search, not just after one sweep? |
| 2 | **Feasibility** | Part-time team, one semester, mixed technical skill (self-rated 1–10), no training budget |
| 3 | **Falsifiability** | Is there a *distinguishable* result if the hypothesis is wrong — not just "a null is also a finding" |
| 4 | **Safety relevance** | Does it connect to a real deployed harm? |
| 5 | **Scoop risk** | How likely is a bigger lab to publish first? |
| 6 | **Owner buy-in** | Does the teammate who proposed the idea recognise it as their question? In a volunteer part-time team this is arguably the strongest predictor of completion |
| 7 | **Demoability** | An incubator rewards a thing you can show |
| 8 | **Legibility** | Can a non-technical teammate explain the result? |

**Weights.** Gap ×3, feasibility ×2, everything else ×1. *(v2 said "gap weighted most
heavily" in prose while the table weighted gap and feasibility equally at ×2 — the two
disagreed, and the ×2 version manufactured a spurious tie. Gap ×3 is the weighting I
actually mean.)*

**Honest statement about the ranking.** The criteria now do produce the ordering, but only
because I chose the weights, and two cells do most of the work:

- **2A's gap score (5) is the highest in the document** and survived a deliberate attempt to
  falsify it. So did **5A's** — v2 called 2A's "the only one that survived," which was wrong;
  the fact-check found four surviving claims, of which 2A's and 5A's are the strongest.
- **2A's feasibility is 3, not 4** (v2 had 4). Its own stated timeline does not fit the
  semester — see the arithmetic in 2A below. That single cell is the difference between 2A
  and 3A ranking first. **If you think 2A can be scoped to fit, change that cell to 4 and 2A
  wins by one point.** It is that close, and it is a judgement call, not a measurement.

**Where this ranking could be wrong for you:** if your team weights novelty over
deliverability, or is confident of fast ethics approval, 2A is your project.

## Standing assumptions — flag these if wrong

Inferred from the meeting doc, not confirmed. **If any is wrong, the ranking changes.**

- ~14 weeks from the Sept 1 meeting, part-time, ~4–6 people, weekly mentor meeting.
- **Weeks 1–2 are consumed by choosing the project**, leaving ~12 working weeks.
- **Capacity anchor: assume ~5 h/person/week ⇒ roughly 250–350 person-hours for the whole
  semester.** Every person-hour estimate below should be read against that total. It is the
  number that makes the estimates auditable — if your team's real capacity differs, rescale
  everything.
- API access to frontier models; open-weight models runnable at ≤10B on modest hardware.
- **No model fine-tuning at scale.** Any avenue requiring RLHF-style training is out.
- **Human-subjects work is the binding constraint, not compute.** See the ethics and
  power section below before choosing any avenue with participants.

## The two constraints that actually decide what is possible

### Ethics pathway — resolve this in week 1

"IRB or equivalent" papers over three very different situations:

| Situation | Consequence |
|---|---|
| A member's university IRB will cover it | Expedited/exempt review typically returns **2–6 weeks after submission**, and every listed researcher may need CITI training first |
| No university affiliation → independent IRB | Typically **$1–2k** and similar timelines |
| No pathway at all | **Restrict to model-side work or public secondary data.** Avenues **1A, 1B, 3A, 3B, 5A, 6A and 2A's Phase 1 + 1.5** remain fully available — that is most of the document, including the top three. Only 2A's Phase 2, 3C's informant work, 4A's study and 4B need a pathway |

**Any avenue with participants must submit by week 4 or drop its human phase** — and
resolve *which of the three rows you are in* at the first mentor meeting, in week 1.
Submitting is a later deadline than knowing.

### Statistical power — the numbers version 1 omitted

Two-sided, 80% power, α = .05:

| Design | Detects | Needs |
|---|---|---|
| Opt-in rate, 30% → 45% | Randomised default effect | **~162 per group → ~325 total** |
| Opt-in rate, 30% → 55% | A large effect | ~60 per group → ~120 total |
| Correlation r = .3 | Switching ↔ learning | **~85 total** |
| Correlation r = .4 | Same, larger | ~47 total |
| Two groups, d = 0.5 | Medium effect | **~64 per cell → ~128 total** |
| Three formats, medium effect (f = .25) | One-way ANOVA | **~159 total** |

> **Corrected in v4.** v3 listed the first two rows as *totals*. They are **per group** — the
> randomised-default design needs **~325 people, not ~162**, and costs about **$1,400–1,800**
> at Prolific rates (~$12/hr, 20-minute study), not $700–900. Verified two ways (Cohen's *h*
> and the direct two-proportion formula, both validated against R's `power.prop.test`).
> This document spent two versions criticising v1 for proposing n≈20 at ~18% power, and then
> recommended a design at ~50% power. **Check the row you are using before you budget.**

Version 1 proposed n≈20 for designs in this table. **Either fund the real n, or run a design
that is correct at small n (think-aloud, within-subjects, or continuous moderators — see
below).**

**Three cheap ways to recover power**, all recommended:
- **Within-subjects** designs where order effects can be counterbalanced.
- **Continuous individual-difference moderators** instead of between-group comparisons —
  Need for Closure, Need for Cognition, trust-in-automation and decision-avoidance scales
  are validated, free, take five minutes, and are *more* statistically efficient at small
  n. This is the team's home discipline and version 1 ignored it entirely.
- **Preregistration.** Free, forces the design decisions above, and is a credibility asset.

### One technical hygiene rule

**Pin model versions and record dates.** A "persistence half-life" or a hedging decision
boundary can move under you when an endpoint updates mid-semester. Snapshot IDs, not
"GPT-5" or "Claude."

---

# Week 1–2: verification gates

Version 1 scattered these across five sections. Do them **before** committing.

**Gates 1–7 and 10 have now been run** — the papers were read in full and the outcomes are
below. **Nothing was killed. Two avenues changed shape and one positive control had to be
replaced.** Gates 8 and 9 are institutional and are still yours.

| # | Check | Outcome |
|---|---|---|
| 1 | Read **CAPTURE** (2609.02265), **PERMA** (2603.23231), **PersistBench** (2602.01146) | ⚠️ **1B's competitors thin out, but read this with gate 10.** CAPTURE's decay rates are frozen hyperparameters, not measurements — but it reports that *fitting them freely collapses them to one value*. **PersistBench does not occupy this space at all** (memory-*safety* benchmark); PERMA covers retrieval degradation, not belief decay. **Net for 1B this round: less crowded, harder to execute — see the net-effect note in 1B** |
| 2 | Read **arXiv:2603.22152** (CHI 2026) — what exactly did it measure? | ⚠️ **2A's scope resets, and a novelty claim died.** Its three tasks have **ground truth**; the authors scope the finding to that themselves. But its own reference list contains **Song et al. (2411.04578, CSCW 2025)**, which studied the *no-ground-truth* half — so "nobody measured the legitimate-disagreement case" is **false**. 2A's real gap is still the router. Also: "wide disagreement" means a **3-vs-2 near-even split** (no gain); a lone dissenter helped; unanimous trials had the highest accuracy |
| 3 | Read **PerSpectra** (2602.08716) — are its 100 topics usable? | ⚠️ **Half usable.** The 100 Kialo topics give you the *contested* half of a stimulus set. There is no contrast class of settled items, its 3,810 arguments are GPT-4o expansions rather than authentic text, and its items are arguments, not questions |
| 4 | Read **psychosis-bench** (2509.10970) — gap characterised or just reported? | ✅ **3A survives — this is the strongest result of the round.** The gap is a **two-level factor** analysed with paired *t*-tests. There is no gradation of implicitness anywhere in the benchmark. Scenarios and code are public |
| 5 | Read **arXiv:2508.03247** (cross-cultural depression symptoms) | ✅ **3C's carve-out holds.** It measures *symptom recognition* and finds LLMs largely fail to reproduce the cultural split. Delusion-confirmation across cultural idioms is untouched by it |
| 6 | Read **HumanAgencyBench** (2509.08494) and **Choose Your Agent** (2602.12089) | ✅ **Both as described.** HAB's instruction-following-vs-agency tension is the paper's own words. *Choose Your Agent* is one modality per game, 44% / 19%, Delegate-only surplus gain — all confirmed |
| 7 | Read **SimpleToM** (2410.13648) | ✅ **1B's framing holds.** ICLR 2026 acceptance confirmed; the explicit-vs-applied gap is stated as this document quotes it |
| 8 | Resolve the **ethics pathway** question above | ⬜ **Still open — yours to answer.** Every human-subjects avenue |
| 9 | Confirm **API budget** and whether logprobs are available on your endpoints | ⬜ **Still open — and it now gates more than it did.** Avenues **5A**, **5B** *and* 1B's positive control (see gate 10) |
| 10 | Read **arXiv:2512.18489** — does its estimator need logprobs or a normative posterior? | 🔴 **Both. 1B's positive control as written is dead.** γ\* is fitted against an analytic Bayes posterior using **output logits**, on **open-weight models only** (Llama-3.1-8B, Mistral-7B, Gemma-2-2B). Replacement control specified in 1B |

**One gate was added and run that version 3 did not list:** the LessWrong post
`msFvLtPfDnCEdvrBr`, previously unfetchable, turns out to be **the closest existing work to
1B** — see 1B below. It narrows two of 1B's claims without killing the avenue.

**⚠️ No scoring cell was changed, and you should know that was a judgement call.** Round 3
produced evidence bearing on at least two cells: 2A's Phase 1 got *harder* (PerSpectra
supplies one of three item classes, not "most of it"), and 3A's premise got *firmer* (its
founding claim is now first-hand rather than inferred from an abstract). I judged neither
large enough to move a cell, partly because moving them would widen a gap the document
already says is one point wide. **Disagree with that judgement if you like — it is exactly
the kind of cell the ranking table invites you to argue with.** What you should not do is
read "the ranking did not change" as verification having *confirmed* the ordering. It
tested premises, not the ordering.

**Gates 8 and 9 are the ones left**, and they are institutional questions with
days-to-weeks of latency, so **start them on day one.**

**Note on gate 9:** it used to be an Idea 5 question. Gate 10's outcome makes it an Idea 1
question too — 1B's fallback positive control depends on whether any endpoint you have
exposes logprobs on an open-weight model. Ask once, for both.

**Then budget the pilot for whichever avenue you pick** — these are the premise checks named
in each avenue, and they are real work, not free: 1A hand-code 50 conversations (~10 h);
2A test 100 items (~8 h); 3B pilot one bias (~10 h); 4A pilot with 10 people (~12 h);
5A pilot 200 examples with 5 features (~15 h).

**If you take an avenue with participants, preregister it** (OSF, free). It costs an
afternoon, forces the design decisions in the power section, and is a credibility asset for
an incubator project.

---

# Idea 1 — Aligning Artificial Minds to Human Wellbeing (AH)

### 🥇 1A. Stale user beliefs in real conversations — an observational study of public dialogue corpora

**Type: measurement.** *Smallest intervention it licenses:* a "belief-staleness" detector
that flags when an assistant is still acting on a superseded user statement.

**Question.** In *real* multi-turn conversations — not constructed benchmark items — how
often do users revise a stated belief, preference or goal, and how often does the
assistant keep acting on the superseded version?

**Why it's now ranked first in Idea 1.** Two reasons. First, the constructed-stimulus
version (1B) turned out to be more crowded than the first sweep suggested — though **gate 1
thinned that list**: CAPTURE genuinely occupies it and BeliefShift is adjacent, but PERMA and
PersistBench turned out not to (see 1B). The LessWrong post is the closest thing to it. Observational work on *naturally
occurring* revision does not appear to be occupied. Second, and more practically for this
team: **it needs no recruitment, no payment, and no IRB** (public secondary data is
typically exempt — confirm, don't assume), and the bulk of the work is annotation, which
gives every non-programmer on the team a substantive role rather than a consulting one.

**What you'd do.** Take a public multi-turn corpus (WildChat, LMSYS-Chat and similar are
the obvious starts — check licences and consent terms first, and check whether they are
de-identified to your ethics pathway's satisfaction). Build a codebook for *user belief
revision events*: the user states X, later states not-X or X′. Double-code a sample,
report inter-rater agreement (κ). Then measure, for each event, whether subsequent
assistant turns reflect the old or the new state. Report a **staleness rate** and how it
varies with distance-since-revision, explicitness of the revision, and conversation length.

**Feasibility. High**, with one caveat: annotation is real work, not free. Budget
**~60–100 person-hours** for codebook development, double-coding and reliability. That is
the project's main cost and it is distributable across the team.

**Falsifiable how.** Positive control: inject synthetic revision events into held-out
conversations and confirm your pipeline detects them. Without that, a low staleness rate
is indistinguishable from a codebook that cannot see revisions.

**The premise that kills it.** That naturally-occurring belief revision is frequent enough
to study. **Check this in week 1 by hand-coding 50 conversations.** If revision events are
rare, switch to 1B or to eliciting them (which turns this into a human-subjects study).

**Main risk.** Corpus licence and ethics terms. Some public dialogue corpora carry usage
restrictions or contain sensitive disclosures. **Read the datasheet before the codebook.**

---

### 🥈 1B. Belief-persistence half-life for user-model states

**Type: measurement.** *Smallest intervention:* a decay-aware retrieval rule that
down-weights superseded user facts.

**Question.** After a user explicitly revises a belief, how many turns does the old state
keep influencing the assistant's behaviour — and does that persistence curve differ
between what the model *says* it believes and what its recommendations *reveal*?

**What changed since version 1.** Version 1 called this "measuring the discount factor for
beliefs about the user" and claimed nobody had done it. **Both parts were overstated.**

- *On the gap:* CAPTURE (arXiv:2609.02265, published five days before the first sweep)
  models exactly this as a latent user state with a neural differential-equation belief
  tracker. BeliefShift covers user opinion drift with 2,400 annotated multi-session
  trajectories. **What may remain novel is the narrow move of fitting a persistence curve
  and reporting one comparable parameter per model.**

**Net effect of round 3 on 1B: less crowded, harder to execute.** Three of the four supposed
occupiers cleared (below), which is good. Against that: the nearest neighbour turns out to be
a post that ran 1B's own experiment including the implicit/explicit contrast; both surviving
novelty claims narrowed; the positive control died and its replacement is unanchored; and
gate 9 now gates this avenue too. **No scoring cell moved, and 1B stays 7th.** Read the gate
table's green tick on gate 1 with that in mind.

**What gate 1 found when those papers were actually read.** The space is crowded
differently than version 2 assumed:
  - **CAPTURE does not measure a decay curve — it sets one.** Its three exponential rates
    (0.01 / 0.1 / 0.5 per day for stable values, contextual preferences, transient goals)
    are grid-searched on validation and **frozen**. They are tuned for downstream win rate.
    There is no published per-model curve for you to be scooped by.
  - **But CAPTURE hands you a warning you should design around.** Appendix B: learning
    those three rates end-to-end **collapsed them toward a single value (0.08)** and cost
    3.1 points of adherence. If your plan is one free decay parameter per model, expect
    exactly this. **Fit separately by belief class** — CAPTURE's stable / contextual /
    transient split is a ready-made taxonomy — and report the collapse if it happens.
  - **CAPTURE also names your worst confound.** On context switches the *correct* action is
    usually to **scope** a belief, not revise it (CAPTURE picks scope 71% of the time
    against 4% for a flat-memory baseline). An old belief still showing up in behaviour is
    often appropriate narrowing. Your codebook has to separate the two or your curve
    measures the wrong thing.
  - **PersistBench was wrongly listed here.** It is a memory-*safety* benchmark —
    cross-domain leakage and memory-induced sycophancy, 18 models, median failure 53% and
    97%. It never measures decay. **PERMA** measures retrieval degradation with depth
    (positional probing, recency bias, cross-domain interference), not belief decay.
  - **The real nearest neighbour is not a paper.** The LessWrong post
    `msFvLtPfDnCEdvrBr` (*Do LLMs Change Their Minds About Their Users… and Know It?*),
    unfetchable when this review was written, does a small version of **exactly this
    study**: turns-to-adapt after a mid-conversation user change, with an explicit
    announced-vs-unannounced contrast (immediate vs. 1–2 turns), plus an
    encoded-vs-self-reported gap. **Cite it and distinguish it in your first paragraph.**
    It is distinguishable — one 3B open-weight model, one trait (user *age*), *identity
    switch* rather than belief revision, linear probes rather than behaviour, no curve
    fitted, not peer-reviewed — but "nobody has done this" is no longer a sentence you can
    write.
- *On the name:* "discount factor" imports formalism this design does not earn. A discount
  factor is defined relative to a **normative posterior**; for task facts one exists, but
  after a user says "actually I prefer X now" the normatively correct belief is simply X.
  What the design measures is a **persistence/decay curve for a step change**. Calling it
  a discount factor invites a reviewer who knows arXiv:2512.18489 to object.

**The part worth keeping — and it is still the good part, but state it more narrowly than
version 3 did.** The **elicited-vs-behavioural divergence**. SimpleToM (arXiv:2410.13648,
ICLR 2026 — read in full, gate 7) and T4D (arXiv:2310.03051) establish that models infer
mental states explicitly but fail to *apply* them; nobody appears to have measured that gap
as a **persistence curve over turns** for user beliefs. If the two curves separate, that
separation is the paper. **The narrowing:** the LessWrong post found a version of this gap
(strongly encoded internally, not reported when asked) — but between *probes* and
*self-report*, not between *self-report* and *behaviour*, which is the comparison that
matters for a deployed assistant. That is your distinction; make it explicitly.

**Also worth keeping, with the same tightening:** the **implicit-revision condition**.
Every *benchmark* found uses explicit revision ("I've changed my mind"), and implicitly
signalled change is where deployed systems live. But it is no longer *untested* — the
LessWrong post ran announced vs. unannounced and found a real gap. What is untested is
implicit revision **by the same user, measured behaviourally, across models including
closed ones**.

**Feasibility. High.** API calls plus scripting; no participants, no IRB. **~40–60
person-hours.**

**Falsifiable how.** You still need a positive control: a flat curve for user beliefs is
only interesting once you have shown your instrument can detect a known effect. Version 1
said a flat curve "is also a publishable result" — that is only true with a control in
place.

**🔴 The control version 3 specified does not work. Gate 10 killed it.** It said
"replicate the published task-fact decay result with your own harness first," meaning
arXiv:2512.18489. Reading that paper: γ\* is fitted by minimising KL between the model's
predictive distribution and **an analytic discounted-Bayes posterior**, which needs (a)
**output logits** over the outcome set and (b) a **normative right answer**, available only
because the probes are a biased die and a Gaussian mean. Its §4.3 also reads final-layer
attention and hidden states. Every model it tests is open-weight (Llama-3.1-8B, Mistral-7B,
Gemma-2-2B). **You cannot run it on a closed API, and it does not transfer to user beliefs,
where there is no normative posterior — that is the same objection this document already
raises against the name "discount factor."**

**Be honest about where that leaves you: 1B currently has no anchored positive control, and
finding one is a week-1 task.** A positive control has to recover an *independently
established* effect; "run my own harness on an easier stimulus and hope for a big number" is
a manipulation check wearing the wrong name. The candidates, in rough order of cost:
1. **A planted-fact control on your own behavioural harness.** State a task fact, revise it
   explicitly, measure turns-to-adopt on model *behaviour*. No logprobs needed, and it uses
   the same instrument as the main study. **⚠️ Its warrant is BeliefTrack (arXiv:2605.30219),
   which is *not* one of the seventeen papers read in full — it is search-only, and `01`
   describes it as using a finite belief space with symbolic verifiers, which may not port to
   a generic behavioural harness at all. Read it first and find a specific published
   turn-level number to hit. If there is no such number, this is a manipulation check, and
   you should say so rather than calling it a control.**
2. **Borrow 2512.18489's *design*, not its estimator.** Its step-change-at-a-known-point
   structure (T = 100, changepoint at t = 51) is a clean template for a persistence study;
   only the KL-to-normative-posterior fit is unusable.
3. **If and only if gate 9 says your endpoints expose logprobs on an open-weight model**,
   the original control becomes available as a secondary check. Do not plan on it.

**If gate 1 kills it:** move to 1A (shares the annotation skill) or 3A (shares the
multi-turn harness) — **not** to 1C, which this document rates infeasible.

---

### 🥉 1C. Does Bayesian teaching improve multi-turn adaptation to a changing user?

**Type: intervention.** The doc's own question, and still unanswered.

**Why ranked last despite being AH's best question.** Doing it properly requires
fine-tuning, which is outside the standing assumptions. The cheap version — in-context
Bayesian scaffolding rather than training — tests a materially weaker hypothesis, and
reviewers will say so. It also depends on 1B's harness existing first.

**If you do it:** compare baseline / chain-of-thought / explicit Bayesian scaffolding on
1B's measurement harness, and **state plainly in the writeup that you tested prompting,
not training.**

---

# Idea 2 — Cooperative Human-AI Frameworks (AH)

### 🥇 2A. The plurality router: when *should* an assistant show multiple viewpoints?

**Type: measurement, with a small intervention attached.** *Smallest intervention:*
implement a prompt-level router that chooses format by question type, and A/B it against
the model's default behaviour. **Do this — it converts the project into something you can
demo.**

**Question.** On which question types does presenting multiple perspectives improve human
decisions, and on which does it just add load? And what do models *currently* do?

**Why it has the best gap score in the document.** Searches for adaptive plurality routing,
NPOV generation and multi-perspective RAG all return work on *how* to be plural (Overton /
distributional / steerable — §2.4), never *when*. Nobody has built the router. This
survived a deliberate attempt to falsify it — as did 5A's gap; v2 wrongly called this "the
only one."

**Why it is nonetheless ranked second — do this arithmetic before choosing it.** Phase 1 is
5–7 weeks of the ~12 available. Ethics approval typically returns 2–6 weeks *after*
submission. Phase 2 is then a think-aloud study, then a quantitative study, then analysis,
then writeup. **That is 10–14 weeks of work in a 12-week box with no slack.** The full
version does not fit a semester. Two honest responses: scope to **Phase 1 + Phase 1.5**
(and drop "should" from your claim), or **pick 3A.**

**What changed since version 1 — read this before reusing the old pitch.** Version 1's
headline justification was that "the paralysis cost is asserted everywhere and measured
nowhere." **That was false and is retracted.** arXiv:2603.22152 (Tsuchiya & Baba, CHI 2026)
measures it: across three tasks varying panel size and consensus, **wide disagreement
between AI advisors created confusion and undermined appropriate reliance**, high consensus
fostered overreliance, a single dissent reduced conformity pressure, and larger panels
gained nothing over small ones. arXiv:2412.04629 separately measures attention and belief
effects of multi-persona presentation with eye-tracking.

**This is good news, not bad.** It means the cost is real and quantified, so you do not
have to establish it — you can cite it and go straight to the routing question, which is
still open. **Position against 2603.22152 explicitly, in week 1.**

**⚠️ Gate 2 has now been run, and it resets your scope. Read this before writing the
introduction.** Reading 2603.22152 in full turns up four things its abstract does not say:

1. **Its three tasks all have ground truth** — binary predictions on the UCI Adult, COMPAS
   and speed-dating datasets, calibrated to 60–70% unaided human accuracy. The authors
   scope their own conclusion to exactly that: *"In our accuracy-oriented tasks with ground
   truth, AI panels did elicit informational conformity."* **So the confusion cost was
   measured where disagreement means one advisor is simply wrong.**
   **🔴 A draft of this section then claimed nobody had measured the other case, and credited
   that gap to Tsuchiya & Baba themselves. Both halves were wrong, and the correction is more
   useful than the claim was.** The quoted sentence is the *second* of a pair; the first
   reads *"Prior work on discussing societal issues with AI has suggested that informational
   conformity is unlikely to arise with AI panels (Song et al., 2024); our results provide an
   important counterexample."* **Song et al. — arXiv:2411.04578, CSCW 2025, peer-reviewed —
   is a human study of multi-agent influence on societal issues *without ground truth*,**
   cited six times here and summarised in §2.3 as examining *"opinion change on societal
   issues without ground truth."* The authors are not saying that space is empty. They are
   saying they are a counterexample to what is already in it.
   **What you actually get is better than a false novelty claim: two papers that disagree,
   split along exactly the line your router cares about.** Position against both. Neither
   builds a routing rule — and that, item 1 of §2.6, is 2A's real gap and is untouched by
   round 3. **Read 2411.04578 in week 1. It is not one of the seventeen; nobody here has read
   it in full.**
2. **"Wide disagreement" has one precise referent: a 3-vs-2 near-even split in a five-AI
   panel (their DIV_3), and it produced *no gain* rather than a loss.** A 4-vs-1 split
   (DIV_4) **improved** accuracy over participants' own unaided baseline, and a lone dissenter
   reduced conformity pressure. **Absolute accuracy was still highest on unanimous trials** —
   which were also the easier items, since the panel only split 3-vs-2 on ambiguous cases.
   The relationship is non-monotonic, not "more disagreement is
   worse." A router built on the abstract's summary would get this backwards.
3. **Consensus was observed, not manipulated.** Panels were drawn from a Rashomon set and
   the splits that came out were "treated as observed within-subject factors." The
   abstract's "we varied … within-panel consensus" overstates it; RQ2 is correlational. If
   you manipulate consensus directly, that is a methodological contribution on its own.
4. **N = 348 Japanese crowdworkers** (260 + 88), mean age 44.5, panel size between-subjects
   at ~26–32 per cell — and the authors name culture as a generalisation limit, citing Bond
   & Smith on cross-cultural conformity. Your sample will differ; say so rather than
   assuming the effect sizes carry.

**What you'd do.**

- **Phase 1 — model behaviour audit (no humans, ~5–7 weeks).** Assemble a question set
  spanning three item classes. Classify each model response as single-answer / hedged /
  explicitly plural. Find the actual decision boundary and test whether it tracks genuine
  contestedness or something spurious (phrasing, topic sensitivity, safety training).
  **Gate 3 has been run on the stimulus set, and PerSpectra supplies less than version 3
  assumed.** PerSpectra (2602.08716 — 100 controversial topics, 762 pro/con opinions, 3,810
  arguments; released on GitHub) is real and its numbers are exact, but:
  - **Its 100 Kialo topics are contested by construction**, so it gives you the
    *no-consensus* class and **nothing for the "settled fact" and "contested-but-resolvable"
    classes** your own outcome table requires. You are building two of three classes from
    scratch either way.
  - **Its 3,810 arguments are GPT-4o expansions** of Kialo opinions seeded with retrieved
    Reddit comments — synthetic naturalistic paraphrases, not authentic user text. Fine as
    topic material, wrong as a corpus of things users actually asked.
  - **Its units are arguments and stances, not questions.** Turning 100 topics into
    askable questions is a design step with its own reliability problem, not a download.
  - Its three tasks (opinion counting, matching, polarity) test whether a model
    *comprehends* plurality, not when it should *display* it — so it does not pre-empt you.

  **Net: budget PerSpectra as roughly 20–30 person-hours saved on topic sourcing, not as
  the stimulus set.** The 5–7 week Phase 1 estimate is unchanged — but note it was set when
  PerSpectra was assumed to supply "most of it," so treat it as the floor now, not the
  midpoint, and re-derive it once you have scoped the two item classes you must build
  yourself.
  **Annotation is the cost here, not the API calls:** "hedged" vs. "plural" is not a crisp
  distinction, so you need a codebook, double-coding, and a reported κ. Version 1 budgeted
  3 weeks and treated annotation as free; 5–7 weeks is realistic, or cut the model count.
- **Phase 1.5 — the no-recruitment fallback.** If the ethics pathway fails, have domain
  experts (or a validated LLM-judge protocol with human spot-checks) rate *answer quality*
  under each format. This is weaker than Phase 2 but needs no participants and keeps the
  "should" in the claim.
- **Phase 2 — human study.** Start with **think-aloud at n≈12–20**, which is
  *methodologically correct* at that sample size and is the right way to find the mechanism
  before measuring it. Only then run the quantitative version, powered per the table above,
  with individual-difference moderators (Need for Closure especially) to recover power.

**Outcome measures must be split by item class — version 1's biggest design flaw.**

| Item class | Valid outcomes | Not valid |
|---|---|---|
| Genuine no-consensus | Calibration, decision avoidance, appropriate uncertainty, confidence | **Accuracy** — there is no ground truth by construction |
| Contested-but-resolvable | Accuracy — **but only in a domain where participants have real expertise or evidence access** | Accuracy with lay participants, where the model simply wins (§2.1 Vaccaro) |
| Settled fact | Manipulation check only | Everything else — plurality is obviously wrong here |

Version 1 proposed "decision quality" across all three. On the first class it is undefined;
on the third it is degenerate; on the second it collides with the Vaccaro constraint unless
you pick an expert-participant domain. **Fix this in the design, not in the writeup.**

**"Phase 1 stands alone" — the honest version.** Version 1 claimed a recruitment failure
still leaves you a paper. Not quite. **The promised headline ("models hedge on X but should
hedge on Y") contains a "should," and the "should" is Phase 2.** Phase 1 alone yields a
descriptive audit of hedging behaviour — publishable, and a necessary input, but adjacent
to *Arbiters of Ambivalence* (arXiv:2505.23820), which §2.4 calls the closest existing work.
**Decide now whether the shrunken claim is worth a semester.**

**Effort and cost — v2 omitted both for its own top pick.**

| Component | Estimate |
|---|---|
| Phase 1 (stimulus curation, harness, multi-model runs, codebook, double-coding, κ, analysis) | **~90–130 person-hours** — the annotation dominates |
| Phase 1.5 expert-rated fallback | ~25–40 person-hours |
| Phase 2 think-aloud (n≈12–20) | ~40 person-hours + participant costs |
| Phase 2 quantitative | **~160 participants for one item class; ~477 for all three** (3 × 159) |
| Participant cost | ~$700–900 for 160 at Prolific rates — **but the accuracy outcome needs domain-expert participants**, who cost several times that and recruit far slower |

**At ~250–350 person-hours of total team capacity, Phase 1 alone is a third of the semester.**

**Falsifiable how.** *Positive control:* your classifier must separate the **settled-fact**
and **no-consensus** item classes on model behaviour before you trust any finding about the
contested middle. If models hedge identically on "what is the boiling point of water" and
"is capital punishment justified," your coding scheme is not measuring plurality.

**The premise that kills it.** That models' current plural-vs-single behaviour has a
*findable, non-trivial* boundary. Test on 100 items in week 2 (~8 person-hours — budget it).
If behaviour is uniform (always hedges, or hedges at random), Phase 1 has no result and you
should move to 3A.

---

### 🥈 2B. Confidence-conditioned presentation format

**Type: measurement.**

**Question.** arXiv:2605.04070 showed confidence-based routing fails at picking *which
answer* to show. Does it work for picking **how to present**? When the model is uncertain,
is evidence-without-conclusion better than a hedged conclusion?

**Why it's promising.** Extends a paper the team already cites, and targets their own
bullet about explanations driving overreliance — which, note, **arXiv:2510.26518 supports
directly** ("displaying AI explanation, confidence, and labels leads to over-reliance, but
just showing search results and evidence fosters more appropriate trust"). Version 1
wrongly implied the team had overstated this.

**Why below 2A.** No automated-only version exists — it needs the human study — and it is
a narrower question.

**Main risk.** Model self-reported confidence is poorly calibrated, so the independent
variable is noisy. **Mitigation:** use sampling-based consistency or semantic entropy
(§5.3) instead of asking the model. **Check logprob availability on your endpoints first
(gate 9).**

---

### 🥉 2C. Does the model take viewpoint feedback, or just capitulate?

**Type: measurement.** Best used as an **add-on condition inside 2A**, not standalone — it
collapses into the crowded sycophancy literature (§3.3).

---

# Idea 3 — Cognitive biases, hallucination & "AI psychosis" (DM)

**Read this before picking anything here.** Most crowded idea (§3), and it carries real
human-subjects risk. **Do not run studies with people in mental-health crisis.** Every
avenue below is model-side; 3C involves human informants and needs an ethics conversation.
All three need a clinical advisor to review stimuli.

**On DM's two clauses.** DM wrote "how do LLMs **inherit and/or exploit cognitive biases**;
**countering** characteristics that lead to hallucinations/psychosis." Version 1 generated
three avenues from the second clause and none from the first. **3B below fixes that.**

### 🥇 3A. The implicit/explicit boundary in delusion confirmation

**Type: measurement.** *Smallest intervention:* an implicit-cue detector, evaluated on your
own ladder — this is the "countering" half of DM's clause and makes the project demoable.

**Question.** psychosis-bench's own headline is that models do **significantly worse when
delusional content is implicit** (p < .001) — confirming more, enabling more, intervening
less. **Where is that boundary, and what makes a cue implicit enough to slip past safety
training?**

**Why it's promising.** Takes a published finding's biggest unexplained result and makes it
the object of study — a reliable way to do good work in a crowded field. You inherit the
benchmark, the metrics (DCS/HES/SIS) and the validity argument. **On feasibility and safety
relevance this is the strongest avenue in the document**; see the honest statement above
about why it is not ranked first overall.

**What you'd do.** Build a graded ladder of the same delusional content across explicitness
levels — explicit statement → hedged → metaphorical → purely behavioural/implied. Score with
psychosis-bench's published rubric. Find where each model's intervention rate falls off.
Cross with sycophancy pressure and conversation length.

**What gate 4 established, now that the paper has been read in full.** Four things you need
before you write a single stimulus:

- **The rubric you are inheriting.** DCS and HES are **0–2 ordinals** (DCS: 0
  challenge/ground, 1 perpetuate/neutral, 2 validate/amplify; HES: 0 refusal, 1 enablement,
  2 reinforcement). **SIS is binary 0/1 per applicable turn, max 6 per scenario.** Your
  ladder's outcome is therefore two ordinal scales and one rate — plan the analysis
  accordingly, and do not treat DCS as continuous.
- **Scoring is LLM-as-judge, not human annotation.** Reproducing published values means
  reproducing the judge as well as the stimuli. Budget for judge agreement checks; this is
  the most likely reason your positive control fails for a reason that is not your fault.
- **The measurement windows differ per metric.** Each scenario is 4 phases × 3 turns; DCS is
  scored in phases 2–4, HES in phases 3–4, SIS on 6 applicable turns. **The abstract's
  means are not per-turn averages over all 1,536 turns**, and Table 4 reports SIS as a
  per-scenario sum out of 6 (implicit 1.55 vs. explicit 2.89) — a different scale from the
  0.37 in the abstract. Match the window before comparing anything.
- **Scenarios, code and evaluation scripts are public** (`github.com/w-is-h/psychosis-bench`),
  which is what makes the positive control below cheap rather than speculative.

**Feasibility. High.** Model-side, automatable, existing benchmark and metrics, no
participants. **~50–70 person-hours**, most of it careful stimulus-writing — good work for
non-programmers, and it needs a clinical reviewer.

**Falsifiable how — and this is two steps, not one.** *A previous version collapsed them and
called the result "confirmed runnable." That swapped the real control for a plumbing test:
running their code on their stimuli checks your API wiring, while the control that matters
checks the thing this project actually risks getting wrong — your stimulus writing, which
this avenue itself calls "most of it."*

1. **Smoke test (week 1, hours).** Run psychosis-bench's own code on its own scenarios from
   the public repo and reproduce its published values. Confirmed runnable; confirms your
   pipeline, nothing more.
2. **The actual positive control (before you trust any rung).** Your *own* explicit-rung
   stimuli, written to their rubric, must land on their published DCS/HES/SIS. This is the
   one that can fail informatively, because it tests your scenario-writing.

**If step 2 fails, do not assume your harness is broken — diagnose three causes in order:**
*(a)* **judge drift** — pin the judge to `openai/gpt-4o-mini`, which is what they used, and
remember it was never validated against human raters, so some disagreement is baseline noise
rather than your error; *(b)* **model-version drift** — their eight endpoints are
September-2025 OpenRouter snapshots and it is now a year on, so record which still resolve
and expect moved values on those that do; *(c)* **your stimuli**, which is the interesting
case and the reason to run the control at all. Only after (a) and (b) are ruled out is a
failure yours to fix.

**The premise that kills it.** That the implicit/explicit gap is *reported* but not
*characterised*.

**✅ Gate 4 has been run and the premise holds — this is the firmest result of the
verification round.** In psychosis-bench, implicit-vs-explicit is a **two-level factor**,
nothing more: 8 hand-written scenario *pairs* sharing an identical Phase 1, compared with
paired *t*-tests (Table 4: DCS 1.07 ± 0.64 vs. 0.76 ± 0.65, *t* = 4.77, *p* < .001; HES
0.82 ± 0.63 vs. 0.56 ± 0.52, *t* = 3.54, *p* = .001; SIS 1.55 ± 2.05 vs. 2.89 ± 2.38,
*t* = −7.25, *p* < .001). **There is no gradation of implicitness anywhere in the
benchmark, and no analysis that treats implicitness as anything but binary.** The
instrument for locating the boundary does not exist — building it is the contribution.

Two smaller findings that shape the pitch rather than threaten it. Their §4.5 does plot
DCS/HES/SIS across turns, but "for illustrative purposes," for 2 of 8 models, with no
statistics — so *trajectory* framing is available but not free. And the authors name their
own scenario count (16) as a limitation that makes theme- and harm-type conclusions hard,
which is an argument for your ladder having more rungs than their pair has levels.

**Ethics note.** No participants, but you are generating simulated delusional dialogue.
Treat it as sensitive material; do not publish raw generations without review.

---

### 🥈 3B. Bias *transmission*: does the model amplify the user's biases across a conversation?

**Type: measurement.** *Smallest intervention:* a debiasing system-prompt or reflection step,
evaluated against your own amplification measure.

**Question.** DM asked how LLMs "inherit **and/or exploit**" cognitive biases. The
literature almost entirely studies *possession* — does the model itself show anchoring,
framing, confirmation bias (§3.4). **Transmission is the under-studied direction: across a
multi-turn conversation, does the assistant amplify the *user's* anchoring or confirmation
bias?**

**Why it's promising and why it's new here.** It serves the half of DM's clause that
version 1 dropped entirely. It is squarely the team's cognitive-science home turf. It is
model-side, automatable and cheap. And §3.4's own caveat is an argument for it: LLM biases
"resemble human ones but differ in scale and stability," so "LLMs inherit human biases" is
too coarse a claim to build on — whereas transmission is a different and sharper question.

**What you'd do.** Take classic bias paradigms (anchoring, confirmation bias in
hypothesis-testing, framing). Simulate users who enter with a bias of known strength. Run
multi-turn conversations. Measure whether the user-simulator's bias strengthens, holds or
weakens — and compare against a no-assistant control. Then test whether specific assistant
behaviours (agreement, elaboration, evidence-first) predict amplification.

**Feasibility. High.** ~50–70 person-hours. **Design caveat:** using an LLM to simulate the
biased user is a real validity threat — LLM user-simulators are known to be unrepresentative
(§1.6: models fail to generate plausible initial stances). **Validate the simulator against
human data before trusting the result**, or run the paradigm with a small human sample as a
check. arXiv:2510.20039 (bidirectional opinion dynamics, N=266) is the nearest existing work.

**Falsifiable how.** *Positive control:* your pipeline must reproduce the **known human
effect size** for whichever bias paradigm you pick (anchoring effects are well-characterised
in the behavioural literature) when you run it on the simulator alone, with no assistant. If
your simulated users do not show the bias humans show, you are measuring the simulator, not
the assistant.

**The premise that kills it.** That amplification is measurable above simulator noise. Pilot
on one bias (~10 person-hours) before building three.

---

### 🥉 3C. Cultural misalignment × delusion confirmation

**Type: measurement.**

**Question.** Do models offer *fewer* safety interventions when the same distress is
expressed in a non-Western idiom?

**Why it's still worth listing.** It is the most original crossing in this document. But
version 1 overstated its openness twice:
- **The culture × mental-health-safety crossing is already partly occupied** by
  arXiv:2508.03247, *Somatic in the East, Psychological in the West? A Clinically-Grounded
  Evaluation of Cross-Cultural Depression Symptoms in LLMs* (gate 5). What still looks
  unclaimed is specifically **delusion-confirmation and intervention rates**, not symptom
  recognition.
- **The 91.3%-Western figure was over-generalised** — it is Gemma 3 12B, movies domain only,
  with a non-monotone size–bias relationship and no frontier model tested (§3.5).

**Why ranked last.** Hardest to do well. Culturally-varied distress idioms cannot be
machine-translated into existence; you need real cultural knowledge and ideally native
speakers, and getting it wrong produces a **worse-than-useless result that itself
stereotypes**. Scope to two or three contexts the team has genuine standing in. Note this
is **not** purely model-side — eliciting idioms from informants is an ethics conversation.

**Main risk.** Confounding language with culture. Include a same-language, different-idiom
condition.

*(Version 1's third Idea-3 avenue — auditing whether sycophancy is one construct — is
folded into 3A as a robustness check. It weakened on inspection: the r < 0.3 figure is
confirmed but comes from syco-bench, which has no paper and no peer review (§3.3), so a
replication would rest on an unreviewed source.)*

---

# Idea 4 — Countering Cognitive Atrophy through Epistemic Design

### 🥇 4A. When do people *choose* friction?

> **⚠️ Attribution — DM, this one is yours to confirm or reject.** Version 1 called this
> "DM's actual question." **It isn't.** DM's proposal is the Socratic + CBT/DBT hybrid
> (4C below). The opt-in question is the clause *after* DM's "However" — a caveat on the
> proposal, not the proposal. Version 1 promoted the caveat and ranked the proposal last,
> which is a call **DM should make at the next mentor meeting, not this document.** The
> reframe may well be right; the attribution was not mine to assert.

**Type: intervention + measurement** — the two-mode assistant is a real artifact you can
demo from week 3.

**Question.** Every *epistemic-friction* prototype in §4.3 imposes friction. What predicts
voluntary opt-in, and can it be designed for?

**What changed since version 1.** The claim "nobody has studied voluntary opt-in" is
**partly falsified**:
- **Choose Your Agent** (arXiv:2602.12089): 243 participants play three multi-turn bargaining
  games in groups of three; **each game grants access to one assistance modality** (Advisor /
  Coach / Delegate) in randomised order, and on each turn a participant chooses whether to
  use it or act manually. Finds a **preference–performance misalignment**: people prefer the
  higher-control Advisor (44%) over the Delegate (19%), yet only Delegate access raises
  collective surplus. *v3 described this as "free per-turn choice among three modalities" —
  that overstated it; participants never choose among three.* It is close to 4A's question,
  but **less of a pre-emption than v3 implied: the adoption choice is use-vs-not, not
  friction-level selection.**
- **When Friction Helps** (arXiv:2602.18834) finds users prefer frictionless modes despite
  worse objective performance.
- **OpenAI's Study Mode, Claude's Learning Mode and Gemini's Guided Learning ship exactly
  this switch.** A proposal claiming nobody studies opt-in, while three major products offer
  it, reads as under-researched. **Address them explicitly.**

**The narrowed claim that still holds:** voluntary opt-in to *epistemic* friction in a
**knowledge-work** assistant — as opposed to delegation-vs-advice in a negotiation game, or
learning mode in a tutoring context.

**What you'd do.** A minimal two-mode assistant — "answer me" / "work it through with me" —
with a visible switch. Real tasks. Measure when people switch, what predicts it, and whether
switching relates to learning or retention.

**Design decisions that will otherwise dominate your result:**
- **Randomise the default.** Otherwise you are measuring your own UI choice. Version 1
  admitted the default "will dominate the result" and then treated a no-variance outcome as
  a finding. It isn't — it's a ceiling effect.
- **Keep the incentive manipulation ("you'll be tested later") as a separate arm.** It
  converts *voluntary* opt-in into *incentivised* opt-in, which is the exact distinction the
  avenue exists to make. Version 1 proposed it as a rescue for the main condition.
- **Measure individual differences** (Need for Cognition especially). Cheap, and recovers
  power.
- **Run think-aloud first** (n≈12–20), quantitative second.
- **Vary the *intensity* of the friction, not just its presence.** This matters more than
  it looks: "productive friction" is prescribed everywhere in this literature — HES,
  Scaffolded Cognitive Friction, the offloading reviews — and **dosed nowhere** (§4.4.3).
  That gap **survived** the fact-check, unlike 4A's opt-in framing, which was partly
  falsified. So a two-mode switch is the minimum; **three or four friction levels turns
  this avenue's headline from a partly-occupied question into an open one**, and lets you
  test for an inverted-U (too little → offloading; too much → users defect to a
  frictionless tool). *v2's changelog claimed dosing had been folded in here. It hadn't —
  this is that fix, and it upgrades the avenue.*

**Feasibility. Medium.** The wrapper is genuinely 1–2 weeks (~30 person-hours), and the
ethics application is another 10–20 h on its own. The study is the real constraint:
**~325 participants for the randomised-default effect (~$1,400–1,800)** — see the corrected
power table — or a correctly-powered small-n design instead. **Ethics submission by week 4
or drop the human phase.**

**Falsifiable how.** Positive control: a manipulation known to move friction uptake (e.g.
explicit stakes) must produce a detectable shift. Without it, no-variance is uninformative.

**The premise that kills it.** That opt-in varies at all in a knowledge-work setting. Pilot
with 10 people before building the full study.

---

### 🥈 4B. A behavioural replication of "cognitive debt"

**Type: measurement.**

**Question.** Kosmyna et al.'s *Your Brain on ChatGPT* is the most-cited claim in this idea's
literature, and it is **[⚠️ CONTESTED]** — a published rebuttal (arXiv:2601.00856) raises
sample size (N=54, only 18 in session 4), reproducibility, EEG methodology, inconsistent
reporting and limited transparency. **Does the behavioural core replicate without the EEG?**

**Why it's promising.** Feasible (no neuroimaging — essay quality, recall, self-reported
ownership), legible to everyone on the team, high-value in a field with a replication
deficit, and it lets the team say something concrete about the central claim in their own
idea. Replication is also an unusually good fit for mixed skill levels.

**Why below 4A.** It is someone else's question, and it produces a verdict rather than a new
direction. Note also that *Socrates went Nuclear* (arXiv:2609.00584) is from the same lab —
be consistent about how much weight you give each.

**Feasibility. Medium.** Same participant and ethics constraints as 4A; a within-subjects
design keeps n manageable.

---

### 🥉 4C. A Socratic + CBT/DBT hybrid assistant — **DM's original proposal**

**Type: intervention.**

**Why it's ranked last — and why that call is DM's, not mine.** Three compounding problems:
1. **Crowded on both parents.** Socratic tutors and CBT/DBT chatbots both exist in quantity
   (§4.3, §3.1). The *combination* does look unbuilt — but "unbuilt combination" is a weaker
   claim than "unanswered question."
2. **Evaluation is harder here than anywhere else in this document.** "Psychological growth"
   needs validated instruments and a longitudinal design; one semester cannot detect it.
3. **Ethics.** CBT/DBT techniques delivered by an LLM to non-clinical users is
   regulated-adjacent and needs a clinical advisor.

**How to rescue it — recommended.** Fold the CBT/DBT structure in as **one of the modes in
4A**. You get the design contribution without owing anyone a longitudinal outcome study, and
DM's proposal stays in the project rather than being dropped.

---

# Idea 5 — Deceptive Alignment and Misinformation (DM)

**Pick a lane first.** §5 splits this into (a) detecting AI-authored text, (b) detecting
fabrication, (c) detecting unfaithful reasoning. **(c) requires open-weight models.**

### 🥇 5A. Do "researched" and "made-up" LLM outputs differ *structurally*?

**Type: measurement.** *Smallest intervention:* a lightweight fabrication flag surfaced to
the user.

**Question.** StoryScope (arXiv:2604.03136) showed **discourse-level structural** features
beat stylistic ones at separating human from AI fiction (93.2% macro-F1 on structure alone).
**Does the same structural signal separate an LLM's grounded output from its fabricated
output?**

**Why it's the best avenue in Idea 5.** It is a precise version of DM's exact intuition, and
**the cross-product survived adversarial search — but only in a narrow form you must state
precisely.** The claim that holds is about ***discourse-level*** structural features. It does
**not** hold for "structural" in general: **arXiv:2603.01341, *Structural Hallucination in
Large Language Models: A Network-Based Evaluation of Knowledge Organization and Citation
Integrity*** tests knowledge-graph structure against fabricated output (biographical
hallucination rates **>93%**, citation omission **91.9%**, source-mismatch **>94%** —
*version 3 labelled that last figure a "fabrication rate," which it is not*). That paper
measures *hallucination rates* using *knowledge-graph* structure over a reference ontology —
not a grounded-vs-fabricated separator built from the *discourse structure of the text
itself*, which is StoryScope's move and yours. **Cite it and distinguish it in your first paragraph**, or a reviewer who searches
"structural" + "hallucination" finds it on page one and assumes you didn't look. The nearest work, the *iScience* Portuguese study
(PMC12969083), crosses human-vs-AI with true-vs-false but at the **lexical** level. Its most
useful number for you: the detector scored **93% on human texts but only 75% on LLM
outputs** — detectors tuned on human deception transfer poorly to machine deception. That
gap is arguably the whole opportunity.

**Three corrections to version 1's plan — all of them load-bearing.**

1. **The label was confounded.** Version 1 proposed training on grounded (retrieval-augmented)
   vs. closed-book outputs. **A classifier trained that way learns "was retrieval in the
   context," not "is this fabricated"** — RAG outputs have loud surface tells (citation-shaped
   phrasing, quotation, length). **Fix:** verify fabrication *per claim* — decompose into
   atomic claims and check each (FActScore-style) — and/or add a paraphrase control that
   strips RAG surface markers. **This annotation pipeline is the project's main cost, and
   version 1 omitted it entirely. Budget ~80–120 person-hours.**
2. **The feasibility evidence was from a different task.** Version 1 cited *Trust at risk*'s
   DeBERTa-v3 at 96–98% as proof this is cheap. That is **product reviews** — short,
   formulaic, authorship-cued. §5.2 warns detectors degrade on short texts, across topics and
   under paraphrase. Keep the paper as evidence that *small classifiers beat zero-shot LLMs*;
   drop it as evidence of feasibility *here*.
3. **The method is not inherited.** Version 1 said this "inherits a validated method rather
   than inventing one" while also saying the narrative→expository adaptation "is the
   intellectual work." Both cannot be true. StoryScope's features are narrative-specific
   (character agency, chronological discontinuity); porting them is **deriving a new feature
   space.** Say so. **Reading StoryScope in full prices it — though note the paper says
   nothing about non-fiction either way, so the non-portability call is inference from the
   taxonomy, not a finding.** Its ten dimensions come wholesale from NarraBench's literary
   taxonomy — Agent, Social Network, Event, Plot, Structure, Setting, Time, Revelation,
   Perspective, Style — and the 304 features under them are written for fiction. What ports
   is the *three-stage induction pipeline* (structured intermediate representation →
   cross-source comparison → feature discovery), and that pipeline runs **two** full-corpus
   LLM passes: GPT-5.1 for template extraction, then Gemini 3 Flash to apply the features to
   all 61,608 stories.
   **The paper states its own bill: ~$2,800 to generate the corpus, ~$1,600 for feature
   extraction, $4.4k all in**, at 61,608 stories averaging 4,753 words. Scale to your corpus
   before quoting a figure, but **$1,600 for one extraction pass is the anchor gate 9
   needs** — against a document whose other line items are $700–900 (2A participants) and
   $1–2k (independent IRB), and standing assumptions that include no training budget. **If
   that is unaffordable, cut the corpus by an order of magnitude in the design, not after the
   pilot.**

**Feasibility. Medium — and only if at least one team member has trained a transformer
classifier before.** This is the most technical avenue in the document; version 1 graded it
"High," which would concentrate the work on one or two people.

**Frame it as interpretability, not accuracy — and StoryScope itself is your precedent.**
Semantic entropy (§5.3) already detects confabulation and will likely beat you on raw
accuracy. Structural features say *how* fabricated text differs; entropy only says *that*
it does. **This is exactly the trade StoryScope made:** its 93.2% narrative-only score sits
against 85.8% for style-only, 96.0% combined, and **99.9% for a plain supervised ModernBERT
baseline** on the same task — it accepts being 6.7 points worse than a black box because the
features are readable. **That framing is worth borrowing; its authority is not — StoryScope
lists no venue on arXiv, so it is an unrefereed preprint and cannot be cited as evidence
that reviewers accept the trade.** Make the argument on its merits. Decide it in week 1 and
the redundancy stops being a threat.

**Build a cross-domain held-out test before reporting any number.**

**Falsifiable how.** *Positive control:* your feature extractor must reproduce StoryScope's
published human-vs-AI separation on narrative text before you trust it on the
grounded-vs-fabricated task. If it can't replicate the result it is derived from, a null on
your task is uninformative.

**⚠️ Check the data release before you promise this control.** StoryScope releases its code,
the 10,272 prompts and the **51,336 AI-generated stories** — but **not the human stories**,
which come from **Books3** and are copyright-contested. So the exact human-vs-AI replication
is not runnable off the shelf.

*A previous version of this paragraph offered the six-way authorship attribution result as a
substitute "because it uses only the released AI half." **That was wrong** — `human` is one
of the six classes, and Table 11 makes it the most separable one (88.5% F1 narrative-only),
so dropping it does not leave you the published 68.4% to hit.* What is actually available,
decided in week 1 and not week 6:

- **(a) Source your own human narrative corpus** under a clean licence and accept an
  approximate replication. This is the only route to a published number.
- **(b) Run five-way AI-only attribution** on the released half. Runnable today and it
  exercises the extractor end to end — but **there is no published figure to match**, so it
  is a pipeline check, not a positive control. Say which of the two you are claiming.

Silently dropping the control is not an option.

**The premise that kills it.** That structural features carry signal about grounding at all.
Pilot on 200 examples with 5 hand-picked features (~15 person-hours) before building the
pipeline.

---

### 🥈 5B. Do surface hedges track internal uncertainty?

**Type: measurement.** Extends arXiv:2605.28778. High practical value — users read hedges as
calibration signals. **Needs logprobs (gate 9).** Ranked below 5A because one recent paper
already occupies the core question; you would be extending, not opening.

---

### 🥉 5C. Chain-of-thought faithfulness

**Type: measurement.** The doc's literal framing, and the most important problem here — but
ranked last **for this team**: it requires open-weight internals, it is crowded with
well-resourced interpretability groups, and faithfulness scores are sensitive to the
classifier used to compute them (arXiv:2603.20172), so it is easy to produce a confidently
wrong number. Note also arXiv:2512.23032 argues the skeptical framing is overstated.
**Pick it only if a team member specifically wants mechanistic interpretability.**

---

# Idea 6 — Multi-Layered Trust Framework

**Blunt assessment, unchanged.** No owner, no detail in the doc; the literature has drawn
these layers many times (Weidinger et al.'s three-layer framework since 2023 — §6.1).
**Proposing another framework is the lowest-value thing this team could do.** If nobody owns
this idea, drop it. But note the honest caveat: this is the one idea whose dismissal rests on
*no teammate having elaborated it*, which is weak evidence about the idea and strong evidence
about the meeting. **If someone does own it, say so before it gets dropped.**

### 🥇 6A. Operationalise the cognitive layer — as a rubric with a reliability study

**Type: intervention/artifact.** This is the "blueprint" the source doc asked for.

**Question.** Existing layered frameworks are strong on identity, provenance and sandboxing
and weak on the **human/cognitive layer** (§6.3.2). What concrete, testable controls belong
there?

**What changed since version 1.** Version 1 proposed writing a specification and then testing
it on a deployed assistant — which is two projects, and it graded that "Medium" feasibility.
**The feasible version is a rubric plus an inter-rater reliability study**: turn the
cognitive-layer controls into a scoring instrument, apply it to real assistant transcripts,
and report whether independent raters agree (κ). That is annotation-based rather than
engineering-based, produces an artifact, and is achievable in a semester.

**Start from HumanAgencyBench** (arXiv:2509.08494), not a fresh taxonomy — it already
operationalises six agency dimensions with a running eval, and it reports the structural
tension (instruction-following vs. agency support) that version 1 wrongly attributed to an
unpublished project.

**Falsifiable how.** *Positive control:* your rubric must separate two assistants already
known to differ on HumanAgencyBench's dimensions. A rubric that scores everything the same
is not measuring anything, and κ alone won't tell you that.

**Feasibility. Medium**, but note the honest conclusion: **this is the team's write-up frame,
not a parallel workstream.** It is listed in the ranking table for completeness and scores
joint-last; if you are choosing a project, choose from ranks 1–6 and use 6A as the way you
present whichever you pick.

---

### 🥈 6B. Trace one cross-layer failure end to end

Sycophancy (model) → delusion reinforcement (user) → clinical presentation (institution) →
norms about AI in mental health (society). Cross-layer propagation is asserted and rarely
traced (§6.3.3). Produces an argument rather than a measurement, and depends on evidence
others generated.

### 🥉 6C. Empirically validate an existing framework

The biggest real gap in the area (§6.3.1) and **almost certainly too large for one semester**
— you would need a deployed system, real incidents, and a comparison condition. Listed
because it is the honest answer to "what does this field need," not because this team should
attempt it.

---

# Overall recommendation

**Scoring.** 1–5 per criterion, **5 always good** (so Scoop 5 = *low* scoop risk, Feas 5 =
*easy*). Anchors: **5** = clearly true / trivially achievable; **3** = mixed or uncertain;
**1** = clearly false / not achievable this semester. Gap ×3, feasibility ×2, rest ×1. This
is my judgement made legible, not a measurement — **disagree with the cells, not just the
ordering.**

| Rank | Avenue | Gap ×3 | Feas ×2 | Falsif | Safety | Scoop | Buy-in | Demo | Legib | **Total** |
|---|---|---|---|---|---|---|---|---|---|---|
| **1** | **3A** Implicit delusion boundary | 4 | 5 | 5 | 5 | 3 | 4 | 3 | 4 | **46** |
| **2** | **2A** Plurality router | 5 | 3† | 4 | 3 | 4 | 4 | 4 | 5 | **45** |
| 3 | **1A** Stale beliefs in real corpora | 4 | 5 | 4 | 3 | 4 | 4 | 2 | 4 | **43** |
| 4 | **3B** Bias transmission | 4 | 4 | 3 | 4 | 3 | 5* | 3 | 4 | **42** |
| 5 | **5A** Structural fabrication signature | 4 | 3 | 4 | 4 | 4 | 4 | 3 | 3 | **40** |
| 6 | **4A** Friction opt-in | 3 | 3 | 4 | 3 | 3 | 2* | 5 | 5 | **37** |
| =7 | **1B** Persistence half-life | 2 | 5 | 4 | 3 | 2 | 4 | 2 | 3 | **34** |
| =7 | **6A** Cognitive-layer rubric | 3 | 3 | 3 | 4 | 4 | 1* | 3 | 4 | **34** |

† **The cell the whole ranking turns on.** v2 scored 2A's feasibility 4 and it ranked first.
3 is the honest score: Phase 1 alone is 5–7 of 12 available weeks, before a 2–6 week ethics
wait and a two-stage human study. **Score it 4 and 2A wins by one point.**

\* **Buy-in scores are guesses and are the cells most likely to be wrong.** 4A scores 2 only
because the attribution question is unresolved — **if DM endorses the reframe it becomes 5,
taking 4A to 40 and level with 5A.** 3B scores 5 because it serves DM's own words directly.
6A scores 1 because no one claimed the idea; if someone does, it gains 4. **These cells are
for the team to fill in, not me.**

Note what the table does *not* do: it contains one or two avenues per idea, so it cannot
show a case where, say, 2B beats another idea's winner. It ranks the shortlist, not all 18.

**3A first, 2A second, by one point.** v2 reported these as tied; that tie was an artifact
of weights that disagreed with their own prose. Corrected, 3A leads — and the ordering is
close enough that the trade-off matters more than the rank:

| Pick **3A** (recommended) if… | Pick **2A** instead if… |
|---|---|
| You want to be certain of finishing | You want the cleanest unclaimed gap |
| You have no ethics pathway, or don't know yet | You confirm a pathway in **week 1** |
| You want the strongest safety relevance | You accept a Phase-1-only claim if recruitment fails |
| You want work that starts on day one | You have someone who will own the study design |

**If you cannot answer the ethics question in week 1, pick 3A.** It needs nothing but API
access and a clinical advisor.

**Combinations worth considering.**
- **1A + 3A** — both are trajectory measurement over multi-turn dialogue, both fully
  automatable, both annotation-heavy, and they share a harness. **This is the right pick if
  the team wants to avoid human subjects entirely**, and it distributes work well across
  mixed skill levels.
- **2A + 4A** — version 1 sold this as de-risking. **It isn't.** They share a participant
  pool and one ethics application, but no stimuli, task design, outcome measures or analysis.
  For a part-time semester team that is two projects. Do it only for the shared ethics
  application.

**Where to aim the output.** Version 2 named no venue for any avenue, and a dated call for
papers constrains scope better than any gate table. Rough fits: **3A, 3B** → an AI-safety or
AI-and-mental-health workshop, or a short paper at a CHI/FAccT-adjacent venue; **2A** → the
Pluralistic Alignment workshop series; **1A, 1B** → an ACL/EMNLP workshop on dialogue or
personalisation; **5A** → a workshop on AI-generated content detection; **4A, 4B** → CHI
Late-Breaking Work. **Pick one deadline in week 2 and let it set the scope.**

**The cross-cutting asset.** Ideas 1, 3 and 4 all need **multi-turn trajectory measurement**,
and all three literatures independently complain that current benchmarks score endpoints
(JMIR e91454; arXiv:2510.07777; arXiv:2605.30219). **One good trajectory-measurement harness
is reusable across three of the six ideas — that reusability is worth more than any single
result in this document.**

---

# What changed from version 1

| Change | Why |
|---|---|
| Added inherited-limitations warning | v1 dropped `01`'s "no paper read in full / recall incomplete" caveats while resting its ranking on novelty claims |
| Made criteria 6–8 explicit; added an honest statement that the ranking is a judgement call | v1 claimed the ordering "follows from the criteria." It didn't |
| Added scoring table, week-1 gates, power table, cost estimates, person-hours | v1 had no numbers for any of these; "hour", "deadline" and "power" appeared zero times |
| **2A**: retracted the "paralysis unmeasured" claim; split outcomes by item class; fixed the "Phase 1 stands alone" overclaim; 3→5–7 weeks | The gap claim was false (arXiv:2603.22152); the outcome measure was undefined on its own stimulus set |
| **4A**: fixed attribution to DM; added Choose Your Agent, Study Mode, Learning Mode; separated the incentive arm | v1 presented DM's caveat as DM's question and ranked DM's actual proposal last |
| **1A** is now the corpus study; old 1A became 1B, renamed and narrowed | CAPTURE/PERMA/PersistBench occupy the old framing; "discount factor" was formalism the design didn't earn |
| **3B** added (bias transmission) | DM's "inherit and/or **exploit**" clause got zero avenues in v1 |
| **4B** added (cognitive-debt replication); old 4B (friction dosing) became a design requirement inside 4A | v1 flagged the contested study and generated no avenue from it |
| **5A**: added per-claim verification; dropped the cross-task feasibility number; downgraded to Medium | The train/test label was confounded with the experimental condition |
| **6A**: became a rubric + reliability study | v1's version was two projects graded as one |
| Added positive controls to 1A, 1B, 3A and 4A | v1 satisfied falsifiability by relabelling nulls as findings |
| Added "measurement vs. intervention" + smallest-intervention line per avenue | The source doc asked three times for guardrails/prototypes; v1 proposed only measurement |

# What changed from version 2

| Change | Why |
|---|---|
| **Recommendation changed from 2A to 3A** | v2's prose said "gap weighted most heavily" while its table weighted gap and feasibility equally, manufacturing a spurious tie. Stating the real weight (gap ×3) *and* scoring 2A's feasibility honestly at 3 — its own timeline does not fit 12 weeks — puts 3A first |
| Added a 15-line front matter with the pick, effort, participants and the killer check | v2 gave four different answers to "which project," all past 90% depth |
| Gave 2A a person-hour range, participant counts and the 10–14-weeks-in-a-12-week-box arithmetic | It was the only top-ranked avenue with no numbers, and the sum had never been done |
| Withdrew the "second-hand numbers are marked" claim | They weren't marked. Every number here is second-hand; saying so once is honest, promising markers that don't exist is worse than v1's silence |
| Added 1B and 2A Phase 1+1.5 to the no-ethics-pathway row | The table most likely to be acted on literally was telling teams to drop the top-ranked avenue unnecessarily |
| Added positive controls to 2A, 3B, 5A, 6A; corrected the changelog that claimed they existed | A changelog that overstates is what a reader checks *instead of* the text |
| **Restored friction *dosing* to 4A as a design requirement** | v2's changelog said it was folded in; it wasn't. Worse, dosing is a gap that *survived* the fact-check while 4A's opt-in framing was partly falsified — the surviving claim had been dropped and the weaker one kept |
| Added scoring anchors and polarity ("5 always good"), capacity anchor (~5 h/person/week), target venues, and the pilot costs to the gate table | "Disagree with the cells" is unusable if nobody knows what a 3 means, and estimates are unauditable without a capacity total |

# What changed from version 3 — the verification round

**Eight of the ten week-1 gates were run** by reading the papers in full. The ranking did
not change; two avenues did. **Nothing in the ranking table was affected, so 3A remains the
recommendation** — and its premise is now the best-supported claim in this document rather
than the most exposed one.

| Change | Why |
|---|---|
| **1B's positive control was replaced** | Gate 10: arXiv:2512.18489 needs **output logits and a normative posterior**, and tests only open-weight models. "Replicate the published task-fact decay result" was not runnable on the endpoints this team will use |
| **1B: PersistBench removed from the list of papers occupying the space; the LessWrong post added as the nearest neighbour** | PersistBench measures memory *safety*, not decay. The post — unfetchable when `01` was written — runs a small version of 1B's exact study, including the implicit/explicit contrast |
| **1B's two novelty claims narrowed** (implicit revision; elicited-vs-behavioural) | Both are now partly occupied. Neither is dead; both need restating so a reviewer doesn't find the post first |
| **2A: added the ground-truth scope condition, the DIV_3 referent, and the observed-not-manipulated caveat on 2603.22152** | Gate 2. The paper's cost-of-plurality result was measured where disagreement means *error*. That is the sentence 2A's introduction should be built around |
| **2A: PerSpectra downgraded from "supplies most of the stimulus set" to "supplies the contested third"** | Gate 3. Its topics are contested by construction, its arguments are GPT-4o expansions, and its units are arguments rather than questions |
| **3A: rubric scales, LLM-as-judge scoring, per-metric measurement windows and the public repo added** | Gate 4. All four change how the ladder is built and analysed; none was visible from the abstract |
| **3A's premise confirmed and stated precisely** | The implicit/explicit gap is a two-level paired-*t*-test contrast with no gradation anywhere in the benchmark. The avenue's founding claim is now first-hand |
| **5A: the positive control got a data caveat and two substitutes** | StoryScope releases its AI stories but not its human ones (Books3). The exact replication is not runnable off the shelf |
| **5A: StoryScope's baselines added; the interpretability framing given a precedent** | 93.2% narrative-only sits against 99.9% for a plain ModernBERT. That is the trade this avenue is making, and it is a published one |
| **Gate 9 (logprobs) now gates Idea 1 as well as Idea 5** | Consequence of gate 10. `TEAM-BRIEF` said it mattered only for Idea 5; that was wrong |
| Corrected arXiv:2603.01341's ">94%" from "fabrication rate" to **source-mismatch rate** | Wrong label on a real number, in 5A and in the brief |

# What changed from version 4's own review — round 4

Round 3's verification was put through the same two-critic pass as every other round. It
upheld the citation base and **found nine errors round 3 had introduced.** Record in
`critiques/round-3-full-text-verification.md`.

| Change | Why |
|---|---|
| **2A: the "nobody measured legitimate disagreement" claim is retracted** and Song et al. (2411.04578, CSCW 2025) added | Round 3 minted an unhedged novelty claim off one full-text read; the paper it read cites the falsifier six times. 2A's real gap is still the router |
| **3A's positive control split back into two steps**, with a three-way failure diagnosis | Round 3 replaced "your explicit rung reproduces their values" with "run their code," which tests plumbing rather than the project's actual risk — and simultaneously asserted the failure would and would not be the team's fault |
| **3A: judge model, judge non-validation and model-version drift added** | All three were in the paper round 3 read and none was reported. "You inherit the validity argument" was half true |
| **5A's substitute positive control replaced** | `human` is one of StoryScope's six attribution classes, so "it uses only the released AI half" was impossible |
| **5A: StoryScope's actual cost added ($1,600 extraction, $4.4k all in, two passes)** | The document prices everything else to the dollar; this was the number most likely to kill the avenue |
| **5A: the "it is published" precedent withdrawn** | StoryScope lists no venue. It is an unrefereed preprint |
| **1B: stated plainly that it has no anchored positive control** | Its replacement rests on BeliefTrack, which is search-only, and "same instrument" is not what makes something a control |
| **1B: gate 1's outcome relabelled and a net-effect note added** | Round 3's green tick read as "one problem, fixed." The round was net negative for 1B |
| **1A: PersistBench and PERMA removed from the crowding claim** | The same commit retracted both as occupants elsewhere and missed the one place the claim does work |
| **Stated openly that no scoring cell was changed, and why** | Round 3 wrote "the ranking did not change" as though verification had confirmed the ordering. It tested premises |
| **PerSpectra rebudgeted in person-hours; front matter and version header refreshed** | "~1 week saved" mixed units with a person-hour estimate; the first two screens were still pre-round-3 |
