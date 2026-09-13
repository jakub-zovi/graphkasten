---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-07-14T23:04
modified: 2026-07-14T23:06
published:
sources:
topics:
  - Agentic Harness
  - Harness Optimization
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Harnesses Optimization
- This note aggregates information about optimizing harnesses
## Papers
- [[Meta-Harness]] ([Link](https://arxiv.org/abs/2603.28052))
	- 2026 — Stanford paper introducing the outer-loop harness-search framework: a coding-agent proposer reads prior code, scores, and traces from a filesystem to propose new harnesses; beats hand-designed ACE by 7.7 points on text classification and ranks #1 on TerminalBench-2 Haiku 4.5
	- [JoelNiklaus/harness-optimization](https://github.com/JoelNiklaus/harness-optimization)
- [[Self-Harness]]
	- 2026-06-14 — agent improves its own harness (prompts, tools, memory) via weakness mining → proposal → validation
- [[Autogenesis]] ([Link](https://arxiv.org/abs/2604.15034))
	- 2026-04-26 — two-layer self-evolving agent protocol with auditable lineage and rollback
- [[Red Queen Gödel Machine]] ([Link](https://nlp.elvissaravia.com/p/top-ai-papers-of-the-week-0b9))
	- 2026-07-05 — co-evolves agents and the evaluators that judge them to escape the stationary-evaluator plateau
- [[Don't Train the Model, Evolve the Harness]] ([Link](https://huggingface.co/spaces/joelniklaus/harness-optimization))
	- 2026-07-01 — Hugging Face applies Meta-Harness to DeepSeek-V4-Pro on Harvey's Legal Agent Benchmark: 0% → 5.0% all-pass, 63.4% → 80.1% criterion pass on held-out test, zero weights changed