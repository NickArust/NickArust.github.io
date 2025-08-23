---
layout: project
title: "Boids"
date: 2025-08-23
excerpt: "I wrote a simple version of the Boids simulation in Python"
permalink: /personal_projects/boids/
---

# Simulating Flocking Behavior with a Boids Model in Python

Flocks of birds, schools of fish, and swarms of insects all move in fascinating, coordinated patterns without any central leader. This kind of **emergent behavior** is one of the most striking examples of complexity arising from simple rules.  

I decided to explore this by building a **Boids simulator** in Python — a program that models flocking behavior using just a handful of simple rules and some math.  

---

## The Idea Behind Boids
The Boids algorithm, first proposed by Craig Reynolds in 1986, is based on three core behaviors:  

1. **Alignment** – Steer towards the average heading of nearby neighbors.  
2. **Cohesion** – Move toward the average position of nearby neighbors.  
3. **Separation** – Avoid crowding by steering away from close neighbors.  

Each "boid" follows these rules locally, but when you simulate hundreds of them together, **realistic flocking patterns emerge naturally**.

---

## Implementation
I built my simulator in **Python** using:  

- **NumPy** for fast vector math  
- **PyGame** for rendering the animation  
- A custom **QuadTree data structure** for efficient neighborhood queries  

With up to 150 boids flying around, a naive all-to-all distance check would have been too slow. By introducing a QuadTree, the simulator reduced the complexity of finding local neighbors, allowing smooth real-time performance at **30 FPS**.  

Key simulation parameters included:  
- Maximum speed: 10 units  
- Maximum acceleration: 2 units  
- Neighborhood radius: 10 units  
- 150 boids initialized with random positions and velocities  

---

## Results
The simulator produces a mesmerizing display of motion. Individual boids move randomly at first, but quickly form **cohesive flocks** that split, merge, and swirl in lifelike patterns.  

The inclusion of separation (with an inverse-square force) prevents collisions, while alignment and cohesion keep the group together. Watching the system evolve shows how **simple local rules can create complex global behavior**.  

I also visualized the QuadTree structure in real time, overlaying faint grid lines on the simulation. This gave an extra layer of insight into how the algorithm partitions space and accelerates neighborhood queries.  

---

## Why This Matters
While this project was built for fun and learning, it connects to real-world applications:  

- **Computer graphics & games**: Flocking is used for crowd simulation, particle systems, and environmental realism.  
- **Robotics & drones**: Swarm robotics uses similar rules for decentralized control.  
- **Scientific computing**: Boids-like models help researchers study collective motion in biology.  

Most importantly, this project reminded me how **powerful simple models can be** when applied thoughtfully. A few lines of code, combined with the right abstractions, can create systems that look surprisingly alive.  

