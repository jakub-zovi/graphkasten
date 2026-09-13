---
name: book-note
description: Creates a book note from the Book Search Template — resolves the book's metadata (title, author, publisher, ISBN, page count, cover URL), downloads the cover image into the attachment store, writes the note into the right topical folder, and links it from that cluster's hub note. Use when the user wants to add, track, or record a book in the vault.
---

# Create A Book Note

A **book note** is a normal vault note carrying the book-metadata frontmatter block from `infra/templates/definitions/Book Search Template.md`. Its `book-view: true` flag makes it render as a card in `infra/bases/Book View.base`, and that card's image is `localCover` — so **a book note without a downloaded local cover is a broken book note**. Resolving `coverUrl` and downloading it are mandatory steps, not optional polish.

The book-search plugin that originally produced these notes is no longer installed. Everything below is done by hand: metadata comes from public APIs, the cover is downloaded with `curl`, the note is written with the normal file tools.

## Phase 1: Identify The Book And Where It Goes

1. Get the title (and author if the title is ambiguous) from the user.
2. **Check it does not already exist** before anything else:

```bash
find topics -iname "*<title fragment>*.md"
```

3. Decide the folder. Book notes live **next to their subject**, not in one central shelf. Confirm with the user when the subject could plausibly sit in two clusters.

Derive the folder from the vault's own clusters — do not assume a fixed list:

```bash
ls topics/                                  # the clusters that exist here
grep -rl "book-view: true" topics/ | sed 's|/[^/]*$||' | sort | uniq -c | sort -rn
```

The second command shows where book notes already live, which is the strongest signal. Rules:

| Rule | Resolution |
|---|---|
| A sibling book on the same subject already exists | put it in that folder, copy its `tags` |
| The subject has a cluster but no books yet | `topics/<cluster>/.../books/`, linked from the nearest MOC |
| The subject spans two clusters | ask the user; do not guess |
| No cluster fits | the book is out of scope for this vault — say so rather than inventing a cluster |

Every book note needs a hub note that links it (`<Subject> Books.md` or the area MOC). If the hub does not exist, create it and link it from the cluster MOC.

Do not trust the table blindly — list the target folder and read a sibling book note, which is the ground truth for that cluster's tags and hub:

```bash
ls "<target folder>"           # the "<X> Books.md" file in it is the hub
```

4. Pick the **note filename**. It is the book's title in natural language. If a note of that name already exists for a different concept, disambiguate with a ` (Book)` suffix (e.g. `Vibe Engineering (Book).md`) — `title:` in frontmatter still holds the real, undisambiguated title.

## Phase 2: Resolve Metadata

Collect every field below. Do not invent values — leave a field empty rather than guessing.

