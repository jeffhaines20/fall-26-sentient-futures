# Literature Review: Recent Work on the Six Sentient Futures Team Ideas

**Prepared:** September 2026 · **Scope:** work published roughly 2023–September 2026, weighted heavily toward 2025–2026.

---

## How to read this document

### Flags

| Flag | Meaning |
|---|---|
| **[REVIEW]** | Systematic review, scoping review, or survey. **Read these first** — fastest way to get to the state of a field. |
| **[META-ANALYSIS]** | Quantitative meta-analysis with pooled effect sizes. Strongest evidence class here. |
| **[BENCHMARK]** | A dataset/eval harness you could actually run. Cheapest path to a result. |
| **[PREPRINT]** | Not peer-reviewed. Treat findings as provisional. |
| **[⚠️ UNVERIFIED]** | Could not confirm details beyond a search-result summary — check before citing. |
| **[⚠️ CONTESTED]** | The finding has a published rebuttal or a serious methodological critique. |

### Method and its limits — read this before trusting any citation below

Search worked in this environment; **direct page fetching did not**. `arxiv.org`,
`nature.com`, `lesswrong.com`, `semanticscholar.org` and similar domains are blocked by
this session's network egress policy, so:

- **No paper below was read in full.** Titles, authors, dates, venues and headline
  numbers come from search-engine result summaries, abstract aggregators, and
  publisher landing-page snippets.
- **Numbers quoted are the numbers those summaries reported.** Effect sizes, accuracy
  figures and sample sizes are second-hand. Anything you plan to build on, or put in a
  writeup, should be checked against the actual PDF.
- **Existence of the paper is well-corroborated; interpretation is not.** Where a
  claim rests on one summary I have marked it [⚠️ UNVERIFIED].
- **Recall is incomplete.** This is a broad sweep of six fields in one pass, not a
  PRISMA-style systematic review. Expect meaningful papers to be missing, especially
  non-English work, ACL/NeurIPS/CHI proceedings not surfaced by general web search,
  and anything published in the last few weeks.

**Practical implication for the team:** treat this as a map of where to dig, not as a
citable evidence base. Before the project is written up, someone should pull the PDFs
for the ~15 papers you actually depend on.

### Revision history — what a fact-check changed

This document was reviewed by an adversarial fact-checking pass that spot-checked 50+
citations. **It found no fabricated papers and no invented arXiv IDs**, and the quoted
numbers were overwhelmingly exact. It did find the following, all now corrected in place
and flagged where they appear:

| What was wrong | Where | Now |
|---|---|---|
| Told AH the doc misread arXiv:2405.18870 | §1.1 | Downgraded to a question — the sentence is ambiguous, not wrong |
| Told the team a bullet was unsourced when it is stated verbatim in their own citation | §2.3 row 2 | Marked **Supported** |
| Said a second bullet was "more contested than the doc implies" | §2.3 row 3 | Marked **Supported**; the contested part is the wider literature, not their cite |
| Attributed the folie à deux paper to "Morrin et al." | §3.1 | **Dohnány et al.** |
| Reported the BMC Geriatrics meta-analysis backwards | §3.1, App. A | Depression **improved**; loneliness was the null |
| Called the plurality/"paralysis" cost unmeasured | §2.6 | **Retracted** — arXiv:2603.22152 (CHI 2026) measures it |
| Attributed the explicit-vs-behavioural ToM gap to the wrong papers | §1.4 | Re-attributed to SimpleToM and T4D |
| Attributed HumanAgencyBench's finding to an unpublished SPAR project | §4.3 | Corrected, HAB added |
| Over-generalised a 91.3% figure | §3.5 | Scoped to one model, one domain |
| Described a supply-side search audit as a user-behaviour study | §2.5 | Corrected |
| Filed an empirical study as a review | §1.2, App. A | Reclassified |

**Three of those were wrong corrections of teammates.** If you read an earlier version of
this file, those are the parts to re-read.

**A second fact-checking round** verified all thirteen of those fixes landed correctly
(author lists, effect sizes and scope statements all re-checked against sources) and
verified 24 of the ~25 newly added works. It found four further problems, now also fixed:

| What was wrong | Where | Now |
|---|---|---|
| A Perspective piece described as "the empirical companion" and filed under an evidence heading | §2.5 | Flagged `[REVIEW]`, described as conceptual with no data |
| *Choose Your Agent* described as giving "free per-turn choice among three modalities" | §4.3 | One modality per game; the choice is use-vs-not. It is a weaker pre-emption than stated |
| A study whose headline is a **null** listed under work that "measures the cost of plurality" | §2.5 | Null stated explicitly |
| arXiv:2606.02976 described as time-based decay weighting | §1.5 | It uses a Bayes factor |

Plus smaller corrections: JMIR Mental Health is volume **13**, not 27; arXiv:2605.06915 is
Apple and Stanford (no Princeton); the "non-Bayesian beats Bayesian" claim is **confirmed**
and its unverified flag lifted; *When Friction Helps* is a **blockchain** study, which
matters for how far it transfers; the depression effect in the commercial-chatbot
meta-analysis comes from **18 RCTs, N = 3,170**, not the headline N of 110,594.

---

# Idea 1 — Aligning Artificial Minds to Human Wellbeing
### (AH's framing: do LLMs track and update user beliefs/desires/goals?)

## 1.1 A question for AH about one citation (not a correction)

> *An earlier draft of this review called this a misreading. That was over-confident —
> a fact-check found the sentence is ambiguous, not wrong. Rewritten.*

The doc says: *"Previous work has argued that LLMs are **not** capable of true Theory of
Mind ... despite their capacity to match human performance on higher-order ToM
benchmarks (arxiv.org/abs/2405.18870)."*

**The citation sits at the end of a sentence with two clauses, and it fits one of them
but not the other.** **arXiv:2405.18870 is Street et al., "LLMs achieve adult human
performance on higher-order theory of mind tasks"** (Google DeepMind /
Oxford / Johns Hopkins; Winnie Street, John Oliver Siy, Geoff Keeling, Adrien Baranes,
Benjamin Barnett, Michael McKibben, Tatenda Kanyere, Alison Lentz, Blaise Agüera y Arcas,
Robin Dunbar). It introduces the **MoToMQA** benchmark and
reports the *positive* result: GPT-4 and Flan-PaLM reach adult or near-adult performance,
and GPT-4 exceeds adults on 6th-order inferences (93% vs 82%). It is the paper making the
capability claim, not the skeptical one.

So:
- If the cite was meant to support **"despite their capacity to match human performance
  on higher-order ToM benchmarks"** — the clause immediately before it — **it is exactly
  right**, and nothing needs changing.
- If it was meant to support **"previous work has argued that LLMs are *not* capable of
  true ToM"**, it is the wrong paper, and §1.2's reviews are the ones that make that
  argument.

**AH — which did you mean?** Either way, cite the peer-reviewed version rather than the
preprint: *Frontiers in Human Neuroscience* (2025), doi:10.3389/fnhum.2025.1633272.

## 1.2 Reviews and surveys — start here

- **[REVIEW]** *A Systematic Review on the Evaluation of Large Language Models in Theory
  of Mind Tasks* — arXiv:2502.08796 (Feb 2025). Taxonomises ToM benchmarks by
  cognitive-science construct; central theme is that LLMs show emerging competence but
  significant gaps remain in emulating human mental-state reasoning. **This is the
  single best entry point for Idea 1.**
- **[REVIEW]** Marchetti, Manzi, Riva, Gaggioli & Massaro (2025), *Artificial
  Intelligence and the Illusion of Understanding: A Systematic Review of Theory of Mind
  and Large Language Models* — *Cyberpsychology, Behavior, and Social Networking*,
  doi:10.1089/cyber.2024.0536 (PMID 40333375). Finds LLMs do well on first-order false
  belief but degrade on second-order and recursive inference; flags that benchmark
  adaptation to LLMs undermines comparability with human ToM data. **This is the
  "illusion of understanding" argument the doc was reaching for.**
**Not a review, despite an earlier draft filing it as one:** *Do Large Language Models
Possess a Theory of Mind? A Comparative Evaluation Using the Strange Stories Paradigm* —
arXiv:2603.18007 (Babarczy, Lukacs, Vedres, Bujka). It is an **empirical study** testing
five LLMs against human controls. Useful, but not an entry point.

## 1.3 Does an LLM update like a Bayesian? — the doc's core sub-question

This turns out to be a genuinely active 2025–2026 literature, and the answer has
converged to something more interesting than yes/no: **LLM updates look Bayesian in
aggregate but are not Bayesian in any individual trajectory, and they systematically
over-discount old evidence.**

- *LLMs are not (consistently) Bayesian: Quantifying internal (in)consistencies of LLMs'
  probabilistic beliefs* — arXiv:2605.06915 (May 2026; Chen, Jörke, Goliński,
  Fedzechkina, Sapiro, Williamson, Foti — Apple, plus academic co-authors). *Cited in the
  doc.* Introduces the "information processing gap" (deviation from a Bayes update).
  Some elicitation methods yield near-Bayesian updates, others a learned heuristic.
  One further claim — that **the non-Bayesian heuristic updates often *outperform* exact
  Bayesian computation on downstream task performance, indicating the LLMs' probabilistic
  models of the world are misspecified** — is the most interesting thing here and is
  **confirmed** against the authors' own research page. *(An earlier draft flagged this as
  uncorroborated; that flag is lifted.)*
