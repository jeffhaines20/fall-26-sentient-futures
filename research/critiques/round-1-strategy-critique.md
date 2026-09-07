# Round 1 Critique — Research Strategy & Reasoning

**Critic role:** adversarial senior-PI review of `02-ranked-avenues.md` (with `01-literature-review.md` as support).
**Verdict: 6/10.** The gap-mapping, the per-avenue "Main risk / Mitigation / Fails if" scaffolding, and several individual calls (Idea 5's "pick a lane," Idea 3's ethics preamble, 3B) are genuinely good — but the overall ranking contradicts the document's own stated criteria, the two top recommendations are underpowered human-subjects studies with no budget, timeline, or power analysis anywhere in the document, and every "nobody has done this" claim that drives the ranking is inherited from a search-only review whose recall caveat is never restated.

---

## MAJOR ISSUES

### 1. The overall ranking does not follow from the stated criteria — and the doc claims it does

Criteria are stated "in this order": gap size, feasibility, falsifiability, safety relevance, scoop risk. But:

| Avenue | Doc's own feasibility label | Doc's own safety label | Rank given |
|---|---|---|---|
| 2A | "High for Phase 1 … **Medium for Phase 2**" | not claimed | **1** |
| 4A | "**Feasibility. Medium.**" | not claimed | **2** |
| 3A | "**Feasibility. High.**" | "**Highest safety relevance**" | **4** |
| 1A | "**Feasibility. High.**" | not claimed | **3** |

By criteria 2 and 4 as written, 3A should be at or near the top. Meanwhile criterion 5 (scoop risk), nominally last in priority, does most of the demotion work (1C, 2C, 5C, part of 4B).

Three criteria are also applied that are not on the list: **demoability**, **legibility to non-technical audiences**, and **institutional fit**. Legitimate for an incubator — but they should be in the list, not smuggled in.

**Fix:** Publish an avenue x criterion scoring table with the three unstated criteria added and explicit weights. If the table produces a different #1 than 2A, either change the ranking or state plainly: "the criteria rank 3A first; I rank 2A first because I weight novelty over safety relevance — here is why." An honest thumb on the scale beats a fake derivation.

### 2. "Phase 1 stands alone" is not true, and the doc's own sentences show it

The promised headline ("models hedge on X but should hedge on Y") contains a "should." The "should" is Phase 2. Phase 1 delivers only a descriptive audit of hedging behaviour, which is (a) adjacent to *Arbiters of Ambivalence* (arXiv:2505.23820), which `01` itself calls "closest existing work to AH's exact question", and (b) built on an existing pluralism benchmark. The doc names the dependency ("Phase 2 is where the real contribution is") one paragraph after denying it.

**Fix:** Rewrite as: "Phase 1 is a publishable *descriptive* result and a necessary input to Phase 2, but it is not the contribution. If Phase 2 is cut, the claim shrinks from 'when models should go plural' to 'what triggers hedging' — decide now whether that shrunken claim is worth a semester." Add a named Phase-1.5 fallback that needs no recruitment (e.g. expert-annotator or LLM-judge evaluation of answer quality under each format).

### 3. 2A's primary outcome cannot be measured on the item class that motivates the study

On genuine no-consensus items there is by construction no ground truth, so "decision quality" is undefined. On settled-fact items plurality is obviously wrong, so the manipulation is degenerate. Only "contested-but-resolvable" supports a decision-quality measure — and that is precisely where the doc's own Vaccaro warning bites, because that is where the model beats a lay participant. The stimulus set, the outcome measure, and the Vaccaro constraint are mutually incompatible, and the doc never notices.

**Fix:** Split outcomes by item class explicitly. No-consensus → calibration, decision avoidance, appropriate uncertainty, stated confidence (no accuracy). Contested-but-resolvable → accuracy, in a domain where participants have real expertise or evidence access (the Vaccaro-compliant regime). Settled-fact → manipulation check only.

### 4. No power analysis anywhere; the one sample-size claim is off by ~an order of magnitude

"power" and "preregist" appear zero times. The only n given is "a pilot with n≈20 is a real result at incubator scale". 4A asks for three inferential things at once. Rough two-sided, 80%, alpha=.05:

- default effect on opt-in, 30% → 45%: **~162 participants total**; 30% → 55%: ~60 total.
- switching↔learning correlation at r=.3: **n ≈ 85**; at r=.4, n ≈ 47.
- any two-group comparison at d=0.5: **~63 per cell**.

At n≈20 with a randomised default that is ~10 per cell — roughly 18% power for a medium effect. It also sits below the document's own stated floor of "n≈30–100". 2A Phase 2 is worse: a one-way three-group design needs ~159 total for a medium effect.