| Field | Meaning |
|---|---|
| `title` / `subtitle` | as printed on the edition; subtitle empty if there is none |
| `author` | list of authors, one per line |
| `publisher` | publishing house of the edition |
| `total` | page count |
| `isbn` | ISBN-10 of the edition |
| `published` | original publication date of the book (`YYYY`, or `YYYY-MM-DD` when known) |
| `topics` | 2–3 sub-themes, title case — the same style as neighbouring notes in the folder |
| `sources` | one markdown link to the canonical page used (publisher page, Goodreads, O'Reilly, Manning …) |

**OpenLibrary** is the reliable default (no key, no quota):

```bash
curl -s "https://openlibrary.org/search.json?q=<title>+<author>&limit=3&fields=title,subtitle,author_name,first_publish_year,publisher,number_of_pages_median,isbn,subject" | python3 -m json.tool
```

The `isbn` array lists every edition — take a 10-character entry for `isbn`. For one specific edition: `curl -s "https://openlibrary.org/isbn/<isbn>.json"`.

**Google Books** gives cleaner subtitles and page counts but is frequently rate-limited (HTTP 429) from an unkeyed IP — try it, and fall back to OpenLibrary when it returns an error:

```bash
curl -s "https://www.googleapis.com/books/v1/volumes?q=intitle:<title>+inauthor:<author>"
```

For a recent or publisher-exclusive book (Manning MEAP, O'Reilly early release) neither API will have it — `WebFetch` the publisher's own page instead, and use that page as the `sources` link.

Also capture a **one-paragraph description** for the note body. Summarize the publisher blurb in your own words; do not paste marketing copy.

## Phase 3: Determine `coverUrl`

Try these in order and stop at the first that passes validation:

1. **Amazon by ISBN-10** — the vault's dominant pattern, ~300px JPEG. The ISBN must be zero-padded to 10 characters:
   `https://images-na.ssl-images-amazon.com/images/P/<ISBN10>.01._SCRM_SX300_.jpg`
2. **The publisher's own cover image** — for Manning / O'Reilly / MEAP titles that never reach Amazon's image host.
3. **Google Books** — `http://books.google.com/books/content?id=<volumeId>&printsec=frontcover&img=1&zoom=1&source=gbs_api` (the `imageLinks` value from the Phase 2 response).
4. **OpenLibrary** — `https://covers.openlibrary.org/b/isbn/<ISBN>-L.jpg?default=false` (`default=false` makes a missing cover a clean 404 instead of a blank placeholder).

**Validate before committing to a URL:**

```bash
curl -sIL "<coverUrl>" | grep -iE "^HTTP/|content-type:|content-length:"
```

Reject the candidate and move to the next when:
- the status is not `200`, **or**
- `content-type` is not `image/jpeg` or `image/png`, **or**
- `content-length` is under ~5000 bytes.

The Amazon host answers a missing cover with **HTTP 200 and a 43-byte `image/gif`** — it never 404s, so the size check is what catches it.

## Phase 4: Download The Cover Into The Store

The attachment store lives outside the git checkout (it is mounted into the vault at `infra/data/images` by the folderbridge plugin). New book covers go in its `books/` subfolder:

```bash
STORE="infra/data/images"   # the folderbridge mount; see CLAUDE.md > Storing Attachments
```

1. **Check the filename is free across the whole store** — links carry no path, so basenames must be globally unique:

```bash
find "$STORE" -iname "<Note Title>.*"
```

2. **Download**, naming the file exactly after the note filename, keeping the source extension:

```bash
curl -fsSL "<coverUrl>" -o "$STORE/books/<Note Title>.jpg"
```

3. **Verify the bytes are a real image**, not a placeholder or an error page:

```bash
file "$STORE/books/<Note Title>.jpg" && ls -l "$STORE/books/<Note Title>.jpg"
```

Expect `JPEG image data` / `PNG image data` and a size in the tens of kilobytes. A 43-byte GIF or `HTML document text` means the URL was wrong — delete the file and go back to Phase 3.

If every candidate URL fails, tell the user the cover could not be resolved and ask them for one rather than writing a note with a dangling `localCover`.

## Phase 5: Write The Note

Fill the template's placeholders with the resolved values. Full shape:

```yaml
---
tags:
  - <cluster tag>
  - <cluster sub-tag>
created: <now, YYYY-MM-DDTHH:mm>
modified:
published: <original publication date>
sources:
  - "[<page title>](<url>)"
topics:
  - <Sub-Theme One>
  - <Sub-Theme Two>
authors:
ai-assisted: true
hidden:
public:
title: <full title>
subtitle: <subtitle, or empty>
author:
  - <Author Name>
publisher: <publisher>
total: <page count>
isbn: <ISBN-10>
coverUrl: <validated cover URL>
localCover: "[[<Note Title>.jpg]]"
status: unread
book-view: true
---
# <Note Title>
- [<page title>](<url>) by [[<Author Name>]]
> <one-paragraph description of what the book is and argues>
- <optional: why it is in the vault — who recommended it, what it is for>
```

Field rules that are easy to get wrong:

- **`author` is the populated field; `authors` stays empty.** The Book View base orders on `author`. This is the opposite of the generic vault schema and matches ~96 of the existing book notes.
- **`localCover` is a bare filename, never a path** — `"[[East of Eden.jpg]]"`, not `"[[images/books/East of Eden.jpg]]"` (CLAUDE.md attachment rule). It must match the file written in Phase 4 exactly, extension included.
- **`book-view: true`** is what puts the note in the base. Without it the note is invisible there.
- **`status`** is one of `unread` (default), `reading`, `read`. Ask the user if they did not say.
- **`isbn` is written unquoted**, as in the existing notes — YAML then drops a leading zero (`0857197681` → `857197681`). That is expected; keep the zero-padded form in `coverUrl`.
- **`tags`** are the *cluster's* tags (`fin`, `fin/books`; `philosophy`, `philosophy/books`; `personal`, `personal/hobbies`), copied from a sibling book note. There is no generic `book` tag.
- Only the author gets a `[[wiki-link]]` in the body. Do not wiki-link topics, publishers, or concepts mentioned in the description — every link is a graph edge.

## Phase 6: Link It From The Hub

A book note that nothing links to is an orphan. Add it to the `## List` section of the cluster's hub note, following the format already used there — the list styles differ slightly per hub, so match the neighbours:

```markdown
- [[<Note Title>]] by <Author Name>
	- <one-line description>
```

Then confirm the note is reachable:

```bash
obsidian backlinks file="<Note Title>" counts
```

## Output Checklist

- [ ] Note written at the cluster-appropriate path, filename in natural language (` (Book)` suffix only if disambiguation was needed)
- [ ] `title`, `subtitle`, `author`, `publisher`, `total`, `isbn`, `published` filled from a real source — no guessed values
- [ ] `sources` has the canonical page; body has a one-paragraph description in your own words
- [ ] `coverUrl` validated: HTTP 200, image content-type, > 5KB
- [ ] Cover downloaded to `infra/data/images/books/<Note Title>.<ext>`, verified with `file`, basename unique across the store
- [ ] `localCover` is the bare filename and matches the downloaded file
- [ ] `book-view: true`, `status` set, `ai-assisted: true`, `authors` left empty
- [ ] `tags` copied from a sibling book note in the same folder
- [ ] Linked from the cluster hub's `## List`; `obsidian backlinks` confirms it
