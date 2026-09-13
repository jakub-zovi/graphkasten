---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-07-22T15:40
modified: 2026-08-02T10:15
published:
sources:
  - "[softmaxdata/engram](https://github.com/softmaxdata/engram)"
topics:
  - Context Database
  - Agent Memory
  - Concept Graph
authors:
  - Opus 4.7
ai-assisted: true
hidden: false
public: true
human-review: true
---
# Engram
- Brain-inspired, portable context database for AI agents that stores knowledge as structured "bullets" in a concept graph rather than raw text ([softmaxdata/engram](https://github.com/softmaxdata/engram)).
- MIT-licensed, maintained by softmaxdata
	- 19 stars
> Any AI system can access and build upon shared context regardless of which LLM or framework powers it ([softmaxdata/engram](https://github.com/softmaxdata/engram)).
## Core Idea
- Cross-model portability — context transfers between Claude, GPT, Gemini, and other LLMs unchanged
- Atomic knowledge units — each bullet is individually tracked with usage statistics
- Reconsolidation — helpful bullets strengthen over time, unhelpful ones fade (memory as a living, biologically-inspired substrate)
## Retrieval Features
- Core memory slot — always-loaded summary (≤512 tokens) preserved across context compaction
- Worked-example retrieval — attaches prior similar inputs together with their successful outputs near new queries
- Diversity ranking — Maximal Marginal Relevance prevents token budgets from filling with near-duplicates
## Architecture
- Separates read (materialization) from write (commit) so retrieval never blocks on ingestion
- Server-side "Reflector" LLM processes all raw input canonically, so bullets are consistent across clients
- Three storage tiers: active, archived, purged
## Components
- Reflector — canonical LLM for knowledge extraction
- Curator — decides what gets stored via deduplication and validity checks
- Delta engine — applies atomic mutations, never full rewrites
- Activity ledger — permanently retains raw text for future re-extraction
