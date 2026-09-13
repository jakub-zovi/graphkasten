---
tags:
  - gen_ai
  - gen_ai/evaluation
  - gen_ai/agents
created: 2026-01-23T11:25
modified: 2026-03-10T09:54
published:
sources:
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Agent Evaluation
This note aggregates information about how to evaluate different agents.
## Metrics
- used in [τ -bench](https://arxiv.org/pdf/2406.12045)
	- [[pass@k]]
		- measures the likelihood that an agent gets at least one correct solution in _k_ attempts
	- [[pass^k]]
		- measures the probability that _all k_ trials succeed. As _k_ increases, pass^k falls since demanding consistency across more trials is a harder bar to clear
## Process Supervision
- [[Agent Behavior Standard]]
	- Braintrust/Basis open standard for writing behavior specs — Markdown files under `.agents/behaviors/` describing intent, evidence, decision, execution, recovery for recurring agent conduct
- [[Behavior Specs for Supervising Long-Horizon Agents]]
	- 2026-07-29 — Braintrust announcement blog on process-supervision evals for hour-long agent trajectories, contrasting with outcome-only evals
## Sources
- [[Demystifying evals for AI agents]] ([Link](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents))
	- 2026-01-09
