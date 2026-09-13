---
tags:
  - cs
  - cs/swe
created: 2026-07-16T10:53
modified: 2026-07-16T10:54
published:
sources:
topics:
  - Claude Code
  - Anthropic
  - Product Updates
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Anthropic Claude Updates
- This note aggregates information about updates by Anthropic on Claude
## List
- [[An update on recent Claude Code quality reports]] ([Link](https://www.anthropic.com/engineering/april-23-postmortem))
	- 2026-04-23
	- Anthropic postmortem on three changes (reasoning-effort default, thinking-clearing bug, verbosity prompt) that degraded Claude Code output between March and April 2026
- [[Agent view in Claude Code]] ([Link](https://claude.com/blog/agent-view-in-claude-code))
	- 2026-05-11 — single place to manage parallel Claude Code sessions; peek/reply inline, `/bg` and `claude --bg` for backgrounding
- [[Keep Claude working toward a goal]] ([Link](https://code.claude.com/docs/en/goal))
	- `/goal` sets a completion condition; a fast model evaluates it after each turn and Claude keeps working until it holds. Requires v2.1.139+