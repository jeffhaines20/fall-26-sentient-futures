# Round 2 Critique — Citation & Fact Verification (pass on v2/v3)

**Verdict: 8/10** (up from 6). **Every one of the 13 round-1 MAJOR issues is closed, and
closed correctly** — the substance of each was re-verified against primary sources, not just
the presence of an edit. The Dohnány author list is exactly right in full order (no
over-correction), the BMC Geriatrics restatement is exact to the digit, and the
arXiv:2405.18870 softening is fair to the teammate. Of ~25 newly added works, 24 were
verified: all exist, all IDs are right, and the described findings are accurate in 21.

*All findings below were accepted and fixed in v4 unless noted.*

## CLOSURE TABLE — round-1 major issues

| # | Status | Verification note |
|---|---|---|
| 1 | **CLOSED** | 2510.26518's own words confirmed: *"as human raters improve through practice, even evidence-only assistance ceases to provide a significant benefit, and leading forms of assistance become actively harmful."* "Or drop the claim" is gone |
| 2 | **CLOSED** | The overreliance quote confirmed verbatim against the paper; the Vasconcelos/Fok–Weld disagreement correctly relocated to "the *wider* CSCW literature" |
| 3 | **CLOSED — no over-correction** | Author list exact and in order; *Nature Mental Health* 4:336–345 confirmed; Morrin correctly reattributed |
| 4 | **CLOSED — exactly right** | g = −0.25, CI −0.48 to −0.02, I² = 10.7%, 8 RCTs, N = 611; loneliness null (g = −0.67, CI −2.57 to 1.23, I² = 89%); subgroup direction correct |
| 5 | **CLOSED** | 2603.22152 verified: Tsuchiya & Baba, CHI 2026; all four quoted findings exact |
| 6 | **CLOSED** | §1.1 presents both parses neutrally. 93% vs 82% verified; Johns Hopkins verified; *Frontiers in Human Neuroscience* DOI verified |
| 7 | **CLOSED** | 24,000 queries / 243 countries / 2.8M results verified; the uncorroborated "recommends surfacing disagreement" sentence is gone |
| 8 | **CLOSED** | SimpleToM and T4D verified; the claim that DToM-Track reports the *opposite* asymmetry verified verbatim |
| 9 | **CLOSED** | SPAR stripped to "reports no results yet"; HumanAgencyBench authors and all six dimensions verified word-for-word |
| 10 | **PARTIALLY** | Narrowing is right, Study Mode / Learning Mode verified — but the paper's design is misdescribed. See N2 |
| 11 | **CLOSED** | CAPTURE, PERMA, PersistBench, BeliefShift all verified; PERMA's description verbatim-accurate |
| 12 | **CLOSED** | Reclassified; title and author list verified; removed from Appendix A |
| 13 | **CLOSED — exact** | 91.3%, 48.0%, 22.0% and the non-monotone size–fairness relationship all verified |

Round-1 minors 1–12 all **CLOSED** and numerically verified; #13 partially.

## NEW MAJOR ISSUES

