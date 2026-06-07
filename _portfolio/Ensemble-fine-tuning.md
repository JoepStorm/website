---
title: "Ensemble-finetuning for Pluralistic Alignment"
date: 2025-01-01
excerpt: "DAISR competition project - 2nd place project."
collection: portfolio
tags:
  - AI Safety
  - Research
header:
  media: "images/projects/ensemble.png"
---

## Ensemble-finetuning for Pluralistic Alignment

This project was part of the Dutch AI Safety Retreat hackathon, and won 2nd place.

### Motivation
Large Language Models (LLMs) have a set of beliefs learned during training. 
However, humans differ in beliefs on many topics.
This project explored a way to have LLMs express this diversity in a direct way, instead of relying on them picking it up during training.
This is known as pluralistic alignment

### Approach
The method taken was to collect a dataset where many different beliefs were expressed.
The LLM was separately fine-tuned on these multiple subsets.
During inference, all instances ran simultaneously, and differences in their predicted probabilities highlighted differences in beliefs.
These can be picked up quantitatively, and used to influence the model's output. 
This could potentially be done by flagging the prediction, or inserting a template string with the multiple beliefs inserted.
To avoid excessive inference costs, fine-tuning should only be done on the final (few) layers, allowing most of the model to be run once. 

### Demonstration
The outcome was demonstrated on Llama-3.1-8B using LoRA, on a very small hand-created dataset.
The prediction probabilities showed large differences between the models on the topic included in that dataset.
However, false positives were observed, where large disagreements were formed on trivial words.
Future work should work on avoiding these false positives through more precise fine-tuning, on figuring out what to do when a difference in beliefs is detected, and on testing if this scales to more complex real world values.

