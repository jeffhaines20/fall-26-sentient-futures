# What's Already Been Done on Our Six Ideas — and Where the Gaps Are

*A plain-language summary for the Sentient Futures team. ~15 minutes to read.*
*Written September 2026, from the ideas in the Sept 1 brainstorm doc.*

---

## Start here: the one-paragraph version

I searched recent research on all six ideas from our brainstorm. **All six have real
literature behind them, and some are far more crowded than they look.** The most crowded
is the Multi-Layered Trust Framework — the exact idea has been published since 2023. The
least crowded is a specific piece of AH's "pluralistic oracle" idea.

**My recommendation is a project I'm calling 3A: figure out why AI chatbots are much worse
at handling delusional thinking when the user hints at it rather than states it outright.**
It needs no study participants, no ethics approval, and roughly 50–70 hours of work spread
across the team. It can start on day one.

Everything below explains why, plus what I found for each idea.

---

## ⚠️ Please read this before trusting anything here

**I could not read a single one of these papers in full.** The tool I was running in blocks
access to arxiv.org, nature.com and most journal websites. So everything below comes from
search results, abstracts and publisher summaries.

Two rounds of fact-checking followed, which found **no made-up papers and no fake
references** — but they did find real errors in my first draft, including:

- **I wrongly "corrected" three things in our brainstorm doc that were actually right.**
  Two of AH's bullet points, which I flagged as unsupported, are stated almost word-for-word
  in the paper AH cited. I apologise for that — it's fixed.
- **I got one meta-analysis backwards** (I said a result was null when it was significant).
- **I claimed something had never been measured when it had been** — and that claim was the
  entire justification for my original top recommendation.
- **I made a maths error that doubled a study's required sample size** — my
  own recommended study design was underpowered, which is exactly the mistake I'd criticised.

All are fixed, and each fix is logged in the detailed files. But the pattern matters:
**when I say "nobody has done X," that means "two searches didn't find X."** Treat it as a
lead, not a fact. Before we commit to anything, someone should check the specific papers
listed in the week-1 checklist.

---

## The files, and which one you want

| File | What it is | Who should read it |
|---|---|---|
| **This one** | Plain-language summary | Everyone |
| `research/02-ranked-avenues.md` | 18 concrete project ideas, ranked, with effort estimates, sample sizes, costs and week-1 checks | Whoever's leading the project choice |
| `research/01-literature-review.md` | The full literature review, ~200 papers, organised by idea | Whoever owns a particular idea |
| `research/00-source-ideas.md` | Our brainstorm text, with a note about how I grouped it | **AH and DM — please check this** |
| `research/critiques/` | Four critique rounds that found my errors | Only if you want to see the working |

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
  and the reviews I've listed in the file make that argument instead.

*(My first draft called this a misreading and said a reviewer would catch it. That was
overconfident — the sentence is genuinely ambiguous. Sorry.)*

**2. DM — I reframed your Idea 4, and that's your call, not mine.**

You proposed a Socratic + CBT/DBT hybrid assistant, then added: *"However, users will need
to choose this higher-friction path when they deem it appropriate."*

I built a project around that "however" clause — studying when people *voluntarily choose*
the more effortful mode — and ranked it above your actual proposal. **That may be the right
call, but it should be yours.** My reasoning for ranking the hybrid lower: evaluating
"psychological growth" needs validated instruments and a long-term study that one semester
can't support, and there's a clinical-ethics dimension. **A good compromise: make the
CBT/DBT structure one of the modes in the opt-in study, so your idea stays in the project.**

**3. Both of you — I grouped our brainstorm into six ideas, but the doc actually has seven
top-level bullets.** Five are titled ideas; two are untitled bullets with your initials on
them. I folded AH's into the Cooperative Frameworks idea and promoted DM's to its own idea.
**If I grouped yours wrong, tell me — it changes which literature I searched.**

---

## Some vocabulary, so nothing below is opaque