**Fix:** Either (a) reframe n≈20 explicitly as descriptive/qualitative, or (b) state the real n, price it (Prolific ~$12/hr x 20 min x 160 ≈ **$700–900 plus fees**), and say who pays. Add a power note and target effect size to every human-subjects avenue, and recommend preregistration.

### 5. There is no budget, no timeline, and no week-1 plan — for a team told to decide in a week

"hour", "deadline", "dataset" appear zero times. Cost is mentioned three times, never with a number. Week-1 instructions are scattered across five sections and never collected.

Fall semester from Sept 1 ≈ 14 weeks; decision consumes weeks 1–2. For 2A: ethics submission needs a finalised protocol, consent form, and often CITI training for every listed researcher; even expedited/exempt review typically returns **2–6 weeks after submission**. Phase 1 at "~3 weeks" (optimistic), Phase 2 build 2wk + run 2wk + analysis 2wk. That is a ~13-week critical path with zero slack.

Also unaddressed: **does this team have IRB access at all?** An incubator is usually not an IRB-holding institution. "IRB or an equivalent ethics review" papers over the difference between university coverage, a paid independent IRB ($1–2k), and no pathway at all.

**Fix:** Add a one-page "Week 1 / Week 2" section collecting the five verification tasks, the ethics-pathway question, and the API-budget question. Add per-avenue estimates in **person-hours**, and a named kill-gate.

### 6. Every top avenue is a measurement study; the source doc repeatedly asked for guardrails, prevention, and prototypes

From `00-source-ideas.md` verbatim: Idea 1 is "translating cognitive science and behavioral insights into **algorithmic guardrails**"; Idea 4 is "design a blueprint or **interactive prototype**"; Idea 5 is "develop methods to **detect and prevent**"; DM's Idea 3 is "**countering** characteristics that lead to hallucinations/psychosis"; Idea 6 is "Research or **design** a deployment framework."