- *LLMs are Bayesian, in Expectation, not in Realization* — arXiv:2507.11768 (Jul 2025;
  Chlon, Rashidi, Khamis, Awada). *Cited in the doc.* Transformers violate the
  martingale property (a hard requirement of Bayesian updating on exchangeable data),
  but the authors argue this targets a structural invariant rather than the operational
  prediction quantity. Note this is a **theory paper with GPT-3-era validation** — its
  empirical base is dated relative to the rest of this list.
- *Are LLM Belief Updates Consistent with Bayes' Theorem?* — arXiv:2507.17951. Direct
  companion question; not in the doc, should be.
- *Large Language Models as Discounted Bayesian Filters* — arXiv:2512.18489. **The most
  directly useful result for AH's question:** LLM belief updates are better described as
  an *exponential forgetting filter with a model-specific discount factor* than as a
  Bayesian posterior — i.e. systematic discounting of older evidence. This is a concrete,
  measurable parameter, and it gives you a quantity to compare across models.
- **Bayesian teaching** — Nature Communications doi:10.1038/s41467-025-67998-6 (preprint
  arXiv:2503.17523), plus the Google Research blog post *Teaching LLMs to reason like
  Bayesians* (Mar 2026) *cited in the doc*. Training LLMs to mimic a normative Bayesian
  model improves probabilistic reasoning **and transfers across domains**. The doc asks
  whether this would improve multi-turn adaptation to changing users — **that specific
  question appears to be genuinely open.**

## 1.4 Belief tracking and updating in multi-turn dialogue — the crowded part

This is where AH's idea is most at risk of duplicating existing work. A cluster of
2026 benchmarks already targets close to exactly this:

- **[BENCHMARK]** *When Should Models Change Their Minds? Contextual Belief Management in
  LLMs* — arXiv:2605.30219. Introduces **BeliefTrack**, with a finite belief space and
  symbolic verifiers giving *exact turn-level* evaluation, and — importantly — a failure
  taxonomy: **Failed Stay / Failed Update / Failed Isolation**. That taxonomy is close to
  the "does it retain artifacts of old beliefs?" question in the doc.
- **[BENCHMARK]** *Dynamic Theory of Mind as a Temporal Memory Problem* — arXiv:2603.14646.
  **DToM-Track** tests recalling beliefs held *before* a change, inferring beliefs after,
  and identifying *when* revision occurred. Also close to the doc's question.
- **[BENCHMARK]** *BeliefShift: Benchmarking Temporal Belief Consistency and Opinion Drift
  in LLM Agents* — arXiv:2603.23848. Multi-session; tracks Temporal Belief Consistency,
  Contradiction Detection, Evidence-Driven Revision.
- **[BENCHMARK]** *OmniToM: Benchmarking Theory of Mind in LLMs via Explicit Belief
  Modeling* — arXiv:2605.26322. 895 stories, 22,343 labeled belief propositions;
  evaluates the *intermediate* mental-state representation, not just the endpoint answer.
- **[BENCHMARK]** *GroupMemBench: Benchmarking LLM Agent Memory in Multi-Party
  Conversations* — arXiv:2605.14498 (Microsoft Research). **Directly occupies the
  multi-user extension named in the doc**: group dynamics beyond concatenated 1:1 chats,
  speaker-grounded belief tracking, audience-adapted language.
- *Language Models use Lookbacks to Track Beliefs* — arXiv:2505.14685. Mechanistic
  account of the internal circuit doing belief tracking. Useful if you want a
  *mechanism* claim rather than a behavioural one.
- *Beyond the Assistant Turn: User Turn Generation as a Probe of Interaction Awareness* —
  arXiv:2604.02315. Clever methodology: probe the model's user-model by making it
  generate the *user's* next turn.

**The finding this idea actually rests on — with its real sources.** An earlier draft
attributed "models pass explicit belief probes but fail behaviourally" to the 2026
benchmarks above. **That attribution was wrong** — DToM-Track in fact reports the
*opposite* asymmetry (models infer an agent's *current* belief reliably but struggle to
retrieve *prior* belief states). The explicit-vs-applied gap is real and well-evidenced,
but its canonical sources are these, and both were missing from the first sweep:

- **[BENCHMARK]** **SimpleToM** — arXiv:2410.13648 (ICLR 2026), *Exposing the Gap between
  Explicit ToM Inference and Implicit ToM Application in LLMs*: models "often reliably
  infer mental state, but fail at applying knowledge about the mental state for secondary
  predictions." **This is the paper avenue 1A depends on — read it first.**
- **T4D** — arXiv:2310.03051, *How FaR Are Large Language Models From Agents with
  Theory-of-Mind?* Models track beliefs but fail to convert that into action.

"Contextual inertia" — failure to revise an earlier inference despite later contradictory
evidence — is separately reported and is the dominant failure mode in the 2026 benchmarks.

## 1.5 The applied/personalisation version of the same question

Framed as personalisation rather than ToM, this literature is more mature and more
damning:

- **[BENCHMARK]** **PrefEval** — arXiv:2502.09597 (**ICLR 2025 Oral**); 3,000
  preference-query pairs, 20 topics, 10 models, contexts up to 100k tokens. Headline:
  **accuracy drops below 10% after ~10 turns (~3k tokens) in nearly all models** — this
  is **confirmed**, with the qualifier that it holds **in the zero-shot condition.**
- **[BENCHMARK]** *Do LLMs Recognize Your Latent Preferences?* — arXiv:2510.17132.
  Tri-agent (User–Assistant–Judge) framework, turn-level evaluation of elicitation and
  adaptation, three settings including 20-Questions.
- **[BENCHMARK]** *AlpsBench* — arXiv:2603.26680. Real-dialogue memorisation + preference
  alignment; explicitly names **preference drift** and retrieval reliability under
  interference as unsolved.
- *Drift No More? Context Equilibria in Multi-Turn LLM Interactions* — arXiv:2510.07777.
  Argues most benchmarks are blind to temporal misalignment because they score end-task
  success or per-turn quality, never the trajectory.
- *Know Me, Respond to Me* — arXiv:2504.14225. Dynamic user profiling at scale.
- **⚠️ Directly occupies the space avenue 1A wants — all missed by the first sweep:**
  - **CAPTURE** — arXiv:2609.02265 (2 Sep 2026), *Disentangling Preference Drift from
    Memory Poisoning in Personalized LLM Agents*. Formulates user-belief tracking as "a
    continuous-time partially observable decision process over latent user state" with a
    **neural differential-equation belief tracker** and a multi-timescale memory ledger.
    It also independently makes the point below about stale ≡ poisoned beliefs. **Anyone
    considering avenue 1A must read this first.**
  - **PersistBench** — arXiv:2602.01146, *When Should Long-Term Memories Be Forgotten by
    LLMs?*
  - **PERMA** — arXiv:2603.23231, *Benchmarking Personalized Memory Agents*; positional
    probing to diagnose recency bias, catastrophic forgetting, context saturation.
  - *Memory Retrieval for Changing Preferences* — arXiv:2606.02976. Uses a **Bayes factor**
    (how much including a turn improves the likelihood of the reference response) as a
    unified signal for memory access and selection — **not** time-based decay weighting, as
    an earlier draft stated.
- **Memory poisoning (adversarial cousin of "stale belief artifacts")**: *MemoryGraft*
  arXiv:2512.16962; *From Untrusted Input to Trusted Memory* arXiv:2606.04329; *Memory
  Poisoning Attack and Defense on Memory Based LLM-Agents* arXiv:2601.05504. Key framing
  from this line: **existing defenses detect malicious actions, not corrupted beliefs.**
  A "stale belief" and a "poisoned belief" are the same measurement problem.

## 1.6 The doc's other Idea-1 citations, verified

- **arXiv:2607.28347** — *LLMs struggle to simulate human belief updates in controlled
  environments* (Pohl, Mehta, Mambayil, Ghafoor, Lesigang, Hou, Hilbe; IT:U Austria;
  30 Jul 2026). Confirmed, and the doc's summary is nearly accurate: overrepresentation
  of neutral positions, more frequent but smaller belief shifts than humans, and a failure
  to rank comments — though the paper's wording is failure to rank **by relevance to
  belief updates**, not "by convincingness." Ground truth = 391 UK Prolific participants
  updating stances on three topics after reading Reddit comments. Two nuances the doc
  omits: **only two of the six models (Qwen3-32B, GPT-5-Mini) match the human post-stance
  distribution, and only when given participants' actual initial stances**; all six fail
  to generate plausible initial stances themselves.
- **LessWrong post "Do LLMs change their minds about their users, and know it?"** —
  **[⚠️ UNVERIFIED]**, could not be fetched (domain blocked). Also note: LessWrong is not
  peer-reviewed. Fine as inspiration, weak as a citation.

## 1.7 What is actually still open in Idea 1

1. **The forgetting-curve question — narrower than an earlier draft claimed.** The
   "discounted Bayesian filter" result gives a *parameter* (a discount factor) measured on
   beliefs about task facts. An earlier draft said nobody had measured decay for **beliefs
   about the user**; adversarial search falsified that — CAPTURE, PersistBench, PERMA and
   arXiv:2606.02976 all work in this space, and BeliefShift covers user opinion drift with
   2,400 human-annotated multi-session trajectories. **What may still be open is the
   specific move of fitting an exponential-discount curve and reporting a single
   comparable parameter per model.** That is a much smaller claim, and it needs checking
   against CAPTURE before anyone commits to it.
