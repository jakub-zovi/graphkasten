---
tags:
  - cs
  - cs/databases
created: 2024-10-12T14:00
modified: 2026-09-05T20:32
published:
sources:
topics:
  - Structured Data
  - Semi-Structured Data
  - Unstructured Data
  - Data Classification
authors:
ai-assisted:
hidden:
public: true
banner: https://media.geeksforgeeks.org/wp-content/uploads/20250624110439573975/2234.webp
---
# Types of Data
- The data can be split into three types based on their structure: structured, semi-structured, and unstructured data [(LI in VDBMS)](https://is.muni.cz/th/hsfz1/).
## List
- **[[Structured]] data** is a record that follows a strict format and has a predefined schema (e.g. CSV), this type of data is usually handled by relation databases [(NoSQL Distilled)](https://books.google.cz/books?hl=en&lr=&id=AyY1a6-k3PIC&oi=fnd&pg=PR7&dq=NoSQL+Distilled:+A+Brief+Guide+to+the+Emerging+World+of+Polyglot+Persistence&ots=6KupEzFFPd&sig=BLCIjkAWDzq7Pg0l0MxLmFWqmF4&redir_esc=y#v=onepage&q=NoSQL%20Distilled%3A%20A%20Brief%20Guide%20to%20the%20Emerging%20World%20of%20Polyglot%20Persistence&f=false).

- **[[Semi-structured]] data**, also called self-describing, does not contain a pre-defined scheme, but its values contain information about its structure (e.g. JSON, XML); this type of data is handled by different NoSQL databases such as document, graph and column databases [(NoSQL Distilled)](https://books.google.cz/books?hl=en&lr=&id=AyY1a6-k3PIC&oi=fnd&pg=PR7&dq=NoSQL+Distilled:+A+Brief+Guide+to+the+Emerging+World+of+Polyglot+Persistence&ots=6KupEzFFPd&sig=BLCIjkAWDzq7Pg0l0MxLmFWqmF4&redir_esc=y#v=onepage&q=NoSQL%20Distilled%3A%20A%20Brief%20Guide%20to%20the%20Emerging%20World%20of%20Polyglot%20Persistence&f=false).

- **[[Unstructured]] data** has no schema defined nor information about its structure and is, therefore, difficult to handle (e.g. MP4, AVI, JPEG). This type of data is now often handled by vector databases [(LI in VDBMS)](https://is.muni.cz/th/hsfz1/).


> [!info] Note💡
> It is important to understand your data (its type) and the use case and, based on this, to select the appropriate database (data model)!
