---
name: graphkasten-setup
description: One-time onboarding that turns a fresh Graphkasten template vault into the user's own — interviews for their domains, tags and attachment storage, creates the clusters, assigns graph colours, strips the template's identity, and regenerates CLAUDE.md. Use when someone is setting up Graphkasten from scratch in a new vault.
---

# Set Up A Graphkasten Vault

Runs **once**, inside a fresh clone of the Graphkasten template vault, and personalizes it.

> **Boundary.** `graphkasten-setup` establishes the initial cluster set. `new-topic` runs forever
> after, one cluster at a time. If the user already has a vault they have been writing in and just
> wants one more cluster, that is `new-topic` — say so rather than running this.

The template is a stripped copy of someone else's vault, so it arrives carrying that vault's
identity: its name in every `obsidian://` URL, its git remote, its machine id in the folderbridge
config, its tags in the sibling skills. **Removing that identity is most of this job.** A cluster
the user never created is cosmetic; a git remote pointing at a stranger's repo is not.

## Phase 0: Preflight, And Close Obsidian For The Whole Run

```bash
ls -d landing infra fleeting topics    # the four LIFT folders must all be present
ls topics/                             # whatever the template shipped — see Phase 3
test -f .graphkasten && echo "ALREADY SET UP — stop and ask"
basename "$PWD"                        # the vault name; goes in every obsidian:// URL
```

There is no template marker file to check. The one thing that must stop the run is `.graphkasten`,
which a previous setup writes on completion — running twice would overwrite config the user has
since edited by hand. If it exists, show its contents and ask before doing anything.

Whatever `topics/` contains is not a reason to refuse. The template ships with real note clusters,
and deciding what happens to them is Phase 3's job, not a precondition.

**Then tell the user to quit Obsidian and leave it closed until Phase 9.**

```bash
pgrep -x Obsidian && echo "RUNNING — ask the user to quit before continuing"
```

Three reasons, all load-bearing:
- Every plugin serialises its in-memory settings on unload, so any `.obsidian/**/*.json` you write
  while Obsidian runs is discarded when the user quits. This is not just `graph.json`.
- `alwaysUpdateLinks` is inert while Obsidian is closed, so **every file you move, you must rewrite
  the wiki-links for yourself.** Nothing else will.
- `.obsidian/types.json` must declare the property types *before* any note is created. Obsidian
  infers a property's type from first use — if a note appears first, `created`/`modified`/
  `published` become text, and every Base that sorts on them mis-sorts silently, forever.

Derive the author name from `git config user.name` and confirm it in one line, then fill the empty
`authors:` field in every `infra/templates/definitions/*.md`.

## Phase 1: Interview

Ask all three in one `AskUserQuestion` batch. Nothing is written before this completes, so an
abandoned interview leaves the vault untouched.

**Q1 — Domains and root tags.** *"Which areas will you actually take notes on? These become your
top-level folders, your root tags, and your graph colours — pick areas you'll still care about in a
year, not this month's project."*

Then per domain confirm: **cluster name** (title case; names the folder and the MOC), **root tag**
(short, lowercase, `snake_case`, no slash — it gets typed forever), and **sub-tags** (propose 2–4
real candidates, multi-select, "none for now" is fine, **exactly one level of nesting**).

Hold the band at **3–6 clusters**. Fewer than 3 and the graph has no topology to show; more than 6
and the hues stop reading as distinct. Push back rather than silently accepting nine.

**Q2 — Attachment storage.** *"Where do your images, PDFs and recordings live?"* Attachments are
linked by bare filename either way — this decides where files sit, not how links are written.

| | **(a) In the vault** — `infra/data/` | **(b) Mounted in** — folderbridge |
|---|---|---|
| Store | `infra/data/{images,documents}` | an external dir (iCloud/Dropbox/…) |
| Synced by | git, with the notes | that service; never enters git |
| `.gitignore` | **drop** the `images/*`+`documents/*` lines, keep `temp_data/*` | keep all three |
| folderbridge | `mountPoints: []`, fresh `deviceId` | two mounts, fresh ids — see Phase 5 |
| Tradeoff | simple, everything works, binaries live in git history forever | repo stays text-only, but the Obsidian UI cannot move files into a mount |

**Q3 — Extra templates.** The template ships `Generic` and `Daily`. Ask which of **Monthly**,
**Book**, **Kanban**, or **one per domain** to generate.

Default **Monthly** in: `Daily Template.md` carries `moc: "[[YYYY-MM]]"`, so without a monthly note
every daily note dangles. If the user declines Book/Kanban, also remove the Bases that read them
(`Book View.base`, `Kanban.base`) and prune the matching keys from `types.json`.

## Phase 2: Scrub The Template's Identity

Answer-independent. Do this before creating anything, so later phases build on a clean base.

