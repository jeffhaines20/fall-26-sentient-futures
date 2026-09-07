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
| `research/critiques/` | Five critique documents from three review rounds |

---

## 🔴 Read this first: the whole review was built without reading a single paper

The session that produced this work ran in an environment where **`arxiv.org`, `nature.com`,
and most publisher domains were blocked by network egress policy.** Every claim in
`01-literature-review.md` comes from search-result summaries, abstracts, and publisher landing
pages. This is disclosed at the top of that file and again in `TEAM-BRIEF.md`.

**If this session has working web access, the highest-value thing you can do is verify the
load-bearing papers against their actual PDFs.** Not re-run the review — verify it.

Two rounds of adversarial fact-checking already ran and found **no fabricated papers and no
invented arXiv IDs** across 50+ spot-checks. But they were *also* search-only. Corroborating a
number from an abstract is not reading the method that produced it.

### Verification queue, in priority order

**Tier 1 — a project dies if these are wrong.** Each is the stated premise of a ranked avenue:

| Paper | What to check | If wrong |
|---|---|---|
| **psychosis-bench** — arXiv:2509.10970 | Is the implicit-vs-explicit gap (p < .001) merely *reported*, or already *characterised*? What scale are DCS/HES/SIS on? | **Kills the #1 recommendation (3A)** |
| **arXiv:2603.22152** (CHI 2026) | Exactly what it measured about plurality → confusion | Resets avenue 2A's scope |
| **CAPTURE** — arXiv:2609.02265 | Does it already fit a decay curve to user-belief state? | Kills avenue 1B |
| **StoryScope** — arXiv:2604.03136 | Is 93.2% macro-F1 on structure alone right, and are the features portable to expository text? | Undercuts avenue 5A |
| **arXiv:2512.18489** | Does its estimator need logprobs or a normative posterior? | Kills 1B's positive control |

**Tier 2 — reshape an avenue but don't kill it:** PERMA (2603.23231) · PersistBench
(2602.01146) · PerSpectra (2602.08716) · SimpleToM (2410.13648) · HumanAgencyBench
(2509.08494) · Choose Your Agent (2602.12089) · arXiv:2508.03247 · arXiv:2603.01341.

**Tier 3 — still flagged `[⚠️ UNVERIFIED]` in the review:** the LessWrong post
(`msFvLtPfDnCEdvrBr`, domain was blocked, also not peer-reviewed) and the Research Square
PRISMA preprint (`rs-10695464`) and its bibliometric claims.

**When you verify something, update it in place and say so** — see the conventions below.

---

## Conventions that must be preserved

**1. Flags.** `[REVIEW]` `[META-ANALYSIS]` `[BENCHMARK]` `[PREPRINT]` `[⚠️ UNVERIFIED]`
`[⚠️ CONTESTED]`. The team explicitly asked for reviews and meta-analyses to be flagged so
they can get oriented fast. Keep the legend at the top of `01` accurate.

**2. Corrections are logged in place, not silently applied.** Both `01` and `02` carry
revision-history tables listing what earlier drafts got wrong. Teammates may have read an
earlier version. **When you correct something, add a row — don't just edit the text.**

**3. Novelty claims are hedged on purpose.** `02` states the rule: *"'Nobody has done X' here
means 'two search passes did not surface X.'"* Three original novelty claims were falsified by
adversarial search. **Do not un-hedge these**, even if a search comes back empty — with real
web access you can now strengthen them properly (forward-citation checks, proceedings
searches), which is better than removing the caveat.

**4. Second-hand numbers are declared collectively, not marked individually.** An earlier
version promised per-number markers and didn't deliver them, which made unmarked numbers read
as verified. If you verify numbers individually, you may reinstate per-number marking — but
then it has to be complete.

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
- **Don't re-run the whole literature review.** It has been through three critique rounds.
  Verify, extend, and correct — don't start over.

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

**Branch:** `claude/team-ideas-literature-review-9wmz0x`. Commit and push as you go; the
container is ephemeral.

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
