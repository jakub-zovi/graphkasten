---
tags:
  - gen_ai
  - gen_ai/rag
created:
modified: 2026-07-26T13:49
published:
sources:
topics:
  - GraphRAG
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Use of Graph in RAG
- GraphRAG represents new approach for constructing the knowledge base for the RAG application. It can improve the quality of the output of the RAG application. But this come at a significant cost. The goal of this task is to explore whether the improvement in quality justifies the cost and whether we can use this approach in our projects.
## Approaches
- [[NaviRAG]] ([Link](https://arxiv.org/abs/2604.12766)): Reframes RAG as active knowledge navigation; builds offline Knowledge Trees and navigates them top-down at query time, outperforming GraphRAG and HippoRAG2 on cross-region evidence tasks
- [[HippoRAG 2]] ([Link](https://arxiv.org/abs/2502.14802)): Builds a flat OpenIE-based KG over passages and applies Personalized PageRank at query time for associative, multi-hop retrieval
- [[G-Retriever]] ([Link](https://arxiv.org/abs/2402.07630)): Retrieves a connected subgraph via Prize-Collecting Steiner Tree, then feeds it to the LLM as both text and a GNN-encoded soft prompt
- [[LightRAG]]: Flat entity-relation KG with dual-level (low/high) index keys; dual vector lookup + 1-hop graph expansion at query time; supports incremental updates by graph union
-  [[GraphRAG]]: initial GraphRAG paper
- [An Ontology-Driven Graph RAG for Legal Norms: A Structural, Temporal, and Deterministic Approach](https://arxiv.org/pdf/2505.00039)
	- Building ontologies for the Legal domain
- [Law GraphRAG: An Advanced Legal QuestionAnswering System](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=11047851)
## Resources
- Papers:
	- Graph Retrieval-Augmented Generation: A Survey
		- https://dl.acm.org/doi/10.1145/3777378
		- https://github.com/pengboci/GraphRAG-Survey
		- The authors formalize the GraphRAG workflow into three core stages: Graph-Based Indexing (constructing and organizing graph databases from open knowledge graphs or self-constructed data), Graph-Guided Retrieval (extracting relevant graph elements like nodes, triplets, paths, or subgraphs using non-parametric, LM-based, or GNN-based retrievers), and Graph-Enhanced Generation (converting retrieved graph structures into formats processable by language models). The survey systematically categorizes existing methodologies across these stages, examines retrieval paradigms (once, iterative, and multi-stage), discusses training strategies, and analyzes downstream applications spanning question answering, recommendation systems, and domain-specific tasks in healthcare, finance, and e-commerce.
    - [HybridRAG](https://arxiv.org/pdf/2408.04948) 
    - [GraphRAG](https://arxiv.org/pdf/2404.16130)
- Existing tools and frameworks for leveraging knowledge graphs in RAG:
    - [GraphRAG](https://github.com/microsoft/graphrag)
    - [GraphRAG Azure Accelerator](https://github.com/Azure-Samples/graphrag-accelerator)
    - [Knowledge graphs with LangChain](https://python.langchain.com/docs/how_to/graph_constructing/) 
- [GraphRAG Website](https://graphrag.com/reference/graphrag/text2cypher/)
- [Good overview video of GraphRAG](https://www.youtube.com/watch?v=knDDGYHnnSI&ab_channel=AIEngineer)
- [[GraphRAG course]]
## Domain-Specific GraphRAGs
- Legal
	- [[An Ontology-Driven Graph RAG for Legal Norms]] ([Link](https://arxiv.org/html/2505.00039v4))
		- JURIX 2025 — ontology-grounded, structure-aware temporal graph for versioned legal text; deterministic point-in-time retrieval and provenance reconstruction
		- Github: [hmartim/sat-graph-api](https://github.com/hmartim/sat-graph-api)
			- 10 stars
	- [[LegalGraphRAG]] ([Link](https://arxiv.org/html/2605.28120v1))
		- ACL 2026 — three-layer Hierarchical Legal Graph (Fact / Ontology / Rule) with a Researcher → Auditor → Adjudicator multi-agent pipeline for legal judgment prediction
		- Github: [Zovi343/LegalGraphRAG](https://github.com/Zovi343/LegalGraphRAG)
	- [Agentic Knowledge Graph Construction](https://info.deeplearning.ai/e3t/Ctc/LX+113/cJhC404/VVTyT63CZ_HgW743mQN7yMfddW54fY-N5BLntvN6tf6Yl3qgz0W95jsWP6lZ3mnW4GMZRv6flbr5W69LD1Y1bHJmTW1v4mVt6X4-vmW1gG4Kg7515zzW6CJzTG2vFKtmW81j65s6n4H5RN36p4F7QlfXlW1z7Nfq7vD6MZW3fBgK79jCC4kW2BlRM_2rVp00W9dtKqq2x-snSN1NKB3ZnpMGtW59pkHN2Pb5z-W4y1mJR940NTWW2DpFNK5yTRMNW4kVhNZ3hWspCW5CZFFj533JHnW8YmtmB1754gvMbQWj2KZYXXW1MpJRT7s6NP6W8d4QTk346W6wW95wdTG4fws-_W6qBcrs6HnWCvW72X3lY3-C3MGMmR_6SZrsN1W792d4c1785F9Vw7WMB3R43xWN9l59s8Mb4wKW1-M0Rc5X5_jSW991d2m1b3Mc1f6FDgVK04).