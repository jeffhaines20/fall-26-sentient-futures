# Round 2 Critique — Strategy (verification pass on v2)

**Verdict: 7/10** (was 6). The rewrite is substantive, not cosmetic: the power numbers are real and were independently re-derived as correct, the week-1 gates are the single most useful addition, the DM attribution fix is exactly right, and three of the four strongest missing avenues were added as first-class avenues. It lost points for three things: the #1-ranked avenue had no person-hour estimate and a stated duration that did not fit the document's own 12-week budget; the justification for ranking it first was false by the document's own text; and the recommendation sat at 91% depth.

*All findings below were accepted and fixed in v3 unless marked otherwise.*

## CLOSURE TABLE (round-1 strategy issues)

| # | Round-1 issue | Status after v2 |
|---|---|---|
| 1 | Ranking doesn't follow stated criteria | **PARTIALLY** — table published and arithmetic correct, but the stated tiebreak was arithmetically inconsistent with the table. See N1. |
| 2 | "Phase 1 stands alone" untrue | **CLOSED** — Phase 1.5 fallback added; the "should is Phase 2" point stated explicitly |
| 3 | 2A outcomes not split by item class | **CLOSED** — three-row table with a "Not valid" column. Best single fix in the document |
| 4 | No power analysis | **CLOSED** — six-row table, all six figures independently re-derived as correct; Prolific costing checks out |
| 5 | No budget/timeline/week-1 plan | **PARTIALLY** — gate table and ethics tree are real, but week-1 tasks still scattered and pilots unbudgeted |
| 6 | All-measurement, no artifacts | **PARTIALLY** — `Type:` and smallest-intervention added, but interventions unbudgeted |
| 7 | DM's "exploit" clause had no avenue | **CLOSED** — 3B added and correctly framed |
| 8 | 4A attribution unfair to DM | **CLOSED — best fix in the rewrite.** Buy-in added as criterion 6 with scores marked as guesses |
| 9 | 5A confounds | **CLOSED** — all three named as load-bearing; downgraded to Medium |
| 10 | 1A "discount factor" ill-defined | **CLOSED** — renamed, gate added, bad fallback fixed |
| 11 | Nulls relabelled as findings | **PARTIALLY** — controls added to 1A, 1B, 3A, 4A, but the changelog claimed *every* avenue had one. See N4 |
| 12 | `01`'s limitations dropped | **PARTIALLY / one part WORSE** — the limitations block is excellent, but a new claim that second-hand numbers are "marked" was false. See N5 |

Round-1 minors: 1, 4, 5, 6, 8, 9, 10, 12, 13 closed; 2–3 partial; **11 (no venue/deadline) not closed**; 7 not addressed.

## Missing avenues — what landed

