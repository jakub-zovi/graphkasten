---
tags:
  - cs
  - cs/data_eng
created: 2024-10-11T18:44
modified: 2025-10-16T10:49
published:
sources:
topics:
  - MapReduce
  - Distributed Computing
  - Shuffling
  - Narrow and Wide Transformations
authors:
ai-assisted:
hidden:
public: true
---
# Map-Reduce
## Definition
- **Input**: a set of key-value pairs
- Programmer specifies two methods:
  - **Map(k, v)** → ⟨k', v'⟩\*
    - Takes a key-value pair and outputs a set of key-value pairs
      - E.g., key is the filename, value is a single line in the file
    - There is one Map call for every (k, v) pair
  - **Reduce(k', ⟨v'\*⟩)** → ⟨k', v'⟩\*
    - **All values v' with the same key k' are reduced together and processed in v' order**
    - There is one Reduce function call per unique key k'
## Workflow
- **Programmer specifies**:
  - Map and Reduce and input files
- **Workflow**:
  - Read inputs as a set of key-value-pairs
  - **Map** transforms input kv-pairs into a new set of k'v'-pairs
  - **Sorts & Shuffles** the k'v'-pairs to output nodes
  - All k'v'-pairs with a given k' are sent to the same **reduce**
  - **Reduce** processes all k'v'-pairs grouped by key into new k"v"-pairs
  - Write the resulting pairs to files
- **All phases are distributed with many tasks doing the work**
## Data Flow
- **Input and final output** are stored on a distributed file system (FS):
  - Scheduler tries to schedule map tasks "close" to physical storage location of input data
- **Intermediate results** are stored on local FS of Map and Reduce workers
- **Output** is often input to another MapReduce task
## Coordination
- **Master node takes care of coordination**:
  - **Task status**: (idle, in-progress, completed)
  - **Idle tasks** get scheduled as workers become available
  - When a map task completes, it sends the master the location and sizes of its $R$ intermediate files, one for each reducer
  - Master pushes this info to reducers
- **Master pings workers periodically to detect failures**
## Shuffling Operations
In the Map-Reduce paradigm, operations can be categorized into two types based on how data is shuffled between the map and reduce stages: narrow and wide transformations.
### [[Narrow Transformations]]
In a narrow dependency, each partition of the output of a stage depends only on a small subset of partitions from the previous stage. No data shuffling is required across the cluster, as each output partition can be computed from data that resides locally.
Examples:
- Map
- Filter
### [[Wide Transformations]]
In a wide transformation, output partitions depend on data from multiple partitions of the previous stage. This requires shuffling of data between nodes, where data from multiple partitions is transferred across the cluster to be redistributed. This has high cost.
Examples:
- Re-partitioning
- ByKey operations (except counting)
- Joins, the worse being cross joins
- Sorting
- Distinct
- GroupBy
### Summary Shuffling Operations
- Try to group wide transformations together for the best automatic optimization
- Aim for: *narrow, narrow, wide, wide, wide, narrow*
- Avoid: *narrow, wide, narrow, wide, narrow, wide*
- One of the most significant, yet often unavoidable, cause of performance degradation\
- Just because it’s slow, it doesn’t mean that it’s bad (don’t polish the cannon ball)



