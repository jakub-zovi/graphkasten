---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-07T16:04
modified: 2026-08-02T10:12
published:
sources:
topics:
authors:
ai-assisted:
hidden:
public: true
---

Sources: [Pinecone Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/)
# Recursive Chunking
Recursive chunking divides the input text into smaller chunks in a hierarchical and iterative manner using a set of separators. If the initial attempt at splitting the text doesn’t produce chunks of the desired size or structure, the method recursively calls itself on the resulting chunks with a different separator or criterion until the desired chunk size or structure is achieved. This means that while the chunks aren’t going to be exactly the same size, they’ll still “aspire” to be of a similar size.

```python
text = "..." # your text
from langchain.text_splitter import RecursiveCharacterTextSplitter
text_splitter = RecursiveCharacterTextSplitter(
    # Set a really small chunk size, just to show.
    chunk_size = 256,
    chunk_overlap  = 20
)

docs = text_splitter.create_documents([text])
```
