---
layout: project
title: "Real-Time Speech Enhancement using Deep Learning"
date: 2025-08-23
excerpt: "I built a speech filtering and enhancement system that runs on a Raspberry Pi"
permalink: /personal_projects/speech/
---

# Real-Time Speech Enhancement System Using Deep Learning

Whether it’s a Zoom call, a podcast recording, or a smart assistant, background noise can make or break the listening experience. I wanted to see if I could push the boundaries of speech clarity by designing a system that not only cleaned up noisy audio, but did it **fast enough to run in real time**.  

---

## The Challenge
Traditional DSP-based noise suppression methods are lightweight, but often fail in complex environments - think crowded cafés, traffic intersections, or multi-speaker scenarios. Deep learning models can achieve much better results, but they usually come with a cost: **large models and high latency** that make them impractical for real-time use on everyday devices.  

My goal was clear:  
- **Improve speech quality significantly** over traditional methods.  
- **Keep latency under 100 milliseconds** so conversations feel natural.  
- **Deploy on resource-constrained devices** like Raspberry Pi or mobile hardware.  

---

## Designing the System
The pipeline started with **100,000+ audio samples** that combined clean speech with realistic background noise (cafés, street noise, office chatter, etc.). After preprocessing and feature extraction, I trained a **denoising autoencoder** in PyTorch, tuned for perceptual quality rather than just raw signal metrics.  

The trained model was then compressed and converted using **TensorFlow Lite (TFLite)** and **ONNX**. By carefully pruning layers and quantizing weights, I managed to reduce the model size by **over 60%** while still preserving performance. This optimization step was crucial for deployment on smaller devices.  

---

## Real-Time Performance
The final system consistently achieved:  
- **30% quality improvement** over baseline DSP methods (measured by PESQ and STOI).  
- **Sub-100ms latency**, making it fast enough for video calls and streaming applications.  

These benchmarks meant the model could handle real-world use cases without lag or distortion.  

---

## From Research to Deployment
One of the most rewarding parts of this project was building the **end-to-end pipeline** - from data preprocessing, to training, to deployment. Instead of stopping at model development, I pushed all the way through to real-world implementation.  

On a Raspberry Pi test device, the model ran efficiently, cleaning up noisy speech while still leaving headroom for other applications. This confirmed that the approach wasn’t just an academic exercise - it was practical, deployable, and impactful.  

---

## Why This Matters
Clear communication is something we take for granted until it breaks down. Whether in telehealth, education, or just a call with friends, poor audio creates barriers.  

This project showed me how **deep learning + optimization can bridge the gap** between cutting-edge research and real-world deployment. By combining modern neural architectures with careful engineering, it’s possible to deliver both **quality and speed** - and make technology more accessible to everyone.  
