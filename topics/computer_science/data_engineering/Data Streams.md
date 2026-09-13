---
tags:
  - cs
  - cs/data_eng
created: 2024-12-30T18:23
modified: 2025-08-08T19:04
published:
sources:
topics:
  - Data Streams
  - Stream Processing
  - Stream Management
authors:
ai-assisted:
hidden:
public: true
---
# Data Streams
- **In many data mining situations, we do not know the entire data set in advance**
- **Stream Management** is important when the input rate is controlled **externally**:
  - Google queries
  - Twitter or Facebook status updates
- We can think of the **data** as **infinite** and **non-stationary** (the distribution changes over time)

## Types of queries one wants on answer on a data stream
  - **[[Sampling data from a stream]]**
    - Construct a random sample
  - **[[Queries over sliding windows]]**
    - Number of items of type **x** in the last **k** elements of the stream
  - **[[Filtering a data stream]]**
    - Select elements with property **x** from the stream
  - **[[Counting distinct elements]]**
    - Number of distinct elements in the last **k** elements of the stream
