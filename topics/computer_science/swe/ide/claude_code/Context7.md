---
tags:
  - cs
  - cs/swe
created: 2026-07-16T11:07
modified: 2026-07-16T11:08
published:
sources:
topics:
  - Context7
  - MCP
  - Claude Code
  - Documentation Retrieval
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Context7
- Upstash Context7 MCP server for live docs lookup. Pull version-specific docs and code examples from source repos into LLM context.

Context7 is an MCP server that delivers up-to-date, version-specific documentation and code examples directly into your prompts. It solves a common problem with LLMs: outdated training data leading to hallucinated APIs and deprecated code patterns. Instead of relying on stale information, Context7 pulls current documentation straight from source repositories.

The plugin provides two main tools: **resolve-library-id** for matching library names to Context7-compatible identifiers, and **query-docs** for retrieving documentation for specific libraries. You can even target specific versions by mentioning them in your prompt.

**How to use:** Simply add "use context7" to any prompt where you need current documentation. For example: "Create a Next.js middleware that checks for a valid JWT in cookies. use context7" or "Configure a Cloudflare Worker script to cache JSON API responses. use context7". You can also specify exact libraries with "use library /supabase/supabase for API and docs".