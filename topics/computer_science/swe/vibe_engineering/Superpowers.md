---
tags:
  - cs
  - cs/swe
created: 2026-07-16T11:03
modified: 2026-09-05T11:36
published:
sources:
  - "[claude.com/plugins/superpowers](https://claude.com/plugins/superpowers)"
  - "[obra/superpowers](https://github.com/obra/superpowers)"
  - "[Superpowers: How I'm using coding agents in October 2025](https://blog.fsck.com/2025/10/09/superpowers/)"
topics:
  - Superpowers
  - Claude Code
  - Skills Framework
  - TDD
authors:
  - Jesse Vincent
ai-assisted: true
hidden:
public: true
---
# Superpowers
- By Jesse Vincent (obra), October 2025
- [obra/superpowers](https://github.com/obra/superpowers)
- Positioning: complete software development methodology for coding agents — strict pipeline, activates automatically when building starts
- Philosophy: deep upfront reasoning, then hands-off execution
## The Six-Stage Pipeline
1. **Brainstorming** — no jump to code; ask questions, explore alternatives, produce design doc
	> Teasing a spec out of the conversation.
2. **Worktree isolation** — git worktree per task; parallel tasks cannot clobber each other
3. **Writing plans** — design broken into 2–5 min tasks with exact file paths, complete code, verification steps
	> Clear enough for an enthusiastic junior engineer with poor taste, no judgement, no project context, and an aversion to testing to follow.
4. **Subagent-driven development** — fresh subagent per task; task reviewer checks spec compliance + code quality before closing; critical issues block progress
5. **Test-driven development** — strict RED-GREEN-REFACTOR; code before tests gets deleted
6. **Code review** — between tasks, review against plan, report by severity
## Key Distinguishers
- **Autonomy** — designed for hand-off of large work chunks, return to reviewed result
- **Subagent architecture** — main agent manages workers, does not implement itself
- **Composability** — skills are building blocks; drop brainstorming subagent into custom skill, use worktree isolation without TDD enforcement
## Trade-off
- Full pipeline feels heavy for one-line bug fixes
## Invocation
- `/brainstorming` — explore requirements and design before implementation
- `/execute-plan` — run batched implementation plans with review checkpoints
- Code-reviewer subagent evaluates against plans, coding standards, architectural principles
- Debugging methodology: root cause → pattern analysis → hypothesis testing → implementation
	- Safeguard: architectural review triggers after 3 failed fix attempts
- `writing-skills` module teaches authoring new skills via TDD applied to documentation
