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
name: obsidian-base
description: Creates a new Obsidian Base (.base file) — a saved, filtered database view over the vault's notes. Use when the user wants a new base, a table/cards/list/kanban view, a dashboard of notes matching some criteria, or wants to add a view to an existing base. Always interviews the user about view type and configuration before writing.
---

# Create An Obsidian Base

A **Base** is a `.base` file: a YAML query that renders vault notes as a table, card grid, list, or kanban board. It is the vault's database layer.

**Never write the file before interviewing the user.** Base configuration has too many degrees of freedom to guess. Phase 1 is mandatory.

## Where Bases Live

- All bases go in `infra/bases/`, named in natural language: `Not Public.base`, `Book View.base`, `Kanban.base`
- Read the existing bases in that folder first — they are the ground truth for what syntax this vault's Obsidian version accepts
- A base is opened directly, or embedded in a note with `![[Some Base.base]]` / `![[Some Base.base#View Name]]` (the `#` picks a view)

## Phase 1: Interview The User

Before anything else, **scan the vault so the options you offer are real**, not invented:

```bash
# properties actually in use, by frequency
find . -name "*.md" -not -path "./.claude/*" -not -path "./.obsidian/*" | while read f; do
  awk 'NR==1&&$0=="---"{f=1;next} f&&/^---$/{exit} f&&/^[A-Za-z][A-Za-z0-9_-]*:/{sub(/:.*/,"");print}' "$f"
done | sort | uniq -c | sort -rn

ls infra/bases/            # existing bases — reuse their conventions
ls topics/                 # top-level folders for scoping filters
```

Then use **AskUserQuestion** — one call, covering these four axes. Pre-fill each option with concrete values from the scan above, never generic placeholders.

| # | Ask | Options to offer |
|---|-----|------------------|
| 1 | **View type** | `Table` (most data per row, default choice) · `Cards` (needs a cover image property) · `List` (compact, scannable) · `Kanban` (needs a status-like property to become columns) |
| 2 | **Scope** — which notes belong in it | By tag (`file.hasTag("...")`) · By folder (`file.inFolder("topics/...")`) · By property value (`note.status == "..."`) · Whole vault |
| 3 | **Columns / properties to show** | Multi-select from the properties found in the scan — `tags`, `topics`, `created`, `modified`, `published`, `authors`, `public`, `status`, `file.folder` |
| 4 | **Grouping & sort** | Group by a property (which one) · sort property + direction |

Ask follow-ups only where the answer materially changes the file:

