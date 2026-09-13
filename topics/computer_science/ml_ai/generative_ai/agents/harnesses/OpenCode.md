---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-03-28T10:30
modified: 2026-08-01T11:15
published:
sources:
  - "[anomalyco/opencode](https://github.com/anomalyco/opencode)"
  - "[OpenCode Docs](https://opencode.ai/docs)"
topics:
  - Coding Agent
  - Agent Harness
  - Terminal Workflow
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# OpenCode
- OpenCode is an open-source AI coding agent focused on terminal-first development workflows.
- Related: [[Agent Harness]]
## Highlights
- Provider-agnostic and compatible with multiple model providers.
- Built-in agent modes:
	- `build` for full-access development tasks
	- `plan` for read-only analysis and code exploration
	- `general` subagent for complex multi-step searches and tasks
- Designed around a TUI and client/server architecture.
## Installation
- Script install: `curl -fsSL https://opencode.ai/install | bash`
- Package managers: `npm i -g opencode-ai@latest`, `brew install anomalyco/tap/opencode`, or `brew install opencode`
- Optional desktop app: [Releases](https://github.com/anomalyco/opencode/releases), [Download page](https://opencode.ai/download)
## Notes
- FAQ positioning highlights differences vs Claude Code: open source, provider flexibility, LSP support, and terminal-first UX.
- For latest stars and releases, check the GitHub repository directly.
