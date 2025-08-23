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
# Accelerating Solvers for the Inverse Acoustic Scattering Problem

One of the projects I’ve been working on in my PhD research focuses on a classic but notoriously challenging task: the **inverse acoustic scattering problem**. In simple terms, you send sound waves at an object, measure the scattered waves, and then try to reconstruct the shape of the object that caused them.  

For two-dimensional **sound-soft domains** (think of rigid obstacles that perfectly reflect sound), solving this problem often comes down to iterative optimization. A Newton-like solver can reconstruct the boundary curve of the scatterer, but only if you provide a good initial guess. A poor starting guess means the solver may converge very slowly — or not at all.  

This motivated my central question:  

**Can machine learning provide better initial guesses for Newton solvers, so that convergence is faster and more reliable?**

## From simulation to training data

To explore this, I generated training data by simulating acoustic scattering from a wide variety of known boundary shapes. Each simulation produced **far-field measurements** — essentially, how the wave looks after interacting with the object. By pairing these measurements with the true underlying boundary, I created a dataset that maps “scattered wave → object shape.”  

The input to the learning task was a **360-point far-field magnitude vector**, and the output was a **64-point parameterization of the boundary curve**. This compact representation let the model capture a rich variety of geometries without becoming too high-dimensional.

---

## Neural network design

The predictive model was a **5-layer convolutional neural network** with ReLU activations, built and trained in PyTorch. The setup looked like this:

- **Architecture**: 5 convolutional layers, ReLU activations.  
- **Input**: 360-point far-field magnitude vector.  
- **Output**: 64-point boundary parameterization.  
- **Training**: MSE loss, learning rate 1e-3, batch size 32, trained for 200 epochs.  

This network effectively learned a direct mapping from noisy wave data to plausible obstacle shapes.  


## Curriculum learning: easing the network into the task

One of the main challenges was training the network to generalize across frequencies. Instead of throwing the hardest examples at it from the start, I used a **curriculum learning strategy**: begin with lower frequencies (easier cases) and gradually step up to higher ones (harder cases).  

This curriculum approach gave the network a smoother path during training and improved stability. I experimented with many parameter combinations to test how the model responded:

- **Starting frequency** of the scattered wave data.  
- **Step size** between frequency levels.  
- **Number of epochs** per stage of the curriculum.  
- **Noise levels** in both the simulated data and the inversion process.  
- **Amount of training data** available.  

By systematically varying these parameters, I could see when curriculum learning really made a difference.  

---

## Using predictions to warm-start solvers

Once trained, the network produced a 64-point curve describing the boundary of a scatterer. I then converted this curve into a **mesh in MATLAB**, which served as the **initial guess for a Newton-CG solver**.  

The solver would then refine this guess iteratively until converging to the true boundary. The idea was not to replace the solver but to **give it a head start** with better initialization.  


## Results

The results showed a clear pattern: the **Curriculum Learning Model (CurrNN)** outperformed a baseline model trained without curriculum strategies, especially under tougher conditions.

- With **less data**, CurrNN still produced reliable initial guesses, while the baseline struggled.  
- With **noisier data**, CurrNN maintained robustness, giving usable boundary predictions even when measurements were corrupted.  
- Across multiple parameter settings (frequency schedules, epoch counts, dataset sizes), curriculum training consistently gave the solver better starting points.  

Once passed into the Newton-CG solver, these improved guesses led to **faster convergence** and reduced the risk of stalling in local minima.  

---

## Why this matters

Inverse scattering is a core problem in fields like radar, sonar, and medical imaging. Traditional solvers are powerful but fragile: they rely heavily on the quality of the starting point. By combining **physics-driven solvers** with **data-driven warm starts**, we can get the best of both worlds — the interpretability and rigor of numerical optimization, with the adaptability of machine learning.  

This project demonstrated that **machine learning doesn’t have to replace classical algorithms**. Instead, it can work alongside them to make them faster, more stable, and more practical in real-world scenarios.  

---

## Looking ahead

There’s plenty of room to extend this work:  
- Scaling to three-dimensional domains.  
- Incorporating uncertainty quantification into the predictions.  
- Exploring different architectures or physics-informed networks.  

But even in 2D, these results show that curriculum learning can help machine learning models bridge the gap between raw data and solver-ready initializations — a small step toward making inverse scattering faster and more reliable.  
