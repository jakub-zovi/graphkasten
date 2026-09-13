## What This Repository Is
- A personal **Obsidian knowledge vault** for organizing thoughts, career, finances, and life. It is not a software project — there is no build system, no tests, and no linting. The "codebase" is a collection of Markdown notes.
## Vault Structure
- The vault uses the **LIFT** four-folder system from [[Graphkasten]]. `topics/` is the only folder rendered in the graph view.

```
graphkasten/
├── Home.md                    # root entry point (not graphed — graph scopes to topics/)
├── landing/                   # INBOX — every new/clipped note lands here first. Contents gitignored.
├── infra/                     # Obsidian machinery. Never graphed, never knowledge.
│   ├── bases/                 # .base files (Book View, Kanban, Not Public)
│   ├── templates/             # Templater definitions + the web-clipper config
│   │   └── definitions/       # Templater templates, one per note type
│   └── data/                  # folderbridge mount of the external attachment store
│       ├── images/            # all images                (gitignored)
│       ├── documents/         # PDFs, audio, video, zips  (gitignored)
│       └── temp_data/         # staging for Obsidian UI drops
├── fleeting/                  # time-based notes, EXCLUDED from the graph view
│   ├── daily/journal/YYYY/YYYY-MM/YYYY-MM-DD.md   # daily → YYYY-MM.md → YYYY.md → Journal MOC.md
│   └── kanban/{personal,work}/
└── topics/                    # the ONLY graphed folder. All durable knowledge. Deep nesting allowed.
    ├── computer_science/      # ml_ai, swe, data_engineering, databases
    ├── finance/               # finance_theory, resources, tools
    └── personal/              # knowledge_management
```

- **Placing a note:** anything durable goes in `topics/<cluster>/…`, never left in `landing/`. Only dated/kanban notes go in `fleeting/`; only machinery goes in `infra/`.
- **`landing/` is gitignored** (`*` + `!.gitignore`). A note left there is invisible to git and to other devices — sorting it into `topics/` is what commits it.
- **Do not wiki-link across the `fleeting/` ↔ `topics/` boundary.** The far end is not rendered, so the edge is invisible — use an obsidian URL instead.
## Note Conventions
- User generally does not like unnecessary use of spaces in the notes.
- Prefer using bullet points when writing notes
	- Use tabs for sub bullet points
### Frontmatter Schema
- Every note must include this YAML frontmatter:

```yaml
---
tags:
  - <domain-tag>
created: 2026-02-28T10:00   # ISO timestamp; auto-set by Templater on creation
modified:                   # auto-updated by Frontmatter Modified Date plugin on save
published:                  # original date of publishing of the main source
sources:                    # List of markdown links/references enclosed in double quotes
topics:                     # List of topics represent sub-theme of the last tag, look at the neighboor nodes (through links) for parent topics if necessary
authors:                     # Original author if specified, if not put your model name here
ai-assisted: true
hidden: false
---
```
- You should always set `ai-assisted` to `true` when working or modifying content of a note. Do not set this to true if you are just moving the 
### Tagging System
- tag denote broad categories of the notes, tags can be nested with "/"
- only one level of the nesting is allowed — three legacy tags still break this (`cs/swe/observability`, `ml_ai/neural_nets/regularization`, `ml_ai/neural_nets/optimizers`); do not add more
- tags are also associated with a colour that is displayed in the graph view e

| Domain           | Tags |
| ---------------- | ---- |
| Computer Science | `cs`, `cs/swe`, `cs/databases`, `cs/data_eng` |
| ML & AI          | `ml_ai`, `ml_ai/neural_nets` |
| Generative AI    | `gen_ai`, `gen_ai/agents`, `gen_ai/rag`, `gen_ai/evaluation`, `gen_ai/models` |
| Finance          | `fin`, `fin/theory`, `fin/books`, `fin/tools` |
| Personal         | `personal`, `personal/pkm` |
| Daily journal    | `daily`, `daily/YYYY` |
| Kanban           | `work` |

- This table lists the tags **in use in this vault**. Adding a new root tag means adding a cluster —
  use the `new-topic` skill, which also registers the tag's colour group and the `Home.md` line.

- When multiple non-slash tags apply to a note, keep **only the most specific** — the last non-slash tag in the ordered list wins. Slash sub-tags are always retained. Example: `cs, ml_ai, gen_ai, gen_ai/agents` → `gen_ai, gen_ai/agents`.

