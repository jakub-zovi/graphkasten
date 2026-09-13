---
tags:
  - cs
  - cs/swe
created: 2026-04-14T00:00
modified: 2026-08-01T10:54
published:
sources:
  - "[Claude Code Memory - Official Docs](https://code.claude.com/docs/en/memory)"
  - "[Adding Persistent Memory to Claude Code with claude-mem](https://dev.to/kanta13jp1/adding-persistent-memory-to-claude-code-with-claude-mem-plus-a-diy-lightweight-alternative-4gha)"
  - "[The Architecture of Persistent Memory for Claude Code](https://dev.to/suede/the-architecture-of-persistent-memory-for-claude-code-17d)"
topics:
  - Claude Code
  - Memory
authors:
  - claude-sonnet-4-6
ai-assisted: true
hidden:
public: true
human-review: true
---
# Claude Code Memory
- Claude Code has two complementary built-in memory mechanisms for persisting context across sessions
## Default Memory System
### CLAUDE.md (User-written)
- Plain markdown files loaded into every session's context window at startup
- Supports `@path/to/file` imports to pull in other files
- `<!-- HTML comments -->` are stripped before injection (save tokens for maintainer notes)
- Best kept under 200 lines per file; use `.claude/rules/` for modular, path-scoped rules
- Four scopes (most specific wins):
	- **Managed policy** (`/Library/Application Support/ClaudeCode/CLAUDE.md` on macOS) — org-wide, IT-managed, cannot be excluded
	- **Project** (`./CLAUDE.md` or `./.claude/CLAUDE.md`) — shared via source control
	- **User** (`~/.claude/CLAUDE.md`) — personal, applies to all projects
	- **Local** (`./CLAUDE.local.md`) — personal + project-specific, gitignored
### Auto Memory (Claude-written)
- Requires Claude Code v2.1.59+, enabled by default
- Claude autonomously decides what to save: build commands, debugging insights, code style preferences, architecture notes
- Stored at `~/.claude/projects/<project>/memory/MEMORY.md`
	- Shared per git repo across worktrees
- Only the first 200 lines / 25KB of `MEMORY.md` is loaded at session start; detailed notes go into separate topic files loaded on demand
- Fully editable plain markdown; manage with `/memory` command inside a session
- Machine-local only — not synced to cloud
## Third-Party Tools
- [[mempalace]]
	- [milla-jovovich/mempalace](https://github.com/milla-jovovich/mempalace)
		- 45.1k stars
		- Open-source AI memory system inspired by the memory palace technique
		- Organizes memories into a hierarchical structure: Wings > Rooms > Halls > Tunnels > Closets > Drawers (mapped to people, projects, topics, verbatim text)
		- Works via MCP with Claude, ChatGPT, Cursor, and Gemini
		- Runs 100% locally — no API calls, no cloud
		- Claims 96.6% recall on LongMemEval benchmarks (raw mode)
- [[Unified Agentic Memory Across Harnesses Using Hooks]] ([Link](https://towardsdatascience.com/unified-agentic-memory-across-harnesses-using-hooks/))
	- 2026-05-08 — Tomaz Bratanic builds a shared Neo4j memory layer plugged into Claude Code, Codex, and Cursor via hooks (passive, deterministic logging instead of agent-initiated MCP writes)
- [[claude-mem]]
	- [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)
		- 53.9k stars
		- Claude Code plugin that automatically captures everything Claude does during coding sessions, compresses it with AI, and injects relevant context back into future sessions
		- Records tool usage, generates AI-compressed summaries stored in SQLite + Chroma vector DB (hybrid semantic search)
		- 3-layer progressive memory retrieval system (~10x token savings vs full retrieval)
		- Real-time web dashboard at `localhost:37777`
		- Supports Claude Code, Gemini CLI, and OpenClaw gateways
		- Install via `npx claude-mem install`
