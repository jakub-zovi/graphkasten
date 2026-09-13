---
tags:
  - cs
  - cs/swe
created: 2025-09-22T11:07:00
modified: 2025-10-14T11:16
published:
sources:
  - "[How a senior engineer at a $140m+ startup actually codes with ai](https://www.reddit.com/r/vibecoding/comments/1nnl19h/how_a_senior_engineer_at_a_140m_startup_actually/)"
topics:
  - Vibe Coding
  - AI Workflow
  - Claude Code
  - Cursor
  - Code Review
authors:
ai-assisted:
hidden:
public: true
---
# How a senior engineer at a $140m+ startup actually codes with ai (95% 'vibe coding' but with system)
  I've met this senior dev in my coworking space yesterday who works at one of those well-funded startups (they raised like $140m+ recently). dude's been coding for 8+ years and mentioned he's basically "vibe coding" 95% of the time now but somehow shipping faster than ever.

got curious and asked him to walk me through his actual day-to-day workflow since there's always debate about whether this ai coding stuff actually works at real companies.

turns out he has this pretty specific but loose process. starts most features by just talking to claude code in terminal - describes what he wants to build and lets it generate rough structure. doesn't worry about it being perfect, just needs to get 70% there without getting stuck on implementation details.

then he switches to cursor for cleanup. says the key difference is he can watch the ai write code in real time instead of getting these massive code dumps to review later. catches weird hallucinations immediately.

but here's what blew my mind - he uses ai tools to review the ai-generated code. sounds redundant but apparently catches different types of issues. tried a bunch of different review tools but ended up sticking with coderabbit's vscode extension for quick checks, then pushes to pr where coderabbit github app does more detailed analysis.

testing pipeline is still totally human though. everything goes through staging with comprehensive test suites before production. ai helps write tests but deployment decisions stay with humans.

he mentioned they're shipping features about 40% faster now but not because ai is making architectural decisions - it's handling repetitive implementation while engineers focus on system design and code quality

said junior engineers who pick up this workflow are getting promoted faster because they can deliver senior-level output by focusing on design while ai handles the boring stuff

their startup has like 80 engineers and this is becoming pretty standard across teams.

anyone else seeing similar workflows at their companies? especially curious about the ai-reviewing-ai part since that seemed counterintuitive but apparently works