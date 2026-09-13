---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-07T16:43
modified: 2026-08-02T10:19
published:
sources:
  - "[Jina - Late Chunking](https://jina.ai/news/late-chunking-in-long-context-embedding-models/), [Paper - LATE CHUNKING: CONTEXTUAL CHUNK EMBEDDINGS](https://arxiv.org/pdf/2409.04701)"
topics:
  - Chunking
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Late Chunking
[Jina - Late Chunking](https://jina.ai/news/late-chunking-in-long-context-embedding-models/):
> Late Chunking approach we propose in this article first applies the transformer layer of the embedding model to _the entire text_ or as much of it as possible. This generates a sequence of vector representations for each token that encompasses textual information from the entire text. Subsequently, mean pooling is applied to each chunk of this sequence of token vectors, yielding embeddings for each chunk that consider the entire text's context. Unlike the naive encoding approach, which generates independent and identically distributed (i.i.d.) chunk embeddings, **late chunking creates a set of chunk embeddings where each one is "conditioned on" the previous ones, thereby encoding more contextual information for each chunk.**

<img src="https://arxiv.org/html/2409.04701v1/x2.png" >

## Related
- [[Visual Late Chunking]] ([Link](https://arxiv.org/abs/2604.10167)) — extends late chunking to the visual domain (ColChunk, Yan et al. 2026)

## Comparison
|                                      | Naive Chunking                                  | Late Chunking                                          |
|--------------------------------------|-----------------------------------------------|------------------------------------------------------|
| The need of boundary cues            | Yes                                           | Yes                                                  |
| The use of boundary cues             | Directly in preprocessing                    | After getting the token-level embeddings from the transformer layer |
| The resulting chunk embeddings       | i.i.d.                                       | Conditional                                          |
| Contextual information of nearby chunks | Lost. Some heuristics (like overlap sampling) to alleviate this | Well-preserved by long-context embedding models |