2. **Does Bayesian teaching fix user-belief updating?** The doc asks it; nobody has
   answered it. The training method exists; the multi-turn user-adaptation eval exists;
   the composition has not been done.
3. **Subtle vs. explicit belief change.** Every benchmark found uses *explicit* revision
   ("actually, I've changed my mind"). Implied, gradual, or behaviourally-signalled
   change is untested.
4. **Stale-belief artifacts after acknowledged change.** BeliefTrack's "Failed Stay /
   Failed Update" is the closest, but measures task beliefs, not persona/user beliefs.

---

# Idea 2 — Cooperative Human-AI Frameworks
### (AH's framing: a "pluralistic oracle" — when should an LLM show multiple viewpoints?)

## 2.1 The one number the whole team should know

- **[META-ANALYSIS]** Vaccaro, Almaatouq & Malone (2024), *When combinations of humans and
  AI are useful: A systematic review and meta-analysis* — **Nature Human Behaviour**,
  doi:10.1038/s41562-024-02024-1 (preprint arXiv:2405.06087). **106 experimental studies,
  370 effect sizes.** Headline: on average, **human–AI combinations performed
  significantly *worse* than the best of human or AI alone.** Critical moderators: losses
  concentrated in **decision-making** tasks, gains in **content-creation** tasks; and
  combination helps when the *human* outperforms the AI, hurts when the *AI* outperforms
  the human.

This is the strongest evidence in this entire review and it constrains every "AI
interface for better human outcomes" project. Any Idea-2 proposal should state
explicitly which side of that moderator it is betting on.

## 2.2 The doc's two Idea-2 citations, verified

- **arXiv:2510.26518** — *Human-AI Complementarity: A Goal for Amplified Oversight*.
  Confirmed; positions complementarity as a scalable-oversight goal.
- **arXiv:2605.04070** — *Toward Human-AI Complementarity Across Diverse Tasks* (13 Apr
  2026). Confirmed and the numbers are worth quoting precisely: 1,886 samples across
  knowledge, factuality, long-context reasoning and deception detection; two assistance
  methods (top-2 assistance, subtask delegation). **Baseline hybridisation gained just
  +0.4pp over AI alone (69.3% vs 68.9%)**, limited by a small complementarity region and
  confidence-based routing's inability to find it. In the low-AI-confidence condition,
  top-2 assistance lifted human accuracy 28.4% → 38.3%, edging past AI alone (37.7%) —
  **but mainly because humans adopted correct AI suggestions, not because they
  successfully overrode AI errors.** That distinction undercuts the optimistic reading.

## 2.3 The doc's three bullet claims, checked

| Doc claim | Status |
|---|---|
| "when AI confidence is low, its reasoning and judgments are worse and may ill-advise humans" | **Supported**, consistent with 2605.04070's low-confidence condition and with the confidence-routing failure. |
| "static AI assistance, delivered in the same manner, degrades over time and may even eventually become harmful" | **Supported — this is arXiv:2510.26518's own longitudinal finding.** The paper reports that *as human raters improve through practice, even evidence-only assistance ceases to provide a significant benefit, and leading forms of assistance become actively harmful.* An earlier draft of this review wrongly flagged this as unsourced. Related: arXiv:2604.04721, arXiv:2605.11350. |
| "Humans overrely on AI when shown its reasoning & explanation vs. only search results and evidence" | **Supported — also a direct experimental result in arXiv:2510.26518**: *"Displaying AI explanation, confidence, and labels leads to over-reliance, but just showing search results and evidence fosters more appropriate trust."* An earlier draft called this "more contested than the doc implies," which unfairly suggested the team had overstated their own source. The *wider* CSCW literature genuinely does disagree with itself — see below — but the doc's bullet is an accurate report of its citation. |

**Where the disagreement actually lives:** not in the team's bullet, but in the broader
explanation/overreliance literature, which does not converge:

- Vasconcelos et al., *Explanations Can Reduce Overreliance on AI Systems During
  Decision-Making* — CSCW 2023, arXiv:2212.06823. Argues overreliance is a **strategic
  cost-benefit choice**, not a cognitive inevitability, and that explanations *can*
  reduce it when they lower the cost of engagement.
- Fok & Weld, *In Search of Verifiability: Explanations Rarely Enable Complementary
  Performance in AI-Advised Decision Making* — arXiv:2305.07722. In domains where human
  and AI perform comparably, explanations do **not** beat a prediction-only baseline and
  appear to **worsen** overreliance.
- **Cognitive forcing works where explanation doesn't:** requiring the human to commit to
  an initial decision *before* seeing AI advice reduces overreliance. This is the most
  robust intervention in the area and is the obvious design lever for Idea 2 *and* Idea 4.
- *Confirmation bias: A challenge for scalable oversight* — arXiv:2507.19486.

## 2.4 The "pluralistic oracle" itself — how crowded is it?

**Crowded on the alignment/technical side, comparatively open on the human-effects side.**

The theory is well-established. The standard taxonomy is **Overton pluralism** (present a
range of reasonable responses), **distributional pluralism** (mirror the population's
value distribution), **steerable pluralism** (faithfully adopt a specified perspective on
request):

- *From Distributional to Overton Pluralism: Investigating LLM Alignment* — arXiv:2406.17692
- *Modular Pluralism: Pluralistic Alignment via Multi-LLM Collaboration* — arXiv:2406.15951
- *Steerable Pluralism: Pluralistic Alignment via Few-Shot Comparative Regression* — arXiv:2508.08509
- *Exploring Chain-of-Thought Reasoning for Steerable Pluralistic Alignment* — arXiv:2510.04045
- **[BENCHMARK]** *PerSpectra: A Scalable and Configurable Pluralist Benchmark of
  Perspectives from Arguments* — arXiv:2602.08716, **ICLR 2026**. 3,810 arguments, 762
  pro/con stances, 100 controversial topics, sourced from Kialo and Reddit. **Avenue 2A's
  first phase depends on what is actually in this — check it in week 1.**
- *Arbiters of Ambivalence: Challenges of Using LLMs in No-Consensus Tasks* — arXiv:2505.23820.
  **Closest existing work to AH's exact question**: what LLMs do when there is no
  consensus answer.
- *Operationalizing Pluralistic Values in LLM Alignment Reveals Trade-offs in Safety,
  Inclusivity, and Model Behavior* — arXiv:2511.14476
- Background: RLHF **narrows** distributional pluralism, concentrating probability mass on
  a few answers and biasing toward majority/culturally dominant views.

What is comparatively thin: **the routing decision** (when *should* a model go plural
vs. singular) and **the downstream human effect** of each choice.

## 2.5 The evidence that plural presentation matters downstream

- CHI 2026, *Narratives and Perspectives: How AI Summaries Steer Users' Opinions and
  Engagement on Social Media* — doi:10.1145/3772318.3790945. Peer-reviewed, and the
  closest thing to a direct test of presentation format → opinion effects.
- *The Rise of AI Search: Implications for Information Markets and Human Judgement at
  Scale* — arXiv:2602.13415 (Aral, Li & Zuo). **A supply-side audit, not a user study:**
  24,000 queries across 243 countries generating 2.8M AI and traditional search results,
  finding that AI search *surfaces* significantly fewer long-tail sources, lower response
  variety, and more low-credibility sources than traditional search. An earlier draft of
  this review described it as measuring what people "ask for and consume" — **that was
  wrong; there are no human participants in it.**
- *From Searchable to Non-Searchable: Generative AI and Information Diversity in Online
  Information Seeking* — arXiv:2604.10258.
- *The Style and Semantic Effects of Generative Search Engine* — arXiv:2509.14436.

**⚠️ And the work that measures the cost of plurality — missed by the first sweep:**

- **arXiv:2603.22152, *More Isn't Always Better: Balancing Decision Accuracy and
  Conformity Pressures in Multi-AI Advice*** — Tsuchiya & Baba (U. Tokyo), **CHI 2026**.
  Three tasks, varying panel size, within-panel consensus, and human-likeness of
  presentation. Findings: accuracy improved for **small** panels vs. a single AI, **larger
  panels yielded no gains**; high consensus fostered overreliance; **a single dissent
  reduced conformity pressure; wide disagreement created confusion and undermined
  appropriate reliance.** *This is the "paralysis" cost, measured, with a dose-response on
  plurality.* **Anyone working on Idea 2 must read this.**
- *Argumentative Experience: Reducing Confirmation Bias on Controversial Issues through
  LLM-Generated Multi-Persona Debates* — arXiv:2412.04629. Within-subjects, eye-tracking,
  multi-perspective debate vs. retrieval-based search. **Note its headline is a null:** the
  debate system did *not* significantly increase attention to opposing views or shift
  beliefs. A methods template and a cautionary result, not evidence that plurality changes
  minds.
- **DeliberationBench** — arXiv:2603.10018; a normative benchmark for LLM influence on
  users' views.
- *Beyond One-Way Influence: Bidirectional Opinion Dynamics in Multi-Turn Human-LLM
  Interactions* — arXiv:2510.20039 (N=266).
- *Not Too Short, Not Too Long: How LLM Response Length Shapes People's Critical Thinking
  in Error Detection* — arXiv:2603.06878. Bridges Ideas 2 and 4.
