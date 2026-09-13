---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-02-03T13:28
modified: 2026-09-12T17:25
published:
sources:
  - "[What is an agent harness?](https://parallel.ai/articles/what-is-an-agent-harness)"
topics:
  - Agent Design 
  - Agent Harness
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Agent Harness
- [What is an agent harness?](https://parallel.ai/articles/what-is-an-agent-harness)
> In simple terms, an agent harness is the software infrastructure that wraps around a large language model (LLM) or AI agent, handling everything except the model itself. One AI architect defines an agent harness as “the complete architectural system surrounding an LLM that manages the lifecycle of context: from intent capture through specification, compilation, execution, verification, and persistence”, essentially everything except the LLM itself. In practical terms, the harness is what connects an AI model to the outside world, enabling it to use tools, remember information between steps, and interact with complex environments.
- Important mental model behind harness focus
	- The Mismanaged Geniuses Hypothesis
## Topics
- [[Agentic Harness Benchmarks]]
- [[List of Harness]]
- [[Harnesses Optimization]]
- [[Harness Design]]
## Resources
- Overview of harnesses 
	- [[Harness, Scaffold, and the AI Agent Terms Worth Getting Right]] ([Link](https://huggingface.co/blog/agent-glossary))
		- 2026-05-25 — HuggingFace glossary grounding "model", "harness", "scaffold", "agent" terms as they've drifted across the field
- Domain specific harnesses
	- [[Open-source agents with frontier advisors matching frontier performance]] ([Link](https://fireworks.ai/blog/open-source-agents-frontier-advisors))
		- 2026-06-03
		- Fireworks + Harvey on Legal Agent Benchmark: GLM 5.1 worker self-triggers Opus 4.7 as a callable advisor, reaching 18/100 all-pass at $368 vs Opus end-to-end at 14/100 for $954
## Papers
- [[Code as Agent Harness]] ([Link](https://arxiv.org/abs/2605.18747))
	- 2026-05-24 — 100+ page survey framing code-as-harness as the path to general agency; proposes an executable/inspectable/stateful/governed test
