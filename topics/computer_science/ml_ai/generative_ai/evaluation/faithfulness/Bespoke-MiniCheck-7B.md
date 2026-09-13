---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2026-06-08T10:00
modified: 2026-07-26T13:38
published: 2024-09-04
sources:
  - "[Bespoke-MiniCheck-7B HF card](https://huggingface.co/bespokelabs/Bespoke-MiniCheck-7B)"
  - "[MiniCheck: Efficient Fact-Checking of LLMs on Grounding Documents](https://arxiv.org/pdf/2404.10774)"
topics:
  - Grounded Fact Verification
  - Evaluation
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
---
# Bespoke-MiniCheck-7B
- Resources
	- Model: [bespokelabs/Bespoke-MiniCheck-7B](https://huggingface.co/bespokelabs/Bespoke-MiniCheck-7B)
	- Library: [Liyan06/MiniCheck](https://github.com/Liyan06/MiniCheck)
	- Paper: [MiniCheck: Efficient Fact-Checking of LLMs on Grounding Documents](https://arxiv.org/pdf/2404.10774)
		- EMNLP 2024
- SOTA on [[LLM-AggreFact]] at the time of release. From the model card:
> Llama-3.1-Bespoke-MiniCheck-7B is the SOTA fact-checking model despite its small size.
## Task
- Binary grounding classifier:
> The model takes as input a document and **a sentence** and determines whether the sentence is supported by the document: **MiniCheck-Model(document, claim) -> {0, 1}**
- Important constraint: multi-sentence claims must first be split via [Claim Decomposition](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fgenerative_ai%2Fevaluation%2Ffaithfulness%2FClaim%20Decomposition) and scored sentence-by-sentence.
## Model Details
- **Parameters:** 7B (BF16)
- **Base model:** `internlm/internlm2_5-7b-chat`
- **Synthetic data generator:** `meta-llama/Meta-Llama-3.1-405B-Instruct`
- **License:** CC BY-NC 4.0 (commercial license via `company@bespokelabs.ai`)
## Training Data
- **35K total examples**, mixing real NLI data with curated synthetic data:
	- 21K from ANLI (Adversarial NLI)
	- 7K synthetic "claim-to-document"
	- 7K synthetic "doc-to-claim"
- From the card:
> While scaling up the model (compared to what is in MiniCheck) helped, many improvements come from high-quality curation, thus establishing the superiority of Bespoke Labs's curation technology.
## Throughput
> Based on our test on a single A6000 (48 VRAM), Llama-3.1-Bespoke-MiniCheck-7B with vLLM and MiniCheck-Flan-T5-Large have throughputs > 500 docs/min.
- Cheap enough to use as an online metric in production, not just an offline eval.
## Sibling Models
- Smaller / cheaper variants from the same MiniCheck family - useful as latency-sensitive fallbacks:
	- `MiniCheck-Flan-T5-Large` (0.8B)
	- `MiniCheck-RoBERTa-Large` (0.4B)
	- `MiniCheck-DeBERTa-v3-Large` (0.4B)
