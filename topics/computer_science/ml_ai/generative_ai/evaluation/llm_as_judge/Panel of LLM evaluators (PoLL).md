---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2024-11-27T10:50
modified: 2026-02-21T10:20
published:
sources:
  - "[Replacing Judges with Juries: Evaluating LLM Generations with a Panel of Diverse Models](https://arxiv.org/pdf/2404.18796)"
topics:
  - Evaluation
  - LLM-as-a-Judge
  - Panel-of-Judges
authors:
ai-assisted:
hidden:
public: true
---
# Panel of LLM evaluators (PoLL)
Also called Panel-of-Judges, the idea is to use multiple diverse LLMs to evaluate the generated output. This stems from the fact that LMMs are biased to evaluate their own outputs with the higher score.
[Medium article](https://medium.com/@techsachin/replacing-judges-with-juries-llm-generation-evaluations-with-panel-of-llm-evaluators-d1e77dfb521e) summary of the original paper.

[Paper abstract:](https://arxiv.org/pdf/2404.18796)
> We propose instead to evaluate models using a Panel of LLm evaluators (PoLL). Across three distinct judge settings and spanning six different datasets, we find that using a PoLL composed of a larger number of smaller models outperforms a single large judge, exhibits less intra-model bias due to its composition of disjoint model families, and does so while being over seven times less expensive

> Figure 1: Top: Rankings of model performance change drastically depending on which LLM is used as the judge on KILT-NQ. Bottom: The Panel of LLm evaluators (PoLL) has the highest Cohen’s κ correlation with human judgements

<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*4ZuaN9t3sxOObSadL-E3FQ.png">