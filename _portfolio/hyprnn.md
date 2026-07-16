---
title: "HyPRNN"
date: 2026-05-01
excerpt: "(ongoing) Conditioning a PRNN on microstructure parameters using a hypernetwork"
collection: portfolio
tags:
  - Computational mechanics
  - Research
header:
    media: "images/projects/HyPRNN.png"
---

## Microstructure-Conditioned Surrogate Models for Graded Multiscale Optimization of Mycelium Composites

This work was performed in collaboration with Iuri Rocha, Sarah Schyck, Kunal Masania, and Frans van der Meer.

Multiscale optimization of microstructured sustainable materials needs surrogate models, but training one across a range of microstructures normally demands prohibitive amounts of data. The work solves this by conditioning a hybrid physics-data surrogate on microstructural variables through a hypernetwork, a HyPRNN, which stays accurate on small datasets and is validated against a full FE$^2$ simulation of a mycelium-woodchip composite. Applied to a functionally graded disk it cuts peak stress by 42% versus a random microstructure, and conditioning directly on manufacturing variables extends the approach into a practical route for engineering the microscale to hit target macroscale behavior. 

Link to preprint: <https://arxiv.org/abs/2607.13688> 

GitHub Repository link: <https://github.com/JoepStorm/HyPRNN>

<figure>
  <img src="/images/projects/hyprnn/Overview.png" alt="Overview" style="max-width: 650px; margin: 0 auto;">
  <figcaption>Overview for optimizing a graded multiscale material using a surrogate model conditioned on either microscale or manufacturing variables. </figcaption>
</figure>

## Multiscale optimization

The HyPRNN makes accurate predictions based on only 32 training samples. We validate this in a FE$^2$ simulation
<figure>
  <img src="/images/projects/hyprnn/val_deformation.png" alt="val_deformation" style="max-width: 650px; margin: 0 auto;">
  <figcaption>Multiscale simulations of the ground truth (top left), and various surrogate models. The HyPRNN performs well, even in the low-data regime. </figcaption>
</figure>

With a well-trained surrogate model, we can run multiscale simulations in seconds. This allows for optimizing the microscale variables:

<figure>
  <img src="/images/projects/hyprnn/disk_grading_comparison.png" alt="disk_grading_comparison" style="max-width: 650px; margin: 0 auto;">
  <figcaption>Optimization, made possible by the HyPRNN, leads to a significant reduction in peak stress. </figcaption>
</figure>

## Conditioning on microscale variables

Parametrizing the microstructure is challenging, and some other works resolve this by, for example, training a variational-autoencoder to capture the microstructure, and conditioning on the latent space. We avoid this complexity by instead conditioning directly on manufacturing variables. This is possible by simulating how the manufacturing properties affect the resulting microscale. We do this using a discrete-element simulation. 

<figure class="half">
  <img src="/images/projects/hyprnn/grav_dep_init_0.png" alt="grav_dep_init_0" style="max-width: 200px; margin: 0 auto;">
  <img src="/images/projects/hyprnn/grav_dep_3d_box.png" alt="grav_dep_3d_box" style="max-width: 300px; margin: 0 auto;">
  <figcaption>Optimization, made possible by the HyPRNN, leads to a significant reduction in peak stress. </figcaption>
</figure>

This allows realistic optimization of multiscale simulation, such as to control the macroscopic deformation. 

<figure class="half">
  <img src="/images/projects/hyprnn/grav_dep_baseline.png" alt="grav_dep_baseline" style="max-width: 200px; margin: 0 auto;">
  <img src="/images/projects/hyprnn/grav_dep_optimal_crop.png" alt="grav_dep_optimal_crop" style="max-width: 300px; margin: 0 auto;">
  <figcaption>Macroscale deformation can be controlled; here the goal was to minimize the horizontal deformation of the center hole. </figcaption>
</figure>
