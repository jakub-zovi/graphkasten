---
tags:
  - cs
  - cs/swe
created: 2026-03-05T13:30
modified: 2026-07-16T11:09
published:
sources:
topics:
  - Vibe Engineering
authors:
ai-assisted:
hidden:
public: true
---
# Cursor Token Optimization
## How to optimise tokens 
* In Cursor user plan mode for complex changes. First use **PLAN** → review the PLAN and make changes if necessary → choose optimal LLM and then hit **BUILD**, so you don’t spend tokens on unwanted code changes.w
* See the Model Guidelines below.
* Some models tend to generate excessive documentation, which might not be necessary — address this in your prompt or in rules/commands.
* Make sure your Cursor workspace is indexed — you can verify and run indexing manually in **Settings → [[Indexing & Docs]]**.
* For documentation, prefer using [Context7](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fswe%2Fide%2Fclaude_code%2FContext7) MCP: https://upstash.com/blog/new-context7
* Sometimes manually changing a couple of lines in a file is more time- and cost-efficient than using the Agent.
* Be hyper-specific in your prompts. Specific requests = narrower context = fewer tokens.
* Use **@mentions** to target context.
* Close irrelevant open files. Cursor includes open files as automatic context. Close tabs you're not actively working on.
* Use **.cursorignore** aggressively. Exclude directories that should never be context.  
* Break large tasks into smaller chunks. Each focused task uses less context and is more token-efficient.
* Clear context between unrelated tasks. Start a new chat for unrelated topics instead of continuing in the same thread.
* Golden rule: **use common sense**.
## Resources
- [[TokenBurner - Cursor Cost Model Efficiency]]
	- https://www.tokenburner.dev/insights/cursor-model-cost-efficiency