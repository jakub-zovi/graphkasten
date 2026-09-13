---
tags:
  - cs
  - cs/swe
created: 2025-10-12T16:27
modified: 2026-02-23T12:25
published:
sources:
  - "[Introducing Plan Mode](https://cursor.com/blog/plan-mode)"
topics:
  - Vibe Engineering
  - Cursor
authors:
ai-assisted:
hidden:
public: true
---
# Introducing Plan Mode
> Oct 7, 2025 by Jai Smith

Cursor can now create plans, research your codebase, and run longer agents.

Plan mode gives the model new tools to create and update plans, as well as an interactive editor to modify plans inline. Most new features at Cursor now begin with Agent writing a plan. We’ve seen this significantly improve the code generated.

When you prompt Agent to create a plan, Cursor researches your codebase to find relevant files, review docs, and ask clarifying questions. When you’re happy with the plan, it creates a Markdown file with file paths and code references. You can edit the plan directly, including adding or removing to-dos.

### [How to use Plan Mode](https://cursor.com/blog/plan-mode#how-to-use-plan-mode)

- Start planning by pressing Shift + Tab in the agent input.
- Answer clarifying questions on your requirements for the best output quality.
- Review or edit the detailed plan, then build directly from your plan when ready.
- Optionally, save the plan as a Markdown file in your repository for future reference.

Cursor will also suggest plan mode automatically when you describe complex tasks.

Try Plan Mode in our latest release.

![Plan Mode in Cursor](https://cdn.sanity.io/images/2hv88549/production/01eeafec9d6c61426f2fee520aba42e2df0da508-1739x1124.png?auto=format)