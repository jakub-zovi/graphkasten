---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-02-03T17:08
modified: 2025-11-08T18:12
published:
sources:
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Model Routing
In Gen AI circles model routing is simple called query routing. The goal of model routing is to decide which model to use based on the difficulty of the user query.

[LLM Routing — Intuitively and Exhaustively Explained:](https://medium.com/towards-data-science/llm-routing-intuitively-and-exhaustively-explained-5b0789fe27aa)
> LLM routing is an advanced inferencing technique which can automatically choose the right language model, out of a selection of language models, for a given prompt; improving the performance, speed, and cost in LLM-powered systems.
## Papers
- [Hybrid LLM: Cost-Efficient and Quality-Aware Query Routing](https://arxiv.org/pdf/2404.14618)
	- **44** citations
- [AutoMix: Automatically Mixing Language Models](https://arxiv.org/pdf/2310.12963)
	- **16** citations
- [FrugalGPT: How to Use Large Language Models While Reducing Cost and Improving Performance](https://arxiv.org/pdf/2305.05176)
	- **175** citations
## Blogs
- [IBM - An air traffic controller for LLMs](https://research.ibm.com/blog/LLM-routers)
- [LLM Routing — Intuitively and Exhaustively Explained](https://medium.com/towards-data-science/llm-routing-intuitively-and-exhaustively-explained-5b0789fe27aa)

## Model Orchestration & Coordinators
- Learned coordinators that go beyond single-model routing to build and manage a pool of models per query.
- [[Learning to Orchestrate Agents in Natural Language with the Conductor]] ([Link](https://sakana.ai/learning-to-orchestrate/))
	- 2026-04-26 — Sakana; 7B Conductor trained with RL writes custom instructions and spins up planner/coder/verifier pipelines
- [[Trinity An Evolved LLM Coordinator]] ([Link](https://sakana.ai/trinity/))
	- 2026-04-25 — Sakana; <20K-param coordinator assigns Thinker/Worker/Verifier roles, optimized with evolutionary search
- [[Sakana Fugu One Model to Command Them All]] ([Link](https://sakana.ai/fugu-release/))
	- 2026-06-21 — Sakana; a single foundation-model API that orchestrates a swappable pool of frontier models
