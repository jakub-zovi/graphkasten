---
tags:
  - cs
  - cs/swe
created: 2025-12-16T17:50
modified: 2025-12-16T17:52
published:
sources:
  - "[Simon Willison - JustHTML is a fascinating example of vibe engineering in action](https://simonwillison.net/2025/Dec/14/justhtml/)"
topics:
  - Vibe Engineering
authors:
ai-assisted:
hidden:
public: true
---
# JustHTML is a fascinating example of vibe engineering in action
I recently came across [JustHTML](https://github.com/EmilStenstrom/justhtml), a new Python library for parsing HTML released by Emil Stenström. It’s a very interesting piece of software, both as a useful library and as a case study in sophisticated AI-assisted programming.

#### First impressions of JustHTML [#](https://simonwillison.net/2025/Dec/14/justhtml/#first-impressions-of-justhtml)

I didn’t initially know that JustHTML had been written with AI assistance at all. The README caught my eye due to some attractive characteristics:

- It’s pure Python. I like libraries that are pure Python (no C extensions or similar) because it makes them easy to use in less conventional Python environments, including Pyodide.
- "Passes all 9,200+ tests in the official [html5lib-tests](https://github.com/html5lib/html5lib-tests) suite (used by browser vendors)"—this instantly caught my attention! HTML5 is a big, complicated but meticulously written specification.
- 100% test coverage. That’s not something you see every day.
- CSS selector queries as a feature. I built a Python library for this [many years ago](https://github.com/simonw/soupselect) and I’m always interested in seeing new implementations of that pattern.
- html5lib has been [inconsistently maintained](https://github.com/mozilla/bleach/issues/698) over the last few years, leaving me interested in potential alternatives.
- It’s only 3,000 lines of implementation code (and another ~11,000 of tests.)

I was out and about without a laptop so I decided to put JustHTML through its paces on my phone. I [prompted Claude Code for web](https://github.com/simonw/tools/pull/156#issue-3726212220) on my phone and had it build [this Pyodide-powered HTML tool](https://tools.simonwillison.net/justhtml) for trying it out:

![Screenshot of a web app interface titled "Playground Mode" with buttons labeled "CSS Selector Query" (purple, selected), "Pretty Print HTML", "Tree Structure", "Stream Events", "Extract Text", and "To Markdown" (all gray). Below is a text field labeled "CSS Selector:" containing "p" and a green "Run Query" button. An "Output" section with dark background shows 3 matches in a green badge and displays HTML code](https://static.simonwillison.net/static/2025/justhtml.jpeg)

This was enough for me to convince myself that the core functionality worked as advertised. It’s a neat piece of code!

#### Turns out it was almost all built by LLMs [#](https://simonwillison.net/2025/Dec/14/justhtml/#turns-out-it-was-almost-all-built-by-llms)

At this point I went looking for some more background information on the library and found Emil’s blog entry about it: [How I wrote JustHTML using coding agents](https://friendlybit.com/python/writing-justhtml-with-coding-agents/):

> Writing a full HTML5 parser is not a short one-shot problem. I have been working on this project for a couple of months on off-hours.
> 
> Tooling: I used plain VS Code with Github Copilot in Agent mode. I enabled automatic approval of all commands, and then added a blacklist of commands that I always wanted to approve manually. I wrote an [agent instruction](https://github.com/EmilStenstrom/justhtml/blob/main/.github/copilot-instructions.md) that told it to keep working, and don’t stop to ask questions. Worked well!

Emil used several different models—an advantage of working in VS Code Agent mode rather than a provider-locked coding agent like Claude Code or Codex CLI. Claude Sonnet 3.7, Gemini 3 Pro and Claude Opus all get a mention.

#### Vibe engineering, not vibe coding [#](https://simonwillison.net/2025/Dec/14/justhtml/#vibe-engineering-not-vibe-coding)

What’s most interesting about Emil’s 17 step account covering those several months of work is how much software engineering was involved, independent of typing out the actual code.

I wrote about [vibe engineering](https://simonwillison.net/2025/Oct/7/vibe-engineering/) a while ago as an alternative to vibe coding.

Vibe coding is when you have an LLM knock out code without any semblance of code review—great for prototypes and toy projects, definitely not an approach to use for serious libraries or production code.

I proposed “vibe engineering” as the grown up version of vibe coding, where expert programmers use coding agents in a professional and responsible way to produce high quality, reliable results.

You should absolutely read [Emil’s account](https://friendlybit.com/python/writing-justhtml-with-coding-agents/#the-journey) in full. A few highlights:

1. He hooked in the 9,200 test [html5lib-tests](https://github.com/html5lib/html5lib-tests) conformance suite almost from the start. There’s no better way to construct a new HTML5 parser than using the test suite that the browsers themselves use.
2. He picked the core API design himself—a TagHandler base class with handle_start() etc. methods—and told the model to implement that.
3. He added a comparative benchmark to track performance compared to existing libraries like html5lib, then experimented with a Rust optimization based on those initial numbers.
4. He threw the original code away and started from scratch as a rough port of Servo’s excellent [html5ever](https://github.com/servo/html5ever) Rust library.
5. He built a custom profiler and new benchmark and let Gemini 3 Pro loose on it, finally achieving micro-optimizations to beat the existing Pure Python libraries.
6. He used coverage to identify and remove unnecessary code.
7. He had his agent build a [custom fuzzer](https://github.com/EmilStenstrom/justhtml/blob/main/benchmarks/fuzz.py) to generate vast numbers of invalid HTML documents and harden the parser against them.

This represents a lot of sophisticated development practices, tapping into Emil’s deep experience as a software engineer. As described, this feels to me more like a lead architect role than a hands-on coder.

It perfectly fits what I was thinking about when I described **vibe engineering**.

Setting the coding agent up with the html5lib-tests suite is also a great example of [designing an agentic loop](https://simonwillison.net/2025/Sep/30/designing-agentic-loops/).

#### “The agent did the typing” [#](https://simonwillison.net/2025/Dec/14/justhtml/#-the-agent-did-the-typing-)

Emil concluded his article like this:

> JustHTML is about 3,000 lines of Python with 8,500+ tests passing. I couldn’t have written it this quickly without the agent.
> 
> But “quickly” doesn’t mean “without thinking.” I spent a lot of time reviewing code, making design decisions, and steering the agent in the right direction. The agent did the typing; I did the thinking.
> 
> That’s probably the right division of labor.

I couldn’t agree more. Coding agents replace the part of my job that involves typing the code into a computer. I find what’s left to be a much more valuable use of my time.