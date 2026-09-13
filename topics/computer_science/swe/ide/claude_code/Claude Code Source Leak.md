---
tags:
  - cs
  - cs/swe
created: 2026-04-03T00:00
modified: 2026-08-01T10:54
published:
sources:
  - "[Here's what that Claude Code source leak reveals about Anthropic's plans](https://arstechnica.com/ai/2026/04/heres-what-that-claude-code-source-leak-reveals-about-anthropics-plans/)"
topics:
  - Claude Code
  - Vibe Coding
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Claude Code Source Leak
- [Here's what that Claude Code source leak reveals about Anthropic's plans](https://arstechnica.com/ai/2026/04/heres-what-that-claude-code-source-leak-reveals-about-anthropics-plans/)
	- Kyle Orland — Ars Technica
	- 2026-04-01
> Yesterday's surprise leak of the source code for Anthropic's Claude Code revealed a lot about the vibe-coding scaffolding the company has built around its proprietary Claude model. But observers digging through over 512,000 lines of code across more than 2,000 files have also discovered references to disabled, hidden, or inactive features that provide a peek into the potential roadmap for future features.
## Planned / Hidden Features
- **[[Kairos]]** — persistent background daemon
	- Operates even when the Claude Code terminal window is closed
	- Uses periodic `<tick>` prompts to review whether new actions are needed
	- `PROACTIVE` flag for surfacing things the user hasn't asked for but needs to see
	- File-based memory system for persistent operation across sessions
	- Goal: "have a complete picture of who the user is, how they'd like to collaborate with you, what behaviors to avoid or repeat, and the context behind the work the user gives you"
- **[[AutoDream]]** — memory consolidation system
	- Triggers when user goes idle or manually ends a session
	- Tells Claude Code it is "performing a dream — a reflective pass over your memory files"
	- Scans day's transcripts for "new information worth persisting"
	- Consolidates memories, avoids near-duplicates and contradictions
	- Prunes memories that are overly verbose or outdated
	- Watches for "existing memories that drifted"
- **Undercover mode** — for Anthropic employees contributing to public open source repos
	- Hides that commits are made by an AI agent
	- Protects "internal model codenames, project names, or other Anthropic-internal information"
	- Commits must never include the phrase "Claude Code" or mention AI
	- No `Co-Authored-By` lines or any other attribution
	- Controversial in open source circles
- **Buddy** — Clippy-like companion widget
	- Sits beside the user's input box, occasionally comments in a speech bubble
	- 18 randomized "species" (blob, axolotl, etc.) as 5×12 ASCII art animations with tiny hats
	- Planned teaser window: April 1–7; full launch: May 2026
- **UltraPlan** — Opus-level extended planning
	- Drafts an advanced plan the user can edit and approve
	- Runs for 10–30 minutes at a time
- **Voice Mode** — chat directly to Claude Code via voice
- **Bridge mode** — expands on Anthropic Dispatch
	- Remote Claude Code sessions fully controllable from a browser or mobile device
- **[[Coordinator]]** — multi-agent orchestration
	- Spawns and orchestrates software engineering tasks across multiple workers
	- Parallel processes communicating via WebSockets
