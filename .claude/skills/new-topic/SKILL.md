---
name: new-topic
description: Creates a new top-level topic cluster in the vault — the folder under topics/, its MOC note, the root tag and sub-tags, registration in CLAUDE.md and Home.md, and the tag colour groups in the graph view. Use when the user wants a new topic, cluster, subject area, or knowledge domain added to the vault.
---

# Create A New Topic Cluster

A **topic cluster** is a top-level area of interest under `topics/` — the L-I-F-**T** of the vault's LIFT structure, and the only folder rendered in graph view.

Creating one is not `mkdir`. A cluster only exists once it is registered in **six** places:

| # | Where | What |
|---|---|---|
| 1 | `topics/<cluster>/` | the folder |
| 2 | `topics/<cluster>/<Cluster Name>.md` | the MOC note, carrying the root tag |
| 3 | `CLAUDE.md` | the tag table row **and** the vault-structure tree |
| 4 | `Home.md` | a line under `## List Of Clusters` |
| 5 | `.obsidian/graph.json` | one colour group per tag |
| 6 | `.obsidian/plugins/obsidian-icon-folder/data.json` | the folder's sidebar icon |

Skip any of these and the cluster is half-real: notes land in it but agents don't know it exists, or it shows up in graph view as an uncoloured grey blob indistinguishable from its neighbours.

## Phase 1: Is This Actually A New Top-Level Cluster?

**Most new subjects are not.** There are only ~10 clusters; adding one is a structural decision, and the wrong call leaves the graph with a near-empty node cluster that never grows.

```bash
ls topics/                                    # the existing clusters
grep -n "^| " CLAUDE.md | head -20            # the tag table
```

A new top-level cluster earns its place when **all** of these hold:
- It does not fit as a subfolder of any existing cluster.
- It deserves its own root tag (it is a *domain*, not a topic within one).
- You expect it to hold many notes over time, not three.

If any fails, it belongs **inside** an existing cluster instead — use the `obsidian-note-cluster` skill to build it at `topics/<existing>/<subject>/`. Say so and stop; do not create a top-level folder to be helpful.

## Phase 2: Interview The User

Never guess the tag. Use `AskUserQuestion` to settle:

1. **Cluster name** — natural language, title case (`Health`, `Law`, `Languages`). This names both the folder (lowercased, `snake_case` if multi-word) and the MOC note.
2. **Root tag** — short, lowercase, `snake_case`, no slash (`health`, `law`). It is typed into every note in the cluster forever, so short wins. Check it is not taken:
   ```bash
   grep -rn "tag:#<tag>" .obsidian/graph.json
   ```
3. **Sub-tags** — propose 3–6 candidates derived from the subject and let the user multi-select (`multiSelect: true`), plus the option of none for now.

**Sub-tag rules:**
- **Exactly one level of nesting.** `health/nutrition` is valid; `health/nutrition/protein` is not — the vault has three legacy violations and does not want more.
- Sub-tags are for *sub-domains*, not note types. `fin/crypto` good; `fin/interesting` bad.
- Starting with none is fine. They can be added later by re-running this skill's Phase 6 for the new tag alone.

Present real candidates, not placeholders — read the subject and suggest what a `health` cluster would actually split into (`health/nutrition`, `health/fitness`, `health/sleep`, `health/medical`).

## Phase 3: Create The Folder And MOC Note

```bash
mkdir -p "topics/<cluster>"
```

The MOC filename is the cluster name in natural language — `Health.md`, not `Health MOC.md`. (`Work MOC.md` and `School MOC.md` are legacy exceptions; do not copy them.)

`topics/<cluster>/<Cluster Name>.md`:

```yaml
---
tags:
  - <root-tag>
created: <now, YYYY-MM-DDTHH:mm>
modified:
published:
sources:
topics:
authors:
ai-assisted: true
hidden:
public:
---
# <Cluster Name>
- <One line saying what this cluster aggregates, in the user's voice.>
## Topics
- [[<Placeholder Child One>]]
	- <one-line description of what will go here>
- [[<Placeholder Child Two>]]
	- <one-line description>
```

Placeholder wiki-links to notes that do not exist yet are correct here — they are the vault's convention for marking intended structure, and they give the fresh MOC outgoing edges so it is not a graph orphan (`showOrphans` is off, so an edgeless MOC would be invisible).

If the user named sub-tags in Phase 2, the natural placeholders are one per sub-tag.

## Phase 4: Register In CLAUDE.md

Two edits, both required.

**The tag table** — add a row in the `### Tagging System` table, root tag first, then sub-tags:

```markdown
| Health           | `health`, `health/nutrition`, `health/fitness`, `health/sleep` |
```

**The vault-structure tree** — add the cluster under `topics/` in the `## Vault Structure` block, with its sub-areas as a trailing comment, matching the existing rows:

```
    ├── health/                # nutrition, fitness, sleep, medical
```

Keep the tree's column alignment. Agents read this tree to decide where a note goes; a cluster missing from it will not receive notes.

## Phase 5: Link From Home.md

Add a line under `## List Of Clusters` in `Home.md`, using an **obsidian URL**, matching every other cluster there:

```markdown
- Health
```

URL-encode the path: `/` → `%2F`, space → `%20`. Verify the target resolves:

```bash
test -f "topics/<cluster>/<Cluster Name>.md" && echo OK
```

These are obsidian URLs rather than wiki-links on purpose — `Home.md` links all ten clusters, and wiki-linking them would make it a hub with edges to everything, which flattens the graph's topology.

## Phase 5b: Give The Folder An Icon

