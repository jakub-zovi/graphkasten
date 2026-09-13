---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-04-25T00:00
modified: 2026-08-01T11:10
published: 2025-07-05
sources:
  - "[🥇Top AI Papers of the Week (April 13 - April 19)](https://nlp.elvissaravia.com/p/top-ai-papers-of-the-week-717)"
topics:
  - Agent Evaluation
  - Agent Benchmarks
  - Production Agents
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# AlphaEval

![|500](https://substackcdn.com/image/fetch/$s_!vS7D!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F655c258e-96c9-40fa-8e4c-934901545aea_635x331.png)

- Agent evaluations are drifting away from production reality
- Most benchmarks use clean tasks, well-specified requirements, deterministic metrics, and retrospective curation
- Production work is messier: implicit constraints, fragmented multimodal inputs, undeclared domain knowledge, long-horizon deliverables, and expert judgment that evolves over time
- AlphaEval is a production-grounded benchmark evaluating agents as complete products rather than model APIs

## Key Properties
- **Seven companies, six O*NET domains:** 94 tasks sourced from seven companies deploying AI agents in core business workflows across six O*NET domains
	- Tasks preserve production complexity rather than stripping it away
	- Materially different distribution from prior coding-centric evaluations
- **Products, not model APIs:** evaluates commercial agent products (e.g. Claude Code, Codex) end to end, not the underlying models in isolation
	- Measures the full agent experience that users actually pay for — tool use, orchestration, and UI behaviors
- **Six production-specific failure modes:**
	- Cascade dependencies
	- Subjective judgment collapse
	- Information retrieval failures
	- Cross-section inconsistency
	- Constraint misinterpretation
	- Format compliance
	- These remain invisible to coding benchmarks
- **Multi-paradigm evaluation:** combines LLM-as-a-Judge, reference-driven metrics, formal verification, rubric-based assessment, automated UI testing, and domain-specific checks
	- Key contribution: requirement-to-benchmark framework that turns production requirements into executable evals

## Results
- Best configuration (Claude Code with Opus 4.6) scores only 64.41/100
	- Exposes a substantial research-to-production gap