- **[REVIEW]** Lopez-Lopez, Abels, Holford, Herzog & Lewandowsky, *Generative artificial
  intelligence–mediated confirmation bias in health information seeking* — **Annals of the
  New York Academy of Sciences** 1550(1):23–36 (2025), doi:10.1111/nyas.15413. Same group as
  the Abels hypercustomization paper in §3.5. **It is a Perspective piece, not an empirical
  study** — a conceptual account of three "pressure points" where bias can emerge, with no
  data. *An earlier draft called it "the empirical companion" and filed it under this
  section's evidence heading; that repeated the same error this review flagged elsewhere.*

## 2.6 What is actually still open in Idea 2

1. **No one has built the router.** Everything above either presents plurality
   unconditionally or studies alignment properties. A *decision rule* for when plurality
   helps vs. paralyses, validated against human outcomes, does not appear to exist.
   **This claim survived a deliberate attempt to falsify it** (searches for adaptive
   plurality routing, NPOV generation, and multi-perspective RAG for controversial topics
   all returned *how* to be plural, never *when*). **This is the load-bearing gap for
   Idea 2.**
2. ~~The paralysis cost is asserted, not measured.~~ **Retracted.** An earlier draft
   called this "an unusually clean gap." It is not: **arXiv:2603.22152 (CHI 2026) measures
   it** — wide disagreement between AI advisors creates confusion and undermines
   appropriate reliance, with a dose-response on panel size. arXiv:2412.04629 measures
   attention and belief effects of multi-persona presentation. What remains open is
   **mapping question type → format**, not whether plurality can cost anything.
3. **Calibrating plurality to AI confidence.** 2605.04070 shows confidence-based routing
   fails for *answer* selection. Nobody has tested it for *format* selection.

---

# Idea 3 — (DM) Inherited/exploited cognitive biases; hallucination & "AI psychosis"

This is the **most crowded** of the six ideas, and it got crowded very fast during
2025–2026. It is also the one where a naive project is most likely to be scooped.

## 3.1 Reviews, meta-analyses and conceptual syntheses — start here

- **[META-ANALYSIS]** *Commercial AI-Based Mental Health Chatbots as Low-Intensity
  Adjuncts to Psychotherapy: Effectiveness, Adherence, and Safety* — **Psychotherapy and
  Psychosomatics**, doi:10.1159/000552072 (PMID 42113705, 2026). **52 studies, 22 RCTs,
  N = 110,594, 13 commercial chatbots.** Depression improved vs. control (**18 RCTs,
  N = 3,170; g = −0.35**, 95% CI −0.56 to −0.13); loneliness only partially (4 RCTs,
  N = 662, **g = −0.21**,
  95% CI −0.39 to −0.03). **Two nuances that change how you should read this:** the
  depression effect is roughly **1.6 PHQ-9 points, below the 5-point minimal clinically
  important difference**, and **anxiety was null** (15 RCTs, N = 2,936, g = −0.37, 95% CI
  −0.87 to 0.12). "Statistically significant" is not "clinically meaningful" here.
- **[META-ANALYSIS]** *Systematic review and meta-analysis of AI-based conversational
  agents for promoting mental health and well-being* — **npj Digital Medicine** (2023),
  doi:10.1038/s41746-023-00979-5. Depression Hedges' g = 0.64 (95% CI 0.17–1.12); distress
  g = 0.70 (0.18–1.22). **Do not read this as "effects shrank over three years"** (an
  earlier draft suggested that): this pools 15 RCTs of *all* AI conversational agents,
  whereas the 2026 analysis pools 22 RCTs of *commercial* chatbots used as psychotherapy
  adjuncts. Different populations, comparators and inclusion criteria — not comparable.
- **[META-ANALYSIS]** Gou, Lefebvre, Yang et al., *Effectiveness of AI-based
  conversational and socially assistive agents in older adults* — **BMC Geriatrics**
  26:887 (2026), doi:10.1186/s12877-026-07418-6 (PMID 42098628). 8 RCTs, N=611.
  **Depressive symptoms improved significantly (Hedges' g = −0.25, 95% CI −0.48 to −0.02;
  I² = 10.7%); loneliness showed no significant effect.** Subgroup analysis found
  cognitive-focused interventions produced greater reductions than companionship-focused
  ones. *An earlier draft of this review reported this backwards (as a null result for
  depression) — corrected.*
- **[META-ANALYSIS]** *Autonomous conversational agents for loneliness, social isolation,
  depression and anxiety in older people without cognitive impairment* — **Psychological
  Medicine**, PMID 41556104. A second, independent older-adults meta-analysis to set
  against the BMC one.
- **[META-ANALYSIS]** *Generative AI Mental Health Chatbots as Therapeutic Tools* — JMIR
  2025;27:e78238. GenAI chatbots outperform rule-based/retrieval-based on depressive
  symptoms.
- **[REVIEW]** *Artificial intelligence (AI) psychosis: mechanisms, clinical risks and
  safety considerations in generative AI chatbots* — **BJPsych Open**, PMC13276754.
  **The best single clinical entry point.**
- **[REVIEW]** *Mass Media Narratives of Psychiatric Adverse Events Associated With
  Generative AI Chatbots: Rapid Scoping Review* — JMIR Ment Health 2026;13:e93040.
- **[REVIEW]** *Exploring the application boundaries of LLMs in mental health: a
  systematic scoping review* — **Frontiers in Psychology** (2025),
  doi:10.3389/fpsyg.2025.1715306 (PMC12983331).
- **[REVIEW]** **Dohnány, Kurth-Nelson, Spens, Luettgau, Reid, Gabriel, Summerfield,
  Shanahan & Nour (2026)**, *Technological folie à deux: feedback loops between AI
  chatbots and mental health* — **Nature Mental Health** 4:336–345,
  doi:10.1038/s44220-026-00595-8 (PMID 41939177; preprint arXiv:2507.19218). *Cited in
  the doc; the PMC link is the article's author-manuscript deposit rather than the version
  of record, so prefer the Nature Mental Health DOI — a citation-style point, not a broken
  link.* **An earlier draft of this review attributed this paper to "Morrin et al." That
  was wrong** — Hamilton Morrin leads the JMIR paper in §3.2 and the KCL "Delusions by
  design?" piece, not this one. **The mechanism set:** sycophancy, role play,
  anthropomimesis, and elevated risk where a condition already involves altered
  belief-updating and reality-testing.
- **[REVIEW]** Osler, L. (2026), *Hallucinating with AI: Distributed Delusions and "AI
  Psychosis"* — **Philosophy & Technology** 39(1):30, doi:10.1007/s13347-026-01034-3
  (preprint arXiv:2508.19588). *Cited in the doc; link verified.* Philosophical, using
  distributed-cognition theory: we do not merely get hallucinated *at*, we hallucinate
  *with*. Good conceptual scaffolding, no empirical contribution.
- **[REVIEW]** *Large Language Model Psychometrics: A Systematic Review of Evaluation,
  Validation, and Enhancement* — arXiv:2505.08245. The methodological review for anyone
  measuring "biases" in models with instruments designed for humans. **Read this before
  running any psychometric instrument on an LLM.**
- **[REVIEW]** *Cognitive bias in clinical large language models* — **npj Digital
  Medicine**, doi:10.1038/s41746-025-01790-0.
- *Characterizing the spiral: potential mechanisms in AI-associated delusions* — **NPP
  Digital Psychiatry and Neuroscience**, doi:10.1038/s44277-026-00065-0. *Cited in the
  doc; link verified.*
- **[PREPRINT]** *Rethinking AI Psychosis: Misnomers, Conceptual Limits, and Existential
  Drift* — arXiv:2605.26858; and *An Echo Chamber of One: Should AI Psychosis Be a
  Distinct Clinical Entity?* — arXiv:2608.23937. **Both push back on the framing.**
  Reading these is the difference between a project that engages the debate and one that
  assumes a contested construct.

## 3.2 Benchmarks that already exist for the harm side

- **[BENCHMARK]** *The Psychogenic Machine: Simulating AI Psychosis, Delusion
  Reinforcement and Harm Enablement in LLMs* (**psychosis-bench**) — arXiv:2509.10970.
  16 structured 12-turn scenarios across erotic / grandiose-messianic / referential
  delusional themes; metrics **Delusion Confirmation (DCS)**, **Harm Enablement (HES)**,
  **Safety Intervention (SIS)**. Across 1,536 turns and 8 models: mean DCS 0.91 ± 0.88,
  HES 0.69 ± 0.84, SIS 0.37 ± 0.48, and **significantly worse in *implicit* scenarios
  (p < .001)**. **If you touch Idea 3, you must know this benchmark exists.**
- **[BENCHMARK]** *Lost in Delusion: Examining LLM Safety Under User Delusions and
  Distress* — arXiv:2606.00975.
- **[BENCHMARK]** *TrustMH-Bench: Evaluating the Trustworthiness of LLMs in Mental
  Health* — arXiv:2603.03047.
- *AI Psychosis: Does Conversational AI Amplify Delusion-Related Language?* — arXiv:2603.19574.
- *The Dynamics of Delusion: Modeling Bidirectional False Belief Amplification in
  Human–Chatbot Dialogue* — arXiv:2604.25096.
