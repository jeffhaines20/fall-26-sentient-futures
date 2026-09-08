# Round 3 — full-text verification

**Date:** 7 September 2026. **What changed since rounds 1–2:** web access. Every previous
round, including both adversarial fact-checks, worked from search summaries and abstracts.
This round read papers.

**Scope.** Seventeen sources, chosen by the priority queue in `CLAUDE.md`: the five whose
falsification would kill a ranked avenue (tier 1), the eight next most load-bearing
(tier 2), the two that were still flagged `[⚠️ UNVERIFIED]` (tier 3), and the two behind
corrections that had been made and then retracted.

**Depth, stated honestly.** Full text was obtained for all seventeen. For the five tier-1
papers, the LessWrong post and the Research Square preprint, that meant reading method,
results and limitations end to end. For the tier-2 papers and the two trap papers, it meant
reading the abstract and introduction in full and then the specific sections bearing on
every claim the documents make — scoring rubrics, sample descriptions, the sentences behind
each quoted number. **That is enough to verify a citation and to catch a scope error, which
is what this round was for. It is not a claim to have read seventeen papers cover to
cover**, and the `[✅ FULL TEXT]` flag in `01` is defined in those terms.

**Method.** Full text via arXiv's HTML renderings where available, publisher PDF otherwise;
the LessWrong post via the site's GraphQL API after the HTML endpoint rate-limited; the
Research Square preprint via its manuscript PDF after the landing page returned a
client-rendered shell. Venue claims were checked against arXiv metadata and, where that was
empty, against the venue's own listing. Claims were compared against the exact sentences in
`01`, `02` and `TEAM-BRIEF.md` rather than against my memory of them.

---

## Headline

**No fabricated paper. No wrong arXiv ID. No wrong headline number.** Every figure the
documents quote from these seventeen sources — psychosis-bench's `p < .001` and its three
means, StoryScope's 93.2% and 61,608, *Choose Your Agent*'s 44% / 19%, PerSpectra's
3,810 / 762 / 100, HumanAgencyBench's six dimensions, Street et al.'s 93% vs. 82% — matched
the source exactly. Two rounds of search-only fact-checking had said the citation base was
sound, and reading the papers confirms it.

**What full text changed was scope, not fact.** Repeatedly — for psychosis-bench,
arXiv:2512.18489, arXiv:2603.22152, CAPTURE, PerSpectra, StoryScope, HumanAgencyBench and
Street et al. — the abstract omitted a condition that decides whether the result transfers to
what this team would be doing. Three of those changed an avenue.

> **The generalisable lesson, since this project will keep citing things:** an abstract
> reports what was found. It does not reliably report *what was varied*, *what scale it was
> measured on*, *which models*, or *what the authors themselves say their finding is limited
> to*. Every material error in this round was in one of those four categories.

---

## Findings that changed a recommendation

**1. Gate 4 — psychosis-bench (arXiv:2509.10970). Avenue 3A's premise holds, and is now
first-hand.** Implicit-vs-explicit is a **two-level factor**: eight hand-written scenario
pairs sharing an identical Phase 1, compared with paired *t*-tests (Table 4). There is no
gradation of implicitness anywhere in the benchmark, and no analysis treating it as
anything but binary. The instrument for locating the boundary does not exist. Also found:
DCS and HES are 0–2 ordinals and SIS is binary with max 6 per scenario; scoring is
LLM-as-judge; the three metrics are scored on different phase windows, so the headline
means are not per-turn averages over all 1,536 turns; scenarios and code are public at
`github.com/w-is-h/psychosis-bench`, which makes 3A's positive control cheap.

**2. Gate 10 — arXiv:2512.18489. Avenue 1B's positive control is dead as written.** The
estimator needs **both** things the gate asked about: γ\* is fitted by minimising KL against
an **analytic discounted-Bayes posterior**, using **output logits** over the outcome set.
§4.3 additionally reads final-layer attention and hidden states. Every model tested is
open-weight and small (Llama-3.1-8B, Mistral-7B, Gemma-2-2B). It is not runnable on a closed
API and does not transfer to beliefs with no normative answer. `02` now specifies three
replacements. **Consequence:** gate 9's logprobs question, which `TEAM-BRIEF` said mattered
"only for Idea 5," now also gates Idea 1.

