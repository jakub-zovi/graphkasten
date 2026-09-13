---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-03-28T10:35
modified: 2026-08-01T11:15
published:
sources:
  - "[openai/codex](https://github.com/openai/codex)"
  - "[Codex Documentation](https://developers.openai.com/codex)"
topics:
  - Coding Agent
  - CLI Tooling
  - Agent Harness
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Codex (OpenAI CLI)
- Codex is a lightweight coding agent by OpenAI that runs locally in your terminal.
- Related: [[Agent Harness]]
## Setup
- Install with npm: `npm i -g @openai/codex`
- Install with Homebrew: `brew install --cask codex`
- Alternative install: download platform binaries from [GitHub Releases](https://github.com/openai/codex/releases)
## Authentication
- Run `codex` and choose sign-in with ChatGPT for supported plans.
- API key auth is also supported via the docs: [Auth guide](https://developers.openai.com/codex/auth#sign-in-with-an-api-key)
## Product surfaces
- CLI for local terminal usage
- IDE integration for VS Code, Cursor, and Windsurf
- Desktop app via `codex app`
- Codex Web at [chatgpt.com/codex](https://chatgpt.com/codex)
## Notes
- Repository license: Apache-2.0.
- For latest stars and releases, check GitHub directly.
