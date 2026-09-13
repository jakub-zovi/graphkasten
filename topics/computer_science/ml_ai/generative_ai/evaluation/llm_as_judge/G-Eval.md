---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2026-02-02T20:54
modified: 2026-02-21T10:19
published:
sources:
  - "[G-Eval Simply Explained: LLM-as-a-Judge for LLM Evaluation](https://www.confident-ai.com/blog/g-eval-the-definitive-guide)"
  - "[G-EVAL: NLG Evaluation using GPT-4 with Better Human Alignment](https://arxiv.org/pdf/2303.16634)"
topics:
  - Evaluation
  - LLM-as-a-Judge
  - G-Eval
authors:
ai-assisted:
hidden:
public: true
---
# G-Eval
- G-Eval is a **SOTA, research-backed framework** that uses LLM-as-a-judge to evaluate LLM outputs on any criteria using everyday language.
- G-Eval uses various techniques such as **chain-of-thought**, token weight summation, and form-filling paradigms to bypass pitfalls LLM judges are commonly vulnerable to.
- G-Eval can be further **optimized by introducing rubrics**, hardcoding criteria, and extended to a multi-turn use case.
- G-Eval can be used to **evaluate AI agents**, for both single-turn and multi-turn use cases.
- **DeepEval** allows anyone to implement G-Eval in under 5 lines of code ([docs here](https://deepeval.com/docs/metrics-llm-evals)).
## What is G-Eval?
G-Eval is a framework that uses LLM-as-a-judge with chain-of-thoughts (CoT) to evaluate LLM outputs based on **ANY** custom criteria. It leverages an automatic chain-of-thought (CoT) approach to decompose your criteria and evaluate LLM outputs through a three-step process:
1. **Evaluation Step Generation:** an LLM first transforms your natural language criterion into a structured list of evaluation steps.
2. **Judging:** these steps are then used by an LLM judge to assess your application’s output.
3. **Scoring:** the resulting judgments are weighted by their log-probabilities to produce a final G-Eval score.

![|500](https://images.ctfassets.net/otwaplf7zuwf/12StS90npeMOTt9xKLt6jg/4479f3f3ca0021931750c2223fd39f0f/image.png)


G-Eval was first introduced in the paper “NLG Evaluation using GPT-4 with Better Human Alignment”, and was originally developed as a superior alternative to traditional reference-based metrics like BLEU and ROUGE, which struggles with subjective and open-ended tasks that requires creativity, nuance, and an understanding of word semantics.
