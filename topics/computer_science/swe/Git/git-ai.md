---
tags:
  - cs
  - cs/swe
created: 2026-03-07T15:00
modified: 2026-07-26T13:34
published:
sources:
  - "[git-ai-project/git-ai](https://github.com/git-ai-project/git-ai)"
  - "[usegitai.com](https://usegitai.com)"
topics:
  - Git
  - AI Code Attribution
  - AI Code Tracking
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# git-ai
- [git-ai-project/git-ai](https://github.com/git-ai-project/git-ai)
	- 1.2k stars
> Git AI is an open source git extension that tracks AI-generated code in your repositories. Once installed, it automatically links every AI-written line to the agent, model, and transcripts that generated it — so you never lose the intent, requirements, and architecture decisions behind your code.
## Key Features
- **AI attribution on every commit** — shows a human vs AI bar with percentages on each `git commit`
- **`git-ai blame`** — drop-in replacement for `git blame` that shows the model, agent, and session behind every line
- **`git-ai stats`** — measures AI authorship across commits with JSON output (additions, deletions, accepted lines, model breakdown)
- **`/ask` skill** — lets you talk to the agent that originally wrote the code about its instructions, decisions, and intent
- **IDE plugins** — gutter decorations color-coded by agent session for VS Code, Cursor, Windsurf, Emacs
## Design Choices
- **No workflow changes** — just prompt and commit as normal
- **No detection** — does not guess AI code; supported agents report exactly which lines they wrote
- **Local-first** — works 100% offline, no login required
- **Git-native** — uses an [open standard](https://github.com/git-ai-project/git-ai/blob/main/specs/git_ai_standard_v3.0.0.md) for tracking via Git Notes
- **Transcripts stay out of Git** — Git Notes link to transcripts stored locally (SQLite), in Git AI Cloud, or self-hosted
## How It Works
1. Agents report written code via pre/post edit hooks
2. Each edit is stored as a checkpoint (small diff in `.git/ai/`)
3. On commit, checkpoints are processed into an Authorship Log attached to the commit via a Git Note
4. Attribution is preserved across rebases, merges, squashes, cherry-picks, and amends
## Install
```bash
curl -sSL https://usegitai.com/install.sh | bash
```
## Supported Agents
- Cursor
- Copilot
- Claude Code
- Codex
- Windsurf
- Antigravity
