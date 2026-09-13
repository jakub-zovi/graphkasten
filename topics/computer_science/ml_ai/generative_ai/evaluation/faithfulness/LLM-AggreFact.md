---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2026-06-08T10:00
modified: 2026-07-26T13:42
published: 2024-04-16
sources:
  - "[LLM-AggreFact Leaderboard](https://llm-aggrefact.github.io/)"
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
# LLM-AggreFact
- Resources
	- Leaderboard: [llm-aggrefact.github.io](https://llm-aggrefact.github.io/)
	- Paper: [MiniCheck: Efficient Fact-Checking of LLMs on Grounding Documents](https://arxiv.org/pdf/2404.10774)
		- EMNLP 2024
	- GitHub: [Liyan06/MiniCheck](https://github.com/Liyan06/MiniCheck)
- From the leaderboard page:
> A fact-checking benchmark that aggregates **11** of the most up-to-date publicly available datasets on grounded factuality (i.e., hallucination) evaluation.
## Composition
- 11 grounded-factuality datasets, **~29K test samples**, all with human-annotated labels:
	- `AggreFact-CNN`, `AggreFact-XSum` - summarization factuality
	- `TofuEval-MediaS`, `TofuEval-MeetB` - dialogue/meeting summarization
	- `WiCE` - claim verification over Wikipedia
	- `Reveal` - reasoning chain verification
	- `ClaimVerify` - search-augmented response verification
	- `FactCheck-GPT` - factuality of ChatGPT responses
	- `ExpertQA` - expert-domain QA
	- `Lfqa` - long-form QA
	- `RAGTruth` - RAG-specific hallucination labels
- Input format is uniform across all datasets: `(document, claim) -> {0, 1}` where `1` = claim is supported by document.
## Leaderboard (top entries)
- Selected snapshot - see live board for current ranking:

| Model                | Size | Avg  |
| -------------------- | ---- | ---- |
| Bespoke-MiniCheck-7B | 7B   | 77.4 |
| Claude 3.5 Sonnet    | -    | 77.2 |
| Granite Guardian 3.3 | 8B   | 76.5 |

- Model sizes on the board range from **0.4B to 405B**, mixing dedicated fact-checkers (MiniCheck family, Granite Guardian) with general-purpose frontier LLMs (Claude, GPT, Llama).
- **Key takeaway:** a well-trained 7B specialized model is on par with or above the best frontier LLMs at this task, at a fraction of the inference cost.
## Embedded Leaderboard
<iframe src="https://llm-aggrefact.github.io/" width="100%" height="700"></iframe>
