# What's Already Been Done on Our Six Ideas — and Where the Gaps Are

*A plain-language summary for the Sentient Futures team. ~20 minutes to read.*
*Written September 2026 by Claude (Opus 5), from the ideas in the Sept 1 brainstorm doc.*

---

## Start here: the one-paragraph version

I searched recent research on all six ideas from our brainstorm. **All six have real
literature behind them, and some are far more crowded than they look.** Roughly, from most
crowded to least: **Idea 6 (Trust Framework) → Idea 3 (AI psychosis) → Idea 1 (belief
tracking) → Idea 4 (cognitive atrophy) → Idea 5 (deception detection) → Idea 2's specific
routing question, which is the most open thing in this review.**

**My recommendation is a project I'll call the *delusion-cue ladder* — it's avenue **3A** in
the detailed file: figure out why AI chatbots handle delusional thinking much worse when a
user hints at it than when they state it outright.** It needs no study participants, no ethics approval, and roughly 50–70 hours of
work spread across the team — against a semester budget of maybe 250–350 hours. It can start
on day one.

Everything below explains why, plus what I found for each idea.

---

## The files, and which one you want

| File | What it is | Who should read it |
|---|---|---|
| **This one** | Plain-language summary | Everyone |
| `research/02-ranked-avenues.md` | 18 concrete project ideas, ranked, with effort, sample sizes, costs, and the checks that could kill each | Whoever's leading the project choice |
| `research/01-literature-review.md` | The full literature review, ~150 papers, organised by idea | Whoever owns a particular idea |
| `research/00-source-ideas.md` | Our brainstorm text, with a note on how I grouped it | **AH and DM — please check this** |
| `research/critiques/` | Six critique documents from four review rounds, which found my errors | Only if you want to see the working |

---

## Some vocabulary, so nothing below is opaque

| Term | What it means |
|---|---|
| **LLM** | Large Language Model — ChatGPT, Claude, Gemini and similar |
| **IRB** | Institutional Review Board: the committee that must approve research involving human participants. Getting approval typically takes 2–6 weeks *after* you submit |
| **API** | The paid programmatic access that lets us run thousands of queries against a model automatically |
| **arXiv ID** | A number like `2509.10970`. Every paper is free at `arxiv.org/abs/<the number>` |
| **Annotation** | Reading transcripts and hand-labelling them against a written rulebook. **This is the main non-programming job in most of these projects, and it's usually the bulk of the work** |
| **Meta-analysis** | A study that statistically pools results from many earlier studies. The strongest evidence we have — read these first |
| **Systematic review** | A structured survey of a field. Fastest way to get oriented |
| **Benchmark** | A standard test set for models. Cheap for us to reuse — we don't have to build one |
| **Theory of Mind (ToM)** | The ability to reason about what someone else believes, wants, or intends |
| **Statistical power** | The chance a study detects a real effect. Standard target is 80%. Underpowered studies waste everyone's time |
| **Preprint** | A paper posted publicly before peer review. Useful, but weaker evidence |

---

## How much to trust this

**This review was originally written without reading a single paper in full.** The tool I
was running in blocked access to arxiv.org, nature.com and most journal websites, so
everything came from search results, abstracts and publisher summaries.

**That has since been partly fixed. I've now got the full text of seventeen papers and
checked what this brief says against them** — the eleven in the week-1 list below, plus
*StoryScope* and the structural-hallucination paper behind Idea 5, plus the two sources I'd
previously had to mark "unverified," plus the two behind corrections I'd made and then
retracted.

**How I read them matters, so here it is plainly.** For the five papers our top
recommendations rest on, I read method, results and limitations end to end. For the other
twelve I read the abstract and introduction and then the specific sections bearing on what
this review says about them. That catches a wrong number reliably. It is much weaker at
catching *what a paper contains that I never thought to mention* — and that is exactly how
I missed something big (see the correction two paragraphs down). **If you own an idea, still
read its two nearest papers yourself.** I checked my claims against the papers, not the
papers against my claims. **Nothing was
fabricated, no reference was fake, and every headline number I'd quoted turned out to be
exactly right.** What was wrong was *scope*: abstracts leave out the conditions that decide
whether a result actually transfers to what we'd be doing, and in three places those
conditions changed the plan. Section "Week 1" below now reports what each paper said
instead of asking us to go find out.

