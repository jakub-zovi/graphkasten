---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-06-14T10:00
modified: 2026-08-01T16:24
published: 2026-06-14
sources:
  - "[Self-Harness (newsletter summary)](https://mail.google.com/mail/u/1/#inbox/FMfcgzQgMMKgQfZtgwGhjmlrXnRTkVbX)"
  - https://arxiv.org/abs/2606.09498?utm_source=substack&utm_medium=email
  - https://x.com/omarsar0/status/2064429834999304247?utm_source=substack&utm_medium=email
topics:
  - Self-Improving Harness
  - Weakness Mining
  - Agent Scaffold
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
---
## **Self-Harness**

![Self-Harness](https://ci3.googleusercontent.com/meips/ADKq_NYCpESBJ6-l_ghI-EVUK0D2mwK8-N2QIZ2-ZVWoUyzKEU3W-vqRrFIgrICFu9af6RAsM6zDZHTTHf7NSOmNnK7uJdQZvW8T_qjAckKLwmfNgRiR307xmEwh4mbJ1Q1biqzlouEDxnqzmCAVksbf-fGEBbuGUoCYhhAHcF8bZ-7s9u69mXWV7J5y3MrZJ3qpQ3anzAHDfE85AnpdzjipJCBIkzE0mRXIGpk9hxZiFd_a_NfMoqSLfe37J7ikl-zQ3fAMh3-1_qvRNvxGu_L_oNR6SNUA2OvaJeiPtya3ZmdHoUPpHUorooGK7-AulMRrD3dRYg=s0-d-e1-ft#https://substackcdn.com/image/fetch/$s_!Illx!,w_1100,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F13f439c2-4126-4914-b1e9-2c1538acd1c7_793x566.png)

> Most agent scaffolds are built once by hand and then frozen, even as the underlying models keep changing. This paper introduces Self-Harness, a paradigm where an LLM agent improves its own operating harness, the prompts, tools, memory, and orchestration around the base model, without human engineers or a stronger external agent. Because every model fails in its own way, the system mines those model-specific weaknesses and turns them into concrete, executable harness edits rather than generic advice.
> 
> - **A three-stage self-improvement loop:** Self-Harness runs Weakness Mining, which clusters execution traces into model-specific failure patterns, then Harness Proposal, which generates diverse but minimal edits tied to those failures, then Proposal Validation, which accepts edits only after regression testing on held-in and held-out splits.
> - **Consistent gains across base models:** On Terminal-Bench-2.0, held-out pass rates rise for every model tested. MiniMax M2.5 improves from 40.5% to 61.9%, Qwen3.5-35B-A3B from 23.8% to 38.1%, and GLM-5 from 42.9% to 57.1%.
> - **Weaknesses become edits:** Rather than appending generic instructions, the loop converts each observed failure mode into a targeted change to memory, tools, or prompts, with reported relative improvements as high as 138%.
> - **Why it matters:** As models proliferate and evolve, hand-tuning a bespoke harness for each one does not scale. Self-Harness shows the scaffold itself can be made to adapt, closing the gap between a frozen harness and the model it wraps.
