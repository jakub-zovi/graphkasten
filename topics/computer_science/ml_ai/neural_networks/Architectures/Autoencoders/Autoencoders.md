---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-09-30T15:07
modified: 2026-02-15T11:21
published:
sources:
  - "PA228 Machine Learning in Image Processing"
topics:
  - Autoencoders
authors:
ai-assisted:
hidden:
public: true
---
# Autoencoders
![[autoencoder.png]]
Autoencoders are a special kind of neural network used to perform dimensionality reduction. We can think of autoencoders as complex systems composed of two networks, an **encoder** $g$ and a **decoder** $f$.

The encoder learns a non-linear transformation $g:X \to Z$ that projects the data from the original high-dimensional input space $X$ to a lower-dimensional **latent space** $Z$. We call $z = g(x)$ a **latent vector**. A latent vector is a low-dimensional representation of a data point that contains information about $x$. The transformation $g$ should have certain properties; for instance, similar values of $x$ should have similar latent vectors and dissimilar values of $x$ should likewise have dissimilar latent vectors.

A decoder learns a non-linear transformation $f: Z \to X$ that projects the latent vectors back into the original high-dimensional input space $X$. This transformation should take the latent vector $z = g(x)$ and reconstruct the original input data $\hat{x} = f(z) = f(g(x))$.

An autoencoder is just the composition of the encoder and the decoder $F(x) = f(g(x))$. The autoencoder is trained to minimize the difference between the input $x$ and the reconstruction ${x'}$ using a kind of **reconstruction loss**. Because the autoencoder is trained as a whole (we say it's trained "end-to-end"), we optimize the encoder and the decoder simultaneously.
## Topics
- [[Latent space]]
- [[Variational Autoencoders]]
