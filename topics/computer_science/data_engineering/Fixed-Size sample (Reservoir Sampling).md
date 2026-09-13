---
tags:
  - cs
  - cs/data_eng
created: 2024-12-31T13:11
modified: 2025-08-08T19:04
published:
sources:
  - "PA152 Course"
topics:
  - Reservoir Sampling
  - Stream Sampling
  - Data Streams
authors:
ai-assisted:
hidden:
public: true
---
# Fixed-Size sample (Reservoir Sampling)
## Reservoir Sampling

- **Store** all the first $s$ elements of the stream to $S$.
- Suppose we have seen $n-1$ elements, and now the $n^\text{th}$ element arrives ($n > s$):
  - With probability $\frac{s}{n}$, **keep** the $n^\text{th}$ element; else **discard** it.
  - If we picked the $n^\text{th}$ element, then it **replaces one of the $s$ elements** in the sample $S$, picked uniformly at random

This algorithm maintains a sample $S$ with the desired property:
- After $n$ elements, the sample contains each element seen so far with probability $\frac{s}{n}$.
## Python Implementation

```python
import random
from typing import List, Any

class ReservoirSampler:
    def __init__(self, k: int):
        """
        Initializes the reservoir sampler.
        
        Args:
            k (int): The number of items to maintain in the reservoir.
        """
        self.k = k
        self.reservoir = []
        self.stream_size = 0  # Tracks the number of items processed in the stream
    
    def add_to_reservoir(self, new_item: Any) -> None:
        """
        Processes a new item from the stream and updates the reservoir.
        
        Args:
            new_item (Any): The new item from the stream to process.
        """
        self.stream_size += 1
        
        if len(self.reservoir) < self.k:
            # Fill the reservoir until it reaches size k
            self.reservoir.append(new_item)
        else:
            # Replace an existing item with a decreasing probability
            j = random.randint(1, self.stream_size)
            if j <= self.k:
                self.reservoir[j - 1] = new_item

    def get_reservoir(self) -> List[Any]:
        """
        Returns the current reservoir.
        
        Returns:
            List[Any]: The list of items in the reservoir.
        """
        return self.reservoir
```
