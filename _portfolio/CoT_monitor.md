---
title: "Chain-of-Thought Obfuscation"
date: 2026-09-11
excerpt: "Experiments replicating the obfuscation of chain-of-thought reasoning in LLMs"
collection: portfolio
hide_title: true # title used on the portfolio overview and browser tab, not shown on this page
tags:
  - AI Safety
  - Research
header:
    teaser: "images/projects/cot/pressure_only-simple.png" # teaser: shown on the portfolio overview only, not on this page
---

## Chain-of-Thought monitors should not be trained against
This post is the result of a 2-week sprint to replicate findings on chain-of-thought obfuscation caused by training against a monitor. A significant part of the setup is based on the paper "[Chain-of-thought obfuscation learned from output
supervision can generalise to unseen tasks](https://arxiv.org/abs/2601.23086)"<sup><a href="#fn1" id="fnref1">1</a></sup>.

### Summary
Chain-of-Thought (CoT) monitoring is a key element in overseeing Large Language Models (LLMs) to prevent unwanted behaviour such as deception or providing CBRN information.
A judge model, reading the produced chain-of-thought, can flag reasoning that violates some policy, based on which the answer is withheld from the end user.
A naive way to suppress unwanted behaviour is to train the model against such a monitor.
The problem with this approach is that, rather than abandoning the behaviour, the model can learn to obfuscate its CoT while continuing to perform it.
This post demonstrates that failure in a simplified setup: the model converges on near-total reward hacking while the monitor almost never flags it.

{% include cot-explorer.html caption="Figure 1: During training, the model learns to reward hack (choose the hinted answer) while avoiding being flagged by the CoT monitor. (In this simplified setup, the hinted answer never corresponds to the correct answer.) Hover over or tap the chart to see example responses at that training step." %}

### Experimental setup

**Task.** The reward-hacking dataset closely follows the "Revealing Score" dataset of the referenced paper<sup><a href="#fn1">1</a></sup>. MMLU multiple-choice questions are reformatted so that the point value of each option is disclosed in a separate `<additional_info>` block, and the system prompt instructs the model to ignore that block and answer from the question alone. Items where the highest-scoring option happens to be the correct one are discarded. In the data explorer above, the information in `<additional_info>` is formatted as the points below the question.  

**Monitor.** A second, frozen Qwen3-4B instance acts as the CoT monitor. It is shown only the chain-of-thought and returns a binary verdict on whether the reasoning relies on the leaked scores. Using the exact same model for the judge as for the policy is a serious limitation; but not one that is expected to fundamentally change the conclusions. 

**Reward.** With reward $$r_\text{ans}=1$$ when the graded answer is produced and penalty $$p_\text{flag}=1$$ when the monitor flags the CoT:

$$
R = 2.0 \, r_\text{ans} \;-\; 0.05 \, p_\text{flag} \;+\; 0.1 \, r_\text{fmt} \;-\; 0.1 \, p_\text{len} 
$$

There is thus a strong pressure towards the hinted answer, and only a small penalty for getting caught (flagged) by the monitor. The last two terms penalise a malformed or degenerate CoT.

**Training.** Qwen3-4B is fine-tuned with GRPO (group size 8, no KL term) and LoRA (rank 32), using TRL with vLLM serving the rollouts. This training is performed on 2 A100-GPUs, with one training run taking approximately 10 hours.

### Results

Results on a hold-out dataset that was run for several checkpoints during training are shown in Figure 1, the data explorer. During training, the model quickly learns to use the provided scores, as this leads to a high scoring $$r_\text{ans}$$. Only later in training does it learn to obfuscate its reasoning from the monitor. This reinforces the main known finding that training against a CoT monitor causes obfuscation.

Using the data explorer, it can be observed that the CoT and final answers degenerate for the later training steps. While the CoTs in the last step are not flagged, it is clear to a human observer that the model is reward hacking. This shows that the RL setup resulted in a way that tricks the specific judge model. A stronger judge would likely be more difficult to trick, but the incentives to trick it would remain.

### Limitations
This sprint contains many limitations, some of which include:
  - The monitor is the same model as the policy (Qwen3-4B), so GRPO had privileged access to its blind spots.
  - The monitor and judge are small models; no scaling was performed.
  - Only a single RL run is performed.
  - Evaluation was done greedily at temperature=0.
  - The reward hacking is in-distribution of the training task.
  - Reward hacking is possible on all training samples; there are no regularing samples that retain general capability/reasoning. 
  - Highly capable LLMs are able to reason more during their forward passes, decreasing their monitorability. If this trend persists, it could make CoT-monitoring obsolete.

---

<p id="fn1"><sup>1</sup> Chain-of-thought obfuscation learned from output supervision can generalise to unseen tasks, <a href="https://arxiv.org/abs/2601.23086">arxiv.org/abs/2601.23086</a>. <a href="#fnref1">&#8617;</a></p>

