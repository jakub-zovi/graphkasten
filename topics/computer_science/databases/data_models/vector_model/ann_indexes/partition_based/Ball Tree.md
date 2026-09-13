---
tags:
  - cs
  - cs/databases
created: 2024-10-29T14:17
modified: 2025-08-09T11:27
published:
sources:
topics:
  - Ball Tree
  - Tree-based Indexes
  - Partition-based Indexes
authors:
ai-assisted:
hidden:
public: true
---
# Ball Tree
- **Partitioning**: Uses **hyperspheres (balls)** to partition data, suited for clusters.
- **Space Coverage**: No, only covers regions where data exists; does not fill the entire space.
- **Region Overlap**: No, uses non-overlapping hyperspheres, although some empty space may remain.
- **Complexity**: **O(log n)** for balanced trees, with better performance than k-d Trees in high dimensions.
- **Query Type**: Suited for **nearest neighbor** and **density-based queries** in high dimensions.
- **Use Case**: Often used in **machine learning**, text/image retrieval, and **high-dimensional clustering** tasks.