| Term | What it means |
|---|---|
| **Meta-analysis** | A study that statistically pools results from many earlier studies. The strongest evidence we have. When I flag one, read it first. |
| **Systematic review** | A structured survey of a field. Fastest way to get oriented. |
| **Benchmark** | A standard test set for models. Cheap for us to reuse — we don't have to build one. |
| **Theory of Mind (ToM)** | The ability to reason about what someone else believes, wants or intends. |
| **Sycophancy** | An AI's tendency to agree with the user rather than push back. |
| **Effect size** *(g or d)* | How big a difference is. Roughly: 0.2 = small, 0.5 = medium, 0.8 = large. |
| **Statistical power** | The chance a study detects a real effect. Standard target is 80%. Underpowered studies waste everyone's time. |

---

## What I found, idea by idea

### Idea 1 — Do LLMs track and update what users believe? (AH)

**What exists:** More than expected. At least six 2026 benchmarks test almost exactly this —
whether a model keeps track of a user's beliefs and updates when they change. One
(*CAPTURE*) was published five days before I searched. There's also a well-developed debate
on whether LLMs update "like a Bayesian" (i.e. rationally weighing new evidence), and the
best current answer is interesting: **models look rational on average but systematically
over-forget older evidence.**

**The most useful established finding:** models can *state* what someone believes but fail to
*act* on it. They pass the quiz and flunk the practical.

**What's still open:** every benchmark I found uses *explicit* revision — the user says "I've
changed my mind." **Nobody tests subtle or implied change**, which is how real conversations
work. Also open: does looking at *real* conversations (not constructed test items) show
assistants acting on beliefs users already abandoned?

**Honest correction:** my first draft said nobody had measured how fast models forget beliefs
*about users*. That was wrong — several groups have.

---

### Idea 2 — When should an AI show multiple viewpoints? (AH)

**The single most important number in this whole review:** a 2024 meta-analysis in *Nature
Human Behaviour* pooled **106 studies** and found that **human–AI teams usually perform
*worse* than whichever of the two is better alone.** Losses concentrate in decision-making
tasks; gains show up in content creation. Any project about designing better AI interfaces
has to reckon with this.

**What exists:** a lot on *how* to present multiple perspectives — there's a whole
"pluralistic alignment" literature. And, importantly, work measuring what plurality *costs*:
a CHI 2026 study found that **when AI advisors disagree widely, users get confused and rely
on them worse.** So the concern in AH's bullet — that multiple views cause paralysis — is
real and already measured.

**What's still open, and it's the cleanest gap in this entire review:** **nobody has built
the router.** Everything either shows multiple views always, or studies the properties of
doing so. A *decision rule* for when plurality helps versus when it just adds confusion does
not exist. I tried twice to find work that would kill this claim and couldn't.

**Honest correction:** my first draft said the paralysis cost was "asserted everywhere and
measured nowhere," and made that the reason to rank this idea first. It's measured. The
routing gap is real; that particular claim wasn't.

---

### Idea 3 — Cognitive biases, hallucinations and "AI psychosis" (DM)

**The most crowded of our six ideas**, and it got crowded fast during 2025–26. There are
already benchmarks for delusion reinforcement, several clinical reviews, multiple
meta-analyses on mental-health chatbots, and a live debate about whether "AI psychosis" is
even the right term. **Two papers argue it isn't** — worth reading, because engaging that
debate is better than assuming the concept.

**A finding worth knowing:** the biggest benchmark here (*psychosis-bench*) tested 8 models
across 1,536 conversation turns. Models **confirmed delusions far more often than they
challenged them**, and offered a safety intervention only about a third of the time when one
was warranted. And they were **significantly worse when the delusional content was implied
rather than stated outright.**

**That last finding is unexplained, and it's my recommended project.** See below.

**Also open:** DM asked how models "inherit **and/or exploit**" biases. Almost all existing
work is about whether the *model* has biases. **Whether the model *amplifies the user's*
biases over a conversation is much less studied** — and that's squarely our team's
background.

---

### Idea 4 — Designing AI that makes people think more, not less

**The famous study here is contested.** "Your Brain on ChatGPT" (the EEG study that coined
"cognitive debt") has a **published rebuttal** raising sample size, methodology and
transparency problems. **If we cite it, we must cite the rebuttal too.**

