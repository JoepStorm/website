---
title: "AI Safety Camp"
date: 2025-03-01
excerpt: "Mechanistic Interpretability Via Learning Differential Equations"
collection: portfolio
tags:
  - AI Safety
  - Research
header:
    media: "images/projects/AISC.png"
---

### Mechanistic Interpretability Via Learning Differential Equations

Mechanistic interpretability aims to uncover the mechanisms through which a neural network model makes predictions.
We investigated a transformer model that learned differential equations, namely ODEFormer, hoping that anything we learned on this medium complexity example might transfer to large language models.
Several techniques from mechanistic interpretability were combined to learn how this model makes predictions.

I developed a [streamlit app](https://odeformer-interp.streamlit.app/) that can be used to investigate the activation patterns throughout the network.
With this, we found a few noteworthy patterns, such as an odd attention pattern seen in the figure below.

<figure>
  <img src="/images/projects/aisc_token.png" alt="Token figure">
  <figcaption>The attention mostly focuses on one token.</figcaption>
</figure>

This token was encoded differently compared to the other tokens.

<figure>
  <img src="/images/projects/aisc_token_norm.png" alt="Token figure" style="width: 60%;">
  <figcaption>The norm of the attended token is significantly lower.</figcaption>
</figure>

This is one of the anomalies that allowed other teams to dive deeper into what causes this behavior.

[Here is a blogpost](https://www.lesswrong.com/posts/qdxNsbY5kYNqcgzFb/mechanistic-interpretability-via-learning-differential) written with more information. 
