---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-12-25T23:06
modified: 2025-12-25T23:08
published:
sources:
  - "[SUMIT - Inf Retrieval Papers -  Vol.134 for Dec 08 - Dec 14, 2025](https://recsys.substack.com/p/a-geometric-analysis-of-bias-in-collaborative?utm_source=substack&publication_id=1662831&post_id=181395964&utm_medium=email&utm_content=share&utm_campaign=email-share&triggerShare=true&isFreemail=true&r=53sn48&triedRedirect=true)"
topics:
  - RouteRAG
  - Agentic RAG
  - Reinforcement Learning
  - Graph RAG
authors:
ai-assisted:
hidden:
public: true
---
# RouteRAG
- 📚 [https://arxiv.org/abs/2512.09487](https://arxiv.org/abs/2512.09487)
- 👨🏽‍💻 [https://github.com/YucanGuo/RouteRAG](https://github.com/YucanGuo/RouteRAG)
> This paper from UCAS presents RouteRAG, a reinforcement learning-based framework that enables LLMs to perform multi-turn RAG using both unstructured text and structured knowledge graphs. Unlike existing RAG systems that rely on fixed retrieval pipelines or single-shot retrieval, RouteRAG learns a unified policy that dynamically decides when to reason, what retrieval mode to use (passage, graph, or hybrid), and when to generate final answers. The system employs a two-stage training approach using Group Relative Policy Optimization: the first stage optimizes for answer correctness, while the second stage introduces an efficiency reward to minimize unnecessary retrieval overhead while maintaining accuracy. Experiments across five question-answering benchmarks demonstrate that RouteRAG significantly outperforms existing baselines, achieving comparable performance to GPT-4o-mini-based graph RAG systems despite using much smaller Qwen2.5 models (3B and 7B parameters), and surpassing the strongest RL-trained baseline (Search-R1) while using only 10k training examples compared to 170k.
