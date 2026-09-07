# Round 1 Critique — Citation Accuracy & Factual Verification

**Critic role:** adversarial fact-check of `01-literature-review.md` and `02-ranked-avenues.md`.
**Verdict: 6/10.** Citation hygiene is genuinely strong — 50+ citations spot-checked, no fabricated papers, no invented arXiv IDs, quoted numbers overwhelmingly exact — but the document makes **three confident public corrections of teammates that are themselves wrong or over-read**, gets **one meta-analysis finding backwards**, **misattributes a first author**, and the **two novelty claims carrying the #1 and #2 ranked recommendations are both falsifiable by papers the sweep missed**.

*(All items below were independently re-verified by the author before acceptance. Verification notes in brackets.)*

---

## MAJOR ISSUES

### 1. §2.3 tells the team to drop a claim stated verbatim in the paper they cited

The review marked "static AI assistance, delivered in the same manner, degrades over time and may even eventually become harmful" as **[⚠️ UNVERIFIED]** and said "Someone should find the real source or drop the claim."

It is in arXiv:2510.26518 — one of the two papers the team cited. The paper reports: *"As human raters improve through practice, even evidence-only assistance ceases to provide a significant benefit, and leading forms of assistance become actively harmful,"* and *"With more skilled raters, the same assistance helps less and can even hurt more."*

**Fix:** Status becomes "Supported — this is arXiv:2510.26518's own longitudinal finding." Delete "or drop the claim."
*[VERIFIED by author: confirmed — "as raters improve, the assistance that was once helpful becomes unnecessary or counterproductive."]*

### 2. §2.3's third row is also mis-framed against the team

The review marked the overreliance-on-explanations claim "Partially supported, and **more contested than the doc implies**."

arXiv:2510.26518 states it as a direct experimental result: *"Displaying AI explanation, confidence, and labels leads to over-reliance, but just showing search results and evidence fosters more appropriate trust."* The team reported their source accurately. The wider CSCW literature does disagree with itself (Vasconcelos vs. Fok & Weld — that part is fine), but "more contested than the doc implies" wrongly implies the team overstated their own citation.

**Fix:** "Supported by arXiv:2510.26518's own experiment; note the broader explanation/overreliance literature is more mixed."
*[VERIFIED by author: confirmed verbatim.]*

### 3. "Morrin et al. (2026)" is the wrong first author

Authors of the *Nature Mental Health* folie à deux paper are **Sebastian Dohnány**, Zeb Kurth-Nelson, Eleanor Spens, Lennart Luettgau, Alastair Reid, Iason Gabriel, Christopher Summerfield, Murray Shanahan, Matthew M. Nour. No Morrin.

Hamilton Morrin is first author of two *different* papers: "Delusions by design? How everyday AIs might be fuelling psychosis" and — the likely source of the mix-up — **JMIR Mental Health 2026;27:e91454**, which the review cites separately in §3.2.

**Fix:** "Dohnány, Kurth-Nelson, Spens et al. (2026)". Attribute Morrin correctly to the JMIR entry.
*[VERIFIED by author: confirmed, Nature Mental Health 4:336–345.]*

### 4. The BMC Geriatrics finding is reported backwards

The review says "Companionship-focused AI showed **no statistically significant effect on depressive symptoms**."

