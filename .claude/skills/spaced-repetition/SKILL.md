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
name: spaced-repetition
description: Generates spaced repetition flashcards from an Obsidian note using the obsidian-spaced-repetition plugin format. Creates a dedicated flashcard note in a flashcards/ subfolder next to the source note and links both notes together.
---

# Spaced Repetition Flashcard Generator

Workflow for generating flashcards from an existing Obsidian note and placing them in a co-located `flashcards/` subfolder.

## Card Formats

| Type | Syntax | Use when |
|---|---|---|
| Single-line Q&A | `Question::Answer` | Definitions, facts, short answers |
| Multi-line Q&A | `Question\n?\nAnswer` | Complex explanations, multi-step answers |

**Deck tagging:** Each flashcard note acts as a deck identified by a unique tag (e.g., `#rl_flashcards`, `#docker_flashcards`). This tag must appear in:
1. The flashcard note's frontmatter `tags` (without `#`)
2. The plugin's `flashcardTags` array in `.obsidian/plugins/obsidian-spaced-repetition/data.json` (with `#`)

## Phase 1: Identify Source Note

1. The user provides a note title or file path. If ambiguous, use `Glob` to find the file.
2. Read the note with the `Read` tool.
3. Extract its frontmatter: `tags`, `topics`, `created` timestamp, and note title (the `# H1` heading).

## Phase 2: Select Card Content

Scan the note and identify **5–15 facts** worth memorizing. Prioritize:
- Definitions and key terms → single-line `::` cards
- Comparisons, workflows, or explanations requiring >1 line → multi-line `?` cards
- Aim for a mix; prefer `::` for ~60% of cards, `?` for the rest

**Do NOT generate cards for:**
- Navigational wiki-links (`[[...]]`) or MOC structure
- Metadata that is already in frontmatter
- Obvious or trivial statements

**Important:** Multi-line card answers must NOT contain blank lines. The plugin stops reading the answer at the first blank line, silently truncating the rest. Use `---` as a visual separator between sub-sections within an answer instead of a blank line.

## Phase 3: Determine Output Path

```
<source-note-dir>/flashcards/<Note Title> Flashcards.md
```

**Example:**
```
topics/<cluster>/<subfolder>/
├── <Note Title>.md                  ← source note
└── flashcards/
    └── <Note Title> Flashcards.md   ← output
```

- Create the `flashcards/` directory if it does not exist (use `Bash`: `mkdir -p`)
- If the flashcard note already exists, **append** new cards below the existing ones (do not duplicate)

## Phase 4: Write the Flashcard Note

### Frontmatter (copy tags from source, add a unique deck tag)

Derive the deck tag from the primary topic in snake_case with `_flashcards` suffix (e.g., `rl_flashcards`, `docker_flashcards`, `prompt_engineering_flashcards`).

```yaml
---
tags:
  - <tags from source note>
  - <topic>_flashcards
created: <ISO timestamp matching now>
modified:
sources:
  - "[[<Source Note Title>]]"
topics:
  - <topics from source note>
ai-assisted: true
---
```

### Body structure

```markdown
# <Note Title> Flashcards

## Cards

<card 1>

<card 2>

...
```

### Card format examples

Single-line:
```
What is a Docker image?::A read-only template used to create containers, built from a Dockerfile.
```

Multi-line:
```
What are the steps to build and run a Docker container?
?
1. Write a Dockerfile
2. Build: `docker build -t name .`
3. Run: `docker run name`
```

Multi-line with multiple sections (use `---` instead of blank lines):
```
How do X and Y differ?
?
**X** — description
- detail 1
- detail 2
---
**Y** — description
- detail 1
- detail 2
```

Separate every card with a blank line.

## Phase 5: Register Deck Tag in Plugin Settings

1. Read `.obsidian/plugins/obsidian-spaced-repetition/data.json`
2. Check if the deck tag (e.g., `#rl_flashcards`) already exists in `settings.flashcardTags`
3. If not, add it to the array and write the file back

## Phase 6: Link Source Note Back

After writing the flashcard note, edit the source note:
- If a `## Flashcards` section does not exist, append it at the very end:

```markdown
## Flashcards
- [[<Note Title> Flashcards]]
```

- If `## Flashcards` already exists but the link is missing, add the wiki-link inside it.
- Set `ai-assisted: true` in the source note frontmatter if not already set.

## Output Checklist

- [ ] Flashcard note is at `<source-dir>/flashcards/<Title> Flashcards.md`
- [ ] Frontmatter has all source tags + unique deck tag (`<topic>_flashcards`), and `ai-assisted: true`
- [ ] 5–15 cards generated; no trivial or duplicate cards
- [ ] Single-line `::` used for short facts; multi-line `?` for complex answers
- [ ] Multi-line answers contain no blank lines — `---` used as section separator instead
- [ ] Deck tag registered in `.obsidian/plugins/obsidian-spaced-repetition/data.json` → `flashcardTags`
- [ ] Source note has `## Flashcards` section linking to the flashcard note
- [ ] Source note frontmatter has `ai-assisted: true`

## Additional Notes

- Card separators (`::`, `?`) are the plugin defaults. Do not change them unless the user configures custom separators in the plugin settings.
- The unique deck tag (e.g., `rl_flashcards`) in frontmatter registers the note as a deck. It must also be listed in the plugin's `flashcardTags` setting. Individual `#flashcard` inline tags on each card tell the plugin which lines to schedule.
- For vault conventions (frontmatter schema, tagging, linking): refer to `CLAUDE.md` in the vault root.
