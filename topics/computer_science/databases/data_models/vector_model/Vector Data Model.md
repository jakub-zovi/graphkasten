---
tags:
  - cs
  - cs/databases
created: 2024-10-08T12:55
modified: 2026-04-09T16:54
published:
sources:
topics:
  - Vector Databases
  - VDBMS
  - ANN Indexes
  - HNSW
  - Vector Search
authors:
ai-assisted:
hidden:
public: true
---
# Vector Data Model
The vector data model manages unstructured data, like images and videos, by encoding it into high-dimensional vectors. Traditional databases can't handle this data efficiently, so Vector Database Management Systems (VDBMS) use embedding models to convert it for storage and querying. Specialized algorithms then index and search the data based on vector similarity, enabling efficient management of unstructured formats.

## Vector Databases
There exist many different vector databases currently. They are described more thouroughly here: [[Vector Databases]].
## Searching
Vector databases perform specific type of searching called [[Similarity Searching]].

### Indexing
Vector databases use [ANN Indexes](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fdatabases%2Fdata_models%2Fvector_model%2Fann_indexes%2FANN%20indexes) to index and search in the data.

#### HNSW
This algorithm is, for now, the de facto standard in modern vector databases. HNSW combines two concepts together to create its indexing structure: skip lists and navigable small worlds [(HNSW)](https://arxiv.org/abs/1603.09320).

Skip list is a probabilistic data structure composed of a hierarchy of linked lists that provides better average time complexity O(logn) for search at the cost of taking more space as opposed to a linked list ([Skip List](https://dl.acm.org/doi/abs/10.1145/78973.78977)). Navigable small worlds is a graph within which a greedy routing can be performed with polylogarithmic or logarithmic search complexity ([Navigable Small Worlds](https://www.sciencedirect.com/science/article/abs/pii/S0306437913001300)).

The combination of these concepts results in the structure shown in the [Figure below](https://www.notion.so/Vector-Databases-362814de265e4186a4872447a4cbfd4e?pvs=21).

Image Source:  [(HNSW)](https://arxiv.org/abs/1603.09320)

For a more thorough explanation of the build and search phases, read the original [HNSW paper](https://arxiv.org/abs/1603.09320) or the [article by Pineconee](https://www.pinecone.io/learn/series/faiss/hnsw/). Next, we explain the parameters of the HNSW algorithm that we can use to improve retrieval in our RAG solutions.

There are three parameters: M, efConstruction and efSearch.

**M** - corresponds to the maximum number of links between the nodes within the graph. Increasing this parameter can improve recall at the cost of a higher index memory footprint [(HNSW)](https://arxiv.org/abs/1603.09320).

**efConstruction** - corresponds to the size of the candidate list from which the neighbours for the new graph node will be picked during building of index. Increasing this parameter can improve the recall at the cost of a longer build time of the index [(HNSW)](https://arxiv.org/abs/1603.09320).

**efSearch** - corresponds to the size of the candidate list from which we pick the next node to visit during the search. Increasing this parameter can improve recall at the cost of longer search time [(HNSW)](https://arxiv.org/abs/1603.09320).

💡 Configuration of HNSW parameters is a balancing act since we are always trading better recall for something (memory footprint, search speed, build speed). Therefore, these parameters should be configured with the application use case in mind.


💭 HNSW is not a perfect algorithm, and it comes with a plethora of shortcomings (e.g. the index is in memory). One SOTA index that addresses these shortcomings and is already being implemented in modern vector databases is [DISKAnn](https://papers.nips.cc/paper_files/paper/2019/hash/09853c7fb1d3f8ee67a61b6bf4a7f8e6-Abstract.html).

## Advanced Search Operators
Regular kANN search is usually not enough to meet our retrieval needs when developing RAG applications. Therefore we employ [[Advanced Search Operators]].
## Other Features
There are some other notable features of vector databases, such as vector compression, query optimization, data partitioning, etc.

 **[[Compression]]**
When working with large datasets and using embeddings with high dimensions, we can quickly run out of disk space and also memory since indexes like HNSW usually operate in memory. Therefore, modern databases implement a quantized version of HNSW. In this version, vectors are compressed using quantization techniques such as product quantization [(LI in VDBMS)](https://is.muni.cz/th/hsfz1/).

💡Modern vector databases such as [Qdrant](https://qdrant.tech/documentation/guides/quantization/) usually apply quantization by default to speed up the search. This feature starts to matter when the dataset size gets large.

## Architecture of Vector Database
It is good to have a general overview of the whole architecture of vector databases since it is a key component in the RAG pipeline. The [Figure below](https://www.notion.so/Vector-Databases-362814de265e4186a4872447a4cbfd4e?pvs=21) visualizes the generic architecture of the modern vector database:

Image Source: [(LI in VDBMS)](https://is.muni.cz/th/hsfz1/)
## Sources
This page is heavily based on my master thesis: [Learned Indexing in Vector Database Management Systems](https://is.muni.cz/th/hsfz1/)

Another series of articles that covers vector databases and is a great source to learn about them: [https://thedataquarry.com/posts/vector-db-1/](https://thedataquarry.com/posts/vector-db-1/)