**Repository.** The template ships the source vault's remote, and `obsidian-git` ships enabled with
`disablePush: false` — one "Commit and sync" click pushes the user's private notes at a stranger's
repository. Show them the remote and offer both fixes:

```bash
git remote -v                       # template ships someone else's origin
git remote remove origin            # minimum
rm -rf .git && git init             # also drops the template's commit history
```

**Config carrying the source vault:**

| File | Action |
|---|---|
| `.obsidian/workspace.json`, `workspaces.json` | **delete** — open tabs and `lastOpenFiles` from the source vault, many pre-LIFT. Obsidian regenerates them. |
| `.obsidian/bookmarks.json` | **empty it.** It holds a "Global Graph" bookmark with its *own* 53-entry `colorGroups` and a stale `search`. Colour `graph.json` all you like — the user clicks their bookmark and gets the old colours. |
| `.obsidian/community-plugins.json` | drop entries with no folder in `.obsidian/plugins/` (the template ships 25 listed, 21 present) — otherwise first launch is a stack of "Failed to load plugin" notices. |
| `.obsidian/appearance.json` | `cssTheme` names a theme that is gitignored and never ships; `enabledCssSnippets` lists a snippet that does not exist. Clear both unless the template actually ships them. |
| `.obsidian/app.json` | drop source-vault `userIgnoreFilters`; **keep `.claude/`**. Keep `newFileLocation: "folder"` + `newFileFolderPath: "landing"` — that pair is the entire reason the inbox works. |
| `.obsidian/plugins/frontmatter-modified-date/data.json` | `excludedFolders: ["templates"]` → `["infra/templates"]`. Unfixed, every Templater definition gets `modified:` rewritten on save and shows as a diff on every commit. |
| `.obsidian/plugins/obsidian-spaced-repetition/data.json` | collapse `flashcardTags` to `["#flashcards"]`. |
| `.claude/settings.local.json` | **delete.** It is a local file listing the template author's absolute paths. Write a minimal replacement only if Q2 = folderbridge. |
| `.gitignore` | drop source-vault entries. Check the globs actually match: the template ignores `.playwright_mcp/*` (underscore) while the real directory is `.playwright-mcp` (hyphen), so it is *not* ignored. |

**The sibling skills are contaminated too, and they will actively misfile notes.**
`book-note` and `sort-landing` both contain destination tables naming the source vault's folders
and tags; `new-topic` and `obsidian-base` embed its vault name and folder filters. Regenerate those
tables from Q1's clusters, and rewrite `book-note`'s `STORE=` line from Q2. Phase 8 greps to confirm.

## Phase 3: Decide What Happens To The Shipped Clusters

Do this **before** creating the user's own clusters, so a kept or renamed cluster can *become*
cluster #1 rather than colliding with one.

The template ships `topics/` already populated — real, readable notes, not an empty skeleton. Most
people setting up their own vault do not want to inherit someone else's reading notes, but some do,
and a few want to keep one cluster as a worked reference for the conventions. **Never decide this
silently — it is the single most destructive step in the skill.**

Show them what is actually there before asking:

```bash
for d in topics/*/; do
  echo "$(find "$d" -name '*.md' | wc -l | tr -d ' ') notes  $d"
done
```

Then ask with `AskUserQuestion`, one question, options in this order:

| Option | What it does |
|---|---|
| **Delete all of them** (recommended default) | `rm -rf topics/*` — start empty, build only the user's own clusters |
| **Keep some, delete the rest** | follow up with a multi-select of the cluster list |
| **Keep all as seed content** | the user is adopting the template's notes as their own starting library |
| **Keep one as a reference, hidden** | `hidden: true` on its notes so they stay readable but leave the graph |

State the note count in the question text (`"topics/ holds 461 notes across 3 clusters"`) so the
answer is informed. Confirm a delete of more than ~50 notes a second time, in one line, before
running it.

Whatever is removed, follow through on all six registrations or the vault is left inconsistent:

1. the folder itself
2. its colour groups in `graph.json` — a colour matching nothing skews Phase 7's hue maths
3. its `Home.md` cluster line
4. its `CLAUDE.md` tree row **and** tag-table row
5. its key in the icon-folder plugin's data
6. dangling wiki-links in whatever survives — sweep afterwards, nothing else will

For a cluster that is **kept and renamed**: `git mv` the folder and the MOC, retag `<old>` → the new
root tag and `<old>/sub` → its sub-tags, and **rewrite its wiki-links by hand** — Obsidian is closed,
so `alwaysUpdateLinks` will not do it for you. This is the #1 breakage on this path. Do not inherit
the old colour; re-pick it in Phase 7 with the rest.

