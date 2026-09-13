---
tags:
  - personal
  - personal/pkm
created: 2026-03-10T00:00
modified: 2026-08-02T10:39
published:
sources:
  - "[Obsidian Git Documentation](https://publish.obsidian.md/git-doc)"
topics:
  - Note Taking
  - Obsidian
  - Community Plugins
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Obsidian Git Plugin
- Community plugin that integrates Git into Obsidian, enabling version-controlled backups of the vault without leaving the app.
## Workflow in This Vault
- Push is disabled (`disablePush: true`) — commits are created locally and pushed manually via terminal
- Diff view is set to split mode for side-by-side comparison
- Commits are milestone-based with descriptive messages (e.g. `"After ICE 2026 Backup"`) rather than automated periodic snapshots
## Key Commands (Command Palette)
- `Obsidian Git: Create backup` — stage all changes and commit
- `Obsidian Git: Open diff view` — review changes before committing
- `Obsidian Git: Open history view` — browse past commits
## Config Highlights
- `disablePush: true` — no auto-push to remote
- `diff.openMode: "split"` — side-by-side diff panel
## Resources
- [[Using Git To Sync Obsidian Notes on iOS with a-shell]] ([Link](https://cwoodall.com/posts/2022-01-02-obsidian-ios-sync/))
	- 2022-01-02 — Chris Woodall on syncing a vault on iOS via a-shell + Shortcuts (free alternative to Working Copy / iSH)
