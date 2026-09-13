---
tags:
  - gen_ai
  - gen_ai/rag
created: 2024-11-27T11:35
modified: 2026-07-19T18:20
published:
sources:
  - "[RULERAG: RULE-GUIDED RETRIEVAL-AUGMENTED GENERATION WITH LANGUAGE MODELS FOR QUESTION ANSWERING](https://arxiv.org/pdf/2410.22353)"
topics:
  - RuleRAG
  - Symbolic Rules
  - In-Context Learning
  - Rule-Guided Retrieval
authors:
ai-assisted:
hidden:
public: true
---
# RuleRAG
- [RuleRAG Paper](https://arxiv.org/pdf/2410.22353)
> **Rule-Guided Retrieval-Augmented Generation** with LMs, which explicitly introduces [[Symbolic Rules]] as demonstrations for in-context learning (RuleRAG-ICL) to guide retrievers to retrieve logically related documents in the directions of rules and uniformly guide generators to generate answers attributed by the guidance of the same set of rules. Moreover, the combination of queries and rules can be further used as supervised fine-tuning data to update retrievers and generators (RuleRAG-FT) to achieve better rule-based instruction following capability, leading to retrieve more supportive results and generate more acceptable answers.
- RuleRAG implementation [Github implementation](https://github.com/chenzhongwu20/RuleRAG_ICL_FT).