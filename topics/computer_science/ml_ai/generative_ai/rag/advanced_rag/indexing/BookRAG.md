---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-12-25T21:36
modified: 2025-12-25T21:39
published:
sources:
  - "[BookRAG: A Hierarchical Structure-aware Index-based Approach for Retrieval-Augmented Generation on Complex Documents](https://arxiv.org/abs/2512.03413?utm_source=substack&utm_medium=email)"
  - "[GPU-Accelerated Feature Interaction for Large-Scale Ad Retrieval, Efficient Neural Sparse Retrieval in Large-Scale Search Engines](https://recsys.substack.com/p/gpu-accelerated-feature-interaction?utm_source=substack&publication_id=1662831&post_id=180773595&utm_medium=email&utm_content=share&utm_campaign=email-share&triggerShare=true&isFreemail=true&r=53sn48&triedRedirect=true)"
topics:
  - BookRAG
authors:
ai-assisted:
hidden:
public: true
---
# BookRAG: A Hierarchical Structure-aware Index-based Approach for Retrieval-Augmented Generation on Complex Documents
> This paper from CUHK presents BookRAG, a RAG system designed for question answering over complex, hierarchically-structured documents like technical handbooks and guidebooks. The approach addresses two key limitations of existing RAG methods: their failure to capture deep connections between document structure and semantics, and their reliance on static query workflows. BookRAG introduces BookIndex, a unified index structure combining a hierarchical tree (preserving the document’s logical organization) with a knowledge graph (capturing fine-grained entity relationships), linked through a Graph-Tree mapping. To construct high-quality knowledge graphs, the authors propose a gradient-based entity resolution method that efficiently identifies and merges semantically equivalent entities by detecting sharp drops in similarity scores. The system employs agent-based retrieval inspired by Information Foraging Theory, which dynamically classifies queries into single-hop, multi-hop, or global aggregation categories and generates tailored operator workflows for each type. Experiments demonstrate that BookRAG significantly outperforms baselines in both retrieval recall and QA accuracy, while maintaining competitive efficiency through targeted information retrieval that minimizes computational overhead.
![](https://substackcdn.com/image/fetch/$s_!jw02!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F147a309f-7a84-4219-bf26-c09e8be0cebd_801x860.png)
