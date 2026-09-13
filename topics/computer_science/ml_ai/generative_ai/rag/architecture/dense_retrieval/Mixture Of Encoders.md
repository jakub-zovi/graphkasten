---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-12-04T15:12
modified: 2026-08-02T09:32
published:
sources:
  - Cursor Answer From 
topics:
  - SuperLinked
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Mixture of Encoders
- An approach used by [[SuperLinked]] to create [[Metadata-aware Embeddings]] that take into account metadata attributes during the similarity search.
## Papers
- [[Utilizing Metadata for Better Retrieval-Augmented Generation]] ([Paper](https://arxiv.org/html/2601.11863v1))
	- 17 Jan 2026
	- 2 citations
	- **Finally a paper that deals with metadata aware embeddings**
## How to Prevent Dwarfing By Large Semnatic Vector
- To make a concatenated vector schema function correctly, practitioners use several normalization and structural strategies:
1. [Independent Space Normalization (Unit Length Scaling)](https://medium.com/data-science/every-scaler-and-its-application-in-data-science-1115bec62660)
	- Before concatenation, you must normalize each sub-vector individually to a unit length of 1 ($\Vert{}V\Vert{} = 1$) [Source](https://osanseviero.github.io/hackerllama/blog/posts/sentence_embeddings/).
		* The Result: If $V_{text}$ is normalized to 1, and $V_{metadata}$ is normalized to 1, they carry exactly equal weight in the final distance calculation, regardless of how many dimensions each possesses.
2. Explicit Sub-Vector Weighting
	- Once both sub-vectors are normalized to a magnitude of 1, you can apply an explicit scalar weight ($w$) to each component prior to concatenation:
	$$V_{composite} = [ w_1 \cdot V_{text} \,\Vert{}\, w_2 \cdot V_{metadata} ]$$ 
	- If your business rules dictate that metadata constraints (like a price ceiling or a specific category) are highly critical, you can set $w_2 = 2.0$ and $w_1 = 0.5$. This ensures the metadata block dictates the geometry of the vector space more than the text chunk.
### Why Concatenation Works:
- **Preserves all information** from each embedding space
- **No parameter learning** required (simpler, more robust)
- **Linear separability**: Different dimensions handle different semantic aspects
- **Query-time flexibility**: Weighting happens during search, not storage
- **Scalable**: Works efficiently with vector databases
### The Trade-offs:
- According to research, there are more sophisticated methods, but they come with costs:
- **Simple concatenation** (Superlinked's approach):
	- ✅ Fast, no training needed
	- ✅ All information preserved
	- ✅ Query-time control via weighting
	- ❌ Treats all dimensions equally at storage time
	- ❌ No learned interactions between spaces
## Different Fusion Strategies
1. **Early Fusion** (concatenation) - Combine before processing
2. **Late Fusion** (weighted averaging) - Combine after separate processing  
3. **Attention-based Fusion** - Dynamic weighting based on context
4. **Bilinear Pooling** - Captures pairwise interactions
5. **Gated Fusion** - Selective information flow (LSTM/GRU-style)
