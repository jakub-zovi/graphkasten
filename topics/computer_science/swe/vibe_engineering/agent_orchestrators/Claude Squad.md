---
tags:
  - cs
  - cs/swe
created: 2026-08-08T10:00
modified: 2026-08-08T15:45
published: 2025-03-09
banner: https://opengraph.githubassets.com/1/smtg-ai/claude-squad
sources:
  - "[smtg-ai/claude-squad](https://github.com/smtg-ai/claude-squad)"
  - "[Claude Squad docs](https://smtg-ai.github.io/claude-squad/)"
  - "[Claude Squad Review — vibecodinghub](https://vibecodinghub.org/blog/claude-squad-review)"
  - "[Run Multiple AI Agents in Parallel Without the Mess — dev.to](https://dev.to/stevengonsalvez/claude-squad-run-multiple-ai-agents-in-parallel-without-the-mess-1hfl)"
topics:
  - Agent Orchestration
  - Terminal Multiplexer
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
---
# Claude Squad
- Go-based TUI that manages multiple AI terminal agents in parallel by combining tmux sessions with git worktrees. Popularized the "one screen, many coding agents" pattern.
## Highlights
- Each task launches in its own git worktree so agents cannot step on each other's changes.
- One TUI shows all running agents at once, with status and quick switching.
- Supports Claude Code, Codex, OpenCode, Aider, Amp, and Gemini through configurable launch commands.
- Written in Go, distributed as a single binary. AGPL-3.0.
- Persistence is bound to the tmux server — sessions die on machine reboot
