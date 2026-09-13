---
tags:
  - cs
  - cs/swe
created: 2026-05-20T10:00
modified: 2026-07-26T13:30
published:
sources:
  - "[tmux GitHub](https://github.com/tmux/tmux)"
  - "[tmux wiki](https://github.com/tmux/tmux/wiki)"
topics:
  - Terminal
  - Terminal Multiplexer
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
banner: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS6UvaSabITB1wYugPwwtnztFHbWFiSv8ECRLB0oVT9-KJxiJvrp-bgbUrL&s=10
banner-x: 47
banner-y: 50
---
# Tmux
- Terminal multiplexer that allows multiple terminal sessions to be accessed within a single window
- Sessions persist after disconnecting, allowing detach/reattach across SSH connections
## Concepts
- **Session**
	- Top-level container, persists in the background; can be detached and reattached
- **Window**
	- Like a tab inside a session; each window has its own working directory and processes
- **Pane**
	- A split inside a window (horizontal or vertical); each pane runs a separate shell
## Prefix Key
- Default prefix: `Ctrl+b` (commonly remapped to `Ctrl+a`)
- Most commands are issued by pressing the prefix, then a key
## Common Commands
- Sessions
	- `tmux new -s <name>`
		- Create a new named session
	- `tmux ls`
		- List sessions
	- `tmux attach -t <name>`
		- Attach to a session
	- `prefix + d`
		- Detach from current session
- Windows
	- `prefix + c`
		- Create new window
	- `prefix + n` / `prefix + p`
		- Next / previous window
	- `prefix + ,`
		- Rename window
- Panes
	- `prefix + %`
		- Split vertically
	- `prefix + "`
		- Split horizontally
	- `prefix + <arrow>`
		- Move between panes
	- `prefix + z`
		- Zoom / unzoom pane
	- `prefix + x`
		- Close pane
## Configuration
- Config file: `~/.tmux.conf`
- Plugin manager: [tpm](https://github.com/tmux-plugins/tpm)
- Popular plugins
	- `tmux-resurrect` — save and restore sessions across reboots
	- `tmux-continuum` — automatic save/restore on a timer
	- `tmux-yank` — system clipboard integration