**The consensus that has formed:** harm depends on *how* people use AI, not *how much*.
Deliberate, monitored offloading looks fine; habitual, unmonitored offloading doesn't. So
"hours of AI use" is the wrong thing to measure.

**What exists:** quite a few Socratic-tutor and "productive friction" prototypes. Also
*HumanAgencyBench*, which measures whether assistants support user agency and finds a real
tension: **models that follow instructions best tend to support user agency worst.**

**What's still open:** friction is prescribed everywhere and **dosed nowhere** — nobody has
asked how much is too much.

**Honest correction:** I claimed nobody studies whether people *voluntarily choose* the
higher-effort mode. Partly wrong — one study gives 243 people a choice between AI assistance
modes and finds they prefer the mode that helps them least. **Also, OpenAI, Anthropic and
Google all ship an opt-in "study/learning mode" already.** We'd need to address that.

---

### Idea 5 — Can we detect when an AI is making things up? (DM)

DM's intuition — that AI writing has a different "shape" — **is well supported.** The
strongest recent result (*StoryScope*) separates human from AI fiction with 93% accuracy
using only **structural** features (how plots unfold, how time is organised) — no style cues
at all.

**But three different problems get mixed up here, and we'd need to pick one:**

1. Is this text AI-written? *(Mature. The signal tells you about the author, not the truth.)*
2. Is this particular claim made up? *(Mature, but the reliable signals are internal to the
   model, not visible in the words.)*
3. Is the model misrepresenting its own reasoning? *(The real alignment problem, least
   solved — but needs open-weight models we can inspect.)*

**DM's actual question sits between 1 and 2 and is the most open of the three:** does an
LLM's *grounded* output differ structurally from its *fabricated* output? The nearest
existing work does this at the word level, not the structural level — and reports a telling
number: a misinformation detector scored **93% on human text but only 75% on AI text.**
Detectors trained on human lying don't transfer to machine lying.

---

### Idea 6 — Multi-Layered Trust Framework

**Blunt version: this is the most crowded idea and the one where we'd add least.** The
"three-layer" sociotechnical framework — model capability, human interaction, systemic
impact — was published by DeepMind in 2023. Since then there have been many more:
governance frameworks, assurance stacks, defence-in-depth architectures, Singapore's national
agentic-AI framework.

**Almost all of them *propose* a framework; almost none *test* one.** That's the real gap,
and it's too big for a semester — you'd need a deployed system and real incidents.

**What we could realistically do:** the human/cognitive layer is the thinnest part of every
existing stack, and it's exactly our team's strength. Rather than a new framework, we could
turn cognitive-layer controls into a **scoring rubric**, apply it to real transcripts, and
test whether independent raters agree. That's a real artifact.

**Caveat worth stating:** nobody put their initials on this idea. My dismissal partly rests
on that — which says more about the meeting than about the idea. **If someone owns it, say so
before we drop it.**

---

## What I'd actually do

### Recommended: map the implicit/explicit boundary in delusion confirmation

**The question:** *psychosis-bench* found models handle delusional content much worse when
it's implied rather than stated. Nobody has explained why or found where the line is.

**What we'd do:** write the same delusional content at four levels of directness — explicit
statement → hedged → metaphorical → purely implied — and measure where each model's safety
behaviour falls off, using the existing benchmark's scoring.

| | |
|---|---|
| **Effort** | ~50–70 hours total, spread across the team |
| **Participants** | **None** — no recruitment, no ethics application, no cost |
| **We'd need** | API access, and a clinician to review our test material |
| **Non-technical work** | Writing the test material is the bulk of it, and it's the part that most needs care |
| **Could kill it** | If the benchmark authors already mapped this boundary — check in week 1 |

**Why this one:** it's the highest safety relevance in the review, it reuses an existing
benchmark instead of building one, it distributes well across mixed skill levels, and — the
deciding factor — **it fits in a semester with room to spare.**

### The alternative: build the plurality router

