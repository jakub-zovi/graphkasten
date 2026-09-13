---
tags:
  - cs
  - cs/databases
created: 2024-11-22T15:08
modified: 2025-08-09T11:29
published:
sources: 
topics: 
  - Cypher
  - Graph Query Languages
  - Neo4j
  - Graph Databases
authors:
ai-assisted:
hidden:
public: true
---
Footnote sources: ChatGPT[^1]
# Cypher Query Language
> **Cypher** is the query language used in Neo4j. It is designed for working with graph databases, providing a simple syntax for querying and manipulating data.

### Example: Neo4j Data and Query
#### Sample Data
Imagine a social network with the following:
- Nodes: 
  - `User` nodes: `Alice`, `Bob`, `Charlie`
- Relationships:
  - `Alice FRIENDS_WITH Bob`
  - `Bob FRIENDS_WITH Charlie`

#### Query Example

```cypher
MATCH (a:User {name: "Alice"})-[:FRIENDS_WITH]->(b:User)
RETURN b.name;
```

#### Explanation of the Query
1. **`MATCH`**: Identifies patterns in the graph.
   - `(a:User {name: "Alice"})`: Matches a node labeled `User` with the property `name: "Alice"`.
   - `-[:FRIENDS_WITH]->`: Traverses an outgoing `FRIENDS_WITH` relationship.
   - `(b:User)`: Matches the connected node labeled `User`.
2. **`RETURN`**: Specifies what to retrieve.
   - `b.name`: Returns the `name` property of the connected user.

#### Output
This query would return:
```
Bob
```

[^1]: Prompt: Provide an example of querying this database. And explain the cypher query.