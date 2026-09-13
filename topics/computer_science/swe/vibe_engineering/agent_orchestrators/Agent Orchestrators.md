---
tags:
  - cs
  - cs/swe
created: 2026-08-08T10:00
modified: 2026-08-15T11:06
published:
sources:
  - "[andyrewlee/awesome-agent-orchestrators](https://github.com/andyrewlee/awesome-agent-orchestrators)"
  - "[Best Tools for Parallel AI Coding Agents (2026)](https://nimbalyst.com/blog/best-tools-for-running-parallel-ai-coding-agents/)"
topics:
  - Vibe Engineering
  - Agent Orchestration
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
---
# Agent Orchestrators
- Terminal-native tools that run multiple AI coding CLIs (Claude Code, Codex, opencode, Gemini, Aider, Cursor Agent, Copilot CLI, Cline…) in parallel, each isolated in its own git worktree and terminal session.
## List
- [[Herdr]]
	- [herdrdev/herdr](https://github.com/herdrdev/herdr)
		- 25.7k stars
		- 2026-03-27
	- Terminals live inside the daemon so agents survive reboot, network drop, and SSH detach. 
- [[Claude Squad]]
	- [smtg-ai/claude-squad](https://github.com/smtg-ai/claude-squad)
		- 8.3k stars
		- 2025-03-09
	- Go TUI over tmux + git worktrees. Manages many parallel coding agents from one screen. Original tool that popularized the pattern.
- [[Workmux]]
	- [raine/workmux](https://github.com/raine/workmux)
		- 2.1k stars
		- 2025-11-04
	- Rust, agent-agnostic. Glue layer between git worktrees and your existing multiplexer (tmux/zellij/kitty/WezTerm). Auto-detects backend from environment variables.
## Comparison
| Tool         | Isolation      | Persistence / reattach                 | Multi-agent CLIs                           | Type                 |
| ------------ | -------------- | -------------------------------------- | ------------------------------------------ | -------------------- |
| Herdr        | owns terminals | reboot-surviving, attach from anywhere | Claude Code, Codex, Cursor, opencode, Grok | Background runtime   |
| Claude Squad | git worktrees  | tmux session (dies on reboot)          | Claude Code, Codex, opencode, Aider        | TUI over tmux        |
| workmux      | git worktrees  | tmux / zellij / kitty / WezTerm        | agent-agnostic                             | Worktree↔window glue |
