---
tags:
  - cs
  - cs/databases
created: 2024-10-29T13:28
modified: 2026-08-13T14:20
published:
sources:
topics:
  - ANN Indexes
  - Partition-based Indexes
  - Hash-based Indexes
  - Graph-based Indexes
authors:
ai-assisted:
hidden:
public: true
---
# ANN indexing
The goal of the index is to prevent scanning the whole database to retrieve the answer. In the case of k-ANN search, that means performing distance computation between the query and each object in the database. Performing distance computation is the most expensive operation in k-ANN search [(LI in VDBMS)](https://is.muni.cz/th/hsfz1/).

Therefore, we use an index that tries to minimize the number of these operations. ANN indexing algorithms can be categorized roughly into three groups: partition-based (e.g. IVF-PQ), hash-based (e.g. LSH) and graph-based (e.g. [HNSW](https://arxiv.org/abs/1603.09320)). Almost all vector databases use graph-based algorithms nowadays. More specifically, they employ the Hierarchical Navigable Small Worlds [(HNSW)](https://arxiv.org/abs/1603.09320) algorithm.
## Categorization
- [[Partition-based]]
- [[Hash-based]]
- [[Graph-based]]
## Filtered Search
- [[The Achilles Heel of Vector Search Filters]]
	- 2025-05-09 — Why filtered ANN often *slows* search: pre/post/integrated strategies compared across HNSW and IVF-PQ, benchmarks across Faiss/Pinecone/Qdrant/Weaviate, and filter-fusion via metadata-encoded embeddings