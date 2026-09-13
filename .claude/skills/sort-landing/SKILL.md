---
tags:
created:
modified:
published:
sources:
topics:
authors:
ai-assisted:
hidden:
public:
name: sort-landing
description: Sorts notes out of the vault's `landing/` inbox into the appropriate cluster — moves each note to the right folder under `topics/`, normalizes its frontmatter, and links it from the relevant MOC/hub note so it is not orphaned. Use when the user asks to sort, organize, process, clean up, or file the landing folder / inbox.
---

# Sort The Landing Folder

Use this skill when the user asks to "sort", "organize", "process", "clean up", or "file" notes from the `landing/` folder — the **L** in the vault's LIFT structure, and the inbox every new or clipped note arrives in.

This skill is the **AI indexing stage of the Graphkasten review process**:

```
landing/  →  AI indexes (this skill)  →  Graph View  →  human review
```

Your job is the middle step: get each note out of the inbox, into the right place in `topics/`, with correct metadata and at least one real edge into the graph. The human then audits your work visually in Graph View — which only works if you produce meaningful links, not link spam.

## What This Skill Does

For every note currently in `landing/`:

1. **Move** it to the topically appropriate folder under `topics/`.
2. **Normalize the frontmatter** so it matches the conventions in `CLAUDE.md`.
3. **Link** it from the most relevant MOC / hub / parent note so it is reachable in the graph.

If `landing/` is empty, stop and tell the user.

## Step 1 — Inventory

List the contents of `landing/` and read each note's frontmatter + first ~30 lines of body to understand the topic. Web-clipper notes carry a `source:` URL and a `clippings` tag; book notes carry `book-view: true`, an ISBN, and a `coverUrl`.

```bash
ls -A landing/        # .gitignore is permanent furniture, not a note
```

## Step 2 — Decide Destination

For each note pick **(a)** a target folder, **(b)** the parent MOC/hub note to link from, **(c)** the right tags from the table in `CLAUDE.md`.

**The rule, which outranks any example below:**

- Sorted notes always land in **`topics/<cluster>/…`**, as deep as the subject warrants. That is the only graphed folder, and a sorted note must be graphed.
- **Never** sort a note into `fleeting/` (time-based notes only — daily, kanban) or `infra/` (Obsidian machinery only). If a landing note really is a dated journal entry or a kanban card, say so and ask rather than guessing.
- Prefer an existing deep folder over creating a new top-level one. Run `ls topics/<cluster>/` before inventing a path.

Discover the destination rather than recalling it — the clusters differ per vault:

```bash
ls topics/                                     # which clusters exist
ls -d topics/<cluster>/*/                      # its existing subfolders
grep -rl "<key term from the note>" topics/    # where sibling notes on this subject already live
```

Resolution order, most reliable first:

| Signal | Destination |
|---|---|
| A sibling note on the same subject exists | its folder; copy its `tags` |
| A MOC covers the subject | the folder that MOC sits in, or a subfolder of it |
| The cluster is right but no subfolder fits | create one subfolder under the cluster, and link from the cluster MOC |
| No cluster fits | leave it in `landing/` and tell the user — a new cluster is the `new-topic` skill's job, not this one |

Note types with a fixed rule regardless of subject:

- **Book notes** (`book-view: true`) → the cluster matching the book's subject; the `book-note` skill owns the frontmatter and the cover.
- **Dated journal entries / kanban cards** → these do **not** belong in `topics/`; say so and ask.

If you are not confident about placement, **ask the user** before moving (use AskUserQuestion). Never silently dump a note into a folder you are guessing at.

## Step 3 — Normalize Frontmatter

Rewrite the frontmatter so it follows the `CLAUDE.md` schema. Required fields and how to fill them:

