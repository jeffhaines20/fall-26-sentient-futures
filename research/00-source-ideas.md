# Source: Project Ideas Brainstorm (extracted)

Extracted verbatim from `SF_ Initial Meeting Sept 1st, 2026 (1).docx`, section
"Project Ideas Brainstorm". Kept here so the literature review and the ranked
avenues can be checked against exactly what the team wrote.

Initials appearing in the doc: **AH**, **DM**.

---

## Idea 1 — Aligning Artificial Minds to Human Wellbeing
> Project focused on translating cognitive science and behavioral insights into algorithmic guardrails, ensuring that advanced systems are explicitly optimized to protect and deliver true benefit to sentient life.

**AH:** How well do LLMs adapt to and update their assumptions about changing user beliefs/desires/goals?
- Previous work has argued that LLMs are not capable of true Theory of Mind (ToM) to appropriately ascribe mental states to other actors despite their capacity to match human performance on higher-order ToM benchmarks (https://arxiv.org/abs/2405.18870) — if so, how do they keep track of user beliefs/desires/goals, and how well are they able to update when these change across multi-turn / more dynamic conversations?
- This may affect the robustness of dynamic systems and how they respond to change/inconsistency; may become even more complex in multi-agent / multi-user environments
- https://arxiv.org/abs/2607.28347: LLM biases of overrepresentation of neutral positions, more frequent but smaller belief shifts than humans, and a failure to rank comments by convincingness
- https://www.lesswrong.com/posts/msFvLtPfDnCEdvrBr/do-llms-change-their-minds-about-their-users-and-know-it: LLMs can adapt to explicit user changes (ex. shifting age groups) but it doesn't qualify how AI might adapt to more subtle user belief changes
- Even when users explicitly mention belief changes, do LLMs retain artifacts from previously held user beliefs?
- Do LLMs perform a form of Bayesian updating?
  - https://arxiv.org/html/2605.06915v1 / https://arxiv.org/abs/2605.06915
  - https://arxiv.org/html/2507.11768v1
  - https://research.google/blog/teaching-llms-to-reason-like-bayesians/ — would this approach improve LLMs' capability to adapt to users changing their beliefs/desires/goals across multi-turn conversations?

## Idea 2 — Cooperative Human-AI Frameworks
> Research how AI interfaces can be designed to support human autonomy rather than creating dependency, ensuring tech acts as a cognitive extension rather than a replacement.

**AH:** Testing varying methods of a sort of "pluralistic oracle": framework for how/when LLMs should vs. should not present multiple viewpoints
- How do LLMs decide in which cases to show users multiple perspectives vs. a single definitive answer? (single answer can induce sycophancy, but multiple can cause unnecessary confusion/paralysis) How do they present this information, and what are the effects of different approaches on human users and AI-assisted performance? How do LLMs respond to human feedback in this case?

**AH:** Can build on research highlighting differences in AI-assisted human performance based on how AI presents information & how hybridization frameworks are designed (https://arxiv.org/abs/2510.26518, https://arxiv.org/abs/2605.04070)
- when AI confidence is low, its reasoning and judgments are worse and may ill-advise humans
- static AI assistance, delivered in the same manner, degrades over time and may even eventually become harmful
- Humans tend to overrely on AI when presented with its reasoning & explanation vs. only being shown search results and evidence, which fosters more legitimate trust

## Idea 3 — (DM) Inherited/exploited cognitive biases; hallucination & "AI psychosis"
> **DM:** How do LLMs inherit and/or exploit cognitive biases; countering characteristics that lead to hallucinations/psychosis during interactions

- Hallucinating with AI: Distributed Delusions and "AI Psychosis" (https://link.springer.com/article/10.1007/s13347-026-01034-3)
- Technological folie à deux: feedback loops between AI chatbots and mental health (https://pmc.ncbi.nlm.nih.gov/articles/PMC7618964/)
- Characterizing the spiral: potential mechanisms in AI-associated delusions (https://www.nature.com/articles/s44277-026-00065-0)
- The governance & behavioral challenges of generative artificial intelligence's hypercustomization capabilities (https://journals.sagepub.com/doi/10.1177/23794607251347020)
- Cultural biases in LLM recommendations (https://www.emergentmind.com/topics/cultural-biases-in-llm-recommendations) — cultural misalignment leads LLMs to reason in a manner that is inappropriate for the user's situations

## Idea 4 — Countering Cognitive Atrophy through Epistemic Design
> Move away from pure task-deference and productivity shortcuts. Mentees will design a blueprint or interactive prototype for an AI assistant explicitly optimized to promote human learning, critical thinking, and psychological growth.

**DM:** can possibly be based on combinations of socratic reasoning framework and talk therapy (e.g., CBT/DBT) frameworks. However, users will need to choose this higher-friction path when they deem it appropriate for the situation.

## Idea 5 — Combatting Deceptive Alignment and Misinformation
> Research or design programmatic guardrails to ensure stable human-AI cooperation. Mentees will analyze how models generate or spread misinformation and develop methods to detect and prevent a model from altering its stated internal logic to manipulate users.

**DM:** are there specific language patterns that give away whether deception or misinformation is occurring? AI writing has a different "shape" from human writing. Are there similarly differences between information that is "researched" vs made up by LLMs?
- Trust at risk: Detecting misinformation in LLM-generated product reviews... (https://www.sciencedirect.com/science/article/pii/S2772503025000994)
- StoryScope: Investigating idiosyncrasies in AI fiction (https://arxiv.org/pdf/2604.03136)
- A linguistic comparison between human- and AI-generated content (https://pmc.ncbi.nlm.nih.gov/articles/PMC12969083/)

## Idea 6 — Multi-Layered Trust Framework
> Research or design a deployment framework that shifts the focus from an individual model's internal logic to its systemic integration.

*(No initials, no further detail supplied in the doc.)*
