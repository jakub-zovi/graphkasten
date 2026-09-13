---
tags:
  - gen_ai
  - gen_ai/evaluation
created:
modified: 2026-06-25T09:54
published:
sources:
topics:
  - Evaluation
authors:
ai-assisted:
hidden:
public: true
---
# Evaluation of LLM/RAG applications
A note dedicated to all the aspects of the evaluation of the AI applications
## Topics
- [[Agent Evaluation]]
- [[Evaluation Libraries]]
	- Libraries that contain metrics definitions that can be used to evaluate LLM outputs
- [[User Simulation]]
- [[Experiment Runners]]
- [[LLM Metrics]] - metrics use to evaluate the output of the LLM
- [[IR Metrics]] - metrics to evaluate retrieval
- Datasets for AI evaluation:
    - RAG-Instruct-Benchmark-Tester -[https://huggingface.co/datasets/llmware/rag_instruct_benchmark_tester](https://huggingface.co/datasets/llmware/rag_instruct_benchmark_tester)
	- LLM Benchmark that uses LLM-as-a-Judge
		- [The FACTS Grounding Leaderboard: Benchmarking LLMs’ Ability to Ground Responses to Long-Form Input](https://storage.googleapis.com/deepmind-media/FACTS/FACTS_grounding_paper.pdf)
- Companies with AI evaluation products
    - Galileo - [https://www.rungalileo.io/](https://www.rungalileo.io/)
    - Humanloop - [https://humanloop.com/](https://humanloop.com/)
    - ComposoAI  - https://www.composo.ai/s
## Resources
- [[Evaluation of AI Applications In Practice]] ([Link](https://medium.com/gooddata-developers/evaluation-of-ai-applications-in-practice-ecbb5a97d878))
	- 2025-08-06 — Practical guide to evaluating LLM-backed applications: dataset construction, metrics selection, and infrastructure for iterative tuning
- [How to evaluate AI applications](https://www.youtube.com/watch?v=OREE2Iui6m0)
- [Gaia2 and ARE: Empowering the Community to Evaluate Agents](https://huggingface.co/blog/gaia2)
- [Understanding the 4 Main Approaches to LLM Evaluation](https://sebastianraschka.com/blog/2025/llm-evaluation-4-approaches.html?ref=dailydev#13-checking-the-generated-answer-letter)
	- Article about evaluating LLMs themselves and not the applications built on top of them