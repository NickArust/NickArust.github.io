---
layout: project
title: "Deep Learning for Acoustic Inverse Scattering"
date: 2025-06-04
image: images/nc10_k10+0.1i_0_50_91 (1)-1.png
excerpt: "In this project, we trained a neural network to generate a warm start for iterative solvers in 2D inverse scattering problems."
permalink: /research_projects/CurrNN/
---

## Abstract

The goal of this project was to accelerate convergence of Newton-like solvers for the inverse acoustic scattering problem in two-dimensional sound‐soft domains. We collected training data by simulating scattering on known boundary shapes, then trained a convolutional neural network in PyTorch to predict initial boundary guesses given scattered field data.

## Methodology

1. **Data Generation**  
   - Used MATLAB to generate ground-truth boundary profiles (circles, ellipses, and random shapes).  
   - Simulated far-field data at 360 angles for each boundary.  
   - Saved each sample as a `(boundary, far-field-array)` pair.

2. **Neural Network Architecture**  
   - A 5-layer convolutional network with ReLU activations.  
   - Input: 360-point far-field magnitude vector.  
   - Output: 64-point parameterization of boundary curve.  
   - Trained with MSE loss for 200 epochs, learning rate 1e-3, batch size 32.

3. **Solver Warm Start**  
   - Once the network predicts boundary parameters, we convert them into an initial mesh in MATLAB.  
   - Passed that mesh into a Newton-CG solver to refine until convergence.  
   - Observed a 40% reduction in iteration count vs. random or zero‐fill initialization.

## Results

![Convergence Comparison](/assets/images/convergence_plot.png)

- **Baseline**: 100–120 iterations to reach tolerance.  
- **With NN warm start**: 60–70 iterations.

Quantitatively, the NN initialization reduced mean iteration count from 110 to 65 (± 5).

## Code & Data

- **MATLAB data generator**: [GitHub link](https://github.com/NickArust/inverse-scattering-data).  
- **PyTorch training code**: [GitHub link](https://github.com/NickArust/acoustic-ml-model).

## Publication

Arustamyan, N., Borges, C. “Neural Warm Starts for Inverse Scattering.” _Journal of Computational Physics_, 2024. [DOI link]

