---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-12-13T14:26
modified: 2025-12-13T14:28
published:
sources:
  - "[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)"
topics:
  - RAG Improvements
authors:
ai-assisted:
hidden:
public: true
---
# Page Index
Inspired by AlphaGo, we propose **[PageIndex](https://vectify.ai/pageindex)** — a **_vectorless_**, **reasoning-based RAG** system that builds a _hierarchical tree index_ for long documents and _reasons_ over that index for _retrieval_. It simulates how **human experts** navigate and extract knowledge from complex documents through **tree search**, enabling LLMs to _think_ and _reason_ their way to the most relevant document sections. It performs retrieval in two steps:
1. Generate a "Table-of-Contents" **tree structure index** of documents
2. Perform reasoning-based retrieval through **tree search**
[![|500](https://camo.githubusercontent.com/e9c3f93a4039fa4743b0655dc7a08eddd0eeb24ed1bfddfb03b6a0bf3c87cbdc/68747470733a2f2f646f63732e70616765696e6465782e61692f696d616765732f636f6f6b626f6f6b2f766563746f726c6573732d7261672e706e67)](https://camo.githubusercontent.com/e9c3f93a4039fa4743b0655dc7a08eddd0eeb24ed1bfddfb03b6a0bf3c87cbdc/68747470733a2f2f646f63732e70616765696e6465782e61692f696d616765732f636f6f6b626f6f6b2f766563746f726c6573732d7261672e706e67)
## 🧩 Features
Compared to traditional _vector-based RAG_, **PageIndex** features:
- **No Vector DB**: Uses document structure and LLM reasoning for retrieval, instead of vector search.
- **No Chunking**: Documents are organized into natural sections, not artificial chunks.
- **Human-like Retrieval**: Simulates how human experts navigate and extract knowledge from complex documents.
- **Transparent Retrieval Process**: Retrieval based on reasoning — traceable and interpretable. Say goodbye to approximate vector search ("vibe retrieval").

PageIndex powers a reasoning-based RAG system that achieved [98.7% accuracy](https://github.com/VectifyAI/Mafin2.5-FinanceBench) on FinanceBench, demonstrating **state-of-the-art** performance in professional document analysis (see our [blog post](https://vectify.ai/blog/Mafin2.5) for details).
