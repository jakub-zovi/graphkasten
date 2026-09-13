---
tags:
  - cs
  - cs/swe
created: 2026-08-08T10:00
modified: 2026-08-08T15:46
published: 2025-11-04
banner: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRFS89guWYlvq_tdbVcM681VQLi7L2bRkbkmrwrSD6fZQ&s
sources:
  - "[raine/workmux](https://github.com/raine/workmux)"
  - "[workmux guide](https://workmux.raine.dev/guide/)"
  - "[Raine Virta — Introduction to workmux](https://raine.dev/blog/introduction-to-workmux/)"
topics:
  - Agent Orchestration
  - Git Worktrees
  - Terminal Multiplexer
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
---
# Workmux
- Rust CLI that glues git worktrees to multiplexer windows so a developer can fan out many parallel AI coding sessions with no manual bookkeeping.
- Agent-agnostic — brings no opinion about which coding CLI you run inside each worktree.
## Highlights
- One worktree ↔ one multiplexer window. Auto-detects the backend from environment variables: `$TMUX`, `$WEZTERM_PANE`, `$KITTY_WINDOW_ID`, `$ZELLIJ`.
- Supported multiplexers: tmux (primary), Zellij (experimental), kitty (experimental), WezTerm.
- Coordinator pattern: keep the main-branch agent as a planner that spawns worktree agents for individual tasks. Workmux surfaces per-window status in the multiplexer window list.
- Distributed as a Rust binary. MIT license.
