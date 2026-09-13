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
name: obsidian-note-cluster
description: Creates a cluster of hierarchical, interlinked Obsidian notes on a large topic. Use when the user wants to document a broad subject (a technology platform, a framework, a domain) as a multi-level note hierarchy with a root hub, section hubs, and detailed leaf notes following vault conventions.
---

# Obsidian Note Cluster

Workflow for building a structured, 3-level note hierarchy on a large topic in this Obsidian vault.

## Hierarchy Model

```
Root hub (topic overview, links to section hubs only)
├── Section Hub A  (domain overview, links to its leaf notes)
│   ├── Leaf Note 1
│   └── Leaf Note 2
├── Section Hub B
│   ├── Leaf Note 3
│   └── Leaf Note 4
└── ...
```

Files live flat in a single `topic/` subdirectory of the relevant vault folder. The logical hierarchy is expressed through `[[wiki-links]]`, not deep nesting.

## Phase 1: Research and Plan

Before writing, always:

1. **Verify current naming** — services and products get renamed. WebSearch the official name for each concept before writing (`"Azure Active Directory renamed 2025"`, etc.)
2. **Design the hierarchy** — propose the full link tree to the user before writing. Show 3 levels: root → sections → leaves
3. **Confirm the scope** — ask the user to approve or trim the hierarchy before executing

Only proceed to Phase 2 after the user approves the plan.

## Phase 2: Create Files (bottom-up)

Build in this order to ensure links are valid when hubs are written:

1. **Leaf notes** — detailed service/concept notes
2. **Section hubs** — domain overview + links to children
3. **Root hub** — brief topic intro + links to section hubs only

### Frontmatter Schema (required on every note)

```yaml
---
tags:
 - <domain-tag>          # e.g. cs, cloud, ml_ai, fin
created: 2026-03-02T19:00
modified:
sources:
 - "[Title](URL)"        # official docs only; at least one per note
topics:
 - Topic Name
ai-assisted: true
---
```

See vault `CLAUDE.md` for the full tag taxonomy.

### Leaf Note Structure

```markdown
# Service Name
- One-line definition with inline citation ([Docs](URL))
- Key fact or rebranding note if relevant

## Core Concepts
- Bullet-point facts; prefer tables for comparisons

## Key Features / Tiers / Patterns
- ...
```

### Section Hub Structure

```markdown
# Section Title
- 2–3 sentence overview of this domain

## Topics
- [[Leaf Note A]]
	- 1–2 bullet summary
- [[Leaf Note B]]
	- 1–2 bullet summary
```

### Root Hub Structure

```markdown
# Topic Name
- One-sentence description; mention it alongside its peers (e.g. [[AWS]], [[GCP]])

## Section A
- One-sentence summary
- → [[Section Hub A]]

## Section B
- → [[Section Hub B]]
```

## Phase 3: Create Subdirectory Structure

After all files are written, move them into topic-named subdirectories under `topics/` —
clusters are durable knowledge, so they never live at the vault root, in `fleeting/`, or in `infra/`:

```bash
mkdir -p topics/<cluster>/section_a topics/<cluster>/section_b
mv "Leaf Note A.md" "Leaf Note B.md" "Section Hub A.md" topics/<cluster>/section_a/
```

`[[wiki-links]]` resolve by filename in Obsidian, so moves do not break links.

## Linking Rules (critical)

### What to link

| Link type | Rule |
|---|---|
| Hierarchical (parent ↔ child, same section) | Always link |
| Cross-section | Only if absolutely necessary (e.g. Key Vault → App Service) |
| Placeholder (note doesn't exist yet) | Max 2–3 per note; only truly important concepts |

### What NOT to link

- Every mention of a related service — if it's just context, write plain text
- Sibling links between leaf notes (creates clutter on Graph View — leaf notes should not link to each other)
- External frameworks/libraries unless the note is specifically about integration

### Attachment links

Images, PDFs and other attachments are linked by **bare filename only** — never with a folder path. Obsidian resolves attachment names vault-wide, and a path breaks as soon as the file is moved.

```
![[dspy_adapter.png]]              # correct
![[dspy_adapter.png|600]]          # correct, sized
![|600](dspy_adapter.png)          # correct, markdown syntax
![[images/cs/ml_ai/dspy/dspy_adapter.png]]   # WRONG — never include the path
```

This holds for `.pdf`, `.svg`, `.m4a`, `.zip` and every other non-note file, and for attachment links inside frontmatter fields. Attachments do not count as graph edges, so the pruning rules below do not apply to them.

### Pruning Check

After writing, scan every note and ask for each `[[link]]`:
- Is this link hierarchical (same section)? → keep
- Is this a cross-section link? → remove unless it's the core integration pattern of the note
- Is this a placeholder? → keep only if the concept is important enough to appear on Graph View

## Output Checklist

- [ ] Each note has valid YAML frontmatter with `ai-assisted: true` and at least one `sources` URL
- [ ] Root hub links only to section hubs (no leaf links)
- [ ] Section hubs link only to their leaf notes
- [ ] Leaf notes have NO `## Related` section and NO sibling links
- [ ] Placeholder links ≤ 2-3 per note
- [ ] Every attachment link (image, PDF, recording) uses the bare filename — no folder path, in either link syntax
- [ ] Cross-section links only where the integration is the primary point of the note
- [ ] Files moved into `topics/<cluster>/section/` subdirectories
- [ ] New note linked from its parent section hub and from the root hub chain

## Additional Resources

- For vault conventions (tags, frontmatter, naming): read `CLAUDE.md` in the vault root
- For citing sources: inline `([Name](URL))` plus frontmatter `sources:` list
