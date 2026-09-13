---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2026-06-08T10:00
modified: 2026-07-26T13:41
published:
sources:
  - "[LLM-AggreFact Leaderboard](https://llm-aggrefact.github.io/)"
topics:
  - Evaluation
  - LLM Metrics
  - Faithfulness
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
---
# Grounded Fact Verification
- A branch of research on **specialized models** that decide whether a **claim** is supported by a **grounding document/fact**. The task is essentially classification:
	- `supported` - the claim is entailed by the document
	- `not supported` / `orthogonal` - the document does not contain enough evidence
	- `contradicting` - the document directly refutes the claim
- Historically this was the domain of [[Natural Language Inference]] (NLI) models trained on SNLI / MNLI / ANLI. Modern variants are purpose-built grounding classifiers (often 0.4B–8B) that drastically outperform NLI baselines on long, noisy documents typical of RAG outputs.
- **Why this matters for production:** these models are small enough and fast enough (often hundreds of docs/min on a single GPU) to be used as an **online faithfulness metric**, not just an offline eval. Pair them with [[Claim Decomposition]] to score each atomic claim in an LLM answer against retrieved context.
## Topics
- [LLM-AggreFact](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fgenerative_ai%2Fevaluation%2Ffaithfulness%2FLLM-AggreFact)
	- Aggregated benchmark of 11 grounded-factuality datasets; the de-facto leaderboard for this task.
- [[Bespoke-MiniCheck-7B]]
	- SOTA 7B grounding classifier (`internlm2_5-7b-chat` base) trained on ANLI + synthetic data.
- [[FaithLens]]
	- ACL'26 8B model that outputs both a faithfulness label **and** a human-readable explanation; trained with cold-start SFT + rule-based RL.
- [[Natural Language Inference]]
	- Classical predecessor task (entailment / neutral / contradiction); models like DeBERTa-MNLI and ANLI baselines are still used as cheap fallbacks.
## Leaderboard
<iframe src="https://llm-aggrefact.github.io/" width="100%" height="600"></iframe>
## Production Use Case
- Because these classifiers return a single `{0, 1}` label plus a probability, they can be wired in as a **streaming faithfulness gate**:
	- Decompose model answer into atomic claims ([[Claim Decomposition]])
	- For each claim, run `MiniCheck(retrieved_doc, claim) -> prob`
	- Aggregate to a faithfulness score, block / flag responses below threshold
- Throughput reference: Bespoke-MiniCheck-7B with vLLM hits **>500 docs/min on a single A6000** ([Bespoke-MiniCheck-7B HF card](https://huggingface.co/bespokelabs/Bespoke-MiniCheck-7B)).
