---
tags:
  - cs
  - cs/swe
created: 2026-03-28T10:00
modified: 2026-06-06T15:03
published:
sources:
  - "[Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?](https://arxiv.org/abs/2602.11988)"
  - "[HN Discussion](https://news.ycombinator.com/item?id=47034087)"
topics:
  - Coding Agents
  - Context Files
  - Agent Evaluation
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Evaluating AGENTS.md
- Paper: [Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?](https://arxiv.org/abs/2602.11988)
	- Thibaud Gloaguen, Niels Mündler, Mark Müller, Veselin Raychev, Martin Vechev
	- 2026-02-12
- [HN Discussion](https://news.ycombinator.com/item?id=47034087)
## Core Question
> Do AGENTS.md-style repository-level context files actually improve AI coding agent performance?

## Key Findings
- **LLM-generated AGENTS.md** files slightly *decrease* task success (~3% decline vs no context)
- **Human-written AGENTS.md** files yield marginal improvement (~4% average) — but inconsistently across models
- Both types increase inference cost **>20%** due to larger context windows
- Evaluated on SWE-bench with Claude Sonnet 4.5, OpenAI Codex, Qwen3-Coder

## Why Context Files Can Hurt
- Encourage broader, less focused exploration patterns
- Overly broad requirements direct agents away from optimal solution paths
- Unnecessary content adds noise without signal

## Recommendations
- Context files should be **minimal and targeted** — not comprehensive docs
- Manual curation beats automated generation
- Include only non-obvious constraints the model cannot infer from code
- Related: [[Optimizing Coding Agent Rules]]

## Criticism (HN)
- Tested primarily on Python repos — generalizability limited
- Quality variance across files makes clean comparison difficult
- **Deterministic guardrails** (linters, pre-commit hooks, type checkers) are more reliable than prose instructions
- LLM nondeterminism makes measurements noisy

## Community Consensus
- **Progressive/nested AGENTS.md** per subdirectory outperforms monolithic project-level files
- **Structured/machine-readable formats** beat free-form markdown
- A 4% success improvement is practically meaningful in agentic workflows (failures compound)
- Real value comes from encoding domain-specific knowledge the model cannot infer (conventions, internal tooling, non-obvious constraints)
- Agent harnesses should auto-ingest standard files (README, CONTRIBUTING) rather than requiring a separate AGENTS.md
