---
tags:
  - cs
  - cs/swe
created: 2026-04-10T00:00
modified: 2026-08-01T10:53
published:
sources:
  - "[Thread by @bcherny - Hidden and under-utilized features](https://x.com/bcherny/status/2038454360418787764)"
topics:
  - Claude Code
  - Vibe Coding
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Claude Code Hidden Features
- [Thread by @bcherny - Hidden and under-utilized features](https://x.com/bcherny/status/2038454360418787764)
	- 2026-03-30
## Features
- **Mobile app**
	- Available for iOS/Android via Claude app > Code tab
	- Convenient for making changes without opening a laptop
- **Session teleportation** (`--teleport` / `/teleport` / `/remote-control`)
	- `claude --teleport` or `/teleport` — continue a cloud session on local machine
	- `/remote-control` — control a locally running session from phone/web
- **[[/loop and /schedule]]**
	- Schedule Claude to run automatically at a set interval, for up to a week
	- Example: `/loop 5m /babysit` — auto-address code review, auto-rebase
- **[[Hooks]]**
	- Deterministically run logic as part of the agent lifecycle
	- `SessionStart` — dynamically load context each time Claude starts
	- `PreToolUse` — log every bash command the model runs
	- Route permission prompts to external channels (e.g. WhatsApp)
- **Cowork Dispatch**
	- Secure remote control for Claude Desktop app
	- Can use MCPs, browser, and manage files/Slack/email when away from computer
- **Chrome extension** (frontend work)
	- Give Claude a way to verify its output — Claude will iterate until result is great
	- Analogy: like asking an engineer to build a website — they need to be able to see it