Of 18 avenues, exactly one produces an artifact (4A's wrapper) and one proposes running tests (6A). Every #1 avenue is descriptive. The intervention half of the brief has been dropped without justification. An incubator demo day rewards a thing you can show — and the doc concedes this in passing, then ranks measurement studies 1, 3, 4, 5.

**Fix:** Add a "measurement vs. intervention" line to each avenue, and for the top three name the *smallest* intervention the measurement licenses (2A → implement a prompt-level plurality router and A/B it; 3A → an implicit-cue detector evaluated on your own ladder).

### 7. DM's "inherit and/or exploit cognitive biases" clause gets zero avenues

`01` covers it properly (§3.4). `02` generates 3A, 3B, 3C — all from the *second* clause. The first produces nothing. Worse, the most interesting version — **exploit** — is untouched: "does the model amplify the *user's* anchoring/confirmation bias across a multi-turn conversation?" is bias *transmission*, not possession; model-side, automatable, on the team's home turf, and §3.4's own caveat is an argument that transmission is the under-studied direction.

**Fix:** Add an avenue on bias transmission/amplification in dialogue, and say which of DM's two clauses each avenue serves.

### 8. 4A is a reframe of DM's idea presented as DM's idea

DM wrote: "can possibly be based on combinations of socratic reasoning framework and talk therapy (e.g., CBT/DBT) frameworks. **However**, users will need to choose this higher-friction path when they deem it appropriate."

The clause after "However" is a *caveat on DM's proposal*, not DM's research question. DM's proposal is the Socratic+CBT/DBT hybrid — ranked **last in its own idea** (4C). The author promoted a subordinate clause to "DM's actual question" and ranked it #2 overall while ranking DM's main clause last.

The reframe may be correct — 4C's reasoning is sound. The problem is attribution. In a five-person team where DM will be a co-author, telling DM his caveat was his real question is how you lose a teammate's buy-in in week 2.

**Fix:** Relabel as "a reframe of DM's caveat — DM should confirm this is the question he wants," and note explicitly that this ranks DM's stated proposal last and that call belongs to DM at the next mentor meeting. Add **owner buy-in** as a ranking criterion — in a volunteer part-time team it is arguably the strongest predictor of completion.

### 9. 5A rests on a confounded label, a benchmark number from a different task, and a "validated method" the doc says must be rebuilt

**(a) The class label is the experimental condition, not the construct.** Retrieval-augmented generations have loud surface tells (citation-shaped phrasing, quotation, source hedging, length). A classifier trained on grounded-vs-closed-book learns "was retrieval in the context," not "is this fabricated." And "verified against ground truth" does enormous unacknowledged work: grounded outputs still contain fabrications, closed-book outputs are often correct. Verifying fabrication properly means atomic-claim decomposition — a FActScore-scale annotation pipeline, which is *the* cost and is nowhere in the estimate.

**(b) The feasibility number is from a different task.** The 96–98% DeBERTa figure is on *product reviews* — short, formulaic, authorship-cued. `01`'s own §5.2 warns detectors "degrade on short texts, across topics, and under paraphrase."

**(c) The "inherited method" is conceded not to exist.** "adapted from narrative to expository text — this adaptation is the intellectual work" vs. "it inherits a validated method rather than inventing one." Both are stated; neither is reconciled.

Also: this is the most technical avenue in the document and is graded "Feasibility. High." For a team where some members self-rate 1–2, it concentrates work on one or two people.

**Fix:** Make per-claim verification (or a paraphrase control stripping RAG surface tells) a *precondition*; state annotation cost in person-hours; downgrade to "Medium, and only if ≥1 member has trained a transformer classifier before"; drop the DeBERTa number as evidence of feasibility for *this* task.

### 10. 1A's backbone is an unread paper, and "discount factor" may not be well-defined for user beliefs

`01` states "No paper below was read in full." arXiv:2512.18489 carries no verification flag but was not read — so "transferring a validated estimator" is an inference from a search snippet, load-bearing for a top-3 avenue.

Deeper: a discount factor in a Bayesian-filter framing is defined *relative to a normative posterior*. For task facts that exists. For "beliefs about the user" it generally doesn't — after the user says "actually I prefer X now," the normatively correct belief is just X. The described design yields a **persistence/decay curve for a step change** — a fine measurement, but "discount factor" imports formalism the design doesn't earn.

Compounding: the mitigation ("If one already does this, pivot to 1B") points at an avenue the same document declares infeasible.

**Fix:** (i) Make "read 2512.18489 and confirm what the estimator needs" an explicit week-1 gate with a stated fallback. (ii) Rename the measurand: "belief-persistence half-life for user-model states." (iii) Add a **positive control** — replicate the published task-fact result with your own harness first; without it a flat curve is indistinguishable from a broken measurement. (iv) Replace "pivot to 1B" with a feasible fallback.

### 11. Falsifiability is being satisfied by relabelling nulls as findings

"Fails if. The curve is flat or noisy — but note that [the null] is also a publishable result." / "Everyone picks 'answer me' … that is itself the finding."

Criterion 3 is falsifiability; answering it with "any outcome is a result" defeats it. A flat curve is equally consistent with a broken elicitation protocol. A 100% "answer me" rate at n≈20 with one UI is a ceiling effect attributable to your own defaults — the doc says so one line later ("Default mode and switch salience will dominate the result"). You cannot both claim the default dominates and claim a no-variance outcome is informative.

Also the 4A hedge ("you'll be tested on this later") converts *voluntary* opt-in into *incentivised* opt-in — the very thing the avenue exists to distinguish from prototypes that impose friction.

**Fix:** Require a **positive control** in every "Fails if" block — a condition where the effect must appear if the instrument works. State the distinguishing test between "real null" and "failed measurement." Move the incentive manipulation into a separate arm.

### 12. `02` drops `01`'s methodology caveat while depending entirely on it, and cites `01` as if it were evidence

`01` is admirably explicit: "No paper below was read in full"; "Recall is incomplete… expect meaningful papers to be missing, especially… ACL/NeurIPS/CHI proceedings not surfaced by general web search"; "treat this as a map of where to dig, not as a citable evidence base."

`02` restates none of it, has no method section, and its criterion #1 is "gap size" — the criterion the method is least able to support. It states negatives at maximum confidence ("essentially nothing", "measured nowhere", "none studying voluntary adoption", "genuinely unfilled", "nobody has answered it", "genuinely unclaimed"), each followed by a § pointer to `01` — but those sections are the *same author's inferences from the same search*. The citation looks like corroboration and is self-reference.

Flagging is also inconsistent: 3C's r<0.3 is marked unverified, but 3A's founding premise (psychosis-bench implicit p<.001), 3B's 91.3%, and 5A's 93.2% are presented as settled and are equally second-hand. An avenue whose founding premise evaporates costs a semester.

**Fix:** Add an inherited-limitations block at the top of `02`, plus: "every 'nobody has done X' means 'this search did not surface X.' Before committing, run a targeted search of ACL/EMNLP/CHI/NeurIPS proceedings and forward-citations on the two nearest papers." Mark every second-hand load-bearing number, and name for each top avenue **the single premise whose falsification kills it**.

---

## MINOR ISSUES

1. **n≈20 is below the doc's own floor** of "n≈30–100". Pick one.
2. **6A is graded feasible and sequenced impossibly** — only worth doing after a full semester project, and "run those tests on a deployed assistant" is a second project.
3. **6A is a category error** in a list headed "if the team picks one project" — it is a write-up strategy, not an avenue.
4. **The overall table is structurally constrained**, containing exactly the #1 of each idea, so it cannot surface a case where 1B or 3B beats another idea's winner.
5. **Phase 1 annotation is treated as free** — hedged vs. plural is not a crisp distinction; needs a codebook, double-coding, and a reliability statistic. 3A demands IRR; 2A, where annotation *is* the method, demands nothing.
6. **"~3 weeks" for 2A Phase 1 is optimistic**; budget 5–7 weeks or cut the model count.
7. **"needs no frontier access" (5A) trades against safety relevance** — a signature from a ≤10B open model may not be the one deployed systems produce.
8. **Semantic-entropy baseline and 5B's logprobs assume API affordances** several frontier APIs restrict.
9. **3B is not purely model-side**, contra the section preamble ("ideally native speakers" is at minimum an ethics-consultation question).
10. **Model-version drift is unflagged** — pin model snapshots and record dates.
11. **No target output per avenue** — no venue, no deadline. Workshop deadlines are what actually set scope.
12. **The "2A + 4A" combination adds scope while being sold as de-risking** — they share no stimuli, task design, outcome measures, or analysis.
13. **`00-source-ideas.md` overstates its fidelity.** It says "Extracted verbatim," but the heading "Idea 3 — (DM) Inherited/exploited cognitive biases…" is authored, not extracted: in the source .docx, DM's bullet has no title and sits at the same list level as the five *titled* ideas. The "six ideas" framing is itself an editorial construction.

---

## WHAT WORKS — preserve these

- **The per-avenue structure** (Question / Why promising / Why ranked here / What you'd do / Feasibility / Main risk + Mitigation / Fails if). Very few research memos state a falsifier at all.
- **§1.1's correction of arXiv:2405.18870** — the single most valuable thing in either document.
- **"Pick a lane first"** for Idea 5 — the sharpest conceptual move in the pair, and "(c) requires open-weight models" is exactly the kind of hard fact a team needs.
- **Idea 3's ethics preamble**, stated before any avenue. Right call, right place.
- **Naming the live competitor** (SPAR Fall 2026) and instructing the team to check its status.
- **Constructive demotions rather than deletions** — folding 4C into 4A as a mode, 2C into 2A as a condition.
- **3B (cultural misalignment x delusion confirmation)** — most original avenue, correctly risk-flagged and correctly scoped.
- **The cross-cutting asset argument** (one trajectory-measurement harness reusable across three ideas) — best strategic sentence in the document; promote it.
- **The Vaccaro meta-analysis as a hard constraint.**
- **The standing-assumptions block existing at all**, with "If any is wrong, the ranking changes."

---

## MISSING AVENUES

1. **Observational analysis of existing public interaction corpora. (Strongest omission.)** "dataset", "WildChat", "LMSYS" appear zero times in `02`. Public multi-turn corpora let the team measure stale-belief artifacts, sycophancy escalation, and single-vs-plural answering **in real conversations** with no recruitment, no payment, no IRB (public secondary data is typically exempt), and annotation-heavy work that gives every non-programmer a substantive role. Cheapest route to a novel empirical result; directly serves AH's "more dynamic conversations" and DM's "during interactions."
2. **A human baseline / human-vs-model comparison.** No avenue collects human data as a *comparison* to model behaviour. arXiv:2607.28347 already provides the template (391 participants updating stances) and its finding is a human-model gap.
3. **Individual differences as moderators.** Need for Closure (paralysis), Need for Cognition (friction opt-in), trust-in-automation, decision-avoidance — validated, free, five minutes, and **statistically more efficient at small n** than between-group comparisons. The team's home discipline, entirely absent.
4. **A qualitative / think-aloud arm.** "Qualitative" appears once, as a pejorative. Think-aloud at n≈12–20 is *methodologically appropriate* at that sample size — unlike the underpowered quantitative designs proposed at n≈20 — needs zero ML skill, and is the mechanism-level evidence the paralysis hypothesis needs first.
5. **Bias transmission/amplification** (serves DM's dropped clause).
6. **A scoped conceptual replication of a contested result.** A behavioural-only replication of Kosmyna et al. (no EEG — essay quality, recall, self-reported ownership) is feasible, legible, high-value in a field with a replication deficit, and well-matched to a mixed-skill team.
7. **An artifact deliverable with a reliability study.** Turn findings into a cognitive-layer evaluation rubric, then test whether independent raters apply it consistently (report kappa). This is 6A made feasible, produces the "blueprint" the source doc asked for twice, and is annotation-based rather than engineering-based.