Every existing cluster has a sidebar icon; a new one without it is the only blank folder in the
list. Add a `topics/<cluster>` key to `.obsidian/plugins/obsidian-icon-folder/data.json`, mapping
to a native Lucide id (the `Li` prefix, e.g. `LiHeartPulse`, `LiScale`, `LiMusic`):

```bash
python3 - <<'ICON'
import json
p = ".obsidian/plugins/obsidian-icon-folder/data.json"
d = json.load(open(p))
d["topics/<cluster>"] = "Li<IconName>"
json.dump(d, open(p, "w"), indent=2)
print("icon set")
ICON
```

Pick from the ids already in that file for style consistency. Like `graph.json`, this file is
rewritten by Obsidian on exit — the Phase 6 "is Obsidian running?" check applies here too.

## Phase 6: Add The Graph Colour Groups

Tag colours are what turn the graph into visible clusters — this is the payoff of the whole exercise, and the step most easily botched.

### First: make sure Obsidian is not running

```bash
pgrep -x Obsidian && echo "RUNNING — stop here" || echo "safe to edit"
```

**Obsidian rewrites `.obsidian/graph.json` from memory when it quits.** If it is running, your edit is silently discarded the moment the user closes the app. If it is running, ask the user to quit it before you continue — do not edit and hope.

### Colour group format

Each group in `colorGroups` is:

```json
{ "query": "tag:#health/nutrition", "color": { "a": 1, "rgb": 14180730 } }
```

`rgb` is a **decimal** integer, not hex: `R*65536 + G*256 + B`. (`#d8617a` → `14180730`.)

### Ordering matters: children before the parent

Obsidian applies the **first** matching group, so a sub-tag's group must come *before* its root tag's group, or every `health/nutrition` note is painted plain `health`. Every family in the file already follows this — verify with:

```bash
FAM=health   # the root tag, without the '#'
python3 - "$FAM" <<'CHECK'
import json, sys
fam = sys.argv[1]
qs = [g["query"].strip() for g in json.load(open(".obsidian/graph.json"))["colorGroups"]]
kids = [i for i, q in enumerate(qs) if q.startswith(f"tag:#{fam}/")]
if f"tag:#{fam}" not in qs:
    print(f"root group tag:#{fam} not present yet - insert it, then re-run")
elif not kids:
    print("OK (no sub-tags)")
else:
    print("OK" if max(kids) < qs.index(f"tag:#{fam}") else "BROKEN: parent precedes its children")
CHECK
```

Insert the new groups as a block, sub-tags first, root tag last. Put the block next to related clusters rather than at the end — the file is loosely grouped by domain.

### Choosing colours that read as distinct

The palette is crowded (80+ groups, all distinct). Find the least-used region of the hue circle rather than picking by eye:

```bash
python3 - <<'PY'
import json, colorsys
g = json.load(open(".obsidian/graph.json"))["colorGroups"]
used = [c["color"]["rgb"] for c in g]
unpack = lambda c: (((c>>16)&255), ((c>>8)&255), (c&255))
hues = sorted(colorsys.rgb_to_hsv(*[v/255 for v in unpack(c)])[0] for c in used)
gap, start = max(((hues[(i+1) % len(hues)] - h) % 1.0, h) for i, h in enumerate(hues))
print(f"{len(used)} groups in use; widest hue gap {gap*360:.0f}deg at {start*360:.0f}deg\n")
for sv in ((0.55, 0.85), (0.40, 0.95), (0.70, 0.70)):
    h = (start + gap/2) % 1.0
    r, gg, b = [int(v*255) for v in colorsys.hsv_to_rgb(h, *sv)]
    rgb = (r<<16)|(gg<<8)|b
    near = min(sum((a-b2)**2 for a,b2 in zip((r,gg,b), unpack(c)))**0.5 for c in used)
    print(f"  #{rgb:06x}  rgb={rgb:<9} sat={sv[0]} val={sv[1]}  nearest existing: {near:.0f}/441")
PY
```

Give the **root tag** the most saturated candidate and its sub-tags neighbouring shades of the same hue — that way the cluster reads as one colour family at a glance, which is the point. Treat a `nearest existing` distance below ~30 as too close; adjust saturation or value.

### Write it back

Edit the JSON with a script, not by hand — the file is ~800 lines and a stray comma breaks graph view entirely. Afterwards:

```bash
python3 -c "import json;json.load(open('.obsidian/graph.json'));print('valid JSON')"
```

## Phase 7: Tell The User To Restart Obsidian

`graph.json` is read **once at startup**. New colour groups do not appear in a running or reopened graph view — the app itself must be restarted.

Close the loop explicitly:

> Restart Obsidian to pick up the new tag colours. Then open Graph View, toggle **Filters → Tags** on, and check that `<cluster>` shows as its own coloured cluster and its sub-tags read as shades of it.

That visual check is the human-review step of the vault's review process — it is the only way to confirm the colours actually separate, so do not skip asking for it.

## Output Checklist

- [ ] Confirmed this warrants a *top-level* cluster, not a subfolder of an existing one
- [ ] Root tag agreed with the user; short, lowercase, unused
- [ ] Sub-tags agreed with the user; **one level of nesting only**
- [ ] `topics/<cluster>/` created
- [ ] MOC note at `topics/<cluster>/<Cluster Name>.md`, carrying the root tag, with placeholder `## Topics` children
- [ ] CLAUDE.md tag table row added
- [ ] CLAUDE.md vault-structure tree updated
- [ ] `Home.md` `## List Of Clusters` line added, target verified to exist
- [ ] Sidebar icon added to `obsidian-icon-folder/data.json`
- [ ] Obsidian confirmed **not running** before touching `graph.json`
- [ ] Colour groups added — sub-tags **before** root tag, distinct hues, JSON still valid
- [ ] User told to restart Obsidian and eyeball the new cluster in Graph View
