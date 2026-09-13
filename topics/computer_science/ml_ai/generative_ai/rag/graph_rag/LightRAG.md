---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-06-08T11:15
modified: 2026-09-12T17:24
published: 2024-10-08
sources:
  - "[LightRAG: Simple and Fast Retrieval-Augmented Generation](https://arxiv.org/abs/2410.05779)"
  - "[LightRAG (EMNLP 2025 Findings)](https://aclanthology.org/anthology-files/anthology-files/pdf/findings/2025.findings-emnlp.568.pdf)"
  - "[HKUDS/LightRAG](https://github.com/HKUDS/LightRAG)"
topics:
  - RAG Improvements
  - Knowledge Graph
  - Dual-Level Retrieval
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# LightRAG
- Graph-based RAG built around a **dual-level retrieval** scheme — combines specific-entity ("low-level") and topic-level ("high-level") keys in the same KG
- Paper: [LightRAG: Simple and Fast Retrieval-Augmented Generation](https://arxiv.org/abs/2410.05779)
	- EMNLP 2025 Findings
- Github: [HKUDS/LightRAG](https://github.com/HKUDS/LightRAG)
	- 36.2k stars

![|700](https://github.com/HKUDS/LightRAG/raw/main/README.assets/b2aaf634151b4706892693ffb43d9093.png)
## Resources
- [LightRAG: Simple and Fast Alternative to GraphRAG for Legal Doc Analysis](https://learnopencv.com/lightrag/)
## Essence
- Two main complaints about earlier graph-RAGs ([[GraphRAG]] in particular)
	- Heavy community detection + hierarchical LLM summarization at index time → expensive
	- Single retrieval granularity — either fine entity lookup *or* coarse community summary, not both
- LightRAG's answer
	- Build a **flat** entity-relation KG (no communities, no hierarchy)
	- Attach **two index keys per node/edge** — one fine, one thematic
	- At query time issue *two* retrievals over those keys and merge
- Result: GraphRAG-style multi-hop quality at a fraction of the indexing cost, plus **incremental updates by graph union**
## Indexing

![|900](https://learnopencv.com/wp-content/uploads/2024/11/LightRAG-VectorDB-Json-KV-Store-Indexing-Flowchart-scaled.jpg)

The pipeline is formalized as $\hat{D} = (\hat{V}, \hat{E}) = \text{Dedupe} \circ \text{Prof}(V, E)$ — three composed steps.
### 1. Recognition (entity + relation extraction)
- Chunk the corpus, then **one LLM call per chunk** asks the model to emit
	- A list of entities (nodes) with type and short description
	- A list of relationships (edges) between those entities with description
- Per-paper: total LLM calls for this stage ≈ `total_tokens / chunk_size` — i.e. linear, no overhead beyond plain dense RAG embedding
- Where this differs from HippoRAG 2: HippoRAG 2 splits NER and RE into two calls; LightRAG fuses them into one richer prompt that returns descriptions as well as triples
### 2. Profiling (key-value generation)
- LLM-empowered function $P(\cdot)$ produces a **(key, value) pair for every node and every edge**
	- Node key = entity name (used as fine-grained / low-level index key)
	- **Edge keys = multiple LLM-generated index phrases** that include "global themes from connected entities" → this is what makes high-level / topical retrieval possible
	- Value = a textual paragraph summarizing the entity or relation, including its description, the names of connected entities, and original passage snippets
- The keys are embedded and stored in a vector DB; the values live in a key-value store (typically JSON)
- This is the step that gives LightRAG its **dual granularity** — each edge carries both its concrete description *and* topic-level keys
### 3. Deduplication
- Identical entities and relations extracted from different chunks are merged
- Done by name match + LLM-assisted profile consolidation; far less aggressive than the community detection [[GraphRAG]] performs
- After this step the graph is much smaller than the raw extraction output and graph operations stay cheap
### Incremental Updates
- New documents $D'$ run through the same φ pipeline → sub-graph $(\hat{V'}, \hat{E'})$
- Final graph = **union of node sets and union of edge sets**: $\hat{V} \cup \hat{V'}$, $\hat{E} \cup \hat{E'}$
- Deduplication handles overlapping entities; no re-indexing of the original graph required
- Contrasts sharply with [[GraphRAG]] (whose community summaries must be partially recomputed)
## Retrieval

![|700](https://learnopencv.com/wp-content/uploads/2024/11/LightRAG-Querying-Flowchart-Dual-Level-Retrieval-Generation-Knowledge-Graphs-scaled.jpg)
### 1. Query keyword extraction
- An LLM call rewrites the query into **two keyword sets**
	- $k^{(l)}$ — **local / low-level**: specific entity mentions ("Pride and Prejudice", "Jane Austen")
	- $k^{(g)}$ — **global / high-level**: themes ("19th-century English literature", "social class commentary")
### 2. Dual vector lookup
- $k^{(l)}$ → vector search against **node keys** → matched entities $N_v$
- $k^{(g)}$ → vector search against **edge keys** → matched relations $N_e$
- Two separate vector indexes, both populated during the Profiling step
### 3. Subgraph expansion (the graph part)
- For every matched node/edge, pull in its **one-hop neighborhood** from the graph
- Formally: include every $v_i \in V$ such that $v_i \in N_v \lor v_i \in N_e$ plus its neighbors
- This is where structural information enters — the graph is used as a *navigator* over the retrieved seeds, not traversed from scratch
### 4. Context assembly + generation
- Concatenate the values (descriptions + original snippets) of all retrieved entities, relations, and neighbor nodes
- Feed to the generator LLM with the original query
- No re-ranking step in vanilla LightRAG (some forks add cross-encoder reranking)
## Comparison Notes
- vs HippoRAG 2 — both are flat KG approaches, but HippoRAG 2 ranks with **Personalized PageRank** over the whole graph at query time, while LightRAG just does **vector lookup + 1-hop expansion**. HippoRAG 2 wins on long multi-hop chains; LightRAG is simpler and faster at retrieval
- vs [GraphRAG](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fgenerative_ai%2Frag%2Fgraph_rag%2FGraphRAG) — LightRAG drops the community detection step entirely. Indexing cost ~order of magnitude lower, but you lose the explicit community-summary retrieval path
- vs [[RAPTOR]] — RAPTOR builds a summary tree; LightRAG builds an entity graph with topic-tagged edges. RAPTOR has fewer LLM calls but re-processes text up the tree; LightRAG has more calls but each is bounded to one chunk
## Results
- On benchmarks from the paper (UltraDomain, mix of agriculture/CS/legal/mix domains) LightRAG outperforms naive RAG, RQ-RAG, HyDE, and GraphRAG on both **comprehensiveness** and **diversity** of generated answers
- Incremental-update experiments show graceful integration of new corpora without quality regression on old queries
- Indexing cost is reported as roughly an order of magnitude below GraphRAG on the same corpora
