# CLAUDE.md — Sentient Futures literature review

## What this repo is

A **research project, not a codebase.** There is no code, no build, no tests. The deliverable
is a literature review and a set of ranked project proposals for an AI-safety incubator team
choosing a semester project.

The source of truth for what the team wants is `SF_ Initial Meeting Sept 1st, 2026 (1).docx`
(extracted to `research/00-source-ideas.md`).

| File | What it is |
|---|---|
| `TEAM-BRIEF.md` | Plain-language summary. **The only file most teammates will open.** |
| `research/00-source-ideas.md` | The team's brainstorm, verbatim, plus a note on how it was grouped |
| `research/01-literature-review.md` | ~150 papers across six ideas; reviews/meta-analyses flagged |
| `research/02-ranked-avenues.md` | 18 avenues (3 per idea), ranked, with effort/cost/gates |
| `research/critiques/` | Six critique documents from four review rounds — the newest, `round-3-full-text-verification.md`, is the record of the papers being read |

---

## 🟢 The verification queue has been run. Don't run it again.

The review was originally built in an environment where **`arxiv.org`, `nature.com`, and most
publisher domains were blocked by network egress policy** — every claim came from search
summaries and abstracts.

**A later session had web access and pulled full text on the seventeen load-bearing
sources**, checking every claim the documents make against the sections that support it. All
five tier-1 papers, all eight tier-2 papers, both tier-3 sources, and the two papers behind
retracted corrections. The record is `research/critiques/round-3-full-text-verification.md`;
the outcomes are logged in the revision tables of `01` and `02` and in `TEAM-BRIEF`'s week-1
table, which is now a results table rather than a reading list.

**Outcome: no fabricated paper, no wrong arXiv ID, no wrong headline number.** Every quoted
figure matched. What full text changed was *scope* — nine of seventeen abstracts omitted a
condition that decides whether the result transfers. Three of those changed an avenue:

