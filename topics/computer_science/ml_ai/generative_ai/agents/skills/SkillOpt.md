---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-05-31T10:00
modified: 2026-08-01T11:14
published: 2026-05-31
sources:
  - "[The Top AI Papers of the Week (May 24 - May 31)](https://nlp.elvissaravia.com/p/top-ai-papers-of-the-week-5ce?utm_source=post-email-title&publication_id=103238&post_id=199893812&utm_campaign=email-post-title&isFreemail=true&r=53sn48&triedRedirect=true)"
  - "[Paper](https://substack.com/redirect/dbfe811f-8905-4b10-8235-4a956957a1f3?j=eyJ1IjoiNTNzbjQ4In0.HDTZC-v9EHMxDCrL4bWlsgejzB3gsbK1e1RSiihbxbI)"
topics:
  - Agent Skills
  - Skill Optimization
  - SKILL.md as Parameter
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
---
## **SkillOpt**
- [The Top AI Papers of the Week (May 24 - May 31)](https://nlp.elvissaravia.com/p/top-ai-papers-of-the-week-5ce?utm_source=post-email-title&publication_id=103238&post_id=199893812&utm_campaign=email-post-title&isFreemail=true&r=53sn48&triedRedirect=true)
> Microsoft Research treats a compact natural-language skill document as the trainable state of a frozen agent, then learns that document through rollouts, reflection, and bounded edits gated by held-out validation. The argument is direct: most engineers handwrite agent skill docs and hope they generalize, when the doc itself should be optimized like a parameter. SkillOpt reframes the SKILL.md file as an external parameter of a model whose weights never change.
> 
> - **The skill doc as a trainable parameter:** An optimizer model proposes validation-gated edits to the skill file, adding, deleting, or replacing instructions. A textual learning rate controls how aggressively each round rewrites the document, with batch and momentum reported in text space rather than gradient space.
> - **Validation gates instead of hope:** Every edit must pass a held-out check before it is kept. This turns skill authoring into a measurable optimization loop with a real objective, rather than prompt tweaking guided by intuition.
> - **52 out of 52 wins:** SkillOpt beats Trace2Skill, TextGrad, GEPA, EvoSkill, human-written skills, and one-shot skills across 6 benchmarks and 7 target models. It adds roughly +23.5 points on GPT-5.5 in direct chat, +24.8 in the Codex loop, and +19.1 in Claude Code from the no-skill baseline.
> - **Why it matters:** If the skill document is the thing you optimize, the bottleneck shifts from base-model capability to how well you can train the natural-language state around a frozen agent. That is a cheap, model-agnostic lever most teams are leaving on the table.


![SkillOpt](https://ci3.googleusercontent.com/meips/ADKq_NbGuLYHzBUEO07badhAk6mgF2fnwfvuglEvTNPKyGKFkzLjxTCWVNKnLuf8pCZMMQEN4K63mrk0ceEl0ECKJdEG2uzZ1k5F4S8sX463AIFAuFdEpefnUlFPjPeHgdZfHDLmwBH-L3IWEg6iCSNyntjWFBOM_LLxRmqhPVlMxjbXaBn4A00Yfn1kmAWFwdH_Hxzxq2QP-EnpkV5r8X80WcRideN2jTCYH77-AAekP7WckjGYVKkWw3-2qxueShVNmCGV5HHAvUto7X8KNNYAG6E8YAKi3m830eZGsGfwVA6UyIgJHO3FcoC2whQXEjvuDPNlxQ=s0-d-e1-ft#https://substackcdn.com/image/fetch/$s_!vt17!,w_1100,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F14e3d838-0e26-4ff1-87be-91836cf1f8ae_793x435.png)