**Then write the demo clipping yourself** — `landing/Unsorted Clipping.md`, on a subject that
plausibly belongs to one of the user's real domains. The template *cannot* ship it: `landing/`'s
`.gitignore` is `*` + `!.gitignore`, so any note placed there is untracked and absent from a clone.
This file is what makes the `sort-landing` demo in Phase 9 work.

## Phase 4: Create The Remaining Clusters

For each Q1 domain not already satisfied by a rename in Phase 3:

```bash
mkdir -p "topics/<cluster>"
```

Write `topics/<cluster>/<Cluster Name>.md` — the MOC, carrying the root tag, with placeholder
`## Topics` children (one per sub-tag is the natural set). Placeholder wiki-links to notes that do
not exist yet are correct: they mark intended structure and give the MOC outgoing edges, so it is
not an orphan.

**A cluster is registered in six places, not five** — folder, MOC, `CLAUDE.md` (tree **and** tag
table), `Home.md`, `graph.json`, and `.obsidian/plugins/obsidian-icon-folder/data.json`
(`topics/<cluster>` → a Lucide id). The icon entry is the one that gets forgotten; without it the
new cluster is the only folder in the sidebar with a blank icon.

## Phase 5: Infra Wiring

**Attachment storage, per Q2.** For in-vault: create `infra/data/{images,documents}` with
`.gitkeep`, and **remove** their `.gitignore` lines — leaving them means attachments exist on one
machine only, which is the trap. For folderbridge: create the external dirs and regenerate
`data.json`.

The folderbridge ids are not cosmetic. Its `main.js` gates mounts with

```js
mountPoints.filter(m => m.enabled && (m.deviceId === settings.deviceId || settings.allowForeignMounts))
```

and the config sets `allowForeignMounts: false`. A clone therefore ships the template author's
`deviceId`, every mount is **inert**, no error is shown, and the mounts cannot even be switched on
from the settings UI. Generate one fresh top-level `deviceId`, stamp that same value on each mount,
and give each mount its own fresh `id`. Use absolute `realPath`s, no `~`. For a user with several
machines, `deviceOverrides[deviceId] → realPath` lets one committed config serve all of them.

**Templates.** Keep `Generic`. De-hardcode `Daily` — its `tags: [daily, daily/<year>]` and
`moc: "[[<YYYY-MM>]]"` are frozen to the template author's calendar; ship `moc:` empty. Generate the
Q3 choices from Generic. Regenerate `infra/templates/Templates.md` from the real file list.

Do **not** "fix" the syntax mismatch between them: `Daily` uses core-Templates `{{Date}}` while
`Generic` uses Templater `<% tp.date.now() %>`. That is deliberate — Templater's
`trigger_on_file_creation` is `false`, so only the core daily-notes plugin runs on daily creation,
and it only understands `{{}}`.

**The journal chain.** `daily → YYYY-MM.md → YYYY.md → Journal MOC.md` is documented but the
template ships only the MOC. Create this year's and this month's notes and wire them up, then point
`daily-notes.json` at the current month **and `mkdir -p` that folder** — if it does not exist,
"Open today's note" fails outright. Note the path is a literal month, not a date format, so it goes
stale on the 1st; put a one-line monthly-maintenance reminder in `CLAUDE.md`.

**`types.json`.** Keep the property declarations the Bases depend on (`created`/datetime,
`modified`/datetime, `published`/date, `topics`/multitext, `sources`/multitext,
`ai-assisted`/checkbox, `public`/checkbox). Prune keys for plugins the template does not ship and
for templates the user declined in Q3.

## Phase 6: Regenerate `CLAUDE.md` And `Home.md`

**Edit `CLAUDE.md` in place, section by section. Never delete-and-rewrite the file** — `AGENTS.md`
is a symlink to it, and a delete breaks the link silently. Confirm with `test -L AGENTS.md`; if a
zip or `cp -r` materialised it as a real file, re-point it, or you have personalized one of two
now-divergent instruction files.

| Section | Verdict |
|---|---|
| What This Repository Is, Vault Structure tree, tag table, Full Note Example | **regenerate** from Q1 |
| The three bullets under the tree (placing a note, `landing/` is gitignored, no cross-boundary links) | **keep verbatim** — pure Graphkasten |
| Frontmatter Schema | **keep verbatim** — the contract `types.json` and every Base depend on |
| Linking, Subtopic Navigation, Tagging rules, attachment filename rule | **keep**, minus source-vault trivia (legacy-tag exceptions, MOC names that no longer exist) and with the obsidian-URL example rebuilt against a note that exists in *this* vault |
| Structuring Of Resources, Displaying With Adjusted Width | **keep the rule, replace the examples** |
| Storing Attachments | **regenerate** from Q2 |
| LaTeX section | **drop** unless a maths/CS domain was chosen |
| Obsidian CLI section | **drop** unless `command -v obsidian` succeeds |

