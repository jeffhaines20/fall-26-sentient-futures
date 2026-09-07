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

**What full text changed was scope, not fact.** Nine times out of the seventeen, the
abstract omitted a condition that decides whether the result transfers to what this team
would be doing. Three of those changed an avenue.

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

## Venue claims

arXiv metadata carried no comments or journal-ref field for any of the eight papers checked,
so the venue attributions in `01` were verified independently: **SimpleToM at ICLR 2026**
(iclr.cc virtual listing) and **arXiv:2603.22152 at CHI 2026** (ACM DL,
doi:10.1145/3772318.3791648, Tsuchiya & Baba) are both confirmed. PerSpectra's ICLR 2026
attribution rests on the authors' own repository name (`caisa-lab/ICLR-2026-Pespectra`),
which evidences a submission, not an acceptance — treat it as the weaker claim.

---

## What is still unverified

**Roughly 130 of the ~150 cited works.** The tiering was deliberate: these seventeen are the
ones a recommendation rests on. Everything else in `01` remains at the evidence level the
original search-only pass produced, and the documents now say so in those terms rather than
claiming a blanket caveat. The next most valuable reads, if anyone wants them, are the
papers behind numbers `TEAM-BRIEF` quotes to non-specialists — the Vaccaro meta-analysis,
the commercial-chatbot meta-analysis, and the iScience 93%/75% detector figure — because
those are the ones teammates will repeat out loud.
