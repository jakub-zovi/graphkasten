---
tags:
  - cs
  - cs/databases
created: 2024-10-30T11:22
modified: 2026-02-16T13:43
published:
sources:
  - My Description of Hybrid Search for DS
topics:
  - Hybrid Search
  - Sparse Retrieval
  - Dense Retrieval
  - BM25
authors:
ai-assisted:
hidden:
public: true
---
# Hybrid Search
- My general description
> This type of search combines sparse retrieval (e.g. BM25 algorithm) with dense retrieval (e.g. ANN index). The outputs of these two retrievals are combined through some weighting scheme (e.g [[Combination of Rankings]]) to obtain the final result.
> 
> Modern vector databases usually employ the BM25 algorithm for hybrid search. This algorithm allows you to specialize keywords to search ([Sparse Retrieval](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fgenerative_ai%2Frag%2Farchitecture%2Fsparse_retrieval%2FSparse%20Retrieval)) for in document chunks. Therefore, when performing hybrid search chunks with these keywords will be prioritized in the search result. Most vector databases nowadays allow the specification of the weight that should be given to sparse and dense retrieval, respectively.
> 
> This search is very beneficial when you can estimate important keywords (in relation to your dataset) that appear within the user prompt. You can then leverage these keywords to improve the search results. Hybrid search was shown to improve performance on document retrieval [(The Chronicles of RAG)](https://arxiv.org/abs/2401.07883).
> 