# Ranked Research Avenues

Up to three avenues per idea, ranked **most → least promising**. Companion to
`01-literature-review.md`; section references (§) point there.

## Ranking criteria

Each avenue is judged on five things, in this order:

1. **Gap size** — is it actually unclaimed after the literature review?
2. **Feasibility for this team** — a part-time incubator team, one semester, mixed
   technical backgrounds (self-rated 1–10), no assumption of GPU training budget.
3. **Falsifiability** — is there a result even if the hypothesis is wrong?
4. **Safety relevance** — does it connect to a real deployed harm?
5. **Scoop risk** — how likely is a bigger lab to publish this first?

## Standing assumptions — flag these if wrong

These shaped the ranking, and I inferred them from the meeting doc rather than being
told. **If any is wrong, the ranking changes.**

- ~1 semester, part-time, ~4–6 people, weekly mentor meeting.
- No budget for large-scale human-subjects recruitment; small-N studies (n≈30–100) via
  Prolific-style panels are plausible but not guaranteed, and would need IRB or an
  equivalent ethics review.
- API access to frontier models; open-weight models runnable at ≤10B on modest hardware.
- **No model fine-tuning at scale.** Any avenue requiring RLHF-style training is out.
- Output is a paper/preprint, a public benchmark, or a demonstrable prototype — not a
  production system.

---

# Idea 1 — Aligning Artificial Minds to Human Wellbeing (AH)

### 🥇 1A. The user-belief forgetting curve: measuring the discount factor on *beliefs about the user*

**Question.** *Large Language Models as Discounted Bayesian Filters* (arXiv:2512.18489)
found that LLM belief updates behave like an exponential forgetting filter with a
**model-specific discount factor**. That was measured on beliefs about *task facts*.
**Does the same hold for beliefs about the user — and is the discount factor different?**

