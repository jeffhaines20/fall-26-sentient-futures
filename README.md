# Sentient Futures — project selection, fall 2026

A literature review and a set of ranked project proposals, built to help this team pick one
semester project out of the six ideas from our September 1st brainstorm.

**This is a research repo, not a codebase.** There is nothing to install, build or run.
Everything here is Markdown.

---

## The recommendation, in three sentences

**Build the delusion-cue ladder** — avenue **3A**. *psychosis-bench* found that models
confirm delusions and enable harm significantly more when a user *implies* delusional
content than when they state it outright, and nobody has mapped where that line sits: the
published comparison is a straight two-way split with no gradation of implicitness anywhere
in the benchmark. Write the same delusional content at four levels of directness, score it
with the existing benchmark's public rubric, and find where each model's safety behaviour
falls off.

| | |
|---|---|
| **Effort** | ~50–70 hours total, of a ~250–350 hour semester |
| **Participants** | **None** — no recruitment, no IRB application, no participant cost |
| **Needs** | API access, and a clinician to review the test material |
| **Non-technical work** | Writing the test material is the bulk of it, and the part that most needs care |

The runner-up is **2A, the plurality router** (*when* should an assistant show multiple
viewpoints?). It has the better gap; it does not fit a semester without scoping down.

---

## Where to start

| If you are… | Read | Length |
|---|---|---|
| **anyone on the team** | [`TEAM-BRIEF.md`](TEAM-BRIEF.md) | ~20 min. Plain language, no jargon. **This is the only file most people need.** |
| **leading the project choice** | [`research/02-ranked-avenues.md`](research/02-ranked-avenues.md) | 18 avenues, ranked, with effort, sample sizes, costs, and the one check that could kill each |
| **owning a particular idea** | [`research/01-literature-review.md`](research/01-literature-review.md) | ~150 papers across the six ideas, organised by idea, with reviews and meta-analyses flagged |
| **checking what we actually said** | [`research/00-source-ideas.md`](research/00-source-ideas.md) | Our brainstorm text verbatim, plus a note on how it was grouped |
| **auditing the working** | [`research/critiques/`](research/critiques/) | Six critique documents from four review rounds — where earlier drafts were wrong and why |

`SF_ Initial Meeting Sept 1st, 2026 (1).docx` is the source meeting doc.
[`CLAUDE.md`](CLAUDE.md) is for AI sessions working on this repo, not for people.

---

## How much to trust this

**Built in three stages, and the provenance matters:**

1. **The review was originally written without reading a single paper.** The environment
   blocked `arxiv.org`, `nature.com` and most publisher domains, so every claim came from
   search summaries and abstracts.
2. **Seventeen sources were later read in full** — every paper a ranked avenue's premise
   rests on, plus the two that had been unverifiable, plus the two behind corrections that
   had been made and then retracted. **No fabricated paper, no wrong arXiv ID, no wrong
   headline number.** What full text changed was *scope*: abstracts leave out the conditions
   that decide whether a result transfers.
3. **That verification round was itself adversarially reviewed**, which caught nine errors it
   had introduced — including a novelty claim it minted that turned out to be false, and a
   positive control it weakened while calling it confirmed.

**What that buys you:** the papers marked `[✅ FULL TEXT]` in `01` are a citable evidence
base. **The other ~130 are not** — they are leads. An unmarked citation has not been read.

**Two standing cautions:**

- **"Nobody has done X" means "three search passes and full text on seventeen papers did not
  surface X."** Three of the original novelty claims have been falsified outright and two
  more narrowed — and a sixth, minted *during* the verification round, was killed by the
  review of it. Assume more will fall, and run a proceedings search plus a forward-citation
  check before committing to any avenue.
- **The ranking is a judgement call and says so.** 3A beats 2A by one point, and that point
  is a single feasibility cell. The scoring table exists so you can disagree with the cells,
  not just the ordering.

---

## The six ideas

Grouped from the brainstorm's seven top-level bullets — **that grouping is a judgement call
and needs AH and DM to confirm it** (see below).

1. **Aligning artificial minds to human wellbeing** — do LLMs track and update what users
   believe? *More crowded than expected; at least six 2026 benchmarks test close to this.*
2. **Cooperative human-AI frameworks** — when should an AI show multiple viewpoints?
   *The most open routing question in the review.*
3. **Cognitive biases, hallucination and "AI psychosis"** — *the second most crowded area,
   and it got crowded fast during 2025–26. Contains the recommended project.*
4. **Countering cognitive atrophy through epistemic design** — designing AI that makes people
   think more, not less.
5. **Combatting deceptive alignment and misinformation** — can we detect when a model is
   making things up? *The most technical avenue here.*
6. **Multi-layered trust framework** — *the most crowded of the six; the closest published
   framework predates the brainstorm by three years.*

Each idea has three avenues in `02`. Eight are scored and ranked; the top three are **3A**
(implicit delusion boundary, 46), **2A** (plurality router, 45) and **1A** (stale beliefs in
real corpora, 43). The full table, with anchors and weights, is in `02`.

---

## Blocked on humans — four questions this repo cannot answer

1. **AH** — arXiv:2405.18870 is cited at the end of a two-clause sentence and fits one clause
   but not the other. Which did you mean? (This is a question, not a correction — an earlier
   draft called it a misreading and that was wrong.)
2. **DM** — do you endorse the reframe of Idea 4? It changes a scoring cell and moves avenue
   4A from 6th to joint-5th.
3. **AH and DM** — is the six-idea grouping right? The source doc has *seven* top-level
   bullets, and two judgement calls were made to get to six.
4. **The team** — **is there an IRB pathway?** University board, paid independent board, or
   none? This decides which avenues are possible at all. Good news: most of the top-ranked
   avenues, including the recommendation, need none.

**Two things to start on day one**, because they have long lead times: the IRB question
above, and **what our API budget is** — including whether our endpoints expose token
probabilities, which now gates work under both Idea 1 and Idea 5.

---

## Conventions, if you edit these files

- **Corrections are logged, not silently applied.** `01` and `02` both carry revision-history
  tables. Teammates may have read an earlier draft, so when you fix something, add a row.
- **Flags are load-bearing.** `[REVIEW]` `[META-ANALYSIS]` `[BENCHMARK]` `[PREPRINT]`
  `[✅ FULL TEXT]` `[⚠️ CONTESTED]` `[⚠️ UNVERIFIED]`. The team asked for reviews and
  meta-analyses to be flagged; keep the legend at the top of `01` accurate. `[⚠️ UNVERIFIED]`
  currently appears in the legend and nowhere else — both papers that carried it were read.
  **Don't read its absence as "everything else is verified";** the live split is
  `[✅ FULL TEXT]` versus everything.
- **Don't re-run the review.** It has been through four rounds. Verify, extend and correct.
- **Every round used two adversarial critics** — one on citations and numbers, one on
  reasoning and feasibility, both instructed to assume the author is overconfident. It is
  4 for 4 on finding real errors, including in the round that "only verified things."