- **[BENCHMARK]** *Between Help and Harm: An Evaluation of Mental Health Crisis Handling
  by LLMs* — arXiv:2509.24857, **JMIR Mental Health** doi:10.2196/88435. A major safety
  benchmark the first sweep missed entirely.
- **Morrin, Au Yeung, Agnew, Østergaard & Pollak — JMIR Mental Health 2026;13:e91454** —
  *It Is the Journey, Not the Destination: Moving From End Points to Trajectories When
  Assessing Chatbot Mental Health Safety.*
  Methodologically the most useful of these: argues safety evaluation should score
  **trajectories, not endpoint outcomes.**

## 3.3 Sycophancy — the proposed mechanism, and how measurable it already is

- **[BENCHMARK]** **SycEval** — separates *progressive* (wrong→right under pressure) from
  *regressive* (right→wrong) shifts; finds preemptive rebuttals cause more drift than
  in-context ones, and that sycophancy persists across turns.
- **[BENCHMARK]** **SYCON-Bench** — multi-turn sycophancy.
- **Syco-bench** — splits sycophancy into picking sides, mirroring, attribution bias, and
  **delusion acceptance**; reports **low inter-test correlation (r < 0.3)**, implying
  sycophancy is *not one construct*. The r < 0.3 figure is **confirmed**. But note the
  provenance, which an earlier draft obscured by listing it alongside the peer-reviewed
  benchmarks: **syco-bench is an independent project (syco-bench.com;
  github.com/timfduffy/syco-bench) with no arXiv paper and no peer review.** That does not
  make it wrong, but it is a different evidentiary class from SycEval / SYCON-Bench /
  PARROT — and **avenue 3C's viability depends on this distinction.**
- **[BENCHMARK]** **PARROT** — *Persuasion and Agreement Robustness Rating of Output
  Truth* — arXiv:2511.17220.
- *Recalling Too Well: Sycophancy Evaluation and Mitigation **in Memory-Augmented Models*** —
  arXiv:2606.10949 (MIST benchmark; up to 25× higher sycophancy with memory). **Benchmarks sycophancy associated with three popular memory systems
  (e.g. Mem0)** — i.e. the memory-layer version. This is the bridge between Idea 1 and
  Idea 3.
- Mitigations: *Sycophancy under Pressure* arXiv:2508.13743; *Bayesian Truth Serum as
  GRPO reward* arXiv:2608.25267; uncertainty-aware RL arXiv:2509.16742; supervised
  pinpoint tuning of specific attention heads.
- **[BENCHMARK]** **DarkBench** — arXiv:2503.10728 (ICLR 2025 oral). 660 prompts, six
  dark-pattern categories (brand bias, user retention, sycophancy, anthropomorphism,
  harmful generation, sneaking); **dark patterns detected in ~48% of cases** across five
  major labs' models. **DarkBench+** (AAAI 2026) extends to 10 categories, 24
  subcategories, 2,088 bilingual samples, ~40 models.

## 3.4 The "inherits cognitive biases" half

- *Anchors in the Machine: Behavioral and Attributional Evidence of Anchoring Bias in
  LLMs* — arXiv:2511.05766.
- **[BENCHMARK]** *CogBias: Measuring and Mitigating Cognitive Bias in LLMs* — arXiv:2604.01366.
- *Confirmation, Framing, and Position Biases in LLM Responses* — **CHIIR 2026**,
  doi:10.1145/3786304.3787879 (peer-reviewed).
- *Vulnerability of LLM Outputs to Heuristics-Inducing Prompt Structures* — **IUI 2026**,
  doi:10.1145/3742413.3789108.
- *Understanding the Anchoring Effect of LLM with Synthetic Data* — arXiv:2505.15392.
- **Important caveat from this literature:** LLM biases *resemble* human ones but differ
  in **scale and stability**, and newer reasoning-trained models show fewer System-1
  errors while biases persist. So "LLMs inherit human biases" is too coarse a claim to
  build a project on without specifying which bias, which model generation, and which
  elicitation method — which is exactly what the psychometrics review (§3.1) warns about.

## 3.5 The doc's remaining Idea-3 citations, verified

- **Hypercustomization** — Abels, Lopez-Lopez, Burton, Holford, Brinkmann, Herzog &
  Lewandowsky (2025), *The governance & behavioral challenges of generative artificial
  intelligence's hypercustomization capabilities* — **Behavioral Science & Policy**
  11(1):22–32, doi:10.1177/23794607251347020. *Verified.* Dynamically tailoring responses
  to explicit and implicit preferences can reinforce biases, false beliefs and
  misconceptions. **This is the strongest theoretical bridge between Ideas 1 and 3** —
  hypercustomization *is* over-fitting to a user model.
- **Cultural biases in LLM recommendations** — the doc links an **emergentmind.com topic
  page**, which is an AI-generated aggregation site, **not a peer-reviewed source. Do not
  cite it.** The underlying primary work does exist: *Invisible Filters: Cultural Bias in
  Hiring Evaluations Using LLMs* (arXiv:2508.16673 — Western communication styles score
  higher on "hireability" than Indian linguistic patterns); *Revealing Potential Biases in
  LLM-Based Recommender Systems in the Cold Start Setting* (arXiv:2508.20401 — **Gemma 3
  12B recommended 91.3% Western content to an attribute-free user in the movies domain**.
  An earlier draft generalised this to "LLM recommendations default heavily Western";
  that overstates it. Only two small open families were tested, across music/movies/
  colleges; the size–bias relationship is **non-monotone** (Gemma 3 4B showed *less* bias
  than both 1B and 12B); persona-conditioned figures differ sharply (48.0% Western for
  "a Chinese," 22.0% for "a Japanese"); **no frontier model was tested**);
  *Mitigating Cultural Bias in LLMs via Multi-Agent Cultural Debate* (arXiv:2601.12091);
  *A framework for evaluating cultural bias and historical misconceptions in LLM outputs*
  (ScienceDirect S2772485925000481).

## 3.6 What is actually still open in Idea 3

1. **Trajectory-level rather than endpoint safety scoring** is explicitly called for
   (JMIR e91454) and mostly not done.
2. **The implicit-scenario gap.** psychosis-bench's own finding is that models do much
   worse when delusional content is *implicit*. Nobody has systematically characterised
   the implicit/explicit boundary.
3. **Sycophancy is probably several constructs, not one.** If the r < 0.3 result holds,
   the field's scores are not measuring one thing.
