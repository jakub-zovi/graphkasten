---
tags:
  - ml_ai
  - ml_ai/neural_nets
created:
modified: 2026-07-21T08:36
published:
sources:
  - "[ROFORMER: ENHANCED TRANSFORMER WITH ROTARY POSITION EMBEDDING](https://arxiv.org/pdf/2104.09864) "
topics:
  - Positional Encodings
authors:
ai-assisted:
hidden:
public: true
---
# Positional Encodings
- Different types of Positional encodings are very well described in [ROFORMER: ENHANCED TRANSFORMER WITH ROTARY POSITION EMBEDDING](https://arxiv.org/pdf/2104.09864) paper.
## List of Encodings Types
###  [[Absolute position embedding]]s (Length-Agnostic):
In the original Transformer architecture, the positional encodings are computed using **sinusoidal functions** as follows:

$$
PE_{(pos, 2i)} = \sin \left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)
$$
$$
PE_{(pos, 2i+1)} = \cos \left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)
$$

Where:
- $pos$ is the position of the token in the sequence.
- $i$ is the dimension of the embedding.
- $d_{\text{model}}$ is the dimension of the model.

Because this formula is deterministic and based on sinusoidal functions, **no additional parameters are learned** to represent positions, and it can naturally generalize to any sequence length. The same pattern can be extended beyond the maximum sequence length it was originally trained with because the positions are just mathematical functions that generalize smoothly.
Thus, in **models using sinusoidal positional encodings**, **nothing special needs to be done** to handle longer sequences. 

### 2. [[Relative position embedding]]s (Length-Limited):
- **TODO:** Refactor this based on ROFORMER paper.

In many variants of Transformer models, including [[BERT]], **positional embeddings are learned** as part of the model’s training process. In these cases, a separate embedding is learned for each possible position in the input sequence, similar to how token embeddings are learned for each token in the vocabulary.

- **Learned positional embeddings** are stored in an embedding matrix, where each row corresponds to a specific position in the sequence.
  - For instance, if the context size is 512 tokens, the positional embedding matrix will have 512 rows (one for each position) and as many columns as the model’s embedding dimension.
  - The model learns specific parameters for each position during training.

The downside of learned positional embeddings is that they are **fixed to the sequence length** used during training. If the model is trained with a maximum context size of 512, it has only learned positional embeddings for positions 0 to 511. When you want to increase the sequence length (e.g., to 1024 or 2048 tokens), there are no learned embeddings for these additional positions. This is why **the positional embedding matrix must be extended** when retraining the model for longer sequences.
### 3. [[Rotary position embedding]]
- **TODO:** Complete this section from [ROFORMER: ENHANCED TRANSFORMER WITH ROTARY POSITION EMBEDDING](https://arxiv.org/pdf/2104.09864).
### 4. [[No Positional Encodings (NOPE)]]
- TODO: Finish this note