**Why it's promising.** It converts AH's qualitative question ("do they retain artifacts
of old beliefs?") into **one number per model**, measured the same way across models.
Single numbers travel: they are easy to plot, easy to compare, easy to cite. The
methodology is already published, so you are not inventing an estimator — you are
transferring a validated one to a new domain, which is a defensible, reviewable
contribution rather than a from-scratch bet.

**What you'd do.** Build multi-turn dialogues where a user states a belief/preference/goal
at turn *t*, then revises it at turn *t+k*. Probe the model's operative user-belief at
turns *t+k+1 … t+k+n* — both by direct elicitation ("what do you think I believe about
X?") *and* behaviourally (does the recommendation still reflect the old belief?). Fit the
discount curve. Vary *k*, distractor density, and how explicitly the revision is signalled.

**Feasibility. High.** API calls plus scripting. No training. Fully automatable, so no
human subjects and no IRB. The main cost is careful stimulus design, which is exactly the
kind of work the cognitive-science-inclined members of the team can lead without writing
model code.

**Two things that make this better than the obvious version.**
- **Elicited vs. behavioural divergence is the real finding.** Multiple papers (§1.4)
  report models pass explicit belief probes but fail behaviourally. If the discount factor
  differs between the two probes, that gap *is* the paper.
- **Include the implicit-revision condition** (§1.7.3). Every existing benchmark uses
  explicit revision. Implicit revision is untested and is where deployed systems live.

**Main risk.** The three 2026 belief-tracking benchmarks (BeliefTrack, DToM-Track,
BeliefShift — §1.4) are close. **Mitigation:** none of them is about *user* beliefs
specifically, and none fits a forgetting curve. Read all three in week 1 and position
against them explicitly. If one already does this, pivot to 1B.

**Fails if.** The curve is flat or noisy — but note that "beliefs about users are *not*
discounted like task facts" is also a publishable result.

---

### 🥈 1B. Does Bayesian teaching improve multi-turn adaptation to a changing user?

**Question.** The doc asks this directly and, as far as this review found, **nobody has
answered it.** Bayesian teaching (Nature Communications; Google Research blog) improves
probabilistic reasoning and transfers across domains. Does that transfer reach *user*
belief updating in dialogue?

**Why it's promising.** Genuinely open, and the doc's own best question. Composing an
existing training method with an existing eval is a legitimate, well-formed contribution.

**Why it is ranked below 1A.** Feasibility. Doing this properly means fine-tuning, which
is outside the standing assumptions above. There is a cheaper version — prompt-level or
in-context Bayesian scaffolding rather than training — but that tests a **weaker
hypothesis** and reviewers will say so. Be honest about which one you ran.

**What you'd do (cheap version).** Compare (i) baseline, (ii) chain-of-thought, (iii)
explicit Bayesian scaffolding in-context, on the 1A measurement harness. **This makes 1A a
prerequisite, which is a point in favour of doing 1A first.**

**Main risk.** The cheap version answers a different question than the doc asks, and the
expensive version may be out of budget.

---

### 🥉 1C. Multi-user belief tracking: whose belief is the model actually holding?

**Question.** In a group conversation, can a model keep separate, correctly-attributed
belief states per participant — and what happens when two users hold contradictory
beliefs?

**Why it's ranked last.** **GroupMemBench (arXiv:2605.14498, Microsoft Research) already
does much of this** — group dynamics, speaker-grounded belief tracking, audience-adapted
language. Competing with a well-resourced industry lab on their own benchmark is a poor
use of one semester.

**When it becomes worth doing.** If GroupMemBench turns out to measure only retrieval
accuracy and not *contradiction handling* — what a model does when two users it is serving
believe incompatible things — there is a real gap there. **Check first.**

---

# Idea 2 — Cooperative Human-AI Frameworks (AH)

### 🥇 2A. The plurality router: when does showing multiple viewpoints help, and when does it paralyse?

**Question.** Two-part, and the pairing is what makes it good. **(i)** What *do* models
currently do — on what features do they decide to hedge into multiple perspectives vs.
give one answer? **(ii)** What *should* they do — on which question types does plurality
improve human decisions, and where does it just add load?

**Why it's the strongest avenue in this whole document.** The literature review found
plenty of work on *how* to be pluralistic (Overton / distributional / steerable — §2.4)
and essentially nothing on **when to be**. Meanwhile the *cost* side — the doc's
"unnecessary confusion/paralysis" — appears to be **asserted everywhere and measured
nowhere** (§2.6.2). That is an unusually clean gap in a field this busy, and it is exactly
the kind of gap a small team can close, because closing it needs careful experimental
design rather than compute.

**What you'd do.**
- *Phase 1 (no humans, ~3 weeks).* Assemble a question set spanning genuine no-consensus
  items, contested-but-resolvable items, and settled-fact items — **PERSPECTRA
  (arXiv:2602.08716) and the no-consensus set from arXiv:2505.23820 give you most of
  this off the shelf.** Classify each model response as single-answer / hedged /
  explicitly plural. Find the actual decision boundary and test whether it tracks genuine
  contestedness or something spurious (question phrasing, topic sensitivity, safety
  training).
- *Phase 2 (small human study).* Same questions, three presentation formats
  (single answer / plural / plural-with-recommendation). Measure decision quality, time,
  confidence, and **decision avoidance** — the paralysis outcome nobody has measured.

**Feasibility. High for Phase 1** (pure API + annotation). **Medium for Phase 2** — needs
participants and ethics review. **Phase 1 is a complete deliverable on its own**, which
makes this low-risk: if recruitment falls through, you still have a paper.

**Why it beats the alternatives.** It answers the doc's question directly, it has a
built-in fallback, it uses existing benchmarks for the expensive part, and the headline
result ("models hedge on X but should hedge on Y") is legible to a non-technical audience.

**Main risk.** Phase 2 is where the real contribution is and it is the part most likely to
get cut. **Mitigation:** design Phase 1 so its result stands alone, and start ethics review
in week 1, not week 8.

**Watch out for.** The Vaccaro meta-analysis (§2.1) says human-AI combination usually
*loses* on decision tasks. Pick tasks where humans are plausibly better than the model, or
you are measuring the wrong regime and will find nothing.

---

### 🥈 2B. Confidence-conditioned presentation format

**Question.** arXiv:2605.04070 showed confidence-based routing fails at picking *which
answer* to show. Does it work for picking **how to present**? Specifically: when the model
is uncertain, is showing evidence-without-conclusion better than showing a hedged
conclusion?

**Why it's promising.** Directly extends a paper the team already cites, and targets the
doc's own bullet about humans over-relying on reasoning-and-explanation vs. evidence. That
bullet is **more contested than the doc suggests** (§2.3) — which is an opportunity, since
adjudicating a genuine disagreement is a real contribution.

**Why below 2A.** It requires the human study — there is no automated-only version — and
it is a narrower question.

**Main risk.** Model self-reported confidence is poorly calibrated, so the independent
variable is noisy. **Mitigation:** use sampling-based consistency (or semantic entropy,
§5.3) instead of asking the model how confident it is.

---

### 🥉 2C. Does the model take viewpoint feedback, or just capitulate?

**Question.** When a user pushes back on a plural answer ("just tell me what you think"),
does the model *update its policy* or simply comply? Is that distinguishable from
sycophancy?

**Why it's ranked last.** It is the third sub-question in AH's bullet, and it collapses
into the sycophancy literature (§3.3), which is very crowded — SycEval, SYCON-Bench,
Syco-bench, PARROT all measure adjacent things. **Best used as an add-on condition inside
2A, not as a standalone project.**

---

# Idea 3 — Cognitive biases, hallucination & "AI psychosis" (DM)

**Read this before picking anything here.** This is the most crowded idea (§3) and it
carries **real human-subjects risk**. Anything involving vulnerable users, or simulating
delusional content, needs ethics review and a clinical advisor. **Do not run studies with
people in mental-health crisis.** Every avenue below is therefore model-side only.

### 🥇 3A. The implicit/explicit boundary in delusion confirmation

**Question.** psychosis-bench's own headline finding is that models do **significantly
worse when delusional content is implicit** (p < .001) — they confirm more, enable more,
intervene less. **Where exactly is that boundary, and what makes a cue "implicit" enough
to slip past safety training?**

**Why it's promising.** It takes a published finding's *biggest unexplained result* and
makes it the object of study. That is a well-worn, reliable way to do good work in a
crowded field: you inherit the benchmark, the metrics (DCS/HES/SIS) and the validity
argument, and you contribute the mechanism. It is also **directly actionable** — if you
can characterise what makes a cue slip through, that is a concrete input to safety
training, not just a measurement.

**What you'd do.** Build a graded ladder of the same delusional content across explicitness
levels — explicit statement → hedged → metaphorical → purely behavioural/implied. Score
with psychosis-bench's existing metrics. Find where each model's intervention rate falls
off. Cross with sycophancy pressure and with conversation length.

**Feasibility. High.** Model-side, automatable, uses an existing benchmark and existing
metrics. No human subjects. The stimulus-writing is the effortful part and needs care and,
ideally, a clinical reviewer — which is a good task for non-programmers on the team.

**Main risk.** Scoring delusion-confirmation reliably. **Mitigation:** reuse
psychosis-bench's published rubric rather than inventing one, and report inter-rater
agreement on a human-scored subsample.

**Ethics note.** No participants, but you are generating simulated delusional dialogue.
Handle it as sensitive material; do not publish raw generations without review.

---

### 🥈 3B. Cultural misalignment × delusion confirmation — does safety behaviour degrade outside Western contexts?

**Question.** Two literatures the review found that **have not been crossed** (§3.6.5):
LLM recommendations default heavily Western (**91.3%** for attribute-free users,
arXiv:2508.20401), and models confirm delusions at high rates. **Do models offer *fewer*
safety interventions when the same distress is expressed in a non-Western idiom?**

**Why it's promising.** Genuinely unclaimed, high safety relevance, and it converts a
diffuse "cultural bias" concern into a specific, measurable, and consequential question.
It also gives non-Western team members a substantive lead role rather than a consulting one.

**Why below 3A.** Harder to do well. Culturally-varied distress idioms cannot be
machine-translated into existence — you need real cultural knowledge, ideally native
speakers, and getting it wrong produces a **worse-than-useless** result that itself
stereotypes. Scope to two or three cultural contexts the team actually has standing in.

**Main risk.** Confounding language with culture. **Mitigation:** include a same-language,
different-idiom condition to separate the two.

---

### 🥉 3C. Is sycophancy one thing? A construct-validity audit

**Question.** Syco-bench reportedly found **inter-test correlations r < 0.3** across
sycophancy sub-tests (§3.3). If that holds, single-number sycophancy scores are measuring
several unrelated things. **Does the r < 0.3 result replicate across benchmarks
(SycEval, SYCON-Bench, PARROT, DarkBench's sycophancy category)?**

**Why it's interesting.** Construct-validity audits are undervalued and genuinely useful,
and the psychometrics review (arXiv:2505.08245) gives you the method.

**Why last.** It is a methods paper — less compelling for an incubator whose goal is
partly to *demonstrate* something — and the r < 0.3 figure is **currently unverified**
(§3.3). **Verify that number before choosing this.** If it turns out to be wrong or
already-replicated, this avenue evaporates.

---

# Idea 4 — Countering Cognitive Atrophy through Epistemic Design

### 🥇 4A. When do people *choose* friction? (DM's actual question)

**Question.** Every existing prototype (§4.3) **imposes** friction. DM's framing says the
harder problem out loud: *"users will need to choose this higher-friction path when they
deem it appropriate."* **What predicts voluntary opt-in — and can it be designed for?**

**Why it's the best avenue in Idea 4, by a distance.** The review found many Socratic and
friction prototypes and **none studying voluntary adoption** (§4.4.2). This is a real gap
*and* it is the actual deployment blocker: an assistant nobody chooses has no effect size.
It also sidesteps the crowding problem — you are not competing to build a better Socratic
tutor, you are asking a question the tutor-builders have skipped.

**What you'd do.** Build a minimal two-mode assistant — "answer me" and "work it through
with me" — with a visible, always-available switch. Give participants real tasks. Measure
**when** they switch, **what predicts switching** (task type, time pressure, stakes,
self-rated confidence, prior mode), and whether switching correlates with better learning
or retention. The instrument is deliberately simple; the finding is behavioural.

**Feasibility. Medium.** The prototype is a thin wrapper over an API — genuinely a
week or two of work. The study needs participants and ethics review. **A pilot with n≈20
is a real result at incubator scale**, and the two-mode wrapper is a demoable artifact
even before any data comes in — which matters if the deliverable is partly a demonstration.

**Design detail that makes or breaks it.** Default mode and switch salience will dominate
the result. Randomise the default; otherwise you are measuring your own UI choice.

**Main risk.** Everyone picks "answer me" and there is no variance. **Mitigation:** that is
itself the finding, and it is a good one — but hedge by including a manipulation
(stakes framing, or an explicit "you'll be tested on this later") likely to move opt-in.

---

### 🥈 4B. Dosing productive friction

**Question.** "Productive friction" is prescribed everywhere (HES, Scaffolded Cognitive
Friction, the offloading reviews) and **dosed nowhere** (§4.4.3). Is there an inverted-U —
too little and you get offloading, too much and users defect to a frictionless tool?

**Why it's promising.** Turns a slogan into a measurable curve, and the inverted-U is a
clean, legible hypothesis with an interpretable answer either way.

**Why below 4A.** Needs more participants for a dose-response curve than a semester
comfortably supports, and *Socrates went Nuclear* (arXiv:2609.00584, Sept 2026) is already
comparing interaction strategies with neural measurement. **Combines well with 4A** — the
opt-in study naturally produces a friction gradient.

---

### 🥉 4C. A Socratic + CBT/DBT hybrid assistant (DM's original proposal)

**Question.** Does combining Socratic questioning with CBT/DBT structure produce better
reasoning and psychological outcomes than either alone?

**Why it's ranked last despite being DM's stated idea.** Three problems compound:
1. **Crowded on both parents.** Socratic tutors and CBT/DBT chatbots both exist in
   quantity (§4.3, §3.1). The *combination* looks genuinely unbuilt — but "unbuilt
   combination" is a weaker claim than "unanswered question."
2. **Evaluation is the hard part, and it is harder here than anywhere else in this
   document.** "Psychological growth" needs validated instruments and a longitudinal
   design; a one-semester study cannot detect it.
3. **Ethics.** CBT/DBT techniques delivered by an LLM to non-clinical users is a
   regulated-adjacent area needing a clinical advisor.

**How to rescue it.** Fold the CBT/DBT structure in as *one of the modes* in 4A. You get
the design contribution without owing anyone a longitudinal outcome study.

---

# Idea 5 — Deceptive Alignment and Misinformation (DM)

**Pick a lane first.** §5 splits this into (a) detecting AI-authored text, (b) detecting
fabrication, (c) detecting unfaithful reasoning. The avenues below are (a×b), (b), and (c)
respectively. **(c) requires open-weight models.**

### 🥇 5A. Do "researched" and "made-up" LLM outputs differ *structurally*? — DM's question, made precise

**Question.** StoryScope (arXiv:2604.03136) showed that **discourse-level structural**
features beat stylistic ones at separating human from AI fiction (93.2% macro-F1 on
structure alone). **Does the same structural signal separate an LLM's grounded output from
its fabricated output?**

**Why it's the best avenue in Idea 5.** It is a precise, testable version of DM's exact
intuition; it inherits a validated method rather than inventing one; and **the cross-product
is genuinely unfilled** (§5.5.1) — the closest work (the *iScience* Portuguese study,
PMC12969083) crosses human-vs-AI with true-vs-false but at the **lexical** level, not the
structural one. There is a clean, defensible delta.

**What you'd do.** Build paired corpora: same questions answered (i) with retrieval/grounding
and (ii) forced closed-book where the model must confabulate — verified against ground
truth so you *know* which outputs are fabricated. Extract StoryScope-style discourse
features (adapted from narrative to expository text — this adaptation is the intellectual
work). Train a small classifier. Compare against a lexical-feature baseline and against a
semantic-entropy baseline (§5.3) so you know whether structure adds anything over methods
that already work.

**Feasibility. High.** A small fine-tuned classifier is the right tool here and it is
cheap — *Trust at risk* found DeBERTa-v3 at 96–98% where zero-shot LLMs did much worse
(§5.2). This runs on modest hardware and needs no frontier access.

**Main risk.** The signal is real but **redundant** — semantic entropy already detects
confabulation, and better. **Mitigation:** decide up front that the contribution is
*interpretability*, not raw accuracy. Structural features say *how* fabricated text
differs; entropy only says *that* it does. Frame it that way from week 1 and the redundancy
stops being a threat.

**Second risk.** Generalisation. Detectors degrade across topics and under paraphrase
(§5.2). Build a held-out cross-domain test **before** reporting any number.

---

### 🥈 5B. Do surface hedges track internal uncertainty?

**Question.** arXiv:2605.28778 asks whether LLMs use linguistic uncertainty markers to
reflect intrinsic confidence. **Extend it:** measure the gap between verbal hedging and
internal uncertainty across models and domains, and ask whether the *gap* is itself a
usable fabrication signal.

**Why it's promising.** High practical value: users read hedges as calibration signals. If
hedging is decoupled from actual uncertainty, that is a concrete, communicable harm — and
it connects Idea 5 to Idea 2 (how confidence should be presented).

**Why below 5A.** Needs internal access (logprobs at minimum) for the "internal" side, and
one recent paper already occupies the core question — you would be extending, not opening.

---

### 🥉 5C. Chain-of-thought faithfulness — "altering its stated internal logic"

**Question.** The doc's literal framing: detecting when a model's stated reasoning
misrepresents its actual computation.

**Why it's ranked last for *this team*, despite being the most important problem.**
1. **Requires open-weight internals** — activations, circuits, probes (§5.4).
2. **Very crowded and very technical** — FaithCoT-Bench, circuit-guided discrepancy
   detection, information-flow training, and several probe families, mostly from
   well-resourced interpretability groups.
3. **Known methodological trap:** faithfulness scores are sensitive to the classifier used
   to compute them (arXiv:2603.20172). Easy to produce a confidently wrong number.

**When to pick it anyway.** If the team has a strong mechanistic-interpretability member
who wants this, it is the highest-ceiling problem in the document. Otherwise the effort is
better spent on 5A.

---

# Idea 6 — Multi-Layered Trust Framework

**Blunt assessment.** The doc gives this idea no owner and no detail; the literature has
drawn these layers many times (Weidinger et al.'s three-layer sociotechnical framework has
existed since 2023 — §6.1). **Proposing another framework is the lowest-value thing this
team could do.** The avenues below all pivot to *validating* or *filling* existing
frameworks. If nobody on the team owns this idea, drop it.

### 🥇 6A. Fill the cognitive layer — the part every stack leaves thin

**Question.** Existing layered frameworks are strong on identity, provenance and
sandboxing and weak on the **human/cognitive layer** (§6.3.2), yet the four-layer social-
engineering framework (AI & Ethics, doi:10.1007/s43681-026-01265-2) names "cognitive" as
layer one. **What concrete, testable controls belong in that layer?**

**Why it's the best version of Idea 6.** It plays to this team's actual comparative
advantage — cognitive science and behavioural insight — instead of competing with security
and governance groups on their turf. And it **turns Idea 6 into an umbrella for the other
five**: findings from Ideas 1–5 become the cognitive-layer controls.

**What you'd do.** Take one existing published stack. Specify the cognitive layer with
concrete controls (e.g. plurality routing from 2A, friction opt-in from 4A, implicit-cue
detection from 3A), each with a measurable pass/fail test. **Then actually run those tests
on a deployed assistant.** The running is the contribution; the specification alone is not.

**Feasibility. Medium.** Only worth doing *after* at least one of the other avenues has
produced a result to install in the layer. **Best treated as the team's framing/write-up
strategy rather than a standalone workstream.**

---

### 🥈 6B. Trace one cross-layer failure end to end

**Question.** Frameworks assert that model-layer failures propagate into systemic harms.
**Pick one and actually trace it:** sycophancy (model) → delusion reinforcement (user) →
clinical presentation (institution) → norms about AI in mental health (society).

**Why it's promising.** Cross-layer propagation is asserted and rarely traced (§6.3.3),
and a single well-documented causal chain is more persuasive than another taxonomy.

**Why below 6A.** It is a synthesis/case-study contribution. Valuable, but it produces an
argument rather than a measurement, and it depends on evidence others have generated.

---

### 🥉 6C. Empirically validate an existing framework

**Question.** Does a published layered framework actually catch harms it claims to catch?

**Why it matters and why it is last.** It is the biggest gap in the area (§6.3.1) and
**almost certainly too large for one semester** — you would need a deployed system, real
incidents, and a comparison condition. Listed because it is the honest answer to "what
does this field need," not because this team should attempt it.

---

# Overall recommendation across all six ideas

If the team picks **one** project, the ranking that follows from the criteria above:

| Rank | Avenue | Why |
|---|---|---|
| **1** | **2A — Plurality router** | Cleanest unclaimed gap in a busy field; the paralysis cost is asserted everywhere and measured nowhere; Phase 1 stands alone if the human study falls through |
| **2** | **4A — When do people choose friction?** | Answers DM's own hardest sub-question; every existing prototype imposes friction instead of studying opt-in; produces a demoable artifact early |
| **3** | **1A — User-belief forgetting curve** | Fully automatable, no ethics review, transfers a validated estimator to a new domain; verify against the three 2026 belief benchmarks in week 1 |
| **4** | **3A — Implicit/explicit delusion boundary** | Highest safety relevance; inherits psychosis-bench's metrics; needs a clinical reviewer |
| **5** | **5A — Structural signature of fabrication** | Precise version of DM's intuition; cheap to run; frame as interpretability, not accuracy |
| **6** | **6A — Cognitive layer** | Best as the write-up frame for whichever of the above you do, not as a standalone project |

**Two combinations worth considering instead of a single pick:**

- **2A + 4A** — both are "how should an assistant present itself so humans think better?",
  they share a participant pool and one ethics application, and together they make a
  stronger story than either alone.
- **1A + 3A** — both are trajectory measurement over multi-turn dialogue, both fully
  automatable, and they share a measurement harness. This is the right pick if the team
  wants to avoid human subjects entirely.

**The cross-cutting asset (§Cross-cutting, point 2):** Ideas 1, 3 and 4 all need
**multi-turn trajectory measurement**, and all three literatures independently complain
that current benchmarks score endpoints. If the team builds one good trajectory-measurement
harness, it is reusable across three of the six ideas — and that reusability is worth more
than any single result in this document.
