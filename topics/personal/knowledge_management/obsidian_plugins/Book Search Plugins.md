---
tags:
  - personal
  - personal/pkm
created: 2026-05-10T00:00
modified: 2026-05-10T00:00
published:
sources:
  - "[anpigon/obsidian-book-search-plugin](https://github.com/anpigon/obsidian-book-search-plugin)"
  - "[DuckTapeKiller/obsidian-book-search-plus](https://github.com/DuckTapeKiller/obsidian-book-search-plus)"
topics:
  - Note Taking
  - Obsidian
  - Community Plugins
  - Book Notes
authors:
  - claude-opus-4-7
ai-assisted: true
hidden:
public: true
human-review: true
---
# Book Search Plugins
- Plugins that streamline creation of book notes by querying external book metadata sources (title, author, publisher, ISBN, cover image) and rendering the result through a customizable template
- Useful for the `finance/resources/books/` and similar reading-list sections of the vault
## List
- [[Book Search Plugin]]
	- [anpigon/obsidian-book-search-plugin](https://github.com/anpigon/obsidian-book-search-plugin)
		- 689 stars
	- Original and most widely used book search plugin
	- Query by title, author, publisher, or ISBN (10/13) via Google Books API (also Naver provider)
	- Customizable template with variables for all book metadata fields and inline scripting
	- Optional cover image download and preview in search results
- [[Book Search Plus]]
	- [DuckTapeKiller/obsidian-book-search-plus](https://github.com/DuckTapeKiller/obsidian-book-search-plus)
		- 16 stars
	- Fork/successor focused on multi-source aggregation
	- Pulls metadata from Google Books, Goodreads, StoryGraph, and Open Library
	- QR/barcode scanning for fast entry, plus local Calibre library integration with batch import and browsing by author/series/tag
	- Handlebars templates, 11-language support, automated duplicate detection
## Setup Guides
- [[Set Up Obsidian Books Search With Google API Key]] ([Link](https://www.zylstra.org/blog/2024/10/set-up-obsidian-books-search-with-google-api-key/))
	- 2024-10-15 — Ton Zijlstra — step-by-step for getting the Google Books API key wired into the plugin
