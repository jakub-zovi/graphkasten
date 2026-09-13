---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-08-02T10:00
modified: 2026-08-02T10:00
published:
sources:
topics:
  - Query Transformation
  - Query Expansion
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
---
# Query Transformation
- RAG methods that reshape or expand the **query** before retrieval, closing the gap between how users phrase questions and how answers are written in the corpus.
## Topics
- [[HyDE]]
	- Zero-shot generates a hypothetical answer document, then retrieves real docs near its embedding. Variants Query2Doc and QA-RAG (both linked from the HyDE note) extend the idea with query-doc concatenation and a fine-tuned domain generator.
