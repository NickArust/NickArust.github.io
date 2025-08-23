---
layout: project
title: "Conway's Game of Life"
date: 2025-07-21
excerpt: "I wrote a simple version of Conway's Game of Life in Python"
permalink: /personal_projects/conway_GOL/
---
# Building a Conway's Game of Life Simulator in Python

Conway’s Game of Life is a classic example of how simple rules can lead to surprisingly complex and beautiful behavior. It’s not really a “game” in the traditional sense — there are no players. Instead, you set up an initial grid of living and dead cells, hit start, and watch as the system evolves according to a few simple rules.  

I decided to build my own version in Python, experimenting with both the **naive cell-by-cell update method** and a faster **convolution-based approach**.  

---

## The Rules of the Game
The Game of Life runs on a grid where each cell is either “alive” (on) or “dead” (off). At every step, each cell updates according to its eight neighbors:  

1. A live cell with fewer than 2 live neighbors dies (underpopulation).  
2. A live cell with 2 or 3 neighbors lives on (survival).  
3. A live cell with more than 3 neighbors dies (overpopulation).  
4. A dead cell with exactly 3 neighbors becomes alive (reproduction).  

That’s it. Out of these four rules, patterns like gliders, oscillators, and chaotic swarms naturally emerge.  

## First pass: naive iteration

I started with the most direct approach: loop over every cell, scan its eight neighbors with two small inner loops, count the live ones, and apply the four Life rules. This version is easy to read and great for validating correctness and boundary behavior. I used **wrap-around (toroidal) edges**, so patterns exiting on one side reappear on the opposite side, and I implemented it by indexing neighbors with modular arithmetic. This first pass is clear and correct, but as the grid grows it becomes the bottleneck (nested loops every frame). 

## Vectorized speedup: convolution for neighbor counts

After validating the naive version, I switched to a vectorized approach that treats neighbor counting as a **stencil** operation. Instead of looping, I define a 3×3 kernel with ones everywhere except the center and use a 2-D convolution to count live neighbors across the entire grid in one shot. With periodic (“wrap”) boundaries, this matches the toroidal world from the naive pass.

```python
# 3x3 neighbor-count kernel (center is 0 to exclude the current cell)
kernel = np.array([[1, 1, 1],
                   [1, 0, 1],
                   [1, 1, 1]])

# Count live neighbors via convolution with wrap-around boundaries
live_neighbors = convolve2d(grid, kernel, mode='same', boundary='wrap')

# Apply Conway's rules with boolean logic (fully vectorized)
new_grid = ((grid == 1) & ((live_neighbors == 2) | (live_neighbors == 3))) | \
           ((grid == 0) & (live_neighbors == 3))
grid = new_grid.astype(int)
```

This change eliminated the nested loops in the hot path and made larger grids feasible at real-time frame rates. The logic is also clearer: “compute neighbors once, apply rules with vectorized boolean expressions.”


## Making it interactive with PyGame

To bring the simulation to life, I built an interface with **PyGame**. Each grid cell is drawn as a square: white for dead, colored for alive. I added a few simple controls to make experimentation fun:

- **Clicking** on the grid toggles cells between alive and dead.  
- Pressing **spacebar** starts or pauses the simulation.  
- Pressing **R** fills the grid with random states.  
- Pressing **Z** clears the grid back to all dead cells.  

I also added a visual cue for the simulation state: when paused, living cells show up in **red**; when running, they switch to **blue**. This made it easy to distinguish “edit mode” from “run mode” at a glance.  

These small touches turned the program from a simple algorithm demo into something interactive and engaging



## Lessons learned

This project reinforced a couple of important lessons about computational problem solving:

- **Naive implementations are useful for clarity.** Writing the cell-by-cell version first made debugging and testing much easier. It gave me confidence that the rules were implemented correctly before trying to optimize.  
- **Optimized methods unlock scale.** Switching to convolution reframed the problem from “loop over cells” to “apply a filter over the whole grid,” which is exactly what numerical libraries like NumPy and SciPy are good at. This reduced the bottleneck dramatically and made real-time simulation smooth even on larger grids.  

---

## Why this matters

Conway’s Game of Life is more than a toy. It’s a classic case study in **emergent complexity**: simple rules leading to unpredictable, fascinating dynamics. It also shows why thinking in terms of **vectorized operations and data-parallel computation** is critical in scientific computing, machine learning, and numerical analysis.  

For me, the project was both fun and a reminder of a key principle: start simple, validate correctness, and then reframe the problem to exploit efficient abstractions.  
