---
tags:
  - cs
  - cs/databases
created: 2025-08-13T11:34
modified: 2026-07-03T11:05
published:
sources:
topics:
  - VDBMS
  - Qdrant
authors:
ai-assisted:
hidden:
public: true
---
# Qdrant
My Master Thesis:
> One of the newer databases that was released in 2021 is Qdrant. This database is written in Rust and uses a custom version of HNSW. It supports both constrained and hybrid search. Qdrant uses rule-based optimization to determine what type of index to use for query execution. Qdrant leverages heavily quantization of vectors to speed up its search.
## Topics
- [[Qdrant Academy]]
	- Free self-paced courses from beginner to expert with certification
- [[Multitenancy]]
- [[computer_science/databases/Hybrid Cloud]]
- Distributed Qdrant
	- [[Raft Consensus]]
		- https://raft.github.io/
	- [Distributed Deployment of Qdrant Cluster with Sharding & Replicas](https://medium.com/@vardhanam.daga/distributed-deployment-of-qdrant-cluster-with-sharding-replicas-e7923d483ebc)
## Features
## [[Qdrant Sync With SQL]]
- Approaches for syncing Qdrant with SQL database like Postgres
### Hybrid Search
- Practice of combining multiple searches with some weighting scheme
- RRF with custom weighting
	- [Weight adjustment for hybrid prefetch statements](https://github.com/qdrant/qdrant/issues/6067)
	- [FormulaQuery with prefetch results](https://github.com/qdrant/qdrant/issues/6836)
#### [IDF Modifier](https://qdrant.tech/documentation/concepts/indexing/#idf-modifier)
For many search algorithms, it is important to consider how often an item occurs in a collection. Intuitively speaking, the less frequently an item appears in a collection, the more important it is in a search.

This is also known as the Inverse Document Frequency (IDF). It is used in text search engines to rank search results based on the rarity of a word in a collection.

IDF depends on the currently stored documents and therefore can’t be pre-computed in the sparse vectors in streaming inference mode. In order to support IDF in the sparse vector index, Qdrant provides an option to modify the sparse vector query with the IDF statistics automatically.

The only requirement is to enable the IDF modifier in the collection configuration:

```python
from qdrant_client import QdrantClient, models

client = QdrantClient(url="http://localhost:6333")

client.create_collection(
    collection_name="{collection_name}",
    vectors_config={},
    sparse_vectors_config={
        "text": models.SparseVectorParams(
            modifier=models.Modifier.IDF,
        ),
    },
)
```
Qdrant uses the following formula to calculate the IDF modifier:
$$
\text{IDF}(q_i) = \ln \left(\frac{N - n(q_i) + 0.5}{n(q_i) + 0.5}+1\right)
$$
Where:
- `N` is the total number of documents in the collection.
- `n` is the number of documents containing non-zero values for the given vector element.