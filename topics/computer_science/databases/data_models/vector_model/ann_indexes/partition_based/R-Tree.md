---
tags:
  - cs
  - cs/databases
created: 2024-10-29T14:09
modified: 2025-08-09T11:27
published:
sources:
topics:
  - R-Tree
  - Tree-based Indexes
  - Spatial Indexing
authors:
ai-assisted:
hidden:
public: true
---
# R-Tree
- **Partitioning**: Uses **rectangular bounding boxes (MBRs)** to partition spatial data.
- **Space Coverage**: Only covers the areas occupied by data; not the entire space.
- **Region Overlap**: Yes, overlapping regions are common, leading to possible inefficiencies.
- **Complexity**: Depends on tree height; generally slower in high dimensions due to overlaps.
- **Query Type**: Best suited for **range queries** and **spatial indexing**.
- **Use Case**: Ideal for **geographic information systems (GIS)**, computer graphics, and **dynamic spatial databases**.