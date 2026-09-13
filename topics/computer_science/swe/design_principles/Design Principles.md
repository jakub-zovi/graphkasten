---
tags:
  - cs
  - cs/swe
created: 2025-01-08T16:42
modified: 2025-09-23T12:59
published:
sources:
topics:
  - Design Principles
  - Design Patterns
authors:
ai-assisted:
hidden:
public: true
---
# Design Principles
This notes aggregates general software design principles that are applicable across different programming languages and projects.
## List
- [[Dependency Injection & IOC]]
- [[Repository Pattern]]: The Repository pattern provides an `abstraction layer` between the data access logic and the rest of the application. It encapsulates the logic for retrieving, storing, and querying data from a `persistent storage`, such as a database. Repositories expose methods to perform `CRUD (Create, Read, Update, Delete) operations` on the underlying data source, hiding the implementation details and providing a consistent interface for data access.
- [[Unit of Work Pattern]]: The Unit of Work pattern is used to manage the transactional boundaries and coordination of multiple repository operations. It ensures that a group of related operations can be treated as a `single transaction`, either `committing all` changes together or `rolling them back` if an error occurs. In other words, it is an abstraction of a database transaction.