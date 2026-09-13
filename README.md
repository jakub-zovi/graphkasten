# Graphkasten

[![Obsidian](https://img.shields.io/badge/Obsidian-%23483699.svg?style=for-the-badge&logo=obsidian&logoColor=white)](https://obsidian.md)

**Graphkasten** is an AI-native evolution of the Zettelkasten: graph-centric note-taking where connections matter as much as the notes themselves. Built for [Obsidian](https://obsidian.md), usable with any agentic system.

Most vaults treat Graph View as a gimmick. Here everything revolves around it — a **global graph** keeps the vault auditable, a **local graph** gives instant neighbourhood around any note. AI does the indexing; the graph makes human review cheap.

See it live: **[graphkasten.com](https://graphkasten.com/)** · [About](https://graphkasten.com/about/)

This repo ships a working vault — **462 notes** across computer science, finance, and personal knowledge management — so you can read the conventions at scale before adopting them.

## Three Components

### 1. Design Pattern — four primitives

**Folders (LIFT).** Graph filter scoped to one folder:

| Folder | Holds | Graphed? |
|---|---|---|
| `landing/` | inbox — every new or clipped note lands here first | no |
| `infra/` | plugins, templates, `.base` files, attachment mount | no |
| `fleeting/` | time-based notes: daily journal, kanban, scratchpads | no |
| `topics/` | durable knowledge, nested as deep as the subject warrants | **yes** |

**Links.** Wiki-links *are* the graph — reserve `[[wiki-link]]` for structural edges (MOC↔note, hub↔child). Everything else: plain text or an `obsidian://` URL (clickable, no edge). Placeholder links to unwritten notes are encouraged. Start from folder hierarchy, then rewire to match how you actually think.

**Tags.** Shallow on purpose — one level of nesting max (`gen_ai/agents`, never `gen_ai/agents/x`). Each tag has a colour, so the graph clusters by topic.

**Frontmatter.** One unified schema across the vault (declared in `types.json`), filled from Obsidian templates per note type.

### 2. Review Process

Medallion-inspired: **Inbox → AI indexes → Graph View → Human review → useful graph** with correct tags and links.

### 3. Insights

- **Global / local graph** — discover structure; review AI indexing; neighbourhood of any note
- **Bases** — alternate views (`Book View`, `Kanban`, `Not Public`)
- **Tag view** — parent/child topics, colour-coded clusters

Full conventions: `CLAUDE.md`.

## Getting Started

```bash
git clone <your-fork> my-vault
cd my-vault
```

Open in Obsidian, enable community plugins, restart. Then in [Claude Code](https://claude.com/claude-code):

```
/graphkasten-setup
```

Setup interviews you for domains, tags, and attachment storage, then rewires folders, MOCs, graph colours, `CLAUDE.md`, and the journal chain.

## What's In The Box

Agent skills in `.claude/skills/` (`AGENTS.md` → `CLAUDE.md` for everyone else):

| Skill | Does |
|---|---|
| `graphkasten-setup` | one-time onboarding: turns this template into your vault |
| `new-topic` | cluster — folder, MOC, root tag, colour group, registrations |
| `sort-landing` | files the inbox, normalizes frontmatter, links from a MOC |
| `obsidian-note-cluster` | 3-level hub/section/leaf hierarchy on a broad subject |
| `book-note` | metadata, cover download, write into the right cluster |
| `obsidian-base` | a `.base` file — saved, filtered database view |
| `spaced-repetition` | flashcards from a note |

Attachments live **outside** git — a cloud-synced folder mounted at `infra/data/{images,documents}`. Links use the **bare filename** (`![[diagram.svg]]`), never a path.

## Requirements

- Obsidian 1.12+ (Bases 1.9+; kanban Base view 1.10+)
- 21 community plugins, vendored in `.obsidian/plugins/`
- Theme: Prism
- Optional: Claude Code, for the skills

## Licence

[Apache License 2.0](LICENSE). Vault machinery (structure, skills, templates, configuration) is yours to reuse. Notes under `topics/` are one person's reading notes and carry their own sources — treat them as such.