**3. Gate 2 — arXiv:2603.22152. Avenue 2A's scope resets.** Its three tasks are binary
predictions **with ground truth** (UCI Adult, COMPAS, speed-dating), calibrated to 60–70%
unaided accuracy, and the authors scope their own conclusion to exactly that: *"In our
accuracy-oriented tasks with ground truth, AI panels did elicit informational conformity."*
So the confusion cost was measured where disagreement means one advisor is wrong — not where
plurality is legitimate. Three further details the abstract omits: "wide disagreement" means
specifically a **3-vs-2 near-even split** (a 4-vs-1 split *improved* accuracy); consensus was
**observed, not manipulated** (Rashomon-set sampling, "treated as observed within-subject
factors"), so RQ2 is correlational despite the abstract's "we varied"; and N = 348 Japanese
crowdworkers at ~26–32 per between-subjects cell.

---

## Findings that corrected the review

**4. PersistBench (2602.01146) was in the wrong place.** Listed in `01` §1.5/§1.7 and
`TEAM-BRIEF` as occupying the belief-decay space. It is a **memory-safety** benchmark —
cross-domain leakage and memory-induced sycophancy across 18 models, median failure 53% and
97%. It never measures decay. The title invites the error; the abstract does not.

**5. CAPTURE (2609.02265) does not measure what it appeared to.** Its three exponential
decay rates are **grid-searched on validation and frozen** (0.01 / 0.1 / 0.5 per day),
tuned for downstream win rate. There is no published per-model curve. Two things in it are
directly useful to 1B and were invisible from outside: Appendix B reports that **learning
those rates end-to-end collapsed all three toward 0.08**, and on context switches the
*correct* action is usually to **scope** a belief rather than revise it (71% vs. 4% for a
flat-memory baseline) — which is 1B's main confound, named by someone else.

**6. PERMA (2603.23231) was credited with the wrong diagnostics.** "Positional probing" and
"recency bias" are correct. "Catastrophic forgetting" and "context saturation" are not its
terms; it reports degradation across temporal depth and cross-domain interference.

**7. Gate 3 — PerSpectra (2602.08716) supplies less than claimed.** Every one of its 100
topics is contested by construction, so it covers one of the three item classes 2A's own
outcome table requires and none of the other two. Its 3,810 arguments are GPT-4o expansions
of Kialo opinions seeded with Reddit comments — synthetic, not authentic user text. Its units
are arguments and stances, not questions.

**8. StoryScope (2604.03136): the numbers are right, the framing needed three additions.**
93.2% narrative-only sits against 85.8% style-only, 96.0% combined, and **99.9% for a plain
ModernBERT baseline** — the contribution is interpretability, not accuracy. Its ten
dimensions are NarraBench's literary categories, which do not instantiate in expository
prose. Its pipeline runs an LLM extraction pass over all 61,608 stories. And **the human
half of the corpus is not released** (Books3), so 5A's positive control as written is not
runnable off the shelf.

**9. arXiv:2603.01341's ">94%" was mislabelled** as a fabrication rate in `02` and the
brief. It is the **source-mismatch** rate; biographical hallucination is >93%; citation
omission 91.9% is correct.

**10. Tier 3 — the Research Square preprint (rs-10695464) makes no bibliometric claims.**
`01` flagged that "its bibliometric claims about a 2025→2026 shift look strong and should be
checked." There are none. Its only statement of that kind is one descriptive sentence about
its own corpus. Weight it accordingly: single author (Connor Nitchals, independent), not
peer-reviewed, no version of record, and a PRISMA search that identified **44 candidate
records** and included **20 articles** — two excluded for being preprints. The HES framework
and its five conditions are exactly as `01` describes them.

**11. Tier 3 — the LessWrong post was dismissed too fast, and it bites.** `01` filed
`msFvLtPfDnCEdvrBr` as "fine as inspiration, weak as a citation" because it could not be
fetched. Read: *Do LLMs Change Their Minds About Their Users… and Know It?* (21 Sep 2025)
runs a small version of **avenue 1B's exact study** — turns-to-adapt after a mid-conversation
user change, with an explicit announced-vs-unannounced contrast (immediate vs. 1–2 turns) —
plus an encoded-vs-self-reported gap. It narrows two of 1B's novelty claims. It does not
close them: one 3B open-weight model, one trait (user age), *identity switch* rather than
belief revision, linear probes rather than behaviour, no curve fitted, not peer-reviewed.
**Per this project's standing rule, both claims were hedged further rather than dropped.**

---

## Things checked *because* an earlier draft got them wrong — all held

`CLAUDE.md` lists three corrections that were made and then retracted, with a warning not to
reinstate them. All three were re-checked against full text and the retractions were right:

- **arXiv:2405.18870** is Street et al.'s *positive* ToM result — MoToMQA, GPT-4 at 93% on
  6th-order inferences against adults' 82%, confirmed verbatim. `01` §1.1 correctly remains
  a **question to AH**, not a correction.
- **"Static AI assistance degrades over time"** is stated near-verbatim in arXiv:2510.26518
  ("the effectiveness of AI assistance is not static: as raters improve with practice, even
  evidence-only assistance ceases to help, and leading forms of assistance become actively
  harmful").
- **"Humans over-rely on AI when shown reasoning vs. evidence"** is that paper's own RQ2
  result ("Displaying AI explanation, confidence, and labels leads to over-reliance, but
  just showing search results and evidence fosters more appropriate trust").

One near-miss worth recording as a method note: **HumanAgencyBench's abstract says only that
agency support "does not appear to consistently result from … instruction-following," which
is weaker than `01`'s "a tension between the post-training objective of instruction-following
and human agency support."** Reading only the abstract, that looks like an overstatement to
correct. It is not — `01`'s phrasing is the paper's own, from §1. **This is the fourth wrong
correction this project would have shipped if abstracts were treated as sufficient**, and
the reason the tier-2 list included papers nobody had complained about.

---

## Venue and peer-review status

**A correction to this document's own method.** An earlier version of this section said
"arXiv metadata carried no comments or journal-ref field for any of the eight papers
checked." **That was false, and it was a tooling error:** the arXiv API returns nothing for
these records, and on the `abs` page the field's class is `tablecell comments mathjax`, so a
regex written for `tablecell comments` returned empty every time. Read from the `abs` page.

Six of the fifteen arXiv sources carry a comment field, and three of them are peer-review
status the review was not using:

| ID | arXiv `Comments:` | Consequence |
|---|---|---|
| 2410.13648 (SimpleToM) | `ICLR 2026` | Confirms the venue directly |
| 2603.22152 | `21 pages, 12 figures, accepted to CHI 2026` | Confirms the venue directly |
| 2602.01146 (PersistBench) | `76 pages, 34 figures, ICML (2026)` | New — not previously recorded |
| **2609.02265 (CAPTURE)** | **`Under review at ICLR 2027`** | **Unrefereed. `[PREPRINT]` added** |
| **2512.18489** | **`Under submission`** | **Unrefereed. `[PREPRINT]` added** |
| 2508.03247 | `C3NLP workshop at ACL 2026` | Workshop, not main conference |

**StoryScope (2604.03136) and PerSpectra (2602.08716) carry no venue.** An earlier version of
this round called StoryScope "published, at CHI-tier length" and used that as a precedent in
`02` and `TEAM-BRIEF`; there is no evidence for it and the claim is withdrawn. PerSpectra's
ICLR 2026 attribution rests only on the authors' repository name
(`caisa-lab/ICLR-2026-Pespectra`), which evidences a submission, not an acceptance — that
hedge was right and stands.

**The general lesson:** `[✅ FULL TEXT]` is a *provenance* signal, not a quality one. Reading
a paper in full does not make it peer-reviewed, and the two most consequential first-hand
sources of this round are unrefereed preprints.

---

## What is still unverified

**Roughly 130 of the ~150 cited works.** The tiering was deliberate: these seventeen are the
ones a recommendation rests on. Everything else in `01` remains at the evidence level the
original search-only pass produced, and the documents now say so in those terms rather than
claiming a blanket caveat. The next most valuable reads, if anyone wants them, are the
papers behind numbers `TEAM-BRIEF` quotes to non-specialists — the Vaccaro meta-analysis,
the commercial-chatbot meta-analysis, and the iScience 93%/75% detector figure — because
those are the ones teammates will repeat out loud.

---

# Round 4 — adversarial review of round 3

Round 3 was itself put through the project's standard two-critic pass — one checking
citations and numbers, one checking reasoning and feasibility, both instructed to assume the
author overconfident. **Every finding below was independently re-verified against the source
before being acted on**, per the working practice in `CLAUDE.md`.

**The critics upheld round 3's headline** — no fabricated citation, no wrong arXiv ID, every
quoted figure and every direct quote exact, no forbidden correction reinstated, no
human-reserved question answered, and the tone clean (every correction in round 3 was aimed
at the author's own earlier drafts, not at a teammate). **They also found nine real errors,
two of them consequential.** All are fixed and logged in `01` and `02`.

## The two that mattered

**1. Round 3 minted a novelty claim and it was false.** Having read arXiv:2603.22152, round 3
wrote that nobody had measured plurality's cost where disagreement is *legitimate*, and
credited that framing to Tsuchiya & Baba. Both halves were wrong. The quoted scope sentence
is the second of a pair; the first names **Song et al., arXiv:2411.04578, CSCW 2025** — a
peer-reviewed study of multi-agent influence on societal issues *without* ground truth, cited
six times in the paper round 3 had just read, and summarised in its §2.3 as examining
"opinion change on societal issues without ground truth." The authors present their own
result as "an important counterexample" to it; they are not saying the space is empty.
**2A's surviving gap is the router, which neither paper attempts.** This is the failure mode
convention 3 exists to prevent, and it happened *inside* a verification round — a caution
worth carrying: reading one paper in full tells you about that paper, not about the field
around it.

**2. Round 3 weakened 3A's positive control while calling it confirmed.** "Your explicit rung
must reproduce their published values" tests the team's *stimulus writing* — the project's
dominant risk. Round 3 rewrote it as "run their code on their stimuli," which tests API
plumbing, and labelled that "confirmed runnable" and "the cheapest de-risking step in this
document." It also asserted "your harness is wrong, not the models" three paragraphs from
"the most likely reason your positive control fails is not your fault." The control is now
two explicit steps with a three-way failure diagnosis, and two facts round 3 had in hand but
did not report are now in `01` §3.2: **the judge is `openai/gpt-4o-mini` and is never
validated against human raters** (a clinician validated the *scenarios*), and **the eight
evaluated models are September-2025 OpenRouter snapshots.**

## The other seven

| Finding | Fix |
|---|---|
| **SimpleToM's affiliations were wrong** — round 3 added "AI2 / Stanford / UW"; the paper says **AI2 / NVIDIA / Stanford** | Corrected. This was the only newly-added false fact in the round |
| **`02` still named PersistBench and PERMA as occupying 1B's space** in the sentence justifying 1A's rank — the same commit retracted both elsewhere | Corrected; the crowding claim now rests on CAPTURE and BeliefShift |
| **StoryScope's 6-way attribution includes `human` as one of the six classes** (and it is the most separable, 88.5% F1), so 5A's substitute control "uses only the released AI half" was impossible | Substitute replaced: source your own human corpus, or run five-way AI-only and call it a pipeline check, not a control |
| **StoryScope states its own cost and round 3 omitted it** — ~$2,800 generation, **~$1,600 feature extraction, $4.4k all in**, across **two** full-corpus passes (GPT-5.1 templates, Gemini 3 Flash features), not one | Figures and both passes now in 5A and the brief, against the document's other line items |
| **Round 3's venue-method claim was false** — it reported no arXiv comment fields existed; six do, because the abs-page class is `tablecell comments mathjax` and the API returns nothing | Corrected above; **CAPTURE and arXiv:2512.18489 are unrefereed and now carry `[PREPRINT]`** |
| **1B's replacement positive control is not anchored** — its warrant, BeliefTrack (2605.30219), is search-only, and "same instrument" is what a control must *share*, not what makes it a control | 1B now says plainly that it has no anchored control and that finding one is a week-1 task |
| **`TEAM-BRIEF` said the 0–2 scales made our analysis "simpler"** while `02` said "do not treat DCS as continuous"; it also omitted that **unanimous trials had the highest accuracy** and that consensus was observed rather than manipulated | Both corrected in the brief. The file most teammates open had the wrong version of two findings |

Smaller: the brief's critique count was updated to the pre-round-3 number; its enumeration of
the seventeen added to fifteen; `CLAUDE.md` named a flag string (`[✅ READ IN FULL]`) that does
not exist; CAPTURE's code is "will be released," not released; PerSpectra had "all four
figures confirmed" when three are listed; HES and SIS share one measurement window rather than
occupying two; and DIV_3 produced *no gain* rather than a loss.

## One thing the critics flagged that was not changed

**No scoring cell moved.** The reasoning critic argued that 2A's feasibility should drop (its
Phase 1 got harder) and 3A's gap should rise (its premise is now first-hand), which would
widen the 3A–2A gap from one point to six. That is a defensible reading and it is now stated
openly in `02` rather than left implicit — but moving cells on the strength of the author's
own verification round, in a ranking the document explicitly presents as a judgement call for
the team to argue with, would be the wrong direction of travel. **The evidence is recorded;
the cells are unchanged; the team can move them.**

## One upside the critics surfaced

psychosis-bench's implicit/explicit binary moves **two** things at once — §3.1 defines both
levels in terms of delusional beliefs *and* harmful intent. A ladder that **crosses**
delusion-implicitness with harm-request-implicitness is a stronger contribution than the
one-dimensional ladder 3A originally proposed, and the confound is the argument for it. Now
in `01` §3.2.