The meta-analysis found a **significant reduction in depressive symptoms** (Hedges' g = −0.25, 95% CI −0.48 to −0.02; I² = 10.7%; 8 RCTs, N=611). The **null was for loneliness**. The companionship point is a *subgroup consistency* observation — cognitive-focused interventions produced greater reductions than companionship-focused ones — not "no significant effect on depression."

**Fix:** Restate correctly in §3.1 and Appendix A.
*[VERIFIED by author: confirmed — Gou, Lefebvre, Yang et al., BMC Geriatrics 26:887.]*

### 5. "The paralysis cost is asserted, not measured" is false — and it is the #1 recommendation's entire justification

**Falsifying evidence:**
- **arXiv:2603.22152, "More Isn't Always Better: Balancing Decision Accuracy and Conformity Pressures in Multi-AI Advice"** — Tsuchiya & Baba, **CHI 2026**. *"Accuracy improved for small panels relative to a single AI; larger panels yielded no gains… High consensus fostered overreliance; a single dissent reduced pressure to conform; **wide disagreement created confusion and undermined appropriate reliance**."* That is the paralysis cost, measured, with a dose-response on plurality.
- **arXiv:2412.04629, "Argumentative Experience: Reducing Confirmation Bias on Controversial Issues through LLM-Generated Multi-Persona Debates"** — within-subjects, eye-tracking, multi-perspective vs. retrieval search.

**Fix:** Rewrite as "*partly* measured." Re-examine whether 2A still deserves rank 1. **§2.6.1 ("no one has built the router") does survive adversarial search — that, not the paralysis claim, should be the load-bearing gap.**
*[VERIFIED by author: 2603.22152 confirmed, CHI 2026, Tsuchiya & Baba, U. Tokyo.]*

### 6. The §1.1 "correction" over-reads what the team actually wrote

The paper facts are right (2405.18870 is Street et al., MoToMQA, GPT-4 exceeds adults at 6th order — 93% vs 82%). But the team's sentence places the citation immediately after the clause **"despite their capacity to match human performance on higher-order ToM benchmarks"** — which is exactly what that paper shows. The natural reading is that the citation supports the *capability* clause, not the *skeptical* one. The review asserts a misreading the sentence does not obviously contain, then escalates ("a reviewer will catch it immediately"). Publicly correcting a teammate on an ambiguous parse is the worst place to be over-confident.

**Fix:** Soften to a question about which clause the cite was attached to. Also: affiliations include **Johns Hopkins**; the work has since appeared in *Frontiers in Human Neuroscience* (2025), doi:10.3389/fnhum.2025.1633272 — cite the peer-reviewed version.

### 7. arXiv:2602.13415 is mischaracterised — a supply-side audit, not a study of user behaviour

The review says "People ask for and consume a narrower set of views with an LLM." Aral, Li & Zuo executed **24,000 queries in 243 countries generating 2.8M results**. The finding is about what the *system surfaces*: *"AI search surfaces significantly fewer long tail information sources, lower response variety, and significantly more low credibility and right- and center-leaning information sources."* No human participants. The "recommends surfacing disagreement" attribution could not be corroborated at all.

**Fix:** Restate as a supply-side audit. Drop the recommendation sentence.

### 8. §1.4's "cross-cutting finding" is attributed to papers that do not report it

None of the five §1.4 benchmarks reports "passes explicit probes but fails behaviourally." DToM-Track reports the *opposite* asymmetry. The claim is *true of the field*, but its real sources are missing:
- **SimpleToM — arXiv:2410.13648, ICLR 2026** — "Exposing the Gap between Explicit ToM Inference and Implicit ToM Application in LLMs."
- **T4D / "How FaR Are LLMs From Agents with Theory-of-Mind?" — arXiv:2310.03051.**

This matters because avenue **1A** rests on it.

**Fix:** Move the claim, cite SimpleToM and T4D, stop attributing it to the 2026 belief benchmarks.

### 9. The SPAR "active competitor" entry describes a *published* paper's finding, and the review missed that paper

The SPAR project page describes a benchmark **to be built**, reports no results, and the "sourcehood-preserving dimensions" phrasing could not be corroborated. That finding is the headline of **HumanAgencyBench (arXiv:2509.08494; Sturgeon, Samuelson, Haimes & Anthis)** — six agency dimensions (Ask Clarifying Questions, Avoid Value Manipulation, Correct Misinformation, Defer Important Decisions, Encourage Learning, Maintain Social Boundaries), reporting *"a tension between current development practices, particularly the post-training objective of instruction-following, and human agency support."*

**Fix:** Strip the unverifiable result from the SPAR entry. Add HumanAgencyBench as a first-class §4 citation — it partly pre-empts both 4A's framing and 6A's "cognitive layer."
*[VERIFIED by author: HumanAgencyBench confirmed, six dimensions exact.]*

### 10. Avenue 4A's core novelty claim is falsifiable

**arXiv:2602.12089, "Choose Your Agent: Tradeoffs in Adopting AI Advisors, Coaches, and Delegates in Multi-Party Negotiation"** — 243 participants, three bargaining games, free choice among three LLM assistance modalities differing in user control/effort. *"Participants strongly prefer the higher-control Advisor (44%) over the Delegate (19%), yet groups only significantly increase collective surplus under Delegate access."* That is the preference/performance-misalignment result 4A proposes to discover.

Also **arXiv:2602.18834, "When Friction Helps"** — participants preferred frictionless mode despite later evidence of degraded objective performance.

**Fix:** Narrow to "voluntary opt-in *to epistemic friction in a knowledge-work assistant*", cite 2602.12089 as the closest analogue. Also note **OpenAI Study Mode** and **Claude Learning Mode** as deployed opt-in friction — a project asserting nobody studies opt-in while two shipped products offer exactly that switch will read as under-researched.
*[VERIFIED by author: 2602.12089 confirmed — Zhu, Thain, Tsai, Wexler, Qian; 243 participants; 44% vs 19% exact.]*

### 11. Avenue 1A's gap is much more occupied than stated

Missed, all directly relevant:
- **CAPTURE — arXiv:2609.02265** (2 Sep 2026, five days before this review): *"a continuous-time partially observable decision process over latent user state… a neural differential-equation belief tracker, multi-timescale memory ledger."* Independently makes the review's own §1.5 point that stale and poisoned beliefs are the same problem.
- **PersistBench — arXiv:2602.01146**, "When Should Long-Term Memories Be Forgotten by LLMs?"
- **PERMA — arXiv:2603.23231** — positional probing for recency bias, catastrophic forgetting, context saturation.
- **Memory Retrieval for Changing Preferences — arXiv:2606.02976** — time-based decay weighting on user facts.
- The review's own **BeliefShift** entry contradicts its mitigation: it *is* about user opinion drift across health, politics, personal values, product preferences, with 2,400 human-annotated multi-session trajectories.

**Fix:** Rewrite 1A's risk section around CAPTURE and PERMA. The exponential-discount *fit* may still be novel; "nobody has measured decay of beliefs about the user" is not defensible.

### 12. arXiv:2603.18007 is filed as a review; it is an empirical study

Full title: *"Do Large Language Models Possess a Theory of Mind? A **Comparative Evaluation Using the Strange Stories Paradigm**"* (Babarczy, Lukacs, Vedres, Bujka). Tests five LLMs against human controls.

**Fix:** Remove from §1.2 reviews and from Appendix A; retitle; drop the [REVIEW] flag.

### 13. The 91.3% figure is over-generalised, and avenue 3B leans on the generalisation

The 91.3% is **Gemma 3 12B**, **movies domain only**. The paper tests two small open families across music/movies/colleges; the picture is non-monotone (Gemma 3 4B showed the *least* bias, below both 1B and 12B). Persona-conditioned figures differ sharply (48.0% Western for "a Chinese," 22.0% for "a Japanese"). No frontier model tested.

**Fix:** State the scope precisely.

---

## MINOR ISSUES

1. **PMID 42113705** — no journal/DOI given. It is *Psychotherapy and Psychosomatics*, doi:10.1159/000552072. Two dropped nuances change the read: the depression effect is *"about 1.6 PHQ-9 points, below the 5-point minimal clinically important difference"*, and anxiety was null (15 RCTs, N=2,936, g=−0.37, CI −0.87 to 0.12). "Modest effects" undersells this.
2. **§3.1's "shrinkage across three years"** is apples-to-oranges: the 2023 npj analysis pools 15 RCTs of all AI conversational agents; the 2026 one pools 22 RCTs of 13 *commercial* chatbots as psychotherapy adjuncts. Different populations, comparators, inclusion criteria. Do not frame as temporal shrinkage.
3. **arXiv:2607.28347** — two drifts. The third bias is *"failure to rank comments by **relevance to belief updates**,"* not "by convincingness." And it should read *"**two of six models** (Qwen3-32B, GPT-5-Mini) match the human post-stance distribution."*
4. **PrefEval** — cited by name only. It is **arXiv:2502.09597, ICLR 2025 Oral** (3,000 preference-query pairs, 20 topics, 10 models). The <10%-at-10-turns figure is confirmed, with the qualifier that it holds **in the zero-shot condition**. Lift the [⚠️ UNVERIFIED] flag.
5. **Syco-bench r<0.3** — confirmed; lift the unverified flag. But flag provenance instead: syco-bench is an independent benchmark at syco-bench.com, **no arXiv paper, no peer review**, listed alongside SycEval/SYCON-Bench/PARROT as if equivalent. Avenue 3C's viability depends on this distinction.
6. **PMC7618964** — "Wrong/stale target" is too strong. It is the correct article's PMC author-manuscript deposit, not a wrong link. A citation-style point.
7. **PERSPECTRA** — published as **PerSpectra, ICLR 2026** (3,810 arguments, 762 pro/con stances, 100 controversial topics, Kialo + Reddit). Give venue and scale; 2A Phase 1 depends on what is in it.
8. **Azaria & Mitchell** — 71–83% exact, but no reference. It is **arXiv:2304.13734, Findings of EMNLP 2023**.
9. **PMC13276754** — give the journal: **BJPsych Open**.
10. **ACL 2026 CoT paper** — add **arXiv:2512.23032** (Zaman & Srivastava), and note it runs *against* the section's skeptical framing: hint-verbalization metrics "misinterpret explanation incompleteness as unfaithfulness."
11. **"Socrates went Nuclear"** — it is **Clin Deffarges, Kosmyna & Maes (HAI'26, n=50)**, i.e. the same MIT group as *Your Brain on ChatGPT*. A document citing the Kosmyna rebuttal in §4.2 and naming a Kosmyna paper as its main competitor in §4.3 should connect those.
12. **iScience paper** — omits its most usable number: the misinformation detector scored **93% on human texts but 75% on LLM outputs**. Directly relevant to 5A's baseline design.
13. **arXiv:2605.06915** — author list exact, Apple confirmed; "Stanford / Princeton" not corroborated. The claim *"the non-Bayesian heuristic often beats exact Bayesian computation"* could not be corroborated from any summary — and it is the part the review calls "the interesting one." Flag or verify from the PDF.
14. **arXiv:2507.11768 "GPT-3-era validation"** — checks out. Validates on GPT-3 (text-davinci-002) via log-prob access. Claim stands.
15. **Farquhar et al. semantic entropy** — not independently verified in this pass; the only high-profile citation left unchecked.

---

## VERIFIED CORRECT

**No fabricated papers and no invented arXiv IDs were found.** Existence, title, authors/venue/year and — where quoted — exact numbers check out for:

**Idea 1:** 2405.18870 · 2502.08796 (Sarıtaş, Tezören, Durmazkeser) · Marchetti et al. *Cyberpsychology* 28(7):505–514 · 2605.06915 · 2507.11768 · 2507.17951 · **2512.18489** (discount factor < 1, Update Divergence / Model Misspecification Divergence — summary faithful) · Nature Comms 10.1038/s41467-025-67998-6 · **2605.30219** (Failed Stay/Update/Isolation, exact) · 2603.14646 · 2603.23848 · **2605.26322** (895 stories, 22,343 propositions, exact) · **2605.14498** · 2604.02315 · 2510.17132 · 2603.26680 (SIGIR 2026) · **2607.28347** (391 UK Prolific participants, all three biases)

**Idea 2:** **Vaccaro et al.** *Nat Hum Behav* 8:2293–2303 — 106 studies, 370 effect sizes, decision-vs-creation moderator, all exact · 2510.26518 (also FAccT 2026, doi:10.1145/3805689.3812308) · **2605.04070** — 1,886 samples, +0.4pp (69.3 vs 68.9), 28.4%→38.3% vs 37.7%, and the "adopted rather than overrode" caveat: **all exact** · 2602.08716 · 2505.23820 (ACL 2025 Findings, Meta) · CHI 2026 doi:10.1145/3772318.3790945

**Idea 3:** **2509.10970** — 16 scenarios × 12 turns, 8 models, 1,536 turns, mean DCS 0.91, implicit-worse p<.001: **all exact** · PMID 42113705 — 52 studies, 22 RCTs, N=110,594, g=−0.35, loneliness g=−0.21: **all exact** · npj 10.1038/s41746-023-00979-5 — g=0.64, distress 0.70: exact · npj 10.1038/s41746-025-01790-0 · PMC13276754 · Osler *Phil & Tech* 39(1):30 · **DarkBench 2503.10728** — ICLR 2025 oral, 660 prompts, 6 categories, 48% (range 30–61%): exact · Abels et al. *Behavioral Science & Policy* 11(1):22–32 — **author list, volume, issue, pages all exact** · JMIR Mental Health 2026;27:e91454

**Idea 4:** **2506.08872** — N=54, 18 completed session 4, connectivity ordering: exact · **2601.00856** (Stanković, Hirche, Kollatzsch, Doetsch) — all five critique points match; the "cite the rebuttal alongside it" advice is sound · rs-10695464 · 2609.00584

**Idea 5:** **2604.03136 StoryScope** — 61,608 stories, 10,272 prompts, 10 dimensions, **93.2% macro-F1 on structure alone, retaining >97%**: **all exact**, framing faithful · iScience S2589004226003512 · S2772503025000994 — **DeBERTa-v3 96–98% vs zero-shot below 45%**: exact · Azaria & Mitchell 71–83%: exact

**Idea 6:** 2310.11986 (the "already published in 2023" point is correct and worth keeping) · MDPI *Systems* 14(4):447 · AI & Ethics doi:10.1007/s43681-026-01265-2

**Novelty claims that survived attempts to falsify them:**
- **§2.6.1 "No one has built the router."** Searched adaptive plurality routing, NPOV generation, multi-perspective RAG. Everything found is *how* to be plural, not *when*. **Holds — make it the load-bearing claim for 2A.**
- **§5.5.1 "Nobody has tested whether structural features separate grounded from fabricated output."** **Holds.** 5A's gap is real.
- **§4.4.3 "Friction is prescribed and never dosed."** Holds, with 2602.18834 as nearest partial.
- **§3.6.5 "cultural misalignment × delusion confirmation not crossed."** Holds *narrowly* — but the culture × mental-health-safety crossing is already occupied (see Missing Work).

---

## MISSING WORK

**Idea 1**
- **SimpleToM — arXiv:2410.13648, ICLR 2026. Must add** — §1.4's cross-cutting claim and avenue 1A both depend on it.
- **T4D — arXiv:2310.03051.**
- **CAPTURE — arXiv:2609.02265.** Direct competitor to 1A.
- **PersistBench — arXiv:2602.01146**; **PERMA — arXiv:2603.23231**; **arXiv:2606.02976**.
- **PrefEval — arXiv:2502.09597, ICLR 2025 Oral.**
- *Re-evaluating Theory of Mind evaluation in LLMs* — arXiv:2502.21098; *Can LLMs Emulate Human Belief Dynamics?* — arXiv:2605.18781; arXiv:2607.25094.

**Idea 2**
- **arXiv:2603.22152, CHI 2026 — *More Isn't Always Better*. Must add.**
- **arXiv:2412.04629** — *Argumentative Experience*.
- **DeliberationBench — arXiv:2603.10018**: a normative benchmark for LLM influence on users' views.
- *Beyond One-Way Influence: Bidirectional Opinion Dynamics in Multi-Turn Human-LLM Interactions* — arXiv:2510.20039 (N=266).
- *Not Too Short, Not Too Long: How LLM Response Length Shapes People's Critical Thinking in Error Detection* — arXiv:2603.06878.
- **Lopez-Lopez et al., "Generative AI–mediated confirmation bias in health information seeking," *Annals NYAS*, doi:10.1111/nyas.15413** — same group as the Abels hypercustomization paper; its empirical companion should not be missing.
- *Effects of AI-assisted review presentation formats on consumer decision-making efficiency* — *Scientific Reports*, doi:10.1038/s41598-026-45101-3.

**Idea 3**
- **arXiv:2508.03247, "Somatic in the East, Psychological in the West? A Clinically-Grounded Evaluation of Cross-Cultural Depression Symptoms in LLMs."** Direct precursor to avenue **3B**; its absence is why 3B reads as more open than it is.
- **"Between Help and Harm: An Evaluation of Mental Health Crisis Handling by LLMs" — arXiv:2509.24857, JMIR Mental Health doi:10.2196/88435.** Major safety benchmark missed entirely.
- **Morrin et al., "Delusions by design? How everyday AIs might be fuelling psychosis"** (KCL).
- *Mass Media Narratives of Psychiatric Adverse Events Associated With Generative AI Chatbots: Rapid Scoping Review* — JMIR Ment Health 2026;27:e93040 **[REVIEW]**.
- *Exploring the application boundaries of LLMs in mental health: a systematic scoping review* — PMC12983331 **[REVIEW]**.
- *Autonomous conversational agents for loneliness, social isolation, depression and anxiety in older people* — *Psychological Medicine*, PMID 41556104 **[META-ANALYSIS]** — a second, independent older-adults meta-analysis.

**Idea 4**
- **HumanAgencyBench — arXiv:2509.08494. Must add.**
- **Choose Your Agent — arXiv:2602.12089.**
- *Cognitive offloading and the speedup illusion in human-AI interaction* — arXiv:2605.23177.
- *When Friction Helps* — arXiv:2602.18834.
- *Using AI-based Learning Assistants in Higher Education* — arXiv:2607.08748.
- Non-academic but load-bearing: **OpenAI Study Mode** and **Claude Learning Mode** are shipped opt-in friction toggles.

**Idea 5** — the thinnest gap found, a point in 5A's favour. Optional: arXiv:2309.13788; *J Big Data* doi:10.1186/s40537-025-01349-6; arXiv:2512.23032.

**Idea 6** — nothing major missing at framework level; the "over-crowded, don't propose another one" verdict is well supported. Add HumanAgencyBench, since 6A's cognitive layer is what it operationalises.

---

## Two structural recommendations

1. **The three wrong corrections (#1, #2, #6) are the most damaging items here.** A review whose stated purpose is partly to catch teammates' errors, and which then miscorrects them three times, will lose the room. Fix those before anyone else reads the document.
2. **The overall ranking in `02` needs revisiting after #5, #10 and #11.** All three top avenues rest on novelty claims that weakened under adversarial search: 2A's paralysis gap is measured (2603.22152), 4A's opt-in gap is partly occupied (2602.12089), 1A's discount-factor gap is crowded (CAPTURE, PERMA). None dies, but the confidence gradient changes, and "unusually clean gap" is no longer defensible.