**N1. The power table was off by 2× on both proportion rows — and it propagated into two
budgets.** "~162 total" is the **per-group** n. Two-sided, 80% power, α=.05: n/group = 162.3
by the direct two-proportion formula and 162 by Cohen's *h* → **~325 total**. The 30→55% row
is likewise 60 per group → ~120 total. This flowed into "160 participants ≈ $700–900" and
4A's "~160 participants (~$700–900)"; the real requirement is **~325 participants,
~$1,400–1,800**. A document whose whole thesis was "v1 proposed n≈20 at 18% power" then
recommended a design at ~50% power. *The other four rows are correct, as is "3 × 159 = 477".*
**[Author's note: independently re-derived and confirmed, including a sanity check against
R's `power.prop.test`. Fixed.]**

**N2. *Choose Your Agent* did not give participants "free per-turn choice."** The design is
within-subjects: three bargaining games in randomised order, **each granting access to a
single modality**; the per-turn choice is whether to use that one modality or act manually.
Nobody chooses among three. "Per-turn" was the revision's own addition — an over-correction
that made the paper look like a *closer* pre-emption of 4A than it is. The 44%/19% figures
and the preference–performance framing are right; only the mechanism of choice is wrong.

**N3. The NYAS paper is a Perspective, and was called "its empirical companion."** Verified
real (Lopez-Lopez, Abels, Holford, Herzog & Lewandowsky, *Ann NY Acad Sci* 1550(1):23–36,
2025), but its own PDF header reads `PERSPECTIVE` and it contains no data. Filing an
unflagged Perspective under an *evidence* heading and calling it empirical is the same error
class as round-1 #7 — a regression in a document whose flag system exists to prevent it.

**N4. 5A's novelty claim is falsifiable by a paper's title.** **arXiv:2603.01341,
*Structural Hallucination in Large Language Models: A Network-Based Evaluation of Knowledge
Organization and Citation Integrity*** tests structural features against fabricated output
(fabrication >94%, citation omission 91.9%). 5A **survives narrowly** — that paper's
"structural" is *knowledge-graph* structure over a reference ontology, not StoryScope-style
*discourse* structure, and it measures hallucination rates rather than training a separator.
But a reviewer searching "structural" + "hallucination" finds it on page one, so the claim
must be restated as "*discourse-level*" with 2603.01341 cited and distinguished.

## NEW MINOR ISSUES

1. arXiv:2606.02976 uses a **Bayes factor**, not time-based decay weighting *(error inherited
   verbatim from round 1's own description — both were wrong)*.
2. **JMIR Mental Health is volume 13, not 27** — affects three citations.
3. Duplicated affiliation parenthetical in §1.1 (editing artifact).
4. Unmatched italic marker in the Dohnány entry left a sentence without a subject.
5. Appendix B still said "Apple/Stanford/Princeton"; verified affiliations are **Apple and
   Stanford**, contradicting the corrected §1.3.
6. The `[⚠️ UNVERIFIED]` flag on 2605.06915's "non-Bayesian beats Bayesian" claim is **stale**
   — Apple's own research page states it verbatim. Lift it.
7. *When Friction Helps* is truncated in a way that hides the domain: the full title ends
   "**in Blockchain Interactions**" (N=109, crypto-wallet confirmation on a blockchain
   Connect Four game). "Lower frustration" is not in the abstract.
8. The depression effect's sub-N (**18 RCTs, N = 3,170**) is missing while anxiety's and
   loneliness's are given, making a misreading of the headline N = 110,594 likelier.
9. arXiv:2412.04629 is filed under work that "measures the cost of plurality," but its
   **headline is a null**.
10. Gate-count drift: front matter said "nine gates"; the table has ten.
11. PMC12983331 given without a journal (*Frontiers in Psychology*, doi:10.3389/fpsyg.2025.1715306).
12. arXiv:2606.10949's title ends "**in Memory-Augmented Models**", not "[in memory systems]".
13. **Gemini's Guided Learning** is a third shipped opt-in study mode — omitting it slightly
    understates the document's own argument against 4A.
14. Version drift: anyone acting on a v2 print-out will act on a superseded ranking.

## VERIFIED

**2A's novelty claim survives a second, independent falsification attempt.** Five framings
tried (adaptive plurality routing; when-to-hedge decision rules; contested-question detection
→ response-strategy selection; Overton/steerable pluralism + "when"; presentation-format ×
question-type user studies). Everything returned is either *how* to be plural or
*model-selection* routing. Nearest three, none of which is the router: **arXiv:2605.01642**
(Adaptive Pluralistic Alignment — preference aggregation, not format routing);
**arXiv:2607.17063** ("When LLMs Over-Answer" — finds multi-answer hedging is *penalised* as
redundancy, 65.7%, in technical QA; **supports 2A's hypothesis rather than scooping it**);
**arXiv:2605.14912** (a normative argument). **2A's gap holds — the strongest claim in the
document.**

**New citations verified (24 of ~25), with correct IDs and accurate descriptions:** SimpleToM
2410.13648 · T4D 2310.03051 · CAPTURE 2609.02265 · PersistBench 2602.01146 · PERMA 2603.23231
· PrefEval 2502.09597 (ICLR 2025 Oral; <10% at 10 turns and the zero-shot qualifier confirmed)
· 2603.22152 · 2412.04629 · DeliberationBench 2603.10018 (4,088 participants, 65 proposals) ·
2510.20039 (N=266) · 2603.06878 (IUI'26) · NYAS 10.1111/nyas.15413 (exists; *type* is the
issue) · 2508.03247 · 2509.24857 (JMIR doi:10.2196/88435) · JMIR e93040 · PMC12983331 ·
Psychological Medicine PMID 41556104 · HumanAgencyBench 2509.08494 · 2602.12089 · 2602.18834 ·
2605.23177 (N=1,237) · 2512.23032 (ACL Anthology ID verified live) · 2304.13734.

**Numbers checked and exact:** iScience 93%/75% · 1.6 PHQ-9 points below the 5-point MCID ·
anxiety 15 RCTs, N=2,936, g=−0.37 · loneliness 4 RCTs, N=662, g=−0.21 · 52 studies/22
RCTs/N=110,594 · 44% vs 19%, 243 participants · 48.0%/22.0%/91.3% · 93% vs 82% · 24,000
queries/243 countries/2.8M results · PerSpectra 3,810 arguments/762 stances/100 topics/ICLR
2026 · 2607.28347's 391 UK Prolific participants and both corrected nuances · syco-bench
provenance (no arXiv, no peer review) · *Socrates went Nuclear* = Clin Deffarges, Kosmyna &
Maes, HAI'26 · OpenAI Study Mode and Claude Learning Mode as shipped toggles.

**Arithmetic checked and correct:** every cell and total in the v3 scoring table
(46/45/43/42/40/37/34/34 under Gap ×3, Feas ×2); the "score 2A's feasibility 4 and it wins by
one point" claim (47 vs 46); the "4A to 40, level with 5A" claim; "3 × 159 = 477"; four of the
six power rows. **The only arithmetic failure in the document is N1.**
