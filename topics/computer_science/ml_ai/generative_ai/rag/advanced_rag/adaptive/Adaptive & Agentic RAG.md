---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-08-02T10:00
modified: 2026-08-02T10:00
published:
sources:
topics:
  - Adaptive RAG
  - Agentic RAG
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
---
# Adaptive & Agentic RAG
- RAG methods that add **dynamic control** over the pipeline — deciding *when* to retrieve, *what* retrieval mode to use, and *when* to stop — rather than running a fixed retrieve-then-generate flow.
- The purpose-trained end of this spectrum — models fine-tuned end-to-end with RL to run the whole retrieval loop — has grown into its own cluster: [[Agentic Search]].
## Topics
- [[Skill-RAG]] ([Link](https://arxiv.org/abs/2604.15771))
	- Failure-state-aware retrieval: probes hidden states to trigger retrieval only when the model is about to fail, then routes to a skill-matched retriever.
- [[RouteRAG]]
	- RL-trained unified policy that dynamically chooses passage, graph, or hybrid retrieval across multi-turn reasoning.