- **Cards** → which property holds the image? (`localCover` is the vault's convention) Cover or contain? Aspect ratio?
- **Kanban** → which property becomes the columns? (`kanban-status`, `status`)
- **Multiple views** → does one base need several views (e.g. one per domain, as `Book View.base` does), or just one?

If the user's request already pins down an axis ("a table of every unread book"), do not re-ask it — confirm it in the summary instead and ask only the open ones.

## Phase 2: Write The File

### Skeleton

```yaml
filters:            # optional — applies to EVERY view (view filters are ANDed on top)
  and:
    - file.hasTag("fin")
formulas:           # optional — computed properties, usable as formula.<name>
  age: '(now() - note.published).format("y")'
properties:         # optional — column display names only
  note.published:
    displayName: Published
summaries:          # optional — custom aggregations over the result set
  customAverage: 'values.mean().round(3)'
views:
  - type: table
    name: All
    filters:
      and:
        - note.status != "done"
    order:              # column order, and the properties shown
      - file.name
      - tags
      - modified
    sort:
      - property: modified
        direction: DESC
    groupBy:
      property: note.status
      direction: ASC
    limit: 100
    summaries:
      note.price: Average
```

### Filters

- Structure is recursive: `and` / `or` / `not`, each holding a list of statements or further nested objects.

```yaml
filters:
  or:
    - file.hasTag("book")
    - and:
        - file.inFolder("topics/<cluster>")
        - note.status != "done"
    - not:
        - file.hasTag("archive")
```

- **Quote any statement starting with `!`** — bare `!foo` is invalid YAML: `- '!note.tags.isEmpty()'`
- **Dashed property names need bracket syntax**: `note["kanban-status"]`, not `note.kanban-status`
- **Empty vs false are different.** `note.public != true` matches both `false` and unset; `note.public == false` matches only explicit `false`; `note.public.isEmpty()` matches only unset. Ask which the user means when a boolean property is involved — most vault notes leave properties blank.

### Property References

| Prefix | Meaning |
|---|---|
| `note.foo` or bare `foo` | frontmatter property |
| `file.name` `file.basename` `file.path` `file.folder` `file.ext` `file.size` | file identity |
| `file.ctime` `file.mtime` `file.tags` `file.links` `file.backlinks` `file.embeds` | file metadata (`backlinks` is slow and does not auto-refresh) |
| `formula.foo` | a formula defined above (no circular references) |
| `this` | the base file itself, or the embedding/active note when embedded — `file.hasLink(this.file)` replicates backlinks |

This vault stores `created` / `modified` as frontmatter, so prefer `note.modified` over `file.mtime` when the user means the vault's own timestamps.

### View Types And Their Keys

Every view takes `type`, `name`, `filters`, `order`, `sort`, `groupBy`, `limit`, `summaries`. Type-specific keys on top of those:

**`table`**
- `rowHeight`: omit for short · `medium` · `tall` · `extra`
- `columnSize`: map of property → pixel width (normally written by the UI when the user drags a column; don't hand-author)

**`cards`**
- `image`: property holding the cover — a local attachment link, URL, or hex color (`image: note.localCover`)
- `imageFit`: omit for cover (fills, crops) · `contain` (scales, no crop)
- `imageAspectRatio`: number 0.25–2.5, default `1`
- `cardSize`: card width in px, 50–800, default `200`

**`list`**
- `markers`: `bullet` (default) · `number` · `none`
- `indentProperties`: `true` puts each property on its own indented line
- `separator`: string between inline properties, default `", "` (ignored when `indentProperties` is true)

**`kanban-view`** — from the `kanban-bases-view` community plugin, not core (core kanban needs Obsidian 1.14+; this vault runs 1.12.7)
- `groupBy` is what creates the columns — it is required
- `columnOrders`, `cardOrders`, `columnColors` are UI-managed state; write them empty or omit and let the user arrange the board

`map` exists upstream but requires the Maps plugin, which is not installed here.

### Function Cheat Sheet

- **Global**: `if(cond, a, b)` `link(path, display)` `list(x)` `file(path)` `image(path)` `icon(name)` `date("2025-01-01")` `now()` `today()` `duration(s)` `number(x)` `min()` `max()` `random()` `html()` `escapeHTML()`
- **File**: `.asLink(display)` `.hasLink(f)` `.hasTag(...)` `.hasProperty(name)` `.inFolder(path)` (matches sub-folders too)
- **String**: `.contains()` `.containsAll()` `.containsAny()` `.startsWith()` `.endsWith()` `.isEmpty()` `.lower()` `.title()` `.trim()` `.split()` `.slice()` `.replace()` `.length`
- **List**: `.contains()` `.containsAny()` `.filter()` `.map()` `.join()` `.sort()` `.unique()` `.flat()` `.reduce()` `.isEmpty()` `.length`
- **Number**: `.round(n)` `.toFixed(n)` `.floor()` `.ceil()` `.abs()`
- **Date**: `.format("YYYY-MM-DD")` (Moment.js patterns) `.relative()` `.date()` `.time()` `.year` `.month` `.day` `.hour`
- **Any**: `.isEmpty()` `.isTruthy()` `.isType()` `.toString()`
- **Date arithmetic**: `note.modified > now() - "1 week"`; units `y M w d h m s`
- **Operators**: `+ - * / %` · `== != > < >= <=` · `&& || !`

### Summaries

Named aggregations attached per column, per view: `Average` `Min` `Max` `Sum` `Range` `Median` `Stddev` `Earliest` `Latest` `Checked` `Unchecked` `Empty` `Filled` `Unique`. Custom ones go in the top-level `summaries:` block using the `values` list.

## Phase 3: Verify And Hand Off

1. **Parse the YAML** — a malformed base fails silently in Obsidian:
   ```bash
   ruby -ryaml -e 'YAML.load_file("infra/bases/NAME.base"); puts "OK"'
   ```
   (`python3 -c "import yaml"` is not available in this environment — use Ruby, which ships with macOS.)
2. **Sanity-check the result count** with a rough grep so the user knows the base is not empty:
   ```bash
   grep -rl --include="*.md" "^status: reading" topics/ | wc -l
   ```
3. **Link it** — if the base is a navigation surface, add a wiki-link to it from `Home.md` or the relevant MOC. Bases are files; an unlinked one is an orphan.
4. Report the file path, each view and what it filters to, and the approximate row count. Flag any judgment call you made (e.g. treating blank as non-public, excluding `infra/templates/`).

## Adding A View To An Existing Base

Same interview, smaller scope. Read the file first, append to `views:`, keep the existing top-level `filters` in mind — they still apply, so the new view only needs the delta. Preserve UI-managed state (`columnOrders`, `cardOrders`, `columnSize`) byte-for-byte; never reformat the whole file.

## References

- [Bases syntax](https://obsidian.md/help/bases/syntax)
- [Bases functions](https://obsidian.md/help/bases/functions)
- [Bases views](https://obsidian.md/help/bases/views)
