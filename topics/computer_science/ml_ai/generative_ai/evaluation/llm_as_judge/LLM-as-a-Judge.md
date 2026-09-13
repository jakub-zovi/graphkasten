---
tags:
  - gen_ai
  - gen_ai/evaluation
created:
modified: 2026-09-08T09:51
published:
sources:
  - "[A Survey on LLM-as-a-Judge](https://arxiv.org/abs/2411.15594)"
  - "[Judge Arena: Benchmarking LLMs as Evaluators](https://huggingface.co/blog/arena-atla)"
topics:
  - Evaluation
  - LLM-as-a-Judge
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
---
# LLM-as-a-Judge
Using LLM to evaluate output of another LLM. Generally, the LLM-as-a-Judge follows structure shown in the [Fig. 2](llm_as_a_judge_pipeline.png).
 [A Survey on LLM-as-a-Judge](https://arxiv.org/abs/2411.15594):
<img height="300px" src="images/llm_as_a_judge_pipeline.png" />

## LLM Comparison For Judging
[Judge Arena: Benchmarking LLMs as Evaluators](https://huggingface.co/blog/arena-atla):
> LLM evaluations aim to capture human preferences, direct human feedback is also key to determining which AI judges are most helpful.
- [**Judge Arena**](https://huggingface.co/spaces/AtlaAI/judge-arena)
##  Improvement Strategies
[A Survey on LLM-as-a-Judge](https://arxiv.org/abs/2411.15594)
> When directly utilizing LLMs to conduct evaluation tasks—such as scoring, selection, pairwise comparison, or ranking—their inherent biases of LLMs like length bias, position bias, and concreteness bias will undermine evaluation outcomes.

> To boost the evaluation performance of LLM-as-a-judge: design strategy of evaluation prompts (in-context learning based), improvement strategy of LLMs’ evaluation capabilities (model-based), and optimization strategy of final evaluation results (post-processing based). See [Fig. 12](llm_as_a_judge_improvements.png).
<img height="300px" src="images/llm_as_a_judge_improvements.png" />
## Advanced Approaches
- [[Logprobs Scoring]] - [Retrieval confidence scoring to reduce hallucinations](https://cookbook.openai.com/examples/using_logprobs#2-retrieval-confidence-scoring-to-reduce-hallucinations)
- [[Panel of LLM evaluators (PoLL)]], 
	- multiple different LLMs evaluate the results.
## Evaluation Frameworks With Custom Metrics
- [[RAGAS]]
	- Library that provides tools to supercharge the evaluation of Large Language Model (LLM) applications.
- In GenAI Eng with DBX they defined this metric somehow through MlFLow using `mlflow.metrics.make_genai_metric`.
## Papers related to this approach:
- [[G-Eval]]
	- [G-EVAL: NLG Evaluation using GPT-4 with Better Human Alignment](https://arxiv.org/pdf/2303.16634)
- [[ChainPoll]] - [https://arxiv.org/pdf/2310.18344](https://arxiv.org/pdf/2310.18344)
- [[How to Correctly Report LLM-as-a-Judge Evaluations]]
- [[How to Calibrate LLM-as-Judge with Human Corrections]] ([Link](https://www.langchain.com/resources/llm-as-a-judge))
	- LangChain walkthrough of the Align Evals workflow: collect human corrections, build few-shot examples, track judge-human agreement over time
- [[Ask, Don't Judge - Binary Questions for Interpretable LLM Evaluation and Self-Improvement]]
	- BINEVAL — decomposes eval criteria into atomic binary questions, beats G-Eval/UniEval on QAGS factual consistency
- [[LLM-as-a-Judge for E-commerce Search Relevance]]
	- Aggregates papers showing LLM judges replacing human annotators for query-product relevance labeling in e-commerce/app-store search
- [[Automating Search Relevance Assessment at Scale with LLM-as-a-Judge]]
	- 2026-08-20 — Allegro engineering write-up on their Relevance Assessment Tool (RAT); Gemini 3.1 Flash Lite prompt design, dual-speed pipeline, and Gemma 4 26B local baseline matching cloud quality at ~60% cost
- [[PRECISE - Reducing Bias of LLM Evaluations]]
	- Extends Prediction-Powered Inference to combine ~100 human labels with ~10k LLM judgments for bias-corrected Precision@K estimation

