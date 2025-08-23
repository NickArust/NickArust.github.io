---
layout: project
title: "Deep Learning for Acoustic Inverse Scattering"
date: 2025-06-04
image: images/equillibira.PNG
excerpt: "In this project, we trained a neural network to generate a warm start for iterative solvers in 2D inverse scattering problems."
permalink: /research_projects/equil/
---
# My First Research Project: Equilibria in Newtonian Systems

My very first research project ended up being published in the *Journal of Mathematical Physics*. It was a collaboration with several faculty and graduate students, and I contributed by writing all the **numerical simulation and plotting code** — in both **Python** and **Macaulay2**, a software system for algebraic geometry and commutative algebra.  

---

## The problem in a nutshell

The paper, *On the Number of Equilibria Balancing Newtonian Point Masses with a Central Force* :contentReference[oaicite:0]{index=0}, asked a deceptively simple question:  

> If you place \(n\) Newtonian point masses in the plane and add a quadratic potential (arising from a centrifugal force), how many equilibrium points can the system have?

Equilibria are critical points of the potential: places where forces cancel out and a test particle would remain at rest. This question is connected to:  
- The **circular restricted \(n+1\)-body problem** in celestial mechanics.  
- **Maxwell’s problem** in electrostatics (point charges).  
- **Gravitational lensing**, where equilibria correspond to the number of images of a lensed star.  

---

## My contribution

My role was to implement and run the simulations that checked the theory against actual computations. This involved two main tools:  

- **Python**: For setting up large-scale numerical experiments, iterating over many parameter values, and producing the plots that appear in the paper.  
- **Macaulay2**: For algebraic computations involving polynomial systems, Gröbner bases, and degree calculations that help bound the number of equilibria.  

This mix of coding and math was my first experience working directly at the boundary of **computational mathematics and theoretical physics**.  

---

## Key results

The team proved several important results:  

- **Finiteness**: For a generic configuration of masses, the number of equilibria is finite.  
- **Lower bound**: There are always at least \(n+1\) equilibria, and this bound is sharp.  
- **Upper bound**: Using algebraic geometry tools, we established an exponential upper bound.  
- **Special configurations**: For ring-shaped arrangements of masses, the system produces at least \(5n-5\) equilibria, agreeing with prior numerical evidence.  

---

## Why this project mattered to me

This was my first real taste of research: taking an abstract math problem and grounding it with computation. I learned how to:  

- Translate mathematical systems into **code that runs experiments**.  
- Use algebraic software like **Macaulay2** alongside more traditional numerical scripting.  
- Collaborate in a research group and contribute code that directly supports new theorems.  

Seeing my name as a coauthor on a published paper — and knowing the simulations I wrote helped verify and illustrate the results — was a formative experience. It showed me how much I enjoy working at the intersection of **mathematics, algorithms, and computation**.  

---

## Reference

Nickolas Arustamyan, Christopher Cox, Erik Lundberg, Sean Perry, and Zvi Rosen.  
[*On the Number of Equilibria Balancing Newtonian Point Masses with a Central Force*](https://arxiv.org/abs/2106.11416). *Journal of Mathematical Physics*, 2021.  
