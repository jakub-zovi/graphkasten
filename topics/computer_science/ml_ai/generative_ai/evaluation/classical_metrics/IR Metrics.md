---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2025-11-01T17:59
modified: 2026-03-21T13:30
published:
sources:
  - "[Redefining Retrieval Evaluation in the Era of LLMs](https://arxiv.org/pdf/2510.21440)"
topics:
  - Evaluation
authors:
ai-assisted:
hidden:
public: true
---
# IR Metrics
- This note aggregates information about different approaches to use for evaluation of the information retrieval performed in order to find relevant context
- For more info about ranking metrics see Ranking Metrics
## Classical Metrics
- Mean Average Precision (MAP)
	- Averages precision across all recall levels and queries—captures both precision and ranking quality
- Mean Reciprocal Rank (MRR)
	- Focuses on how high the first relevant result appears in the ranking
- Normalized Discounted Cumulative Gain (nDCG)
	- Weighs the usefulness of each result by its position—higher-ranked relevant items count more
## RAG-tailored Metric
- Utility and Distraction-aware Cumulative Gain ([[UDCG]])
	- A metric using an LLM-oriented positional discount to directly optimize the correlation with the end-to-end answer accuracy
	- Paper: [Redefining Retrieval Evaluation in the Era of LLMs](https://arxiv.org/pdf/2510.21440)
## Metrics Comparison
- **Note the below table considers question answering task**
- Table 3: Spearman correlation between IR metrics and end-to-end RAG accuracy. Bold indicates best per model dataset combination. UDCG improvements are statistically significant (bootstrap, p < 0.05) ([Source](https://arxiv.org/pdf/2510.21440)).
![[rag_metrics_comparison.png|800]]
