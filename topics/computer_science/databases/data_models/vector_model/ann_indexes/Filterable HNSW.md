---
tags:
  - cs
  - cs/databases
created: 2025-11-25T18:26
modified: 2025-11-28T17:11
published:
sources:
  - "[Filtered Vector Search Improvements](https://qdrant.tech/blog/qdrant-1.16.x/#acorn---filtered-vector-search-improvements)"
topics:
  - Filterable HNSW
  - HNSW
  - Filtered Vector Search
  - Qdrant
  - ACORN
authors:
ai-assisted:
hidden:
public: true
---
# Filterable HNSW
To enhance the scalability and speed of vector search, Qdrant employs a graph-based index structure known as [HNSW (Hierarchical Navigable Small World)](https://qdrant.tech/documentation/concepts/indexing/#vector-index). While traditional HNSW is primarily designed for unfiltered searches, Qdrant has addressed this limitation by implementing a [filterable HSNW index](https://qdrant.tech/articles/filtrable-hnsw/). This innovative approach extends the HNSW graph with additional edges that correspond to indexed payload values. This enables Qdrant to maintain search quality even with high filtering selectivity, without introducing any runtime overhead during the search process.

Even with filterable HNSW graphs, there are instances where the quality of search results can deteriorate significantly. This can happen when you use a combination of high cardinality filters, leading to the HNSW graph becoming [disconnected](https://qdrant.tech/documentation/concepts/indexing/#filtrable-index). It is impractical to build additional links for every possible combination of filters in advance due to the potentially vast number of combinations. Another case where filterable HNSW may break down is in situations where filtering criteria are not known in advance.

To address these limitations, in version 1.16 we are introducing support for [ACORN](https://qdrant.tech/documentation/concepts/search/#acorn-search-algorithm), based on the ACORN-1 algorithm described in the paper [[ACORN]]: Performant and Predicate-Agnostic Search Over Vector Embeddings and Structured Data. With ACORN enabled, Qdrant not only traverses direct neighbors (the first hop) in the HNSW graph but also examines neighbors of neighbors (the second hop) if the direct neighbors have been filtered out. This enhancement improves search accuracy at the expense of performance, especially when multiple low-selectivity filters are applied.

![](https://qdrant.tech/blog/qdrant-1.16.x/hnsw-acorn.png)

Filtering and the HNSW graph without ACORN (left) and with ACORN (right).

You can enable ACORN on a per-query basis, via the optional [query-time `acorn` parameter](https://qdrant.tech/documentation/concepts/search/#acorn-search-algorithm). This doesn’t require any changes at index time.