---
tags:
  - ml_ai
  - ml_ai/neural_nets
created:
modified: 2026-02-15T11:22
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
# Latent space
Imagine that we have a large, high-dimensional dataset, one that consists of thousands of images. Every image  is made up of hundreds of pixels, so each data point has hundreds of dimensions. The **[manifold hypothesis](https://en.wikipedia.org/wiki/Manifold_hypothesis)** states that real-world high-dimensional data actually consists of low-dimensional data that is embedded in the high-dimensional space. This means that, while the actual data itself might have hundreds of dimensions, the underlying structure of the data can be described adequately using only a few dimensions.
  
This is the motivation behind dimensionality reduction techniques, which try to take high-dimensional data and project it onto a lower-dimensional surface. For humans who visualize most things in 2D (or sometimes 3D), this usually means projecting the data onto a 2D surface. Examples of dimensionality reduction techniques include [principal component analysis (PCA)](https://en.wikipedia.org/wiki/Principal_component_analysis) and [t-SNE](https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding). Chris Olah's blog has a [great post](https://colah.github.io/posts/2014-10-Visualizing-MNIST/) reviewing some dimensionality reduction techniques applied to the MNIST dataset.

Neural networks are often used in the **supervised learning** context, where data consists of pairs $(x, y)$ and the network learns a function $f:X \to Y$. This context applies to both regression (where $y$ is a continuous function of $x$) and classification (where $y$ is a discrete label for $x$). However, neural networks have shown considerable power in the **unsupervised learning** context as well, where data just consists of points $x$. There are no "targets" or "labels" $y$. Instead, the goal is to learn and understand the structure of the data. In the case of dimensionality reduction, the goal is to find a low-dimensional representation of the data.