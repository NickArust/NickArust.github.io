---
layout: project
title: "Optimizing MTA Transit by Forcasting Ridership"
date: 2025-06-16
excerpt: "I built a dashboard to predict ridership for NYC MTA"
permalink: /personal_projects/transit/
---


# Optimizing Public Transit Routes with NYC MTA Data

New York City’s subway and bus system is one of the busiest in the world, moving millions of people every single day. But like any massive system, it faces challenges: peak-hour congestion, unpredictable demand, and delays that ripple across the network. I wanted to explore whether open data could help make the system run a little smarter.  

---

## Diving into the Data
The MTA provides a treasure trove of open datasets — ridership counts, schedules, turnstile entries, and more. Over the course of this project, I analyzed **over 1 million transit records**, focusing on when and where the biggest bottlenecks occur.  

The first step was **time-series analysis**: identifying daily, weekly, and seasonal patterns. It quickly became clear that rush hours weren’t created equal — some stations consistently spiked 20–30% higher than others during the same time window.  

I also layered in **geospatial analysis** to see which routes consistently funneled too many passengers into already crowded transfer points. By mapping ridership flows across boroughs, I could highlight problem corridors that might benefit most from rerouted buses or additional service frequency.

---

## Building a Predictive Model
Of course, it’s not enough to describe what’s happening now — the real challenge is forecasting what’s coming next. To do this, I trained a **Random Forest regression model** to predict ridership demand at different times and locations.  

The model achieved an **R² score of 0.85**, which gave it strong predictive power for estimating short-term ridership trends. In practical terms, this means the system could anticipate when and where congestion is about to form, allowing planners to proactively adjust schedules or resources.  

---

## Bringing Insights to Life
Raw numbers and CSV files don’t mean much to most people. To make the analysis more accessible, I built an **interactive dashboard using Streamlit**.  

The dashboard lets users:
- Explore ridership data across stations and routes.  
- Visualize congestion hotspots on dynamic maps.  
- Test out “what-if” optimization scenarios, like shifting bus schedules or adding service to underserved lines.  

This way, transportation planners — or even curious commuters — can experiment with the data in real time.

---

## Why This Matters
At its heart, this project wasn’t about writing the flashiest machine learning code. It was about **using data to solve problems that affect everyday life**. Congestion and delays don’t just waste time; they ripple into lost productivity, higher costs, and frustrated communities.  

By combining open data, predictive modeling, and interactive visualization, I showed how data science can offer **concrete, actionable insights** into something as complex and vital as New York City’s transit system.  

And who knows? The next time you catch a train that feels just a little less crowded, maybe a model like this one played a small role behind the scenes.  