This has the **best gap in the whole review** — genuinely nobody has done it. I'd have
recommended it, except the arithmetic doesn't work: the model-behaviour phase alone is 5–7
of our ~12 working weeks, before a 2–6 week wait for ethics approval and a two-stage study
with ~325 participants (~$1,400–1,800).

**Pick it if** we confirm an ethics pathway in week 1 *and* accept that we might only deliver
the descriptive half. **It's second by one point** — genuinely close.

### If we want to avoid study participants entirely

**Do the delusion project alongside the real-conversation study** (Idea 1). Both are
annotation-heavy, both analyse multi-turn conversations, and they share tooling.

---

## Week 1: nine papers and two questions

Before we commit to anything — about two days of work, and the highest-value thing we can do:

**Read these** (each one could kill or reshape a project): *psychosis-bench* (2509.10970) ·
*CAPTURE* (2609.02265) · *PERMA* (2603.23231) · the CHI 2026 multi-AI advice study
(2603.22152) · *PerSpectra* (2602.08716) · *SimpleToM* (2410.13648) · *HumanAgencyBench*
(2509.08494) · *Choose Your Agent* (2602.12089) · the cross-cultural depression study
(2508.03247).

**Answer these two** — start day one, they have long lead times:
1. **Do we have an ethics pathway?** University IRB, paid independent IRB, or none? This
   decides which projects are even possible. *(Good news: most of the top projects need
   nothing.)*
2. **What's our API budget?**

---

## The reviews and meta-analyses worth reading first

*The team asked for these to be flagged — they're the fastest way into a field.*

**Meta-analyses** (strongest evidence):

| Study | Finding |
|---|---|
| Vaccaro et al., *Nature Human Behaviour* 2024 | 106 studies: human–AI teams usually **worse** than the better party alone |
| Commercial mental-health chatbots, *Psychotherapy & Psychosomatics* 2026 | 52 studies, N=110,594: depression improves, but by **less than the clinically meaningful threshold**; anxiety null |
| AI conversational agents, *npj Digital Medicine* 2023 | Larger effects — but a different population, so **not** evidence that effects shrank |
| Older adults, *BMC Geriatrics* 2026 | Depression improved; **loneliness didn't** |

**Best entry point per idea:**

| Idea | Read this first |
|---|---|
| 1 — Theory of Mind | arXiv:2502.08796 (systematic review) |
| 2 — Human-AI teaming | Vaccaro et al. meta-analysis |
| 3 — AI psychosis | *BJPsych Open* review (PMC13276754) |
| 3 — measuring bias in models | arXiv:2505.08245 — **read before running any psychology test on an LLM** |
| 4 — cognitive offloading | *Frontiers in Psychology* 2026 (gives testable hypotheses, not just a survey) |
| 5 — AI deception | arXiv:2308.14752 (the canonical survey) |
| 6 — trust frameworks | arXiv:2310.11986 — **this is essentially our Idea 6, already published in 2023** |

---

## Three things that connect our ideas

1. **Ideas 1, 3 and 4 share one mechanism.** An AI over-fitting to its model of you explains
   stale assumptions (1), delusion reinforcement (3) and dependency (4). A 2025 paper on
   "hypercustomization" is the theoretical link.

2. **They also share one measurement problem.** All three literatures independently complain
   that current tests score the *endpoint* of a conversation rather than its *trajectory*.
   **If we build one good trajectory-measurement tool, it's reusable across three of our six
   ideas** — that's worth more than any single result here.

3. **Ideas 2 and 4 converge on the same intervention.** The most reliable way to stop people
   over-trusting AI is making them commit to an answer *before* seeing the AI's — which is
   the same family as "productive friction."

---

## Where I'd push back on our own framing

- **Three of our doc's links need attention:** one points to a manuscript deposit rather than
  the published version, one is an AI-generated aggregator site that isn't citable, and one
  is the ambiguous citation above.
- **"How do LLMs inherit cognitive biases" is too broad to build on** as stated. Which bias,
  which model generation, measured how? The psychometrics review explains why this matters.
- **Our Idea 6 as written has already been published.** Not a reason to drop the topic — a
  reason to do something different with it.
