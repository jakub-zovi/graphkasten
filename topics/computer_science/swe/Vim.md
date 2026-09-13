---
tags:
  - cs
  - cs/swe
created: 2026-05-20T10:00
modified: 2026-07-26T13:30
published:
sources:
  - "[Vim](https://www.vim.org/)"
  - "[Neovim](https://neovim.io/)"
topics:
  - Terminal
  - Text Editor
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
banner: https://media2.dev.to/dynamic/image/width=1600,height=900,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2b1dm3hiulonmzuhm2f4.png
banner-x: 54
banner-y: 14
banner-height: 580
---
# Vim
- Modal, keyboard-driven text editor originally created by Bram Moolenaar (1991)
- Designed for efficient editing via composable commands rather than mouse interaction
- Modern fork: [[Neovim]] — extensible, Lua-configured, with a more open development model
## Modes
- **Normal**
	- Default mode; keys are commands for navigation and manipulation
- **Insert**
	- Text entry; entered with `i`, `a`, `o`, etc.
- **Visual**
	- Selection mode; `v` (character), `V` (line), `Ctrl+v` (block)
- **Command-line**
	- Triggered by `:` for ex commands like `:w`, `:q`, `:s/old/new/g`
- **Replace**
	- Triggered by `R`; overwrites existing characters
## Core Concepts
- **Operators + motions**
	- Commands compose: `d` (delete) + `w` (word) = `dw`; `c` (change) + `i"` (inside quotes) = `ci"`
- **Text objects**
	- `iw` inner word, `aw` a word, `ip` paragraph, `i(` inside parens, etc.
- **Registers**
	- Named clipboards; `"ay` yanks into register `a`, `"ap` pastes from it
- **Marks**
	- `ma` sets mark `a`; `'a` jumps to its line
- **Macros**
	- `qa` records into register `a`, `q` stops, `@a` replays
## Essential Commands
- Navigation
	- `h j k l` — left, down, up, right
	- `w` / `b` — next / previous word
	- `gg` / `G` — top / bottom of file
	- `0` / `$` — start / end of line
	- `Ctrl+u` / `Ctrl+d` — half page up / down
- Editing
	- `dd` delete line, `yy` yank line, `p` paste
	- `u` undo, `Ctrl+r` redo
	- `.` repeat last change
- Search & replace
	- `/pattern` search forward, `?pattern` search backward
	- `n` / `N` next / previous match
	- `:%s/old/new/g` replace globally
- Files
	- `:w` write, `:q` quit, `:wq` / `ZZ` save and quit, `:q!` discard
## Configuration
- Vim: `~/.vimrc`
- Neovim: `~/.config/nvim/init.lua` (or `init.vim`)
- Popular plugin managers
	- `vim-plug`, `packer.nvim`, `lazy.nvim`
- Popular distributions
	- [LazyVim](https://www.lazyvim.org/), [AstroNvim](https://astronvim.com/), [NvChad](https://nvchad.com/)
