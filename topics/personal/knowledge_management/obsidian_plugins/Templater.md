---
tags:
  - personal
  - personal/pkm
created: 2026-03-10T00:00
modified: 2026-03-10T16:39
published:
sources:
  - "[Templater Documentation](https://silentvoid13.github.io/Templater/)"
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
# Templater
- Templater is the most critical community plugin in this vault. It extends Obsidian's built-in template system with a full scripting engine — dynamic dates, prompts, user-defined functions, and folder-triggered auto-insertion.
## Syntax
- `<% tp.date.now("YYYY-MM-DD") %>` — insert formatted date
- `<% tp.file.title %>` — current file name
- `<% await tp.system.prompt("Enter value") %>` — interactive input prompt
- `<% tp.file.cursor() %>` — place cursor after template insertion
## Folder Templates
- Templater can automatically apply a template when a new note is created inside a specific folder (configured under *Templater → Folder Templates*)
## Templates in This Vault
- All templates live in `templates/definitions/` and use `<% %>` syntax
- Available templates: `Daily Template.md`, `Monthly Template.md`, `Generic Template.md`, `Finance Template.md`, `CS Template.md`, `ML AI Template.md`, `Work Template.md`, `Personal Template.md`
