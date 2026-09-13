---
tags:
  - gen_ai
  - gen_ai/rag
created: 2024-10-30T13:11
modified: 2026-09-12T17:22
published:
sources:
  - "[Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html)"
topics:
  - RAG
  - Retrieval-Augmented Generation
  - Open Book QA
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
---
# RAG
Originally, in the [RAG paper](https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html) they train both the generator and the retriever.
This approach was preceded by [Open Book Abstractive Question Answering](https://www.pinecone.io/learn/series/nlp/question-answering/).
Currently, almost no production ready solution do the proper RAG but rather open book abstractive question answering.
## Concepts
-  [[Advanced RAG]]
- [[Modern RAG Architecture]]
- [[RAG Preprocessing]]
- [[RAG Evaluation]]
- [[RAG Benchmarks]]
- [[Production RAGs]]
- [[Context Databases]]
- [[Agentic Search]]
	- RL-trained retrieval agents that replace the fixed embed→ANN→rerank pipeline with an iterative loop
- [[Deep Search]]
	- Long-horizon browsing/research agents that plan searches, read sources, and synthesize cited answers or reports
## Resources
- [Vector Database Pricing Calculator](https://www.tokenburner.dev/vector-db-cost)
## Papers
- [[How Do LLMs Cite?]]
	- 2026-07-03 — mechanistic study showing citation decisions rely on shallow entity co-reference, not genuine use of document content
- [[How Retrieved Context Shapes Internal Representations in RAG]]
	- 0 citations
	- 2026-02-26
- [Breaking the Curse of Dimensionality: On the Stability of Modern Vector Retrieval](https://arxiv.org/abs/2512.12458?utm_source=substack&utm_medium=email)
	- 2025-12-13
	- This paper from Lakshman et al. investigates why modern high-dimensional vector retrieval systems succeed despite classical theory predicting they should suffer from the “curse of dimensionality,” where distances between points become indistinguishable. The authors extend foundational stability theory, i.e., the property that small query perturbations don’t drastically alter nearest neighbors, to three practical retrieval settings: (1) multi-vector search, proving that ColBERT’s Chamfer distance preserves stability when the underlying single-vector problem is strongly stable, while average pooling may not; (2) filtered vector search, demonstrating that sufficiently large penalties for filter mismatches can induce stability even when base search is unstable; and (3) sparse vector search, where they formalize “concentration of importance” (mass concentrated in few dimensions) and introduce “overlap of importance” (shared important dimensions between queries and documents), proving both properties together ensure stability. Through theoretical analysis using relative variance criteria and experiments on synthetic and real datasets (including ColBERT, SPLADE embeddings, and standard IR benchmarks), they validate that these conditions explain why modern neural embeddings enable efficient sub-linear search algorithms, providing actionable guidance for practitioners designing retrieval systems and embedding models.
- [Searching for Best Practices in Retrieval-Augmented Generation](https://aclanthology.org/2024.emnlp-main.981.pdf)
	- Investigates existing RAG approaches and their potential combinations to identify optimal RAG practices. Through extensive experiments, we suggest several strategies for deploying RAG that balance both performance and efficiency.
- [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/pdf/2312.10997)
	-  This comprehensive review paper offers a detailed examination of the progression of RAG paradigms, encompassing the Naive RAG, the Advanced RAG, and the Modular RAG. It meticulously scrutinizes the tripartite foundation of RAG frameworks, which includes the retrieval, the generation and the augmentation techniques.
## Libraries/Frameworks
- ChatGPT Retrieval Plugin - [chatgpt-retrieval-plugin](https://github.com/openai/chatgpt-retrieval-plugin)
	- The ChatGPT Retrieval Plugin repository provides a flexible solution for semantic search and retrieval of personal or organizational documents using natural language queries. It is a standalone retrieval backend, and can be used with [ChatGPT custom GPTs](https://chat.openai.com/gpts/discovery), [function calling](https://platform.openai.com/docs/guides/function-calling) with the [chat completions](https://platform.openai.com/docs/guides/text-generation) or [assistants APIs](https://platform.openai.com/docs/assistants/overview), or with the [ChatGPT plugins model (deprecated)](https://chat.openai.com/?model=gpt-4-plugins).