- **3A (the #1 recommendation) survives and is now the best-supported claim in the
  document.** psychosis-bench's implicit/explicit contrast is a two-level paired-*t*-test
  with no gradation of implicitness anywhere. Its code and scenarios are public.
- **2A's scope reset.** arXiv:2603.22152's tasks all have ground truth, and the authors
  scope their finding to that themselves.
- **1B's positive control was replaced.** arXiv:2512.18489 needs output logits *and* a
  normative posterior, on open-weight models only.

### What is worth doing now, if you have web access

**Not the tier-1/2/3 queue — it's done.** The remaining ~130 cited works are still
search-only. The highest-value next reads are the papers behind numbers `TEAM-BRIEF` quotes
to non-specialists, because those are what teammates will repeat out loud: the **Vaccaro
*Nature Human Behaviour* meta-analysis**, the **commercial-chatbot meta-analysis**
(*Psychotherapy & Psychosomatics* 2026), and the **iScience 93%/75% detector figure**
(PMC12969083). Same protocol: verify in place, log a revision row, don't re-run the review.

**One method note from round 3, because it nearly caused a fifth wrong correction.**
HumanAgencyBench's *abstract* states its instruction-following finding much more weakly than
`01` does — read only the abstract, `01` looks like it overstates. It doesn't; `01`'s
phrasing is the paper's own words from §1. **Check the body before "correcting" the review
against an abstract.**

---

## Conventions that must be preserved

**1. Flags.** `[REVIEW]` `[META-ANALYSIS]` `[BENCHMARK]` `[PREPRINT]` `[⚠️ UNVERIFIED]`
`[⚠️ CONTESTED]`. The team explicitly asked for reviews and meta-analyses to be flagged so
they can get oriented fast. Keep the legend at the top of `01` accurate.

**2. Corrections are logged in place, not silently applied.** Both `01` and `02` carry
revision-history tables listing what earlier drafts got wrong. Teammates may have read an
earlier version. **When you correct something, add a row — don't just edit the text.**

**3. Novelty claims are hedged on purpose.** `02` states the rule: *"'Nobody has done X' here
means 'three search passes and seventeen full-text reads did not surface X.'"* Three original
novelty claims were falsified by adversarial search and **two more were narrowed by round 3**
(1B's implicit-revision and elicited-vs-behavioural claims, both partly occupied by the
LessWrong post). **Do not un-hedge any of these**, even if a search comes back empty — the
right way to strengthen them is forward-citation checks and proceedings searches, not removing
the caveat.

**4. Second-hand numbers are declared collectively, not marked individually.** An earlier
version promised per-number markers and didn't deliver them, which made unmarked numbers read
as verified. **Round 3 introduced the one split that is honest and complete: papers marked
`[✅ READ IN FULL]` (seventeen of them) versus everything else.** Keep that split exact — if
you read a new paper, add the flag; do not add it to anything you have only searched.

---

## ⚠️ Traps — things a well-meaning session will get wrong

**Do not reinstate these three corrections. They were made, then retracted as wrong:**

1. **arXiv:2405.18870 is not "misread" by the team.** AH's sentence has two clauses and the
   citation fits one of them. §1.1 asks AH which they meant. It is a *question*, not a
   correction. An earlier draft called it a misreading and that was over-confident.
2. **"Static AI assistance degrades over time"** is **supported** — stated almost verbatim in
   arXiv:2510.26518, which the team itself cited. An earlier draft flagged it as unsourced.
3. **"Humans over-rely on AI when shown reasoning vs. evidence"** is **supported** by the same
   paper's own experiment. An earlier draft called it "more contested than the doc implies,"
   which unfairly implied the team overstated its own source.

**Other live traps:**

- **`Choose Your Agent` (2602.12089): participants never choose among three modalities.** Each
  game grants one; the choice is use-vs-not. This wrong description was introduced *by a
  correction* and had to be fixed in three separate places. Check before restating it.
- **The power table's first two rows are per-group, not totals.** ~162 per group = ~325 total.
  A 2× error here survived two revisions.
- **The ranking is a judgement call and says so.** 3A beats 2A by one point, and that point is
  one feasibility cell. Don't present it as a measurement.
- **`02` has 18 avenues but the ranking table shows 8.** That's deliberate and stated.
- **Don't re-run the whole literature review.** It has been through four review rounds.
  Verify, extend, and correct — don't start over.
- **`PersistBench` (2602.01146) is not about forgetting curves**, despite its title *When
  Should Long-Term Memories Be Forgotten by LLMs?* It measures memory *safety* — cross-domain
  leakage and memory-induced sycophancy. An earlier draft listed it as occupying avenue 1B's
  space; round 3 removed it. Don't put it back on the title.
- **The LessWrong post `msFvLtPfDnCEdvrBr` is now read and is load-bearing.** It is the
  nearest existing work to avenue 1B. Do not restore the old "fine as inspiration, weak as a
  citation" framing, and do not delete the "not peer-reviewed" caveat either — both halves
  are needed.
- **arXiv:2603.01341's `>94%` is a source-mismatch rate, not a fabrication rate.** Hallucination
  is >93%, citation omission 91.9%. This was mislabelled once already.

---

## Open questions only humans can answer

These are asked in `TEAM-BRIEF.md` and are **not** yours to resolve:

1. **AH** — which clause was arXiv:2405.18870 cited for?
2. **DM** — do you endorse the reframe of your Idea 4? (It changes a scoring cell and moves
   avenue 4A from 6th to joint-5th.)
3. **AH and DM** — is the six-idea grouping right? The source doc has *seven* top-level
   bullets; two judgement calls were made to get to six.
4. **The team** — is there an IRB pathway? This decides which avenues are possible at all.

If a new finding bears on one of these, note it — don't answer on their behalf.

---

## Working practices

**Branch:** whichever branch your session is told to use — rounds 1–2 used
`claude/team-ideas-literature-review-9wmz0x`, round 3 used
`claude/project-context-papers-61rhca`, both merged to `main` via PR. Commit and push as you
go; the container is ephemeral.

**Commits:** descriptive body explaining *what was wrong* and *why it changed*, not just what
was edited. Keep the `Co-Authored-By` trailer your session specifies.

**The critic pattern worked and is worth reusing.** Every round used two adversarial
subagents — one checking citations and numbers, one checking reasoning and feasibility — with
instructions to assume the author is overconfident. It caught, among other things, a 2× power
error, a backwards meta-analysis, a misattributed first author, and three wrong corrections of
teammates. **Independently re-verify a critic's claims before acting on them:** one round-2
critic asserted a power-formula error that was itself checkable, and checking it confirmed the
critic — but the reverse has also happened.

**Editing style:** these are long documents. Use exact-match Python replacements with
assertions rather than freehand rewrites, so a failed match is loud rather than silent.
Verify arithmetic in tables with a script — two errors and an unsorted ranking table shipped
before that check was added.

**Tone:** the documents correct teammates by name in places. Keep that fair, specific, and
non-condescending — a review that miscorrects colleagues loses the room, which is exactly what
happened in round 1 and had to be walked back.
