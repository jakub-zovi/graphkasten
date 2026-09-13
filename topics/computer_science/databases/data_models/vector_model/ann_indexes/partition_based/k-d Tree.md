---
tags:
  - cs
  - cs/databases
created: 2024-10-29T14:08
modified: 2025-08-09T11:27
published:
sources:
topics:
  - k-d Tree
  - Tree-based Indexes
  - Spatial Indexing
authors:
ai-assisted:
hidden:
public: true
---
# k-d Tree
- **Partitioning**: Uses **axis-aligned hyperplanes**, splitting each dimension alternately.
- **Space Coverage**: Yes, partitions cover the entire space even if data is sparse.
- **Region Overlap**: No, partitions are non-overlapping with clear rectangular boundaries.
- **Complexity**: **O(log n)** for balanced trees; performance degrades with high dimensions.
- **Query Type**: Optimized for **nearest neighbor searches** in low-dimensional data.
- **Use Case**: Common in **computer graphics (ray tracing, collision detection)** and **search algorithms** for static datasets.