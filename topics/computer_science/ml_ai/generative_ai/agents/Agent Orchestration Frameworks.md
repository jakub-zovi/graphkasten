---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-05-20T10:00
modified: 2026-08-01T11:16
published:
sources:
  - "[paperclipai/paperclip](https://github.com/paperclipai/paperclip)"
  - "[openai/symphony](https://github.com/openai/symphony)"
topics:
  - Agent Orchestration
  - Multi-Agent Coordination
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
---
# Agent Orchestration Frameworks
- Orchestration frameworks sit one level above [[Agent Frameworks]] — they do not tell you how to build an individual agent, but how to coordinate many of them (often heterogeneous: Claude Code, Codex, custom) toward shared goals.
- Concerns typically handled at this layer
	- Task decomposition and assignment to agents
	- Isolated execution environments per run
	- Budget, cost, and approval controls
	- Persistent agent state across runs
	- Org structure, roles, and governance
	- Proof-of-completion and review workflows
## List
- [[Paperclip]]
	- [paperclipai/paperclip](https://github.com/paperclipai/paperclip)
		- 66.7k stars
		- 2026-03-02
	- "The open-source app everyone uses to manage agents at work"
	- Control plane for running organizations of agents — org charts, budgets, governance, task management across Claude Code, Codex, OpenClaw and others
	- Explicitly *not* an agent framework: "We don't tell you how to build agents. We tell you how to run a company made of them."
- [[Symphony]]
	- [openai/symphony](https://github.com/openai/symphony)
		- 24.3k stars
		- 2026-02-26
	- Turns project work into isolated, autonomous implementation runs
	- Shifts the operational model from *supervising* coding agents to *managing work* — agents complete tasks independently and return proof of completion