The examples matter more than they look: a rule is advice, but an example is a template the model
imitates. Leave the source vault's AI-research citations in and every note the agent writes drifts
toward that shape. Add a tag-table row documenting `#private` and `hidden: true` — `graph.json`
already filters on both and nothing currently tells the user or the agent they exist.

**`Home.md`** — rebuild `## List Of Clusters` from Q1 using this vault's name in each
`obsidian://` URL, drop the `banner`/`banner-height` frontmatter and the `## Ambience` block (both
point into the gitignored attachment store and can never resolve), and **keep `topics: - Home` in
the frontmatter** — it is what `graph.json`'s first colour group matches to colour the entry point.

## Phase 7: Assign Graph Colours

Batch, against the final tag set — which is why this comes last.

**Do not loop `new-topic`'s hue picker.** That one finds the widest gap in the *current* palette,
which is correct for adding one cluster to a crowded vault and wrong here: run per-cluster against a
nearly-empty palette and every pick lands in almost the same place. Split the circle instead:

```python
hue_i = (offset + i / N) % 1.0        # N root tags, evenly spaced
# sub-tags of a root: same hue, vary saturation/value so the cluster reads as one family
```

Write each family **sub-tags first, root tag last**. Obsidian applies the first matching group, so a
root tag placed before its children repaints every sub-tag note plain. `rgb` is a decimal integer
(`R*65536 + G*256 + B`), not hex.

## Phase 8: Validate

```bash
python3 -c "import glob,json;[json.load(open(f)) for f in glob.glob('.obsidian/**/*.json',recursive=True)];print('all JSON valid')"

# no trace of the template's origin anywhere
grep -rn "<source-vault-name>\|<template-author>" \
  CLAUDE.md Home.md .gitignore .obsidian/*.json .claude/skills/ || echo "clean"

# plugin list matches reality
python3 -c "
import json,os
print(set(json.load(open('.obsidian/community-plugins.json'))) - set(os.listdir('.obsidian/plugins')) or 'plugin list OK')"

# folderbridge mounts will actually activate (only if Q2 = folderbridge)
python3 -c "
import json;d=json.load(open('.obsidian/plugins/folderbridge/data.json'))
print('mounts OK' if all(m['deviceId']==d['deviceId'] for m in d['mountPoints']) else 'MOUNTS INERT')"

test -L AGENTS.md && echo "symlink intact"
# every wiki-link resolves to a note that still exists (Phase 3 deletions break these)
python3 -c "
import os,re
have={f[:-3].lower() for _,_,fs in os.walk('topics') for f in fs if f.endswith('.md')}
bad=[t for d,_,fs in os.walk('topics') for f in fs if f.endswith('.md')
     for t in re.findall(r'(?<!!)\[\[([^\]|#]+)', open(os.path.join(d,f),encoding='utf-8',errors='replace').read())
     if t.split('/')[-1].lower() not in have and '.' not in t.split('/')[-1]]
print(f'{len(bad)} dangling wiki-links' if bad else 'no dangling wiki-links')"
```

## Phase 9: Hand Off

Tell the user, **in this order** — the sequence matters:

1. **Open Obsidian and enable community plugins when prompted.** If they decline and stay in
   Restricted Mode, `community-plugins.json` is emptied and everything configured here is inert:
   no mounts, no Templater, no icons.
2. **Restart Obsidian once more** so the graph config is read at startup.
3. Open **Graph View**, toggle **Filters → Tags**, and check each cluster is its own colour and
   sub-tags read as shades of their parent.
4. Press `Cmd-N` — the new note should land in `landing/`.
5. Run **`/sort-landing`** on the demo clipping to see the review process end to end.
6. Run **`/new-topic`** when they want cluster #2.

Finally, write a `.graphkasten` record (vault name, clusters, tags, storage mode, what happened to
the shipped clusters) so Phase 0 can stop a second run and a later session knows what was chosen.

## Output Checklist

- [ ] `.graphkasten` absent (or the user confirmed a re-run); Obsidian closed for the whole run
- [ ] 3–6 clusters agreed, each with a short root tag and one level of sub-tags
- [ ] Template identity gone: git remote, vault name, workspace/bookmarks, settings.local.json
- [ ] `bookmarks.json` stale `colorGroups` cleared — otherwise the saved graph bookmark wins
- [ ] Shipped clusters' fate chosen by the user, with all six registrations followed through
- [ ] Demo clipping written into `landing/` by the skill (the template cannot ship it)
- [ ] Storage wired per Q2; if folderbridge, fresh `deviceId` + per-mount `id`s
- [ ] Journal chain created and `daily-notes.json` folder exists on disk
- [ ] `CLAUDE.md` edited in place (symlink intact), tree + tag table regenerated, examples replaced
- [ ] Colours assigned by even hue split, children before parents, JSON valid
- [ ] User told: enable plugins → restart → Graph View → `/sort-landing`
