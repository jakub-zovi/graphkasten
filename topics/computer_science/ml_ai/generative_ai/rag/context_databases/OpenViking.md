---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-07-22T15:40
modified: 2026-08-02T10:15
published:
sources:
  - "[volcengine/OpenViking](https://github.com/volcengine/OpenViking)"
topics:
  - Context Database
  - Agent Memory
  - Filesystem Retrieval
authors:
  - Opus 4.7
ai-assisted: true
hidden: false
public: true
human-review: true
---
# OpenViking
- Open-source context database for AI agents that organizes memories, resources, and skills as a virtual filesystem addressed via the `viking://` protocol ([volcengine/OpenViking](https://github.com/volcengine/OpenViking)).
- Maintained by Volcengine (ByteDance's cloud subsidiary)
	- 27.1k stars
> Rather than querying a black-box vector store, an agent navigates a deterministic `viking://` hierarchy of directories and files, each carrying its own abstraction layers ([volcengine/OpenViking](https://github.com/volcengine/OpenViking)).
## Core Idea
- Replaces opaque similarity queries with a browsable, addressable filesystem
- Directories hold resources, user memories, preferences, skills, and peer contexts
- Every path exposes deterministic, reproducible retrieval trajectories
## Tiered Content Loading
- L0 — abstract
- L1 — overview
- L2 — details
- Layers load on demand, keeping input tokens low without losing global structure
## Retrieval Behaviour
- Directory-recursive retrieval preserves surrounding context around a hit
- Trajectories are observable — every read is a traceable path, useful for debugging
- Session memory is automatically extracted into long-term storage between runs
## Components
- OpenViking Server — HTTP backend
- `ov` — CLI client
- VikingBot — agent framework
- OpenViking Helper — desktop console (macOS/Windows)
- Integrations for Claude Code, Codex, Cursor, and other coding agents
## Benchmarks
- 80–83% accuracy on user-memory tasks with OpenViking vs 24–57% without it (per repo README)
