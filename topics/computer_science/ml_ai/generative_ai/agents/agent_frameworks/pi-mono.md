---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-04-26T20:37
modified: 2026-07-26T13:50
published:
sources:
  - "[badlogic/pi-mono](https://github.com/badlogic/pi-mono)"
topics:
  - Agent Harness
  - Coding Agent
  - LLM API
authors:
  - claude-sonnet-4-6
ai-assisted: true
hidden:
public: true
human-review: true
---
# pi-mono
- [badlogic/pi-mono](https://github.com/badlogic/pi-mono)
	- 31.1k stars
	- Monorepo by Mario Zechner containing an opinionated, minimal AI agent toolkit
	- Philosophy: build only what's needed — no MCP, no built-in todos, no plan mode, no sub-agents, no background bash
	- Runs on Windows, Linux, macOS (Node.js runtime)
## Videos
- [Video 1](https://www.youtube.com/watch?v=RjfbvDXpFls)
- [Video 2](https://www.youtube.com/watch?v=fdbXNWkpPMY)
## Packages
- [pi-ai](https://github.com/badlogic/pi-mono/tree/main/packages/ai)
	- Unified LLM API with multi-provider support (Anthropic, OpenAI, Google, xAI, Groq, Cerebras, OpenRouter, any OpenAI-compatible endpoint)
	- Streaming, tool calling with TypeBox schemas, thinking/reasoning support
	- Cross-provider context handoffs, token and cost tracking
	- Works in the browser (Anthropic and xAI support CORS)
- [pi-agent-core](https://github.com/badlogic/pi-mono/tree/main/packages/agent)
	- Agent loop: tool execution, validation, event streaming
	- `Agent` class: state management, message queuing, attachment handling, transport abstraction
- [pi-tui](https://github.com/badlogic/pi-mono/tree/main/packages/tui)
	- Minimal terminal UI framework with differential rendering
	- Synchronized output (`CSI ?2026h/l`) for flicker-free updates
	- Components: editors with autocomplete, markdown rendering
	- Works well in Ghostty / iTerm2; some flicker in VS Code terminal
- [pi-coding-agent](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)
	- CLI coding agent wiring all the above together
	- Session management (continue, resume, branching), custom slash commands, OAuth for Claude Pro/Max
	- Minimal system prompt (~1000 tokens total), minimal toolset (read, write, edit, bash)
	- YOLO mode by default — no permission prompts, no safety rails
	- HTML session export, headless JSON streaming / RPC mode
## Related
- [[What I learned building an opinionated and minimal coding agent]] ([Link](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/))
	- Author's blog post detailing design decisions, lessons learned, and benchmark results
- [[Building Pi With Pi]] ([Link](https://lucumr.pocoo.org/2026/5/24/pi-oss/))
	- 2026-05-24 — Armin Ronacher on dogfooding Pi: how clanker-generated issues and over-engineered fixes change the maintainer's role
