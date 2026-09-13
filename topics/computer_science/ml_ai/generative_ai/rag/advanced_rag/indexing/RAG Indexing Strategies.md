---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-08-02T10:00
modified: 2026-08-02T10:00
published:
sources:
topics:
  - RAG Indexing
  - Chunk Preprocessing
  - Hierarchical Indexing
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
---
# RAG Indexing Strategies
- RAG methods whose innovation happens **at index time** — enriching chunks, imposing structure, or precomputing reasoning before any query arrives.
## Topics
- [[Contextual Retrieval]]
	- Prepends LLM-generated, chunk-specific context to each chunk so isolated chunks stay interpretable.
- [[RAPTOR]]
	- Recursively embeds, clusters, and summarizes chunks into a tree, retrieving across abstraction levels.
- [[BookRAG]]
	- Structure-aware index unifying a hierarchical tree with a knowledge graph for complex, hierarchically-organized documents.
- [[IndexRAG]] ([Link](https://arxiv.org/abs/2603.16415))
	- Precomputes multi-hop "bridging facts" at index time so cross-document reasoning needs a single retrieval pass.
- [[QB-RAG]]
	- Pre-generates a database of potential questions from the content and matches incoming queries against it for tighter query-content alignment.
