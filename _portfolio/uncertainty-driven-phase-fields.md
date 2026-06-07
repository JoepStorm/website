---
title: "Uncertainty-driven phase fields for hybrid constitutive models"
date: 2025-06-01
excerpt: "Adaptive mixing of physics-based and data-driven models"
collection: portfolio
tags:
  - Computational mechanics
  - Research
header:
  media: "images/projects/perforated_plate.gif"
---

See the publication: [Mixing data-driven and physics-based constitutive models using uncertainty-driven phase fields](https://onlinelibrary.wiley.com/doi/full/10.1002/nme.70162).

This work was performed as part of my PhD, in collaboration with my advisors, Iuri Rocha and Frans van der Meer, as well as in collaboration with WaiChing Sun, whom I got to visit at Columbia University for three months.

### Summary
Surrogate constitutive models in computational mechanics require a lot of data to be accurate, and this data is expensive to compute.
In this work, we use a surrogate model (that is insufficiently trained) when possible, but locally revert back to the high-fidelity ground-truth model when necessary.
This way, accurate simulations are maintained, while the use of the surrogate does lead to real speedups in computation time.
Switching between the surrogate and ground-truth model can cause solver instabilities.
Therefore, we use a phase-field to smoothen this transition.



