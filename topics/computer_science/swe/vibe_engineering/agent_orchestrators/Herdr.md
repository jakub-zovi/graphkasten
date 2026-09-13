---
tags:
  - cs
  - cs/swe
created: 2026-08-08T10:00
modified: 2026-08-13T10:00
published: 2026-03-27
banner: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQutWKRR-bJdKPUM-KRCGroUfILdHR7vu02Zk-DxgIimw&s=10
sources:
  - "[herdrdev/herdr](https://github.com/herdrdev/herdr)"
  - "[herdr.dev](https://herdr.dev)"
  - "[cli-agent-orchestrator/docs/herdr.md](https://github.com/awslabs/cli-agent-orchestrator/blob/main/docs/herdr.md)"
  - "[Herdr Review — bitdoze](https://www.bitdoze.com/herdr-agent-multiplexer/)"
topics:
  - Agent Orchestration
  - Terminal Multiplexer
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
---
# Herdr
- "The runtime your coding agents live on." Rust-powered background daemon that hosts terminal sessions and the AI coding agents running inside them.
- Herdr **owns** the terminals — closing the lid, dropping the network, or rebooting the machine does not kill the agents.
## Highlights
- Single Rust binary, roughly 10 MB, no runtime dependencies.
- Persistent background sessions with workspaces, tabs, and panes — reattach from any terminal, including remote SSH.
- Unix socket API emits real-time status events (`working`, `idle`, `done`, `blocked`) so external tools can subscribe instead of polling.
- Multi-agent support: Claude Code, Codex, Cursor, opencode, Grok, and other CLIs launched as configured commands.
- Apache-2.0 license. No account, no cloud dependency.
## Mobile Companion
- [[Moshi]] — iOS/Android terminal recommended by Herdr for attaching to Herdr-owned sessions from a phone. Mosh transport survives network switches; Live Activities and Watch controls expose agent status on the go.
