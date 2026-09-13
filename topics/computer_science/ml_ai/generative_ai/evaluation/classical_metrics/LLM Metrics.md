---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2024-10-19T15:22
modified: 2026-07-19T18:31
published:
sources:
  - "[AI Metrics that Matter](https://encord.com/blog/generative-ai-metrics/)"
topics:
  - Evaluation
  - LLM Metrics
authors:
ai-assisted:
hidden:
public: true
banner: https://images.ctfassets.net/otwaplf7zuwf/318a5bHCph0uVwng9NnYqJ/b483c114b5434e7a00bcf0a4c985edc4/image.png
banner-x: 50
banner-y: 29
---
# LLM Metrics
- List of metrics that are used to evaluate performance and outputs of LLM powered applications. 

## Metrics Categories
- [[Qualitative Metrics]]
	- Quantitative metrics are objective, numerical measures used to evaluate specific attributes of a system or process.
- [[LLM-as-a-Judge]] 
	- Use of LLM to evaluate LLM outputs
- [[Agent-as-a-Judge]]
	- [Agent-as-a-Judge: Evaluate Agents with Agents](https://arxiv.org/pdf/2410.10934)
		- 2024-10-16
		- 104 citations
	- [A Survey on Agent-as-a-Judge](https://arxiv.org/pdf/2601.05111)
		- 2026-01-08
		- 0 citations
- [[Grounded Fact Verification]]
	- Specialized classifiers (MiniCheck, FaithLens, NLI models) that score whether a claim is supported by a grounding document
- [[Rubrics based criteria scoring]]
	- https://docs.ragas.io/en/latest/concepts/metrics/available_metrics/general_purpose/#rubrics-based-criteria-scoring
- Other
	- [[Deterministic Assertion]] - check that the output does not contain specified substring
	- [[Cosine Similarity]] - between answer and expected answer