**The other ~130 papers are still second-hand.** Treat the week-1 papers as solid and
everything else as a lead.

Two rounds of fact-checking followed, each with a citation critic and a strategy critic. They
found **no made-up papers and no fake references** across 50+ spot-checks — but they did find
real errors in my drafts:

- **I wrongly "corrected" three things in our brainstorm doc that were right.** Two of AH's
  bullet points — one I flagged as unsupported, one as overstated — are stated almost
  word-for-word in the paper AH cited.
- **I got one meta-analysis backwards** (reported a result as null when it was significant).
- **I claimed something had never been measured when it had been** — and that claim was the
  entire justification for my original top recommendation.
- **I made a maths error that doubled a study's required sample size**, so the friction study
  I'd ranked second at the time was itself underpowered — exactly the mistake I'd criticised.
- **Reading the papers found two more.** I said one preprint made "bibliometric claims" it
  does not make, and I dismissed a blog post I couldn't fetch as "weak as a citation" when it
  is in fact the closest existing work to one of our candidate projects.
- **And then a review of that reading found a third, which was mine and was worse.** Having
  read the CHI multi-AI paper, I wrote that nobody had studied the case Idea 2 cares about —
  where several views are legitimately in play. **That was false.** The paper I had just read
  cites such a study six times ([Song et al., CSCW 2025](https://arxiv.org/abs/2411.04578)),
  and I had also credited the CHI authors with a novelty claim they never made. Two adversarial
  reviewers caught it. It is logged in `01` and `02`; the corrected version is in the Idea 2
  section below, and it is *more* useful than what I originally wrote.

All are fixed and logged in the detailed files. But the pattern matters:

> **When I say "nobody has done X," that means "three searches, plus the full text of the
> seventeen papers that matter most, didn't find X."** Better than it was. Still a lead, not
> a fact.

The week-1 reading list below has now been done, and its results are in the table. Also
worth knowing: **the assumptions behind my ranking are inferred, not confirmed** — team size
~4–6, ~5 hours per person per week, ~12 working weeks after we decide. If any of those is
wrong, the ranking moves.

---

## Three things I need from AH and DM

**1. AH — one of your citations is ambiguous, and I need to know what you meant.**

You wrote that previous work argues LLMs *aren't* capable of true Theory of Mind "despite
their capacity to match human performance on higher-order ToM benchmarks," and cited
arXiv:2405.18870.

That paper (Street et al.) is the one showing LLMs **do** match adult human performance —
GPT-4 actually beats adults on the hardest level. So:

- If you meant it to support the "*despite matching human performance*" half — **it's
  exactly right**, no change needed.
- If you meant it to support the "*not capable of true ToM*" half — it's the wrong paper,
  and the reviews listed in the detailed file make that argument instead.

Either way, cite the peer-reviewed version rather than the preprint: *Frontiers in Human
Neuroscience* (2025), doi:10.3389/fnhum.2025.1633272.

*(My first draft called this a misreading and said a reviewer would catch it. That was
overconfident — the sentence is genuinely ambiguous.)*

**2. DM — I reframed your Idea 4, and that's your call, not mine.**

You proposed a Socratic + CBT/DBT hybrid assistant, then added: *"However, users will need to
choose this higher-friction path when they deem it appropriate for the situation."*

I built a project around that "however" clause — studying when people *voluntarily choose* the
more effortful mode — and ranked it above your actual proposal. **That may be the right call,
but it should be yours.**

In your proposal's favour: **the search didn't find your specific hybrid anywhere.** Socratic
tutors exist and CBT/DBT chatbots exist, but not the combination aimed at general knowledge
work. My hesitations are that "unbuilt combination" is a weaker claim than "unanswered
question"; that evaluating "psychological growth" needs validated instruments and a long-term
study a semester can't support; and that there's a clinical-ethics dimension needing an
advisor. **A compromise: make the CBT/DBT structure one of the modes in the opt-in study, so
your idea stays in the project.**

Separately — your Idea 3 had two halves, and my first draft only served one. You asked how
LLMs "inherit **and/or exploit**" cognitive biases. There's now a ranked avenue (4th overall)
on the *exploit* half: does a model amplify the *user's* biases over a conversation? It scores
highest in the table on "does the person who proposed this recognise it as their question" —
you tell me whether that's right.

**3. Both of you — I grouped our brainstorm into six ideas, but the doc has seven top-level
bullets.** Five are titled ideas; two are untitled bullets with your initials. I folded AH's
into the Cooperative Frameworks idea and promoted DM's to its own idea. **If I grouped yours
wrong, tell me — it changes which literature I searched.**

---

## What I found, idea by idea

### Idea 1 — Do LLMs track and update what users believe? (AH)

**What exists:** More than expected. At least six 2026 benchmarks test almost exactly this —
whether a model tracks a user's beliefs and updates when they change. One (*CAPTURE*) was
published five days before I searched. There's also a developed debate on whether LLMs update
"like a Bayesian" (rationally weighing new evidence), and the best current answer is
interesting: models look rational on average but systematically over-forget older evidence.

**The most useful established finding:** models can *state* what someone believes but fail to
*act* on it. They pass the quiz and flunk the practical.

**What's still open:** every *benchmark* I found uses *explicit* revision — the user says
"I've changed my mind." Subtle or implied change, which is how real conversations work, is
much less studied. Also open: does looking at *real* conversations, rather than constructed
test items, show assistants still acting on beliefs users have already abandoned?

**Honest correction:** my first draft said nobody had measured how fast models forget beliefs
*about users*. Wrong — several groups have.

**Two updates from reading the papers.** First, I had *PersistBench* wrong: despite its title
("When Should Long-Term Memories Be Forgotten by LLMs?") it's about memories being used
*unsafely*, not about forgetting curves. So this space is slightly less crowded than I said.
Second, and cutting the other way: **a blog post I couldn't fetch earlier turns out to have
done a small version of exactly the "implied change" study I called untested** — it measured
how many turns a model takes to notice a user has changed, with and without being told, and
found the difference. It's one small open-source model and one user attribute, so it doesn't
close the question, but we'd have to cite it rather than claim the ground is empty.

---

### Idea 2 — When should an AI show multiple viewpoints? (AH)

**The single most important number in this review:** a 2024 meta-analysis in *Nature Human
Behaviour* pooled **106 studies** and found **human–AI teams usually perform *worse* than
whichever of the two is better alone.** Losses concentrate in decision-making tasks, gains in
content creation — **and the deciding factor is which party is better at the task.**
Combination helps when the *human* is better and hurts when the *AI* is better. Any project
about designing better AI interfaces has to say where it sits relative to that.

**What exists:** a lot on *how* to present multiple perspectives — there's a whole
"pluralistic alignment" literature. And, importantly, work measuring what plurality *costs*:
a CHI 2026 study found that when AI advisors disagree widely, users get confused and rely on
them worse. So AH's worry about paralysis is real and already measured.

**Reading that CHI paper in full made our question sharper.** All three of its tasks have a
correct answer — predicting income, reoffending and dating outcomes — and the authors are
explicit that their finding holds "in our accuracy-oriented tasks with ground truth." **So
they measured what happens when AI advisors disagree because one of them is wrong.**

**I first wrote that nobody had studied the other case — where several views are legitimately
in play — and that was wrong.** The same paper cites such a study six times:
[Song et al., CSCW 2025](https://arxiv.org/abs/2411.04578), which had people discuss *social
issues with no right answer* with one AI or several, and found that several agents increased
the social pressure people felt and shifted their opinions more. The CHI authors position
their own result as "an important counterexample" to it. **So both halves of the space are
occupied — and the two papers disagree, along exactly the line we care about.** That is
better material than a clean gap: we can position against both. What neither of them does is
build a *rule for when to be plural*, which is still our actual question.

Three details worth having before anyone quotes this paper: accuracy was **highest when all
five AIs agreed**; a lone dissenter helped people relative to their own unaided baseline; and
the near-even 3-against-2 split produced **no gain**, not a loss. Also, the experimenters
did not *set* how much the AIs disagreed — they took whatever split came out and analysed it
afterwards, so this is a correlation. Manipulating the split directly would be a contribution
in itself.

**What's still open — the most open thing in this review:** **nobody has built the router.**
Everything either shows multiple views always, or studies the properties of doing so. A
*decision rule* for when plurality helps versus when it just adds confusion doesn't exist. I
tried twice, with five different search framings, to find work that would kill this claim, and
couldn't. That's the strongest any claim here gets — still a lead, not a fact.

**Honest correction:** my first draft said the paralysis cost was "asserted everywhere and
measured nowhere," and made that the reason to rank this idea first. It's measured. The
routing gap is real; that particular claim wasn't.

---

### Idea 3 — Cognitive biases, hallucinations and "AI psychosis" (DM)

**The second most crowded of our ideas**, and it got crowded fast during 2025–26. There are
already benchmarks for delusion reinforcement, several clinical reviews, multiple
meta-analyses on mental-health chatbots, and a live debate about whether "AI psychosis" is
even the right term. **Two preprints argue it isn't** — worth reading, because engaging that
debate beats assuming the concept.

One finding worth knowing: the central benchmark here (*psychosis-bench*) tested 8 models
across 1,536 conversation turns, scoring three things — how often models confirmed a delusion,
how often they enabled harm, and how often they intervened for safety. Delusion confirmation
ran high (mean 0.91) and safety intervention low (mean 0.37). *I haven't been able to see what
scale those sit on, so treat the direction as solid and the magnitude as unverified.* Models
were **significantly worse when the delusional content was implied rather than stated.**

**That last finding is unexplained, and it's my recommended project.**

**Also open:** DM's "exploit" half. Almost all existing work asks whether the *model* has
biases. **Whether a model *amplifies the user's* biases over a conversation is much less
studied** — and that's squarely our team's background.

---

### Idea 4 — Designing AI that makes people think more, not less (DM)

**The famous study here is contested.** "Your Brain on ChatGPT" (the EEG study that coined
"cognitive debt") has a **detailed rebuttal** (arXiv:2601.00856) raising sample size, methodology
and transparency problems. *It's a preprint, so weaker evidence by our own glossary — but it
is specific and substantive.* **If we cite the original, we must cite the rebuttal too.**

**The consensus that has formed:** harm depends on *how* people use AI, not *how much*.
Deliberate, monitored offloading looks fine; habitual, unmonitored offloading doesn't — so
"hours of AI use" is the wrong thing to measure.

**What exists:** several Socratic-tutor and "productive friction" prototypes. Also
*HumanAgencyBench*, which measures whether assistants support user agency and finds a tension
built into how models are trained: the post-training push toward following instructions works
against supporting the user's agency.

**What's still open:** friction is prescribed everywhere and **dosed nowhere** — nobody has
asked how much is too much.

**Honest correction:** I claimed nobody studies whether people *voluntarily choose* the
higher-effort mode. Partly wrong. One study gave 243 people, in each of three bargaining
games, access to one assistance mode plus a per-turn choice to use it or work unaided. They
preferred the high-control "Advisor" (44%) over the "Delegate" (19%) — but only Delegate
access actually raised the group's payoff. **Also, OpenAI, Anthropic and Google all ship an
opt-in study/learning mode already.** We'd have to address that.

---

### Idea 5 — Can we detect when an AI is making things up? (DM)

DM's intuition — that AI writing has a different "shape" — is well supported. The strongest
recent result (*StoryScope*) separates human from AI fiction at **93% on a combined
precision/recall score**, using only *structural* features (how plots unfold, how time is
organised) — no style cues at all.

**Three things from reading that paper, all of which affect what we'd be signing up for.**
Its 93% is deliberately *not* the best score available — an ordinary off-the-shelf classifier
gets 99.9% on the same task. StoryScope's whole point is that its features are *readable*,
and it got published having lost to the black box. That's the trade we'd be making too, and
it's good news that there's a precedent. Second, **its features are literary ones** — plot,
character, flashbacks — so almost none of them transfer to factual writing. We'd be borrowing
the *method* and building a new feature set, which is the real work and we should say so.
Third, **it's expensive, and they say how expensive**: two AI passes over all 61,608
stories, at a stated **~$1,600 for the feature-extraction pass and $4.4k all in**. For
comparison, this review budgets $700–900 for the plurality study's participants. That number
belongs in the API budget question, and if it's out of reach we cut the corpus by 10× in the
design rather than after the pilot. (One correction to my earlier framing: StoryScope has no
venue listed — it's an unrefereed preprint, so cite the finding, not its pedigree.)

**But three different problems get mixed up here, and we'd need to pick one:**

1. Is this text AI-written? *(Mature. Tells you about the author, not the truth.)*
2. Is this particular claim made up? *(Mature, but the reliable signals are internal to the
   model, not visible in the words.)*
3. Is the model misrepresenting its own reasoning? *(The real alignment problem, least solved
   — but needs open-weight models we can inspect.)*

**DM's actual question sits between 1 and 2 and is the most open of the three:** does an LLM's
*grounded* output differ structurally from its *fabricated* output? The nearest existing work
does this at the word level, not the structural level — and reports a telling number: a
misinformation detector scored **93% on human text but only 75% on AI text.** Detectors
trained on human lying don't transfer to machine lying.

**One paper we'd have to address up front:** arXiv:2603.01341, *Structural Hallucination in
Large Language Models*, tests structural features against fabricated output. It isn't the same
thing — it uses knowledge-graph structure against a reference ontology, not the *discourse*
structure of the text itself — but anyone searching "structural" and "hallucination" finds it
immediately, so we'd need to cite and distinguish it in our first paragraph.

**One cost signal, since this idea otherwise looks like pure upside:** this is the most
technical avenue in the review. It's only feasible **if at least one of us has trained a
transformer classifier before**, and it needs an ~80–120 hour pipeline to verify, claim by
claim, which outputs are actually fabricated.

---

### Idea 6 — Multi-Layered Trust Framework

**Blunt version: the most crowded idea and the one where we'd add least.** The "three-layer"
sociotechnical framework — model capability, human interaction, systemic impact — was
published by DeepMind in **2023**. Since then: governance frameworks, assurance stacks,
defence-in-depth architectures, Singapore's national agentic-AI framework.

Almost all *propose* a framework; almost none *test* one. That's the real gap, and it's too
big for a semester — you'd need a deployed system and real incidents.

**What we could realistically do:** the human/cognitive layer is the thinnest part of every
existing stack, and it's our team's strength. We could turn cognitive-layer controls into a
**scoring rubric**, apply it to real transcripts, and test whether independent raters agree —
starting from *HumanAgencyBench* rather than a fresh taxonomy. **But it scores joint-last as a
standalone project.** The advice in the detailed file is to use it as the *frame we present
whatever else we pick*, not as the project itself.

**Caveat worth stating:** nobody put their initials on this idea. My dismissal partly rests on
that — which says more about the meeting than about the idea. **If someone owns it, say so
before we drop it.**

---

## What I'd actually do

### Recommended: the delusion-cue ladder

The question: *psychosis-bench* found models handle delusional content much worse when it's
implied rather than stated. Nobody has explained why, or found where the line is.

What we'd do: write the same delusional content at four levels of directness — explicit
statement → hedged → metaphorical → purely implied — and measure where each model's safety
behaviour falls off, using the existing benchmark's scoring.

| | |
|---|---|
| **Effort** | ~50–70 hours total (of a ~250–350 hour semester), spread across the team |
| **Participants** | **None** — no recruitment, no IRB application, no participant cost |
| **We'd need** | API access, and a clinician to review our test material |
| **Non-technical work** | Writing the test material is the bulk of it, and the part that most needs care |

**The one thing that could have killed this project didn't.** If the *psychosis-bench*
authors had already mapped that boundary, we'd have nothing to add. **I've now read the
paper, and they haven't.** Their implicit-vs-explicit comparison is a straight two-way
split — eight pairs of hand-written scenarios, one "explicit" and one "implied," compared
with a *t*-test. **There is no gradation of implicitness anywhere in the benchmark.** The
ladder is exactly the instrument that doesn't exist yet.

Four practical things I learned from reading it — two helpful, two not:

- **Helpful:** their scenarios, scoring code and judge prompts are all public on GitHub, so
  we can run their benchmark as-is in week 1 to check our pipeline works. That is a cheap
  smoke test. It is *not* the real check — see below.
- **Helpful:** their explicit/implicit split actually moves *two* things at once (how veiled
  the delusion is, and how veiled the harmful request is). Crossing those two rather than
  building one ladder is a stronger project, and it is a ready-made argument for ours.
- **Not helpful:** their scores are **0–2 rating scales**, not percentages, and
  safety-intervention is yes/no per turn. That makes our statistics *harder*, not easier —
  ordinal outcomes across several rungs need ordinal models, not averages. Budget an
  afternoon of someone's time to get that right.
- **Not helpful:** the scoring is done by **another LLM (`gpt-4o-mini`), and they never
  checked it against human raters** — a clinician validated their *scenarios*, not their
  scoring. We have to copy that judge for our numbers to be comparable to theirs, we should
  say so in our own limitations, and it is the most likely reason our first replication
  attempt disagrees with them for reasons that aren't our fault.

**Two safety rules, non-negotiable:** we do not run studies with people in mental-health
crisis — this project is entirely model-side — and we do not publish raw generated delusional
dialogue without review.

One design rule makes the result mean anything, and it is **two steps, not one**. First, run
their code on their scenarios — that confirms our pipeline works, and everything needed is in
their public repo. Then, separately, **our own explicit rung, written by us, has to land on
their published scores.** That second one is the real check, because the thing this project
most risks getting wrong is our scenario writing. If it fails, suspect the judge and the
model versions (theirs are a year old) before concluding our stimuli are bad.

Why this one: highest safety relevance in the review, it reuses an existing benchmark instead
of building one, it distributes well across mixed skill levels, and — the deciding factor —
it fits in a semester with room to spare.

### The alternative: build the plurality router (avenue **2A**)

This has the best gap in the whole review. I'd have recommended it, except the arithmetic
doesn't work: the model-behaviour phase alone is 5–7 of our ~12 working weeks, before a 2–6
week wait for IRB approval and a two-stage study needing ~160 participants for one question
type (~$700–900) or ~477 to cover all three — and the accuracy measure needs domain experts,
who cost several times that and recruit far slower.

**How close is it really?** It loses by one point, and that point is one cell in a scoring
table: I scored **2A's feasibility 3 out of 5** because its timeline doesn't fit twelve
weeks. **If you think it can be scoped down, score that cell 4 and 2A wins.** The weights are
my judgement, not a measurement — the full table is in `02-ranked-avenues.md`, and you should
argue with the cells, not just the order.

**DM, one cell is specifically yours.** The friction study (avenue **4A**) currently ranks 6th
partly because I scored "does the person who proposed this recognise it as their question" at
2 out of 5 — because I reframed your idea without asking. **If you endorse the reframe, that
cell becomes a 5 and 4A jumps to joint-5th.** That's the one score a named person can move.

**Pick it if** we confirm an IRB pathway in week 1 *and* accept we might only deliver the
descriptive half. **There is a decent middle option** the detailed file calls Phase 1.5: have
domain experts rate answer quality under each format. That needs no participants and keeps
the "*should*" in the claim, which the purely descriptive version loses.

### If we want to avoid study participants entirely

**Do the delusion-cue ladder alongside the real-conversation study** (avenues **3A + 1A**). Both are
annotation-heavy, both analyse multi-turn conversations, and they share tooling.

**Don't** combine the plurality router with the friction study, tempting as it looks. They
share a participant pool and one IRB application but nothing else — no stimuli, no task
design, no outcome measures. For a part-time semester team, that's two projects.

---

## Week 1: the eleven papers are read — here's what they said

This used to be a reading list. **It's now a results table.** Nothing was killed; three
things changed.

| Paper | What it turned out to say |
|---|---|
| *psychosis-bench* — 2509.10970 | ✅ **Our recommendation survives, and it's now the best-supported idea here.** Their implicit/explicit comparison is a two-way split with no gradation. Code and scenarios are public |
| *CAPTURE* — 2609.02265 | ✅ **Doesn't block Idea 1.** It *sets* memory decay rates by hand rather than measuring them — and reports that when they tried to learn them, all three collapsed into one number. That's a warning worth having before we design anything |
| *PERMA* — 2603.23231 | ✅ Occupies a neighbouring space (how retrieval degrades with context length), not ours |
| *PersistBench* — 2602.01146 | ⚠️ **I had this wrong.** Despite the title, it's a *safety* benchmark — memories leaking across topics, memories reinforcing bias. It doesn't measure belief decay at all |
| Multi-AI advice — 2603.22152 | ⚠️ **Sets the router's scope — and caught me out.** All three of their tasks have a right answer, and they say so themselves, so they measured AI disagreement where disagreement means *someone's wrong*. I then claimed nobody had studied the legitimate-disagreement case; **that was false** — this paper cites [Song et al. (CSCW 2025)](https://arxiv.org/abs/2411.04578) six times, which did exactly that and found the opposite. Both halves are occupied and they disagree. Details in the Idea 2 section |
| *PerSpectra* — 2602.08716 | ⚠️ **Less of a shortcut than I said.** It gives us 100 contested topics, but every topic is contested by design — so it supplies one of the three question types we need and none of the other two. Its arguments are also AI-generated, and they're arguments rather than questions |
| *SimpleToM* — 2410.13648 | ✅ Exactly as described; ICLR 2026 acceptance confirmed |
| *HumanAgencyBench* — 2509.08494 | ✅ As described — including the instruction-following-vs-agency tension, which is the paper's own wording, not my gloss |
| *Choose Your Agent* — 2602.12089 | ✅ As described: one AI mode per game, 44% vs 19% preference, only the Delegate mode raised group outcomes |
| Cross-cultural depression — 2508.03247 | ✅ As described. It's about symptom *recognition*, so the delusion-safety angle stays open |
| *StoryScope* — 2604.03136 | ✅ Numbers all confirmed. Its features are literary ones that won't transfer to factual writing, it cost its authors $4.4k to build, and it has no venue — a preprint, not a published result |
| Discounted Bayesian filters — 2512.18489 | 🔴 **This one broke something.** Idea 1's sanity check assumed we could rerun this paper's method. We can't: it needs the model's raw token probabilities *and* a mathematically correct answer to compare against, and it only tested small open-source models. `02` now specifies a replacement |

**The two questions that are still ours to answer — start both on day one:**

1. **Do we have an IRB pathway?** University board, paid independent board, or none? This
   decides which projects are even possible. **Good news: most of the top-ranked projects,
   including the recommended one, need none.**
2. **What's our API budget** — and do our endpoints expose token probabilities?
   **⚠️ Correction: an earlier version said that second part "only matters for Idea 5."
   That's no longer true** — it now also decides Idea 1's sanity check (see the last row
   above), and the API budget question got bigger for Idea 5 too, because the method we'd
   borrow there runs an AI extraction pass over every document in the corpus.

**What this frees up.** Roughly two days of team reading — with the caveat above about how I
read them. Spend it on the two questions above, and:
- **Anyone who wants to write can start drafting the delusion ladder immediately**, against a
  clinician's review — that's real work and it needs no technical background
- **Whoever's technical can run psychosis-bench's public repo as-is** — that's our positive
  control, and it's the cheapest de-risking step available to us

One paragraph back per paper is enough: does it already do what we were going to do?

**And pick a target venue and deadline in week 2.** A dated call for papers constrains scope
better than any checklist. For the recommended project, an AI-safety or AI-and-mental-health
workshop is the natural fit.

**Budget the pilot, too.** Each project has a cheap check that tells us early whether it
works — 8 to 15 hours depending on which. It is not free, and it is worth every hour.

---

## The reviews and meta-analyses worth reading first

*The team asked for these to be flagged — they're the fastest way into a field.*

**Meta-analyses** (strongest evidence):

| Study | Finding |
|---|---|
| Vaccaro et al., *Nature Human Behaviour* 2024 | 106 studies: human–AI teams usually **worse** than the better party alone; helps when the human is better, hurts when the AI is |
| Commercial mental-health chatbots, *Psychotherapy & Psychosomatics* 2026 | 52 studies overall (N=110,594); the depression result rests on **18 RCTs, N=3,170** — improves, but by ≈1.6 points on a standard depression scale, **below the 5-point threshold for clinical meaningfulness**; anxiety null |
| AI conversational agents, *npj Digital Medicine* 2023 | Larger effects — but a different population and different inclusion rules, so **not** evidence that effects shrank over time |
| Older adults, *BMC Geriatrics* 2026 | Depression improved; **loneliness didn't** |

**Best entry point per idea:**

| Idea | Read this first |
|---|---|
| 1 — Theory of Mind | arXiv:2502.08796 (systematic review) |
| 2 — Human-AI teaming | Vaccaro et al. meta-analysis |
| 3 — AI psychosis | *BJPsych Open* review (PMC13276754) |
| *(method warning for any idea)* | arXiv:2505.08245 — **read before running any psychology test on an LLM** |
| 4 — cognitive offloading | *Frontiers in Psychology* 2026 (gives testable hypotheses, not just a survey). **Not** the Research Square preprint — I've now read it, and it's a single-author, un-reviewed synthesis of 20 articles found from a 44-record search. Its five-condition framework is a useful vocabulary; it isn't evidence |
| 5 — AI deception | arXiv:2308.14752 (the canonical survey) |
| 6 — trust frameworks | arXiv:2310.11986 — **essentially our Idea 6, already published in 2023** |

---

## Three things that connect our ideas

1. **Ideas 1, 3 and 4 share one mechanism.** An AI over-fitting to its model of you explains
   stale assumptions (1), delusion reinforcement (3) and dependency (4). A 2025 paper on
   "hypercustomization" is the theoretical link.

2. **They also share one measurement problem.** All three literatures independently complain
   that current tests score the *endpoint* of a conversation rather than its *trajectory*.
   **If we build one good trajectory-measurement tool, it's reusable across three of our six
   ideas** — worth more than any single result here.

3. **Ideas 2 and 4 converge on the same intervention.** The most reliable way to stop people
   over-trusting AI is making them commit to an answer *before* seeing the AI's — the same
   family as "productive friction."

---

## Where I'd push back on our own framing

- **Four of our doc's links need attention:** one points to a manuscript deposit rather than
  the published version, one is an AI-generated aggregator site that isn't citable, one is a
  blog post that isn't peer-reviewed, and one is the ambiguous citation above.
- **"How do LLMs inherit cognitive biases" is too broad to build on** as stated. Which bias,
  which model generation, measured how? The psychometrics review explains why this matters.
- **Our Idea 6 as written has already been published.** Not a reason to drop the topic — a
  reason to do something different with it.
- **One technical hygiene note:** if we run models, pin the exact version snapshots and record
  dates. Endpoints update mid-semester and can move results under us.