4. **Memory × sycophancy** (arXiv:2606.10949) is brand new and thin.
5. **Cultural misalignment × delusion-confirmation** — still the most open crossing here,
   but **narrower than an earlier draft claimed.** The culture × mental-health-safety
   crossing is already partly occupied by **arXiv:2508.03247, *Somatic in the East,
   Psychological in the West? A Clinically-Grounded Evaluation of Cross-Cultural
   Depression Symptoms in LLMs*** — read it before assuming this is open ground. What
   still looks unclaimed is specifically **delusion-confirmation and safety-intervention
   rates** (psychosis-bench's DCS/HES/SIS) across cultural idioms, as opposed to symptom
   recognition.

---

# Idea 4 — Countering Cognitive Atrophy through Epistemic Design

## 4.1 Reviews — start here

- **[REVIEW]** *Generative AI, Cognitive Offloading, and Learner Agency in Higher
  Education: A Scoping Review* — PMC13405335.
- **[REVIEW]** *The critical-thinking paradox in generative AI-integrated learning:
  distinguishing efficiency from cognitive depth* — **Frontiers in Psychology** (2026),
  doi:10.3389/fpsyg.2026.1906070 (PMC13521781). Framework + testable propositions —
  **useful because it hands you hypotheses to test rather than yet another survey.**
- **[REVIEW][PREPRINT]** *Epistemic Agency in AI-Mediated Education: A PRISMA 2020
  Systematic Review and Philosophical Synthesis* — Research Square rs-10695464. Proposes
  the **Human Epistemic Stewardship (HES)** framework: five conditions for legitimate
  AI-mediated learning — **contestability, justificatory ownership, productive friction,
  plural authority, relational oversight**. *[⚠️ UNVERIFIED — preprint, not peer-reviewed;
  its bibliometric claims about a 2025→2026 shift look strong and should be checked.]*
  Note that "plural authority" is essentially AH's pluralistic oracle, arrived at from
  the education side — **Ideas 2 and 4 converge here.**

## 4.2 The empirical base, including its most-cited and most-criticised study

- **[⚠️ CONTESTED]** Kosmyna et al., *Your Brain on ChatGPT: Accumulation of Cognitive
  Debt when Using an AI Assistant for Essay Writing Task* — arXiv:2506.08872. The famous
  EEG study; coined **"cognitive debt"**; LLM users showed the weakest neural
  connectivity, Brain-only the strongest, Search Engine intermediate. **N = 54 across
  sessions 1–3, only 18 completed session 4.**
  **Read the rebuttal alongside it:** *Comment on: Your Brain on ChatGPT* —
  arXiv:2601.00856, which raises limited sample size, reproducibility of analyses, EEG
  methodology, inconsistent reporting, and limited procedural transparency. There is also
  a developmental critique (*Your brain on ChatGPT, but whose brain? The missing
  adolescent in AI-cognition research*, Frontiers in Developmental Psychology 2026). **If
  the team cites this study without the rebuttal, that is a credibility problem.**
- *When Thinking Is Outsourced: Cognitive Offloading and the Heterogeneity of Critical
  Thinking Among Chinese University Students Using Generative AI* — PMC13413235. Key
  distinction: **episodic offloading** (deliberate, monitored) vs. **habitual offloading**
  (routine, weakly monitored). Only the latter looks harmful.
- *Generative AI Use and Critical Thinking Dispositions in Higher Education: ... the
  Sequential Role of Metacognitive Weakness and Epistemic Laziness* — PMC13413021.
- *From Co-Design to Metacognitive Laziness: Evaluating Generative AI in Vocational
  Education* — arXiv:2512.12306.
- *AI Assistance Reduces Persistence and Hurts Independent Performance* — arXiv:2604.04721.
- *Confidence Without Competence in AI-Assisted Knowledge Work* — arXiv:2604.09444.
- *Fostering human learning is crucial for boosting human-AI synergy* — arXiv:2512.13253.
  Explicitly links Idea 4's mechanism to Idea 2's meta-analytic problem.

**The consensus that has formed:** harm tracks **how** people engage, not **how much**
they use. Frequency-of-use is the wrong independent variable. Any Idea-4 design should
manipulate engagement mode, not dosage.

## 4.3 Socratic / friction prototypes — how much already exists

Quite a lot, and this is the risk for Idea 4's "build a prototype" framing:

- *Cognitive Agency Surrender: Defending Epistemic Sovereignty via Scaffolded AI
  Friction* — arXiv:2603.21735. Proposes **"Scaffolded Cognitive Friction"**, repurposing
  multi-agent systems as explicit cognitive forcing functions.
- *Socrates went Nuclear: Comparing Interaction Strategies for AI systems in a Learning
  Context using Brain Sensing* — arXiv:2609.00584 (Clin Deffarges, Kosmyna & Maes; HAI'26,
  n=50, nuclear-safety learning task). **Comparative study of interaction strategies with
  neural measurement — the most direct competitor to a naive Idea-4 prototype study.**
  **Note the same-group connection:** this is the Kosmyna lab, i.e. the authors of *Your
  Brain on ChatGPT* in §4.2. If you cite the rebuttal to that study, be consistent about
  how much weight you put on this one.
- *Enhancing Critical Thinking in Education by means of a Socratic Chatbot* — arXiv:2409.05511.
- **SocraticLLM / SocraticMATH** (CIKM 2024); **SPL (Socratic Playground for Learning)**.
- *Sycophancy is an Educational Safety Risk: Why LLM Tutors Need Sycophancy Benchmarks* —
  arXiv:2605.14604. **Directly connects Ideas 3 and 4.**
- *AnchoredAI: Contextual Anchoring of AI Comments Improves Writer Agency and Ownership* —
  arXiv:2509.16128. A worked example of an interface change improving agency.
- *Boosting metacognition in entangled human-AI interaction to navigate
  cognitive-behavioral drift* — arXiv:2602.01959.
- *Althea: Human-AI Collaboration for Fact-Checking and Critical Reasoning* — arXiv:2602.11161.
- *Learning with machines: Toward a theory of epistemic co-agency* — ScienceDirect S2666920X26000354.
- **[BENCHMARK] HumanAgencyBench (HAB)** — arXiv:2509.08494 (Sturgeon, Samuelson, Haimes
  & Anthis). Six agency dimensions: **Ask Clarifying Questions, Avoid Value Manipulation,
  Correct Misinformation, Defer Important Decisions, Encourage Learning, Maintain Social
  Boundaries.** Finds low-to-moderate agency support across current assistants, wide
  variation by developer, and — critically — **a tension between the post-training
  objective of instruction-following and human agency support**. *An earlier draft of this
  review attributed that finding to the SPAR project below; it belongs here.* **This paper
  partly pre-empts both avenue 4A's framing and avenue 6A's "cognitive layer" — read it
  before committing to either.**
- **[⚠️ ACTIVE PROJECT]** SPAR (Fall 2026): *Does your assistant respect your agency? A
  behavioral benchmark for autonomy-preserving AI* (Juan Cadile, U. Rochester). A
  benchmark **to be built** — paternalism, manipulation, dependency-fostering,
  value-substitution — with the stated gap "nothing that measures agency-respect as a
  construct." **It reports no results yet.** Worth tracking; not yet a competitor with
  findings.
- **⚠️ Work on voluntary adoption of assistance — missed by the first sweep:**
  - **Choose Your Agent: Tradeoffs in Adopting AI Advisors, Coaches, and Delegates in
    Multi-Party Negotiation** — arXiv:2602.12089 (Zhu, Thain, Tsai, Wexler, Qian).
    **243 participants** play three multi-turn bargaining games in groups of three.
    **Each game grants access to a single assistance modality** (Advisor / Coach /
    Delegate) in randomised order; on each turn a participant chooses whether to use it or
    act manually. **Participants never choose among the three** — an earlier draft of this
    review said they did, which overstated how closely this pre-empts avenue 4A. Result: a
    **preference–performance misalignment** — participants strongly prefer the
    higher-control **Advisor (44%)** over the **Delegate (19%)**, yet groups only
    significantly increase collective surplus under Delegate access. **The closest existing
    analogue to avenue 4A, but the adoption choice is use-vs-not, not friction-level
    selection.**
  - *When Friction Helps: Transaction Confirmation Improves Decision Quality **in Blockchain
    Interactions*** — arXiv:2602.18834 (N=109; a crypto-wallet confirmation study on a
    blockchain Connect Four game; Wave 2 win rate −11.8%, p=.044). Participants **preferred**
    the frictionless mode and rated their own performance higher in it, **despite objectively
    worse outcomes.** *Note the domain gap:* transaction confirmation is not epistemic
    friction, so treat this as suggestive rather than a direct analogue.
  - *Cognitive offloading and the speedup illusion in human-AI interaction* — arXiv:2605.23177.
  - **Not academic, but load-bearing:** **OpenAI's Study Mode**, **Claude's Learning Mode**
    and **Gemini's Guided Learning** are *shipped, opt-in friction toggles*. Any project claiming voluntary opt-in
    is unstudied has to address the fact that two major products already ship the switch.

## 4.4 What is actually still open in Idea 4

1. **DM's specific combination — Socratic + CBT/DBT — appears genuinely unbuilt.** Socratic
   tutors exist; CBT/DBT chatbots exist; the *hybrid* framing for general knowledge work
   (not therapy, not tutoring) is not in this search's results.
2. **DM's harder sub-question — "users must *choose* the higher-friction path" — is
   partly open, but narrower than an earlier draft claimed.** Every *epistemic-friction
   prototype* above imposes friction. But voluntary adoption of assistance modes **has**
   been studied: arXiv:2602.12089 gives participants a free choice among three modalities
   and finds a preference–performance misalignment, and arXiv:2602.18834 finds users
   prefer frictionless modes despite worse objective outcomes. What appears still open is
   **voluntary opt-in to *epistemic* friction in a knowledge-work assistant specifically**
   — and even that has to contend with Study Mode, Learning Mode and Guided Learning as
   deployed existence-proofs.
3. **Friction is universally prescribed and rarely dosed.** "Productive friction" appears
   in HES, in Scaffolded Cognitive Friction, in the offloading reviews. No one has a
   dose-response curve.

---

# Idea 5 — Combatting Deceptive Alignment and Misinformation
### (DM's framing: does deception/fabrication have a linguistic signature?)

**Important framing note before the citations.** The idea statement mixes two problems
that the literature keeps firmly apart, and a project needs to pick one:

- **(a) Detecting AI-authored *text*** — is this passage machine-written? (Stylometry,
  forensics.) Mature, and the signal is *about the generator*, not about truth.
- **(b) Detecting *fabrication* within an AI's output** — is this particular claim made
  up? (Hallucination detection, uncertainty.) Also mature, but the reliable signals are
  **internal** (entropy, activations), not surface linguistic.
- **(c) Detecting a model *misrepresenting its own reasoning*** — the doc's phrase
  "altering its stated internal logic to manipulate users." (CoT faithfulness, deception
  probes.) This is the actual alignment problem, and the least solved.

DM's question — *"are there differences between information that is 'researched' vs. made
up by LLMs?"* — sits between (a) and (b) and is, as posed, **the most open of the three.**

## 5.1 Reviews and surveys — start here

- **[REVIEW]** Park et al., *AI Deception: A Survey of Examples, Risks, and Potential
  Solutions* — arXiv:2308.14752 (published in *Patterns*). The canonical survey.
- **[REVIEW]** *A Survey on the Honesty of Large Language Models* — arXiv:2409.18786.
  Organises self-knowledge vs. self-expression; the right conceptual map for (b) and (c).
- **[REVIEW]** *A Survey of AI-generated Text Forensic Systems: Detection, Attribution,
  and Characterization* — arXiv:2403.01152. The map for (a).
- **[REVIEW]** *Trust & Safety of LLMs and LLMs in Trust & Safety* — arXiv:2412.02113.
- **[REVIEW]** *Building trust in the generative AI era: a systematic review of global
  regulatory frameworks to combat the risks of mis-, dis-, and mal-information* — **AI &
  Society**, doi:10.1007/s00146-025-02698-9. The governance-side review; bridges to Idea 6.

## 5.2 (a) Linguistic / stylometric signatures — DM's "different shape" intuition

The doc's intuition is correct and well-supported, and the strongest recent result is the
one DM already found:

- **StoryScope: Investigating idiosyncrasies in AI fiction** — arXiv:2604.03136 (Russell,
  Rajendhran, Pham, Iyyer, Wieting; Apr 2026). *Cited in the doc; verified.* **61,608
  stories (~5k words) from 10,272 prompts, one human source and five LLMs.** Induces an
  interpretable feature space of **discourse-level narrative** features across 10
  dimensions — character agency, chronological discontinuity, etc. **93.2% macro-F1
  separating human from AI fiction using narrative structure alone**, retaining >97% of
  the performance of the version that also uses style cues. Signature: tidy plots,
  explicit themes, reduced structural variety. **This is the paper to build on** — its
  key move is that the signal is *structural*, not stylistic, which is exactly DM's
  "different shape."
- *A linguistic comparison between human- and AI-generated content* — **iScience** /
  ScienceDirect S2589004226003512 (PMC12969083). *Cited in the doc; verified.*
  Portuguese-language; notably builds **two datasets: factual vs. false human-written
  texts, and LLM-generated texts (GPT-4o, Mistral Large, Llama 3.3 70B)** — i.e. it
  already crosses the human-vs-AI axis with the true-vs-false axis. **The closest
  existing work to DM's exact question; read it first.** Its most usable number for
  avenue 5A: the misinformation detector scored **93% on human texts but only 75% on LLM
  outputs** — i.e. detectors tuned on human deception transfer poorly to machine
  deception. That gap is arguably the whole opportunity.
- *Stylometric detection of AI-generated texts: evidence from human and machine-written
  essays* — **Digital Scholarship in the Humanities** (Oxford), doi:10.1093/llc/fqag064.
- *Why AI-Generated Text Detection Fails: Evidence from Explainable AI Beyond Benchmark
  Accuracy* — arXiv:2603.23146. **The necessary skeptical counterweight.**
- *Beyond checkmate: exploring the creative chokepoints in AI text* — arXiv:2501.19301.
- *Decoding LLMs' verbal deception in online reviews* — ScienceDirect S0167923625001307.
- *Trust at risk: Detecting misinformation in LLM-generated product reviews...* —
  ScienceDirect S2772503025000994. *Cited in the doc; verified.* **DeBERTa-v3 reaches
  96–98% accuracy/F1 on paraphrased and rewritten reviews, while zero-shot
  instruction-tuned LLMs do markedly worse.** Practical lesson: **a small fine-tuned
  classifier beats a big LLM at this task.** Good news for a small team's compute budget.
- *LLMs as "Hidden Persuaders": Fake Product Reviews are Indistinguishable to Humans and
  Machines* — arXiv:2506.13313. **Humans detect fake reviews at chance and are
  overconfident.** Note the tension with the paper above: *humans* fail, trained
  *classifiers* succeed.

**Hard constraint to design around:** the human-vs-AI gap is closing as models improve,
and detector performance degrades on short texts, across topics, and under paraphrase.
Any detection project needs a robustness story, not just an accuracy number.

## 5.3 (b) Fabricated vs. grounded — hallucination detection

- Farquhar et al., *Detecting hallucinations in LLMs using semantic entropy* — **Nature**
  (2024), doi:10.1038/s41586-024-07421-0. **Semantic entropy** — cluster
  semantically-equivalent samples, then compute entropy over meanings rather than tokens.
  The reference method.
- *HACK: Hallucinations Along Certainty and Knowledge Axes* — arXiv:2510.24222.
  Decomposes hallucination by whether the model *knows* and whether it is *certain* —
  **the most directly relevant framing for "researched vs. made up."**
- *Hallucination as Commitment Failure: Larger LLMs Misfire Despite Knowing the Answer* —
  arXiv:2605.22007.
- *Can LLMs Use Linguistic Uncertainty Markers to Reliably Reflect Intrinsic Confidence?*
  — arXiv:2605.28778. **Directly tests whether surface hedging tracks internal
  confidence.** If the answer is "poorly," that is precisely the gap DM's question opens.
- *PoLLMgraph: Unraveling Hallucinations via State Transition Dynamics* — arXiv:2404.04722.
- *Teaming LLMs to Detect and Mitigate Hallucinations* — arXiv:2510.19507.
- Background (OpenAI, Sept 2025): next-token objectives and leaderboards **reward
  confident guessing over calibrated uncertainty**, so models learn to bluff. This
  reframes hallucination as an incentive problem, and is the strongest argument that
  surface-level markers will be weak — the model is trained *not* to signal.

## 5.4 (c) Unfaithful reasoning — "altering its stated internal logic"

- **[BENCHMARK]** *FaithCoT-Bench: Benchmarking Instance-Level Faithfulness of
  Chain-of-Thought Reasoning* — arXiv:2510.04040.
- *Measuring Faithfulness Depends on How You Measure: Classifier Sensitivity in LLM CoT
  Evaluation* — arXiv:2603.20172. **Methodological warning: faithfulness scores are
  sensitive to the classifier used.**
- *Detecting Unfaithful Chain-of-Thought via Circuit-Guided Internal-External Discrepancy*
  — arXiv:2605.25603.
- *Why Models Know But Don't Say: CoT Faithfulness Divergence Between Thinking Tokens and
  Answers in Open-Weight Reasoning Models* — arXiv:2603.26410.
- *Faithfulness as Information Flow: Evaluating and Training Faithful CoT Reasoning* —
  arXiv:2605.24286.
- *Can We Predict Alignment Before Models Finish Thinking?* — arXiv:2507.12428.
- *Is Chain-of-Thought Really Not Explainability?* — ACL 2026 (2026.acl-long.2217),
  arXiv:2512.23032 (Zaman & Srivastava). **Read this as a counterweight to the rest of
  this subsection:** it argues hint-verbalization metrics "misinterpret explanation
  incompleteness as unfaithfulness," and that CoT can be faithful without verbalizing
  every influential factor. The skeptical framing above is not settled consensus.
- **Internal probes:** Azaria & Mitchell, *The Internal State of an LLM Knows When It's
  Lying* — arXiv:2304.13734, **Findings of EMNLP 2023** (**probing accuracy ~71–83%**); *Truth is Universal: Robust Detection of Lies in
  LLMs* arXiv:2407.12831; *When Truthful Representations Flip Under Deceptive
  Instructions* arXiv:2507.22149 (representational shift concentrated in early-to-mid
  layers); *Beyond Liars' Bench* arXiv:2607.20479; *Deep Minds and Shallow Probes*
  arXiv:2605.11448.

**Critical practical constraint:** every reliable method in (c) needs **open-weight model
internals**. If the team wants to work on (c), the project must be scoped to
Llama/Gemma/Qwen-class models, not to API-only frontier models.

## 5.5 What is actually still open in Idea 5

1. **The cross-product nobody has filled.** StoryScope showed *structural* features beat
   *stylistic* ones for human-vs-AI. Nobody has tested whether **structural** features
   separate an LLM's *grounded* output from its *fabricated* output. The Portuguese
   iScience paper is closest but works at the lexical level.
2. **Hedging vs. actual uncertainty.** arXiv:2605.28778 opens it; the calibration of
   surface markers against internal signals across models and domains is not settled.
3. **Verbal deception in *dialogue*.** The review/product-review work is single-shot
   text. Signatures of deception in multi-turn interaction are largely unexplored.

---

# Idea 6 — Multi-Layered Trust Framework

The doc gives this one no initials and no elaboration. The literature, by contrast, is
**dense and institutionalised** — this is the most crowded idea of the six, and the one
where a small team adds the least marginal value by proposing another framework.

## 6.1 Reviews and framework papers — start here

- **[REVIEW]** Weidinger et al., *Sociotechnical Safety Evaluation of Generative AI
  Systems* — arXiv:2310.11986 (DeepMind). **The canonical three-layer framework:
  capability → human interaction → systemic impact.** *This is essentially the idea as
  stated in the doc, already published in 2023.* Read it before writing anything.
- **[REVIEW]** *International AI Safety Report 2026* — internationalaisafetyreport.org.
  The Bengio-chaired synthesis; includes the defence-in-depth argument.
- **[REVIEW]** *Towards trustworthy agentic AI: a comprehensive survey of safety,
  robustness, privacy, and system security* — arXiv:2605.23989.
- **[REVIEW]** *From Agent Traces to Trust: A Survey of Evidence Tracing and Execution
  Provenance in LLM Agents* — arXiv:2606.04990.
- **[REVIEW]** *Risks & Benefits of LLMs & GenAI for Platform Integrity, Healthcare
  Diagnostics, Financial Trust and Compliance, Cybersecurity, Privacy & AI Safety: A
  Comprehensive Survey, Roadmap & Implementation Blueprint* — arXiv:2506.12088.
- **[BENCHMARK]** **HumanAgencyBench** — arXiv:2509.08494 (see §4.3). Listed here too
  because it is the closest thing that exists to an *operationalised cognitive layer*:
  six measurable agency dimensions with a running eval. **Avenue 6A should start from it
  rather than from a fresh taxonomy.**

## 6.2 Layered architectures already published

- *Layered Control Architectures for AI Safety: A Cybersecurity-Oriented Systems
  Framework* — **MDPI Systems** 14(4):447 (2026).
- *Defending against AI-driven social engineering: a conceptual framework* — **AI and
  Ethics**, doi:10.1007/s43681-026-01265-2. **Four-layer socio-technical defence:
  cognitive, system, institutional, societal.** Note the **cognitive** layer — this is
  the natural bridge from Ideas 3 and 4 into Idea 6.
- *Trustworthy AI Posture (TAIP): A Framework for Continuous AI Assurance of Agentic
  Systems* — arXiv:2603.03340.
- *Toward Pre-Deployment Assurance for Enterprise AI Agents: Ontology-Grounded Simulation
  and Trust Certification* — arXiv:2606.04037.
- *Trust Without Trusting: A Recomputable Trust Protocol for Autonomous Agents* — arXiv:2605.06738.
- *Quantifying System-Level Harms from AI Adoption in Complex Sociotechnical Systems* —
  arXiv:2608.23906. **The rare paper that tries to *measure* rather than propose.**
- *Exploring Systems-Thinking Approaches to Loss of Control Risk* — arXiv:2606.13474.
- Industry/standards: Cloud Security Alliance **Agentic Trust Framework** (Feb 2026);
  Google DeepMind **AI Control Roadmap v0.1**; Microsoft end-to-end agentic security
  guidance (Mar 2026); **Singapore IMDA Model AI Governance Framework for Agentic AI**
  (Jan 2026 — first comprehensive governance framework for autonomous agents, requiring
  verifiable per-agent digital identity and an authorisation audit trail).

## 6.3 What is actually still open in Idea 6

Very little at the *framework* level — the layers have been drawn many times over.
What is scarce:

1. **Empirical validation.** Almost every entry above *proposes* a stack. arXiv:2608.23906
   is one of few attempting measurement. **Testing whether a layered framework actually
   catches harms is wide open, and much harder than proposing one.**
2. **The cognitive/human layer is the thinnest.** Most stacks are strong on identity,
   provenance, sandboxing, and weak on the human-interaction layer — which is where this
   team's expertise sits.
3. **Cross-layer failure propagation.** How a model-layer failure becomes a systemic harm
   is asserted, rarely traced.

---

# Cross-cutting observations

1. **Ideas 1, 3 and 4 share one mechanism.** Over-fitting to a user model
   (hypercustomization) explains stale user beliefs (Idea 1), delusion reinforcement
   (Idea 3), and dependency (Idea 4). Abels et al. (2025) is the connective tissue. A
   project framed on that mechanism could cover two ideas at once.
2. **The measurement problem is the same across Ideas 1, 3 and 4.** All three need
   **trajectory-level, multi-turn evaluation**, and all three literatures independently
   complain that current benchmarks score endpoints (JMIR e91454; arXiv:2510.07777;
   arXiv:2605.30219). **A team that builds good multi-turn trajectory measurement has an
   asset reusable across three ideas.**
3. **Ideas 2 and 4 converge on cognitive forcing.** The most robust intervention for
   overreliance (commit before seeing advice) is the same family as "productive friction."
4. **The single most important empirical constraint** is the Vaccaro meta-analysis:
   human-AI combinations usually underperform the better party alone, and the moderator
   is *which party is better at the task*. Any interface-design project should say where
   it sits relative to that.
5. **Crowding, ranked** (revised after adversarial fact-checking, which found the first
   sweep had under-counted competition in Ideas 1 and 4). Idea 6 (most crowded, mostly
   framework proposals) > Idea 3 > **Idea 1** > Idea 4 > Idea 5 > Idea 2's routing
   question (least crowded — and the only "nobody has done this" claim in this document
   that survived a deliberate attempt to falsify it).

---

# Appendix A — Reviews and meta-analyses, all in one place

*The team asked for these to be flagged. Fastest way into each field.*

## Meta-analyses (quantitative, pooled effects)

| Work | Field | Headline |
|---|---|---|
| Vaccaro, Almaatouq & Malone (2024), *Nature Human Behaviour*, doi:10.1038/s41562-024-02024-1 | Human-AI teaming | 106 studies / 370 effects; combos **worse** than best alone on average; losses in decision tasks, gains in content creation |
| *Commercial AI-Based Mental Health Chatbots...* — *Psychotherapy and Psychosomatics*, doi:10.1159/000552072 (2026) | Mental-health chatbots | 52 studies, 22 RCTs, N=110,594; depression g=−0.35 (**≈1.6 PHQ-9 points, below the 5-point MCID**); loneliness g=−0.21; **anxiety null** |
| npj Digital Medicine (2023), doi:10.1038/s41746-023-00979-5 | Conversational agents & wellbeing | Depression g=0.64; distress g=0.70 |
| BMC Geriatrics 26:887 (2026), doi:10.1186/s12877-026-07418-6 | Older adults | 8 RCTs, N=611; **depression improved, g=−0.25** (CI −0.48 to −0.02); **loneliness null**; cognitive-focus > companionship-focus |
| *Psychological Medicine*, PMID 41556104 | Older adults | Second, independent older-adults meta-analysis — read alongside the BMC one |
| JMIR 2025;27:e78238 | GenAI mental-health chatbots | GenAI > rule-based/retrieval-based on depressive symptoms |

## Systematic reviews / scoping reviews / surveys

| Work | Field |
|---|---|
| arXiv:2502.08796 | LLM Theory of Mind evaluation — **best Idea-1 entry point** |
| *Cyberpsychology* doi:10.1089/cyber.2024.0536 | ToM & the "illusion of understanding" |
| arXiv:2505.08245 | **LLM psychometrics** — read before running human instruments on models |
| npj Digital Medicine doi:10.1038/s41746-025-01790-0 | Cognitive bias in clinical LLMs |
| PMC13276754 (*BJPsych Open*) | AI psychosis: mechanisms & clinical risk — **best Idea-3 clinical entry point** |
| JMIR Ment Health 2026;13:e93040 | Psychiatric adverse events in media narratives (rapid scoping review) |
| PMC12983331 | Application boundaries of LLMs in mental health (scoping review) |
| *Nature Mental Health* doi:10.1038/s44220-026-00595-8 | Technological folie à deux |
| *Philosophy & Technology* doi:10.1007/s13347-026-01034-3 | Distributed delusions (conceptual) |
| PMC13405335 | GenAI, cognitive offloading & learner agency (scoping) |
| *Frontiers in Psychology* doi:10.3389/fpsyg.2026.1906070 | Critical-thinking paradox — **gives testable propositions** |
| Research Square rs-10695464 **[PREPRINT]** | Epistemic agency in AI-mediated education (PRISMA) |
| arXiv:2308.14752 | AI deception (canonical) |
| arXiv:2409.18786 | Honesty of LLMs |
| arXiv:2403.01152 | AI-generated text forensics |
| arXiv:2412.02113 | Trust & safety of LLMs |
| *AI & Society* doi:10.1007/s00146-025-02698-9 | Regulatory frameworks vs. mis/dis/mal-information |
| arXiv:2310.11986 | **Sociotechnical safety evaluation — the three-layer framework** |
| International AI Safety Report 2026 | Global synthesis |
| arXiv:2605.23989 | Trustworthy agentic AI |
| arXiv:2606.04990 | Agent provenance & evidence tracing |
| arXiv:2506.12088 | LLM/GenAI risk & benefit blueprint |

---

# Appendix B — Status of every link in the brainstorm doc

| Doc link | Status |
|---|---|
| arxiv.org/abs/2405.18870 | ✅ Real. It is the *positive* result (LLMs reach adult ToM performance). Whether the doc misuses it depends on which clause the cite was attached to — **AH, please clarify.** See §1.1 |
| arxiv.org/abs/2607.28347 | ✅ Real; doc's summary accurate; one nuance omitted (§1.6) |
| lesswrong.com/posts/msFvLtPfDnCEdvrBr/... | ⚠️ Not verified (domain blocked). Not peer-reviewed |
| arxiv.org/abs/2605.06915 | ✅ Real; **Apple and Stanford** (no Princeton — an earlier draft said otherwise), May 2026 |
| arxiv.org/html/2507.11768v1 | ✅ Real; note it is **July 2025** with GPT-3-era validation |
| research.google/blog/teaching-llms-to-reason-like-bayesians/ | ✅ Real; underlying paper in *Nature Communications* |
| arxiv.org/abs/2510.26518 | ✅ Real |
| arxiv.org/abs/2605.04070 | ✅ Real; see §2.2 for the numbers in context |
| link.springer.com/article/10.1007/s13347-026-01034-3 | ✅ Real — Osler, *Philosophy & Technology* 39(1):30 |
| pmc.ncbi.nlm.nih.gov/articles/PMC7618964/ | ✅ Correct article — it is the author-manuscript deposit. Prefer the version of record: *Nature Mental Health* doi:10.1038/s44220-026-00595-8 (**Dohnány et al.**, not Morrin) |
| nature.com/articles/s44277-026-00065-0 | ✅ Real |
| journals.sagepub.com/doi/10.1177/23794607251347020 | ✅ Real — Abels et al., *Behavioral Science & Policy* 11(1):22–32 |
| emergentmind.com/topics/cultural-biases-in-llm-recommendations | ❌ **Not a citable source** (AI-generated aggregator). Primary sources listed in §3.5 |
| sciencedirect.com/.../S2772503025000994 | ✅ Real |
| arxiv.org/pdf/2604.03136 | ✅ Real — StoryScope |
| pmc.ncbi.nlm.nih.gov/articles/PMC12969083/ | ✅ Real — *iScience*; **most relevant to DM's question** |
