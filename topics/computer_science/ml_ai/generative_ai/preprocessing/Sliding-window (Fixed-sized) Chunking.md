---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-07T16:04
modified: 2026-08-02T10:12
published:
sources:
  - "[Pinecone Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/)"
topics:
  - Chunking
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Sliding-window (Fixed-sized) Chunking
This is the most common and straightforward approach to chunking: we simply decide the number of tokens in our chunk and, optionally, whether there should be any overlap between them. In general, we will want to keep some overlap between chunks to make sure that the semantic context doesn’t get lost between chunks.

```python
text = "..." # your text
from langchain.text_splitter import CharacterTextSplitter
text_splitter = CharacterTextSplitter(
    separator = "\n\n",
    chunk_size = 256,
    chunk_overlap  = 20
)
docs = text_splitter.create_documents([text])
```
