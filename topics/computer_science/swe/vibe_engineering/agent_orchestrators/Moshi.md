---
tags:
  - cs
  - cs/swe
created: 2026-08-13T10:00
modified: 2026-08-16T11:04
published: 2026
sources:
  - "[getmoshi.app](https://getmoshi.app)"
  - "[getmoshi.app/compare](https://getmoshi.app/compare)"
topics:
  - Mobile Terminal
  - iOS SSH Client
  - Agent Orchestration
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
---
# Moshi
- Native iOS/iPadOS (and Android) terminal for driving AI coding agents on a remote machine. Recommended by [[Herdr]] as its mobile companion.
- Direct SSH / Mosh / ET into your own Mac, Linux, WSL, or VPS — no relay servers, no cloud account.
- Positions itself as "the phone-first terminal built for driving Claude Code."
## Highlights
- Mosh protocol keeps sessions alive across network switches, sleep, and app kills.
- Multiplexer-aware: first-class pickers, gestures, and deep integration for **tmux**, **Zellij**, and **[[Herdr]]**.
- Agent-first UX: structured approval inbox, diff viewer in terminal header, webhook alerts, voice-to-terminal (Parakeet, Whisper, Apple on-device).
- iOS-native affordances: Live Activities, Dynamic Island, Apple Watch controls, Face ID for SSH keys, image paste for screenshot prompts, in-app browser preview for local dev servers.
- Hardware keyboard shortcuts on iPad (⌘K nav, ⌘O, ⌘1–9), OSC 52 remote clipboard, CJK input.
- Tailscale one-tap for reaching machines across a tailnet.
- Free to start, no account, no trial timer. Paid tier for extras.
	- 4.8★ over 750+ App Store reviews.
## Herdr Integration
- Herdr owns the terminal sessions on the remote host so agents survive reboot and detach; Moshi is the mobile front-end that attaches to those sessions with Mosh resilience, Live Activities, and the agent approval flow.
- Together: laptop closes, phone opens, same running Claude Code / Codex / Cursor / opencode / Grok session, no reconnect ceremony.
