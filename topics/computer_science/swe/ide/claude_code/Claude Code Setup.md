---
tags:
  - cs
  - cs/swe
created: 2026-07-16T10:52
modified: 2026-09-01T12:15
published:
sources:
topics:
  - Claude Code
  - Setup
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Claude Code Setup
- This note aggregates information about setup for Claude Code
## Settings
- [[Claude Code Allow WebFetch All Domains]] ([Link](https://wow.pjh.is/journal/claude-code-allow-webfetch-all-domains))
	- 2026-03-02
	- Argues against default per-domain permission prompts due to permission fatigue; recommends allowing `WebFetch` globally and using hooks/sandboxing for real guardrails
- [[Claude Code Hidden Features]]
	- 2026-03-30
- [[Claude Code Memory]]
	- Built-in CLAUDE.md + auto-memory system, plus third-party tools like mempalace and claude-me
## Skills
- find-skills
- https://github.com/pbakaus/impeccable
	- For FE designs that do not look like AI slop
- task observer
## MCP Servers
- [[Context7]]
	- Context7 MCP Server -- Up-to-date code documentation for LLMs and AI code editors
	- [upstash/context7](https://github.com/upstash/context7)
## Orchestrators
- [[claude-flow]]
	- https://github.com/ruvnet/claude-flow
		- 13k stars
		- The leading agent orchestration platform for Claude. Deploy intelligent multi-agent swarms