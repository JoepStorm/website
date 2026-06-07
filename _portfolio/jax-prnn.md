---
title: "JAX-PRNN"
date: 2025-07-01
excerpt: "Vectorized, JIT-compiled PRNNs in JAX"
collection: portfolio
tags:
  - Computational mechanics
link: https://github.com/JoepStorm/jax-prnn
header:
    media: "images/projects/jax_prnn.png"

---

### Physically Recurrent Neural Networks using JAX

This is a JAX-based implementation of PRNNs. This version accelerates training and inference time by >10x.

Features:
- Just-In-Time compilation
- Scan function instead of for loop
- Encoder and Decoder run only once per sequence, instead of once per time step
- Einsum notation
- Jupyter notebook that demonstrates a simple PRNN training