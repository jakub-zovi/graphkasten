---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-04-05T14:00
modified: 2026-07-26T13:57
published:
sources:
  - "[Making Sparse Neural IR Models More Effective](https://arxiv.org/pdf/2205.04733)"
  - "[Splade_PP_en_v1 HuggingFace](https://huggingface.co/prithivida/Splade_PP_en_v1)"
  - "[SparseEmbed](https://storage.googleapis.com/gweb-research2023-media/pubtools/pdf/79f16d3b3b948706d191a7fe6dd02abe516f5564.pdf)"
topics:
  - Sparse Retrieval
  - Neural IR
authors:
  - claude-sonnet-4-6
ai-assisted: true
hidden:
public: true
human-review: true
---
# SPLADE
- **SPLADE** (Sparse Lexical and Expansion Model) is a transformer-based sparse retrieval model that outputs vocabulary-weighted sparse vectors — effectively a "semantic BM25"
- Addresses the vocabulary mismatch problem of traditional lexical search (BM25) while keeping the efficiency and interpretability of sparse representations

## Resources
- Papers
	- [Making Sparse Neural IR Models More Effective](https://arxiv.org/pdf/2205.04733)
		- 2022-05-10
		- Introduces SPLADE++ with distillation, hard negatives, co-condenser init; systematic ablation of what makes SPLADE effective
	- [SparseEmbed](https://storage.googleapis.com/gweb-research2023-media/pubtools/pdf/79f16d3b3b948706d191a7fe6dd02abe516f5564.pdf)
		- Google; extends SPLADE-style sparse encoding with contextual dense embeddings per token
	- [[Rescaling MLM-Head for Neural Sparse Retrieval]]
		- 2026-06-19 — dividing the MLM-head matrix by a constant at init fixes the scale mismatch that makes strong encoders (ModernBERT, Ettin) underperform BERT in SPLADE
- Models
	- [naver/splade-cocondenser-ensembledistil](https://huggingface.co/naver/splade-cocondenser-ensembledistil) — official SPLADE++ checkpoint
	- [prithivida/Splade_PP_en_v1](https://huggingface.co/prithivida/Splade_PP_en_v1) — industry-optimized variant
## How It Works
- Uses a Masked Language Model (MLM) head (e.g. BERT) to project dense token representations into vocabulary-space scores
- For each input token, the model assigns weights to vocabulary terms — enabling **term expansion** (matching semantically related terms not present in the original text)
- Final sparse vector: aggregation (max pooling) of per-token vocabulary distributions → most dimensions are zero
- Example output for a query:
	- `[('stress', 2.36), ('glass', 2.15), ('thermal', 2.06), ('pan', 1.83), ('glasses', 1.67), ('break', 1.47)]`
- Stored in an inverted index and retrieved efficiently like BM25
## Architecture
![](https://raw.githubusercontent.com/jakub-zovi/advanced_ai_driven_search/main/images/splade.png)

## Variants
| Variant | Notes | Doc tokens | Query tokens |
| -------------------- | -------------------------------------------- | ---------- | ------------ |
| SPLADE v1 | Original | low budget | low budget |
| SPLADE v2 | Higher token budget, most expressive | ~234 | ~234 |
| SPLADE++ | State-of-the-art; co-condenser initialization | 256 | 256 |
| SPLADE_PP_en_v1 | Industry-optimized, ~10% fewer tokens than SPLADE++ | 128 | 24 |
## Training
- Trained on MS-MARCO with hard-negative mining
- Loss includes a lambda-weighted FLOPS regularizer ($\lambda_Q$, $\lambda_D$) to control sparsity:
	- Lower $\lambda$ → more tokens, higher FLOPS, better effectiveness
	- Higher $\lambda$ → fewer tokens, lower FLOPS
- SPLADE++ uses co-condenser initialization for improved in-domain and zero-shot performance
- Knowledge distillation from a cross-encoder teacher improves effectiveness further
