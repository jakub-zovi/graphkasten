---
tags:
  - personal
  - personal/pkm
created: 2026-04-04T19:00
modified: 2026-04-04T20:02
published:
sources:
  - "[Karpathy tweet 1](https://x.com/karpathy/status/2040470801506541998)"
  - "[Karpathy tweet 2](https://x.com/karpathy/status/2039805659525644595)"
  - "[llm-wiki.md gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)"
topics:
  - LLM Knowledge Bases
  - Organization Systems
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# LLM Knowledge Bases
-  Andrej Karpathy pattern for building personal knowledge bases maintained by LLMs
- Detailed spec: [[LLM Wiki]]
## Core Idea
- Most RAG systems re-derive knowledge from scratch on every query — no accumulation
- Instead: LLM **incrementally builds and maintains a persistent wiki** between you and raw sources
	- When a new source is added, LLM reads it, integrates it into existing wiki, updates cross-references, flags contradictions
	- Knowledge is compiled once and *kept current*, not re-derived on every query
- The wiki is a **persistent, compounding artifact** — richer with every source and every question asked
- You never write the wiki yourself — LLM writes and maintains all of it
	- Obsidian as the IDE; LLM as the programmer; wiki as the codebase
## Architecture
- **Raw sources** — immutable source documents (articles, papers, images); LLM reads but never modifies
- **The wiki** — LLM-generated markdown files; LLM owns this layer entirely
- **The schema** — config doc (e.g. CLAUDE.md) telling the LLM how the wiki is structured and what workflows to follow
## Operations
- **Ingest** — LLM processes a new source: summarizes, updates entity/concept pages, appends to log
- **Query** — LLM searches wiki pages, synthesizes answer; good answers are filed back as new wiki pages
- **Lint** — periodic health check: contradictions, orphan pages, stale claims, missing cross-references
## Indexing
- `index.md` — content-oriented catalog; LLM reads this first when answering queries
- `log.md` — append-only chronological record of ingests, queries, lint passes
## Use Cases
- Personal tracking (goals, health, self-improvement)
- Research deep-dives over weeks/months
- Reading a book chapter-by-chapter
- Business/team internal wikis fed by Slack, meetings, project docs
## Why It Works
- Humans abandon wikis because maintenance burden grows faster than value
- LLMs don't get bored, don't forget to update cross-references, can touch 15 files in one pass
- Related in spirit to [[Vannevar Bush's Memex]] (1945) — private, actively curated, associative trails
