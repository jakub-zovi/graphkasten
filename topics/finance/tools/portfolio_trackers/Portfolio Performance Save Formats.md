---
tags:
  - fin
  - fin/tools
created: 2026-09-05T11:38
modified: 2026-09-05T12:38
published:
sources:
  - "[File > Save - Save As - Save All](https://help.portfolio-performance.info/en/reference/file/save/)"
  - "[File > Export](https://help.portfolio-performance.info/en/reference/file/export/)"
  - "[Neue Portfolio Datei anlegen](https://help.portfolio-performance.info/de/erste-schritte/intro-neue-portfoliodatei-anlegen/)"
topics:
  - Portfolio Performance
  - Save Formats
  - File Formats
authors:
  - GPT-5
ai-assisted: true
hidden: false
public: true
---
# Portfolio Performance Save Formats
- Portfolio Performance supports three main save options through `File > Save as`: XML, Binary, and Password protected (AES-256) ([Portfolio Performance Manual](https://help.portfolio-performance.info/en/reference/file/save/)).
- The same portfolio can be converted between formats by opening it and using `File > Save as` again ([Portfolio Performance Handbuch](https://help.portfolio-performance.info/de/erste-schritte/intro-neue-portfoliodatei-anlegen/)).
## Topics
- XML Format
	- Placeholder for the human-readable portfolio file format; useful for inspection, backups, and external tooling
- Binary Format
	- Placeholder for the compact and faster format; better default for larger portfolios
- Password Protected AES-256 Format
	- Placeholder for the encrypted binary format; useful when local privacy matters
## Comparison
- XML
	- Advantages
		- Human-readable and inspectable in a text editor
		- Easier to diff, diagnose, and recover manually
		- Can be exported from another Portfolio Performance file through `File > Export > Portfolio Performance XML`
	- Tradeoffs
		- Larger and slower to open/save than binary
		- Not supported by the Portfolio Performance mobile app according to the manual
- Binary
	- Advantages
		- More compact
		- Opens and saves faster, especially for large files
		- Suitable as the practical default for active use
	- Tradeoffs
		- Not human-readable
		- Harder to inspect or manually repair outside the app
- Password protected (AES-256)
	- Advantages
		- Encrypts the portfolio with a password
		- Better for sensitive personal financial data
		- Uses the binary family of formats, so it is relevant for mobile-app usage
	- Tradeoffs
		- Password management becomes critical
		- Not human-readable and less convenient for automation
## Practical Choice
- Use Binary for the main working file.
- Use Password protected (AES-256) if the file is synced, shared across devices, or stored where local privacy matters.
- Use XML as an export/interchange/debug format rather than the daily working format.
