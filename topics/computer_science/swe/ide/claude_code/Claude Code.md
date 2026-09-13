---
tags:
  - cs
  - cs/swe
created: 2026-01-12T12:28
modified: 2026-07-19T18:04
published:
sources:
  - "[Claude Code: Best practices for agentic coding](https://www.anthropic.com/engineering/claude-code-best-practices)"
topics:
  - Vibe Coding
  - Claude Code
authors:
ai-assisted:
hidden:
public: true
banner: https://hieufromwaterloo.ca/post/claude-code-complete-guide/featured.jpg.png
banner-x: 64
banner-y: 60
banner-height: 370
---
# Claude Code
- [Claude Code: Best practices for agentic coding](https://www.anthropic.com/engineering/claude-code-best-practices)
> Claude Code is a command line tool for agentic coding. This post covers tips and tricks that have proven effective for using Claude Code across various codebases, languages, and environments.
## Topics
- [[Claude Code Setup]]
- [[Anthropic Claude Updates]]
## Resources
- [[Claude Code Source Leak]]
	- 2026-04-01
	- 512k+ lines across 2000+ files leaked; reveals Kairos daemon, AutoDream, Undercover mode, Buddy companion, UltraPlan, Voice Mode, Bridge mode, Coordinator multi-agent tool
- X
	- [Tips For Using Claude Code  From Its Creator Borish Cherny](https://x.com/bcherny/status/2017742741636321619?s=46&t=mKNRsrUkQkQ0weQxqYcCjw)
		- 2026-02-01
	- https://x.com/affaanmustafa/status/2012378465664745795
		- TLDR:
			- Quite nice summary from Anthropic Hackathon winner, i think everybody can get something out of it.
			- He mentions using mgrep instead of grep - Which seems to be good improvement (ignores .gitignore files, skips node_modules/, build dirs, etc..) - gdc_nas/gdc-ui / gdc_ruler speedup perhaps ?
			- More info about mgrep: https://github.com/mixedbread-ai/mgrep
			- Hookify tool which is essentially a strong guardrail - maybe if it would be hallucinating too much it would remind and say if it used the get_rules. Otherwise maybe not needed since it is already robust. (edited) 
- Blogs
	- [[Claude Code and What Comes Next]]
		- 2026-01-08
- Videos
	- [800+ hours of Learning Claude Code in 8 minutes](https://www.youtube.com/watch?v=Ffh9OeJ7yxw&t=360s)
		- 2025-10-27



