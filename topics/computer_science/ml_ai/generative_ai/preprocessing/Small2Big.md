---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-08T11:41
modified: 2026-08-02T10:13
published:
sources:
  - "[Advanced RAG 01: Small-to-Big Retrieval](https://medium.com/towards-data-science/advanced-rag-01-small-to-big-retrieval-172181b396d4)"
  - "[RAG for LLMs: A Survey](https://arxiv.org/pdf/2312.10997)"
topics:
  - Chunking
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Small2Big
[Advanced RAG 01: Small-to-Big Retrieval](https://medium.com/towards-data-science/advanced-rag-01-small-to-big-retrieval-172181b396d4):
> Specifically, decoupling text chunks used for retrieval vs. the text chunks used for synthesis could be advantageous. Using smaller text chunks enhances the accuracy of retrieval, while larger text chunks offer more contextual information. The concept behind small-to-big retrieval is to use smaller text chunks during the retrieval process and subsequently provide the larger text chunk to which the retrieved text belongs to the large language model.