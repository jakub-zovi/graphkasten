---
tags:
  - cs
  - cs/databases
created: 2025-04-14T15:57
modified: 2026-07-13T12:43
published:
sources:
topics:
  - Reciprocal Rank Fusion
  - Rank Fusion
  - Information Retrieval
authors:
ai-assisted:
hidden:
public: true
---
## Reciprocal Rank Fusion (RFF)
ChatGPT[^1]:
Reciprocal Rank Fusion (RRF) is an ensemble-based rank aggregation technique commonly used in information retrieval to combine the results from multiple ranking algorithms or search systems. 
### Basic RFF
In RRF, **each ranked list contributes to the final ranking based on the rank of each document in the list**. For a given document in each ranking, its reciprocal rank score is computed as:
$$
 \text{score}_{\text{RRF}} = \sum_{i=1}^{n} \frac{1}{k + \text{rank}_{i}}
$$
where:
-  $n$ is the number of ranked lists being combined,
-  $\text{rank}_{i}$ is the rank of a specific document in the  $i$-th ranked list,
-  $k$ is a small constant (usually 60 or another positive integer), used to dampen the impact of high ranks, ensuring that lower-ranked results do not contribute excessively to the final score.

The reciprocal rank score for each document is then used to produce a new, combined ranking, where documents with higher scores are ranked higher in the final list. This approach is effective because it takes into account the position of each document in the various rankings, allowing documents that consistently rank high to receive more weight.

### RFF with Weighting
In a weighted variant of RRF, each ranked list may be assigned a weight that reflects its relative importance or reliability. This allows more trusted or relevant lists to have a stronger impact on the final combined ranking. The modified formula with weights becomes:
$$
\text{score}_{\text{Weighted RRF}} = \sum_{i=1}^{n} w_{i} \cdot \frac{1}{k + \text{rank}_{i}}
$$
where:
-  $w_{i}$ is the weight assigned to the  $i$-th ranked list,
- Other variables are defined as above.

In this weighted version, lists with higher weights contribute more to the final rank score for each document. This technique is beneficial when some ranking methods are known to be more accurate or reliable, enabling the system to balance between multiple ranking approaches based on their respective strengths.

[^1]: Prompt: "Reciprocal rank fusion definition and with weighting definition."
