---
tags:
  - gen_ai
  - gen_ai/rag
created: 2024-11-27T13:37
modified: 2025-11-08T18:12
published:
sources:
  - "[Precise Zero-Shot Dense Retrieval without Relevance Labels](https://arxiv.org/pdf/2212.10496)"
topics:
  - HyDE
  - Hypothetical Documents
  - Zero-Shot Dense Retrieval
  - Query Expansion
authors:
ai-assisted:
hidden:
public: true
---
# HyDE Paper
[HyDE Paper:](https://arxiv.org/pdf/2212.10496)
> Hypothetical Document Embeddings (HyDE). Given a query, HyDE first zero-shot instructs an instruction-following language model (e.g. InstructGPT) to generate a hypothetical document. The document captures relevance patterns but is unreal and may contain false details. Then, an unsupervised contrastively learned encoder (e.g. Contriever) encodes the document into an embedding vector. This vector identifies a neighborhood in the corpus embedding space, where similar real documents are retrieved based on vector similarity. This second step ground the generated document to the actual corpus, with the encoder’s dense bottleneck filtering out the incorrect details

Article that summarizes HyDE paper well: [How to Use HyDE for Better LLM RAG Retrieval](https://towardsdatascience.com/how-to-use-hyde-for-better-llm-rag-retrieval-a0aa5d0e23e8)
LangChain specifically offers implementation of the [HyDE retriever](https://js.langchain.com/docs/integrations/retrievers/hyde/).
There are two approaches that use both the query and hypothetical document for the retrieval:
1. [[Query2Doc]]
2. [[QA-RAG]]