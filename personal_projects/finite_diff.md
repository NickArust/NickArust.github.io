---
layout: project
title: "Finite Difference for Laplace Equation"
date: 2025-06-16
excerpt: "In this project, I built a finite difference solver for the Laplace equation using C++"
permalink: /personal_projects/finite_diff/
---

# Solving the Poisson Equation in C++

As part of exploring numerical methods in scientific computing, I implemented a **Poisson solver in C++**. The goal was to solve the 2D equation

\[
-\Delta u(x, y) = f(x, y), \quad (x,y) \in [0,1]^2
\]

with zero boundary conditions and a known exact solution for validation.  

---

## The problem setup

I chose a smooth, well-behaved test case so that the solution could be checked against an exact formula:

- **Exact solution**:  
  \[
  u(x, y) = \sin(\pi x)\sin(\pi y)
  \]

- **Right-hand side**:  
  \[
  f(x, y) = -2\pi^2 \sin(\pi x)\sin(\pi y)
  \]

This setup is standard in numerical PDE testing: the forcing term is constructed from the Laplacian of the exact solution, which gives a clear way to measure numerical error.  

---

## Numerical method: Jacobi iteration

I implemented the **Jacobi iterative method**, one of the simplest relaxation schemes for elliptic PDEs. At each step, the algorithm updates interior grid points using the average of their four neighbors plus the effect of the source term.  

Key implementation details:  
- Uniform grid of size \(n \times n\).  
- Step size \(h = 1/(n-1)\).  
- Iteration stops once the maximum update difference is below a tolerance.  
- Boundary values fixed at zero (Dirichlet conditions).  

This method is not the fastest compared to Gauss–Seidel or multigrid, but it’s easy to implement and a good baseline solver.  

---

## Implementation highlights

- **Grid abstraction**: I wrote a `Grid` class to handle indexing and swapping between current and new solution states.  
- **Jacobi solver**: Loops over interior points, updating values based on neighbors and the right-hand side.  
- **Error computation**: After convergence, I compute both **maximum error** and **L2 error** against the analytical solution.  
- **Visualization**: The final solution is written out as a grayscale PNG using the `stb_image_write` library. This makes it easy to “see” the solution surface.  

---

## Results

On a 100×100 grid, the solver converges to a solution with:  

- Small maximum error (on the order of 1e-3 depending on tolerance).  
- L2 error that decreases as grid resolution increases.  

The output image clearly shows the smooth sinusoidal shape of the solution, matching the exact function \( \sin(\pi x)\sin(\pi y) \).  

---

## Why this matters

The Poisson equation underlies countless problems in physics and engineering: heat diffusion, electrostatics, fluid dynamics, and more. Writing a solver from scratch helped me see how numerical PDE methods work at the lowest level: discretization, iteration, and error analysis.  

This project also reinforced an important workflow in scientific computing:  
1. Start with a **test problem** that has a known exact solution.  
2. Implement a solver and validate it by measuring numerical error.  
3. Add features like visualization to better understand results.  

---

## Next steps

Some natural extensions include:  
- Replacing Jacobi with faster iterative methods (Gauss–Seidel, SOR, conjugate gradient).  
- Implementing **multigrid acceleration** for efficiency.  
- Parallelizing the solver with OpenMP or CUDA for larger grids.  

Even in its basic form, this project gave me a solid hands-on foundation in PDE solvers and how they connect to both theory and applications.  
