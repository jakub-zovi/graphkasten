---
tags:
  - cs
  - cs/databases
created: 2025-08-09T16:54
modified: 2025-11-28T17:42
published:
sources:
  - "[Hierarchical Navigable Small World graphs](https://arxiv.org/abs/1603.09320)"
topics:
  - HNSW
  - ANN Indexes
  - Graph-based Indexes
  - Navigable Small World
authors:
ai-assisted:
hidden:
public: true
---
# HNSW
> Hierarchical NSW incrementally builds a multi-layer structure consisting from hierarchical set of proximity graphs (layers) for nested subsets of the stored elements. The maximum layer in which an element is present is selected randomly with an exponentially decaying probability distribution. This allows producing graphs similar to the previously studied Navigable Small World (NSW) structures while additionally having the links separated by their characteristic distance scales. Starting search from the upper layer together with utilizing the scale separation boosts the performance compared to NSW and allows a logarithmic complexity scaling.

<img height="200px" src="https://assets.zilliz.com/hnsw_visualized_a9b401e55b.jpg" />

## Technical Aspects
- **Complexity**
	- ​Search - (poly)logarithmic
	- ​Build -  $n \times log(n)$
- **Parameters**
	-  M – number of neighbors added on insertion​
	- efConstruction​
	- efSearch​
	- L – number of layers​
	- m_L (recommended 1/ln(M)) - level multiplier that normalizes prob. func
## Modifications
- [[Distributed HNSW]]
- [[Filterable HNSW]]
## Additional Topics
- Some strange mention of caching that I do not understand (Maybe just upsell?)
	- HNSW can be used for large indexes when combined with an effective caching strategy. Aerospike uses a distributed cache with query steering approach which allows you to have many indexes, including large ones and load them into memory as your application needs them. ([Source](https://news.ycombinator.com/item?id=42496465&utm_source=chatgpt.com))