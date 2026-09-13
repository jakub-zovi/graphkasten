---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-01-17T10:59
modified: 2026-08-02T10:17
published:
sources:
topics:
  - RAG Improvements
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Advanced RAG
- This note aggregates different RAG improvements and replacements, organized by the **stage of the RAG pipeline** each method innovates on.
## Categories
- [[Query Transformation]]
	- Reshape or expand the query before retrieval (HyDE and its variants).
- [[RAG Indexing Strategies]]
	- Enrich chunks, impose structure, or precompute reasoning at index time (Contextual Retrieval, RAPTOR, BookRAG, IndexRAG, QB-RAG).
- [[Advanced Retrieval Strategies]]
	- Innovate on the retrieval mechanism itself (Page Index, LATTICE, GrepRAG, RuleRAG).
- [[Adaptive & Agentic RAG]]
	- Add dynamic control over when, what, and how to retrieve (Skill-RAG, RouteRAG).
- Context Pruning
	- [[LLM Context Pruning Improving RAG and Agentic AI Systems]] ([Link](https://milvus.io/blog/llm-context-pruning-a-developers-guide-to-better-rag-and-agentic-ai-results.md))
	- [[Provence: efficient and robust context pruning ]]
		- https://arxiv.org/abs/2501.16214
## Resources
- Comparison of RAG approaches - [Searching for Best Practices in Retrieval-Augmented Generation](https://aclanthology.org/2024.emnlp-main.981.pdf)