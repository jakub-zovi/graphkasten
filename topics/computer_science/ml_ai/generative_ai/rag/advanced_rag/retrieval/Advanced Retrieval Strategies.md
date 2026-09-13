---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-08-02T10:00
modified: 2026-08-02T10:10
published:
sources:
topics:
  - RAG Retrieval
  - Vectorless Retrieval
  - Lexical Retrieval
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
---
# Advanced Retrieval Strategies
- RAG methods whose innovation is the **retrieval mechanism itself** — how candidate documents are matched and fetched, often replacing or augmenting plain dense vector search.
## Topics
- [[Page Index]]
	- Vectorless, reasoning-based retrieval: builds a table-of-contents tree and navigates it via LLM tree search, no vector DB or chunking.
- [[LATTICE - LLM-guided Hierarchical Retrieval]] ([Link](https://arxiv.org/html/2510.13217v1))
	- LLM navigates a semantic tree with logarithmic search complexity, using calibrated latent relevance scores for reasoning-intensive queries.
- [[GrepRAG]]
	- Lightweight lexical retrieval where the LLM issues grep/ripgrep commands, refined with identifier-weighted BM25 reranking for code completion.
- [[RuleRAG]]
	- Rule-guided retrieval that injects symbolic rules as in-context demonstrations to steer retrievers and generators.