### Structuring Of Resources & References
- User likes proper, concise structuring of resources or list of topics for a given note.
#### Example 1
- [[SimpleMem - Efficient Lifelong Memory for LLM Agents]]
	- Paper: [SimpleMem: Efficient Lifelong Memory for LLM Agents](https://arxiv.org/pdf/2601.02553)
		- 0 citations
		- 2026-01-26
	- Github: [aiming-lab/SimpleMem](https://github.com/aiming-lab/SimpleMem)
		- 2.9 stars 
- [[Memory Control for Long-Horizon Agents]]
	- Paper
		- 0 citations
		- 2026-01-15
#### Example 2
- Blogs
	- [A Complete Guide to Meta Prompting](https://www.prompthub.us/blog/a-complete-guide-to-meta-prompting#:~:text=)
		- 2025-08-12
		- Focuses heavily and explains really well automatic prompt optimization
- Papers
	- [Meta-prompting: Enhancing language models with task-agnostic scaffolding](https://arxiv.org/pdf/2401.12954)
		- 109 citations
		- 2024-01-23
		- Use of meta-prompting for orchestrating domain-specific expert models
### Full Note Example
```
---
tags:
  - cs
  - ml_ai
  - gen_ai
  - gen_ai/agents
created: 2026-02-03T13:28
modified: 2026-02-03T13:38
published: 2026-01-04
sources:
  - "[What is an agent harness?](https://parallel.ai/articles/what-is-an-agent-harness)"
topics:
  - Agent Design 
  - Agent Harness
authors: 
  - Opus 4.7
ai-assisted: true
hidden: false
---
# Agentic Harness
- [What is an agent harness?](https://parallel.ai/articles/what-is-an-agent-harness)
> In simple terms, an agent harness is the software infrastructure that wraps around a large language model (LLM) or AI agent, handling everything except the model itself.
## List
- OpenSource
	- [[OpenCode]]
		- [anomalyco/opencode](https://github.com/anomalyco/opencode)
			- 96.3k stars
	- [[Codex]]
		- [openai/codex](https://github.com/openai/codex)
			- 58.7k stars
```
### Naming Conventions
- **MOC (index) files:** broad term for the cluster or subcluster (e.g., `Computer Science.md`, `Generative AI.md`)
- **Daily notes:** `YYYY-MM-DD.md`
- **Monthly notes:** `YYYY-MM.md`
- **Yearly notes:** `YYYY.md`
- **Concept/asset notes:** natural language title (e.g., `Stellantis.md`, `Precision.md`)
### Linking
- Use `[[wiki-links]]` for internal navigation **within `topics/`**. MOC files are the primary navigation mechanism — when you place a new note in `topics/`, add a link to it from the relevant MOC. Do not MOC-link a note that is still in `landing/`; sort it first.
- **Be stingy with wiki-links — every one is a graph edge.** Reserve them for a note's primary structural connection (MOC↔note, hub↔child). Do **not** wiki-link a concept just because it is mentioned in prose, and do **not** re-link something already reachable one hop away (e.g. if a hub links a child, don't also link the child's own topics from the hub). For everything else use plain text or an obsidian URL (no graph edge).
- Every note **in `topics/`** must be reachable from another note — when creating one, decide up front which parent note will link it. Notes in `landing/` are unlinked by design (that is what marks them unsorted), and `fleeting/` notes link only to each other (daily → monthly → yearly → `Journal MOC.md`).
- It is good practice to create so called placeholder links that do not point to yet created note. This is useful for important topics of a note or if a note is listing some subtopics to be explored later. 
- There is also an option of using obsidian URL instead of wiki links (eg. [Computer Science](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2FComputer%20Science)), they do not create edges in the graph, making it more readable
- **Do not add a trailing `## Related Notes` / `## See Also` / `## Related` section that just lists wiki-links to neighboring concepts.** It pollutes the graph view with low-signal edges. Instead, weave related links inline where they are actually relevant (in the prose, in a `## Topics` list for child notes, or in `sources`). If a link does not have a natural inline home, that is usually a sign it is not worth adding.
### Subtopic Navigation
- When a note lists child/subtopic notes, use a flat `## Topics` list — **not** separate `##` headings per subtopic.
- Format: wiki-link on the top level, one-line description indented below.

```
## Topics
- [[Helm chart]]
	- Packaging format containing templates, values, and metadata
- [[Helm Commands]]
	- CLI for managing charts, releases, repos, and plugins
- [[Helm Templating]]
	- Go template engine with Sprig functions for rendering K8s manifests
```
## Text Citations
- User prefers proper citing in the notes. Sources on which a given note is based should be listed in the frontmatter "sources" section as shown above.
- Also, the text excerpts in the note should be cited if the whole note is not just a copy of some article that is cited in the frontmatter.
### Citing Example 1
- [RAPTOR PAPER](https://arxiv.org/pdf/2401.18059):
> We introduce the novel approach of recursively embedding, clustering, and summarizing chunks of text, constructing a tree with differing levels of summarization from the bottom up.
## Citing Example 2
- Prompt engineering is a relatively new discipline for developing and optimizing prompts to efficiently use language models (LMs) for a wide variety of applications and research topics ([Prompt Engineering Guide](https://www.promptingguide.ai/)).
## Latex Equations
When writing Latex equations use the following dollar sign syntax:
- Block equations: `$$...$$`
- Inline equations: `$...$` — **never** use `\$...\$` (escaped dollar signs break Obsidian rendering)
$$
 \text{score}_{\text{RRF}} = \sum_{i=1}^{n} \frac{1}{k + \text{rank}_{i}}
$$
where:
-  $n$ is the number of ranked lists being combined,
-  $\text{rank}_{i}$ is the rank of a specific document in the  $i$-th ranked list,
-  $k$ is a small constant (usually 60 or another positive integer), used to dampen the impact of high ranks, ensuring that lower-ranked results do not contribute excessively to the final score.
## Attachments (Images, PDFs, Recordings)
### Linking — Filename Only, Never A Path
- **Every link to a local attachment uses the bare filename, never a folder path.** Obsidian resolves attachment filenames across the whole vault, so the path adds nothing — and it breaks the moment the file is moved, because Obsidian's link-updater does not rewrite it.
- This applies to **both** link syntaxes and to **every** attachment type (`.png`, `.jpg`, `.svg`, `.pdf`, `.m4a`, `.mp4`, `.zip`, …), including attachment paths inside frontmatter fields such as `localCover`.

| | Correct | Wrong |
|---|---|---|
| Embed | `![[stock_options_chat_8.png]]` | `![[images/work/gooddata/organization/stock_options_chat_8.png]]` |
| Embed, sized | `![[diagram.svg\|700]]` | `![[images/cs/diagram.svg\|700]]` |
| Markdown image | `![\|500](GoldCPI.jpg)` | `![\|500](images/finance/aswath/GoldCPI.jpg)` |
| File link | `[[Offer letter.pdf]]` | `[[documents/work/job_hunt/Offer letter.pdf]]` |
| Frontmatter | `localCover: "[[Ergodicity.jpg]]"` | `localCover: "[[images/new_images/book_search/Ergodicity.jpg]]"` |

- Remote images keep their full URL — this rule is only about files stored in the vault's attachment store.
- Note wiki-links are unaffected: `[[Some Note]]` and `[[linshenkx/prompt-optimizer]]` (a note whose *title* contains a slash) stay as they are. The rule keys on the link target having a non-`.md` file extension.
- To audit the whole vault for links that still carry a folder path:

```bash
grep -rnE '!?\[\[[^]]*/[^]]*\.(png|jpg|jpeg|gif|svg|pdf|m4a|mp4|zip)' --include='*.md' .
```

  Strip the path down to the bare filename. Before renaming anything, check the basename is not already taken elsewhere in the store — links carry no path, so two files sharing a basename are indistinguishable.
### Displaying With Adjusted Width
![|500](https://media.beehiiv.com/cdn-cgi/image/fit=scale-down,format=auto,onerror=redirect,quality=80/uploads/asset/file/5d08c4ee-47df-4ffb-8f4f-ef05be5e01dd/CleanShot_2025-12-23_at_22.19.33_2x.png?t=1766508581)
### Storing Attachments
- The attachment store is **not in git**. It lives outside the vault (e.g. a cloud-synced folder) and is mounted in by the folderbridge plugin at `infra/data/images` and `infra/data/documents` (both gitignored). Configure the mount points in Settings → Folder Bridge; until you do, `infra/data/` is empty and attachment embeds will not resolve.
- Writing through the mount and writing to the real iCloud path are the same files. Prefer the mount so Obsidian indexes the file immediately.
- All new images go under `infra/data/images/` and nowhere else.
- All other new data files — PDFs, recordings, ZIPs, audio, video — go under `infra/data/documents/`.
- Subfolders inside the store are for *human* organization only. They never appear in a link.
- **Filenames must be unique across the whole store**, since links carry no path. Before adding a file, check the name is not already taken; if it is, pick a more specific name.
- When creating new notes based on some source, try to include relevant images from the source.
## Agent Skills
- Reusable procedures for this vault live in `.claude/skills/<name>/SKILL.md`, exposed to non-Claude agents at `.agents/skills/` (a symlink to that same directory — add a skill once and both paths see it).
- `sort-landing` — file everything sitting in `landing/` into `topics/`
- `new-topic` — add a top-level topic cluster (folder, MOC, tag, graph colour, registrations)
- `book-note` — create a book note and download its cover into the attachment store
- `obsidian-note-cluster` — build a multi-level note hierarchy on a broad subject
- `obsidian-base` — create a `.base` database view
- `spaced-repetition` — generate flashcards from an existing note
- `graphkasten-setup` — one-time onboarding for a fresh Graphkasten vault
## Searching
- When user asks you about a knowledge in the second brain only search the notes and not the commits.
## Obsidian CLI
The vault is accessible via the `obsidian` CLI. **Always prefer the  raw file tools and bash you are used to** . Only uses `obsidian` CLI for Obsidian specific operations like opening note so it is display to the user in obsidian, or getting information about links.
### Backlinks & Links
```bash
obsidian backlinks file="Note Title" format=json  # what links to this note
obsidian backlinks file="Note Title" counts       # with link counts
obsidian links file="Note Title"                  # outgoing links from a note
obsidian unresolved format=json                   # broken/placeholder wikilinks
obsidian orphans                                  # notes with no incoming links
obsidian deadends                                 # notes with no outgoing links
```
### Vault Health
```bash
obsidian orphans                                  # notes no other note links to
obsidian unresolved counts verbose format=json    # all broken wikilinks
```