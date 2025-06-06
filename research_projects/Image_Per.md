---
layout: project
title: "Mixup Barcodes: Quantifying Geometric-Topological Interactions between Point Clouds"
date: 2025-06-04
image: images/mixup_barcode_visualization.png
excerpt: "Automated Python pipeline for computing mixup barcodes, generating topological statistics, and visualizations of point-cloud interactions."
permalink: /research_projects/MixupBarcodes/
---

## Project Overview

Mixup barcodes extend standard persistence barcodes by incorporating image-persistence information to measure how one point cloud \(B\) perturbs the homological features of another \(A\).  For each feature born in \(A\), the mixup barcode records its “premature death” when \(B\) is added, yielding quantitative descriptors of overlap, encirclement, and more.  We proved correctness under simplex-wise filtrations, implemented an efficient algorithm compatible with Ripser, and applied it to analyze class-wise disentanglement in neural-network embeddings on MNIST and CIFAR-10.

## My Contribution

I developed the entire end-to-end Python pipeline that automates data ingestion, Ripser integration, and result processing:

1. **Data handling**  
   - Wrote routines to generate example point clouds or accept arbitrary user-provided data.  
   - Converted raw points into the filtration format required by Ripser.

2. **Ripser integration**  
   - Built a command-line script and Python function so users can invoke the pipeline via a simple function call (e.g. `compute_mixup(...)`) or CLI.  
   - Automated feeding of formatted data into the Ripser library for persistence and image-persistence computation.

3. **Result parsing & segmentation**  
   - Parsed Ripser’s output to extract intervals by homological degree (dimension).  
   - Segmented the raw barcodes into standard and image bars for each dimension.

4. **Mixup computation & statistics**  
   - Computed mixup triples \((b,d',d)\) and derived mixup sub-bar lengths for each degree.  
   - Calculated key statistics: mean-mixup %, total mixup %, and overall mixup.

5. **Visualization**  
   - Used Matplotlib (and TensorFlow when processing ML embeddings) to generate all figures in the paper—from mixup barcodes to layer-wise mixup profiles.  
   - Packaged plotting routines so that visuals are produced automatically alongside statistics.

## Pipeline & Usage

- **Implementation**: Python 3 with NumPy, Matplotlib; TensorFlow for embedding examples.  
- **Invocation**:  
  - **Function call**:  
    ```python
    from mixup_pipeline import compute_mixup
    stats, figures = compute_mixup(A, B, degrees=[0,1])
    ```  
  - **CLI**:  
    ```bash
    $ mixup_pipeline --inputA A.csv --inputB B.csv --output-dir results/
    ```  
- **Outputs**:  
  - Structured JSON or CSV of mixup statistics per degree.  
  - Publication-ready PNG and PDF figures for barcodes and mixup profiles.

## Performance

The pipeline executes end-to-end in seconds for typical point-cloud sizes; the only significant time cost is the Ripser calls themselves.  All data formatting, parsing, analysis, and plotting code runs with negligible overhead.

## Code & Repository

A public GitHub repository containing the full pipeline, usage examples, and Jupyter notebooks will be released upon journal acceptance.

## Publication

Wagner, H., Arustamyan, N., Wheeler, M., & Bubenik, P.  
“Mixup Barcodes: Quantifying Geometric-Topological Interactions between Point Clouds.”  
Submitted to SoCG 2024; arXiv:2402.15058v2 (December 2024).  
[PDF on arXiv](https://arxiv.org/abs/2402.15058v2)
