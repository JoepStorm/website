---
title: "LLM-Evolved Digital Art"
date: 2026-02-01
excerpt: "An iterative generative art project where an LLM repeatedly extends a p5.js simulation by one feature at a time, producing increasingly complex visuals."
collection: portfolio
tags:
header:
  iframe: "https://joepstorm.github.io/digital-art/viewer.html?run=run_02&gen=1"
---

A digital art project exploring what happens when you let a language model **incrementally evolve** a generative simulation. Starting from a small set of rules and an initial p5.js sketch, a screenshot is taken 30 seconds into the simulation, and shared with the LLM together with the current code, asking the LLM to add a single feature based on a thematic prompt. The new code, together with a new output screenshot, becomes the input for the next iteration, and the cycle repeats — so each generation builds on the previous version's behaviour and look.

This is similar to <a href="https://github.com/karpathy/autoresearch" target="_blank" rel="noopener">autoresearch</a>, but instead of a hard objective, we aim to incrementally increase beauty and complexity.

Note that all these simulations run locally in your browser.

### Agent-interactions

<div style="position: relative; width: 100%; max-width: 720px; margin: 1.5em auto; aspect-ratio: 16 / 10; border: 1px solid var(--global-border-color); border-radius: 6px; overflow: hidden; background: #000;">
  <iframe
    src="https://joepstorm.github.io/digital-art/viewer.html?run=run_03&gen=16"
    title="LLM-evolved simulation, 'Multi-agent'"
    loading="lazy"
    style="position: absolute; inset: 0; width: 100%; height: 100%; border: 0;"
    allow="autoplay; fullscreen"
    referrerpolicy="no-referrer-when-downgrade"
  ></iframe>
</div>

<p style="text-align: center; font-size: 0.9em;">
  <a href="https://joepstorm.github.io/digital-art/gallery.html?run=run_03" target="_blank" rel="noopener">Browse all iterations of this type.</a> ·
</p>

[//]: # (### Flocking)

[//]: # ()
[//]: # (<div style="position: relative; width: 100%; max-width: 720px; margin: 1.5em auto; aspect-ratio: 16 / 10; border: 1px solid var&#40;--global-border-color&#41;; border-radius: 6px; overflow: hidden; background: #000;">)

[//]: # (  <iframe)

[//]: # (    src="https://joepstorm.github.io/digital-art/viewer.html?run=run_11&gen=02")

[//]: # (    title="LLM-evolved simulation, 'Multi-agent'")

[//]: # (    loading="lazy")

[//]: # (    style="position: absolute; inset: 0; width: 100%; height: 100%; border: 0;")

[//]: # (    allow="autoplay; fullscreen")

[//]: # (    referrerpolicy="no-referrer-when-downgrade")

[//]: # (  ></iframe>)

[//]: # (</div>)

[//]: # ()
[//]: # (<p style="text-align: center; font-size: 0.9em;">)

[//]: # (  <a href="https://joepstorm.github.io/digital-art/gallery.html?run=run_11" target="_blank" rel="noopener">Browse all iterations of this type.</a> ·)

[//]: # (</p>)

### Chaos vs Order

<div style="position: relative; width: 100%; max-width: 720px; margin: 1.5em auto; aspect-ratio: 16 / 10; border: 1px solid var(--global-border-color); border-radius: 6px; overflow: hidden; background: #000;">
  <iframe
    src="https://joepstorm.github.io/digital-art/viewer.html?run=run_07&gen=01"
    title="LLM-evolved simulation, 'Multi-agent'"
    loading="lazy"
    style="position: absolute; inset: 0; width: 100%; height: 100%; border: 0;"
    allow="autoplay; fullscreen"
    referrerpolicy="no-referrer-when-downgrade"
  ></iframe>
</div>

<p style="text-align: center; font-size: 0.9em;">
  <a href="https://joepstorm.github.io/digital-art/gallery.html?run=run_07" target="_blank" rel="noopener">Browse all iterations of this type.</a> ·
</p>

### About

- **Live viewer (click a snapshot to run that simulation):** <https://joepstorm.github.io/digital-art/gallery.html?run=run_03>
- **GitHub output website:** <https://github.com/JoepStorm/digital-art>
