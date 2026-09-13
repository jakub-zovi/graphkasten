---
tags:
  - personal
  - personal/pkm
created: 2026-03-10T00:00
modified:
published:
sources:
  - "[Obsidian Spaced Repetition](https://www.stephenmwangi.com/obsidian-spaced-repetition/)"
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
# Spaced Repetition Plugin
- Community plugin that brings a spaced repetition system (SRS) into Obsidian, allowing flashcard-based review of notes using an SM-2-based algorithm.
## Flashcard Syntax
- Single-line card: `Question::Answer`
- Multi-line card:
```
Question
?
Answer
```
- Cloze deletion: `==highlighted text==` or `**bolded text**`
## Review Modes
- **Flashcard review** — works through cards due today, rating each as Easy / Good / Hard
- **Note review** — reviews entire notes (not individual cards) on a schedule
## Usage in This Vault
- Flashcard notes live in `flashcards/` subfolders next to the source note
- The `#flashcards` tag marks a note as a flashcard deck for the plugin
- Review stats and next-due dates are stored in `.obsidian/plugins/obsidian-spaced-repetition/data.json`