Six of seven addressed. Public corpora → 1A (#3). Bias transmission → 3B. Contested replication → 4B. Artifact + reliability → 6A rebuilt. Individual differences and think-aloud correctly folded in as *methods* rather than avenues. **Only omission: a human-vs-model baseline** — the team's own cited paper (arXiv:2607.28347, 391 participants) appears zero times in `02`. Minor; defensible as scope control.

## NEW MAJOR ISSUES (all fixed in v3)

**N1. The tiebreak rationale contradicted the table's own weights.** Prose said "I weight gap size most heavily"; the table weighted gap and feasibility equally at ×2. Under gap ×3 the totals become 2A 47 / 3A 46 and **there is no tie**. Symmetrically, the tie survived only because 2A scored Feas 4 — drop it to 3 and 3A leads. The document flagged that buy-in cells could reorder ranks 4–8; it did not flag that **one feasibility cell reorders ranks 1 and 2**.

**N2. "The only gap that survived falsification" was false by the document's own text.** The citation fact-check listed four surviving claims; 5A's is explicitly described as surviving too. This was the entire stated reason 2A outranked 3A.

**N3. The #1 recommendation had no hours, no n, and did not fit the budget.** Every other top-eight avenue carried a person-hour range; 2A carried only "~5–7 weeks" for Phase 1 — 42–58% of the semester — before a 2–6 week ethics wait and a two-stage human study. That is 10–14 weeks of work in a 12-week box with no writeup time, and **the document never did this sum for its own top pick**. Also: the accuracy outcome forbids lay participants, so expert panels cost multiples of the quoted rate, and the full three-item-class design needs ~477 participants, not 160.

**N4. The changelog claimed two changes that did not happen.** (a) "Added positive controls to every 'fails if'" — 2A, 3B, 5A and 6A had none. (b) "old 4B (dosing) folded into 4A" — the word *dosing* appeared nowhere outside that changelog row. Worse: **friction dosing is a gap that SURVIVED the fact-check, while 4A's opt-in framing was partly falsified** — so a surviving novelty claim had been silently deleted and the weaker one kept as the headline. That is the wrong way round.

**N5. "Second-hand numbers are marked" was false.** `01` says no paper was read in full, so *every* number is second-hand and none carried a marker. v1 said nothing and the reader assumed nothing; v2 promised marking and delivered none, so an unmarked number read as verified. A regression.

**N6. The ethics decision tree omitted two avenues that need no pathway** — 1B ("no participants, no IRB" in its own text) and 2A's Phase 1 ("no humans") and Phase 1.5 ("the no-recruitment fallback"). A team in that row would have crossed off the top-ranked avenue unnecessarily. This is the table most likely to be acted on literally.

**N7. Four different answers to "which project," all past 90% depth** — "ranked first overall" (2A), the =1 tie, "if you cannot resolve ethics, pick 3A", and the 1A+3A combination. Each individually reasonable; together, four answers behind ~6,000 words of caveats.

## Is the 2A/3A tie honest or a cop-out?

**Honest in disclosure, evasive in effect, and technically an artifact.** The disclosure ("these criteria do not mechanically produce the ordering… if the team weights safety relevance above novelty, 3A is your project") is exactly what round 1 asked for and most memos never do it. But a tie you can dissolve by writing down the weight you *say* you use is a bookkeeping outcome, not genuine indifference. Combined with N3 and N6, **the document's own machinery pointed at 3A while its prose pointed at 2A.** Recommendation: break the tie for 3A in the first three lines, with 2A named as the pick if ethics is confirmed in week 1 and a Phase-1-only claim is acceptable.

## Feasibility realism, second pass

Estimates are credible in isolation but scoped to the *named* activity only. 1A's 60–100 h excludes corpus licence review, the detection pipeline, the positive control, statistics and writeup — realistically 1.5–2×. 5A's 80–120 h is right for a pilot and wrong for the design as written (a transformer training set plus cross-domain held-out test implies ~10³ generations × ~10 claims, ≈80 h of verification for one annotator before double-coding). 4A's 30 h for the wrapper is honest but excludes the ethics application (10–20 h alone). **3A is the most credible estimate in the document.** Structural problem: with no hours-per-person-per-week, none of the estimates is auditable against the budget.

Verdict by avenue on ~12 working weeks: **3A, 1B, 3B — comfortable. 1A — yes if the pilot is honest. 5A — only as a pilot. 2A as written — no. 4A — only with fast university ethics.**

## NEW MINOR ISSUES

1. Two deadlines for one decision three lines apart (ethics by week 4 vs. week 1–2).
2. Scoring table had no polarity key and no anchors — "disagree with the cells" is unusable when nobody knows what a 3 means.
3. Preregistration appeared once as a bullet, with no gate and no place in the timeline.
4. **Still no target venue or deadline for any avenue** — cheap to fix, and a dated CFP constrains scope better than the gate table.
5. "Version 1" appeared 32 times in a document whose readers never saw version 1; that material belongs in the changelog, not the avenue bodies.
6. Bold inflation: 293 bolded spans in 6,692 words, one every ~23 words. When an ethics warning and a parenthetical carry the same emphasis, emphasis stops working.
7. 6A was both a ranked project (#8) and explicitly "not a parallel workstream."
8. Per-avenue premise checks presented as free — each is 5–15 hours and none appeared in the gate table or the hour lines.
9. arXiv:2512.18489 not in the gate list although 1B's positive control presupposes it.
10. Round-1 minor 7 (5A's "no frontier access" trading against safety relevance) still unaddressed.

## WHAT WORKS — do not break

- **The "Read this before using the ranking" block.** *"'Nobody has done X' here means 'two search passes did not surface X'… An adversarial fact-check then falsified three of the original novelty claims outright. Assume more will fall."* The most valuable paragraph in the corpus.
- **The week-1 gate table** — nine numbered checks each keyed to the avenue it kills.
- **The ethics decision tree** — three rows, three different worlds, consequences spelled out.
- **The power table and three recovery routes**, arithmetic verified.
- **2A's outcome-by-item-class table**, including the "Not valid" column — better than what round 1 asked for.
- **The DM attribution box** and criterion 6 (buy-in) with scores marked as guesses.
- **`Type:` + smallest-intervention on every avenue** — cheap, and it reconnects the document to the source brief.
- **The four real positive controls**, especially 3A's.
- **Naming what the table can't do** (one or two avenues per idea, so it can't surface 2B beating another idea's winner).
- **The cross-cutting asset paragraph** — best strategic sentence in the corpus.
- **`00-source-ideas.md`'s editorial note** — goes further than asked, correctly identifies *seven* top-level bullets, names both judgement calls, hands the correction to AH and DM. The model the rest of the corpus should follow.
- **`01`'s revision-history table**, including "Three of those were wrong corrections of teammates." Retracting a correction of a colleague in public is the hardest thing in the rewrite and it was done cleanly.