- `tags:` — list, drawn from the `CLAUDE.md` tag table; **never** keep the literal `clippings` tag.
- `created:` — keep existing or copy from `modified` if blank. Never blank.
- `modified:` — leave (the Frontmatter Modified Date plugin updates it).
- `published:` — keep existing.
- `sources:` — list of markdown links in double quotes, e.g. `"[Title](https://...)"`. Move the web-clipper `source:` field into this list and strip tracking params (`?utm_source=...`, etc.). For book notes, link the parent series/author wiki-link (e.g. `"[[Incerto]]"`).
- `topics:` — 2–5 sub-themes of the last tag, in natural language (`Fama-French`, `Factor Model`, `Investor Psychology`).
- `ai-assisted: true` — always set this when the skill modifies the note.
- `author:` — keep existing; if it is a known person, convert plain text to a wiki-link (e.g. `"[[Aswath Damodaran]]"`).
- Remove web-clipper-only fields that don't belong in the schema: `title`, `description`. For book notes **keep** the book-specific fields (`subtitle`, `publisher`, `total`, `isbn`, `coverUrl`, `localCover`, `book-view`, `status`) — those are part of the Book Search template.

## Step 3b — Normalize Attachment Links

Web clippers and hand-written notes often leave folder paths on image and file links. Strip them: an attachment is always linked by **bare filename**, because Obsidian resolves attachment names vault-wide and a path silently breaks when the file moves.

```
![[stock_options_chat_8.png]]                                    # correct
![|500](GoldCPI.jpg)                                             # correct
localCover: "[[Ergodicity.jpg]]"                                 # correct
![[infra/data/images/work/stock_options_chat_8.png]]             # WRONG
[[infra/data/documents/work/job_hunt/Offer letter.pdf]]          # WRONG
```

Applies to every non-`.md` target — images, PDFs, recordings, archives — including those inside frontmatter fields such as `localCover`. Leave note wiki-links and remote URLs alone.

If a batch is large, find every offender in one pass instead of editing note by note:

```bash
grep -rnE '!?\[\[[^]]*/[^]]*\.(png|jpg|jpeg|gif|svg|pdf|m4a|mp4|zip)' --include='*.md' topics/
```

## Step 4 — Move The File

Prefer `git mv` when the file is tracked, plain `mv` when it is untracked. Do not delete then re-create — keep history.

**Never delete the `landing/` directory itself.** It is a permanent inbox whose `.gitignore` (`*` + `!.gitignore`) preserves the folder while ignoring its contents. Leave the folder and that `.gitignore` in place even after every note has moved out.

Note the consequence of that `.gitignore`: a note sitting in `landing/` is **untracked**, so it exists only on this machine. Moving it into `topics/` is what makes it real for git and for the user's other devices — which is exactly why a half-sorted inbox is worse than an unsorted one.

## Step 5 — Link From The Parent MOC

Open the chosen parent/MOC note and add a wiki-link to the new note under an appropriate `##` section. Match the surrounding style — usually a bulleted list with the wiki-link on the first level and a one-line description indented below:

```
- [[New Note Title]]
	- YYYY-MM-DD — short description of what the source covers
```

If a more specific concept note exists (e.g. `Fama and French Three Factor Model.md` rather than the top-level `Asset Pricing Models.md` MOC), link from the more specific note. Add new section headings (`## Explainers`, `## Setup Guides`, `## Books`, `## Companies`) only when no existing section fits.

Placeholder wiki-links (e.g. `[[Czechoslovak Group]]` even if that note does not yet exist) are encouraged per vault convention — they create graph edges for future expansion.

**Be stingy.** Every wiki-link is a graph edge, and the human reviews this work in Graph View. One good structural edge (hub → note) beats five incidental ones. For a link that is merely *mentioned* rather than structural, use an obsidian URL, which navigates without creating an edge.

## Step 6 — Verify

- `ls -A landing/` — confirm the originally listed notes are gone (only `.gitignore` should remain). Do not remove the folder.
- Spot-check 1–2 moved notes: frontmatter is well-formed, body unchanged, parent MOC contains the new link.
- the `grep` above must return nothing — no attachment link may carry a folder path.
- Optionally `obsidian unresolved counts verbose format=json` — check no *unexpected* new broken links appeared (intentional placeholder links are fine).

## Step 7 — Hand Back To Human Review

Report concisely: a small table of `note → new location → parent MOC`. Do not dump the full diff into the chat.

Then tell the user to review the result in **Graph View** — the audit step the whole Graphkasten process is built around. Point out anything you were unsure of, so they know where to look: notes you placed on a judgment call, placeholder links you created, and any note you could not confidently place.
