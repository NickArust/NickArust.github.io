---
layout: project
title: "Mixup Barcodes: Quantifying Geometric-Topological Interactions between Point Clouds"
date: 2025-06-04
image: images/mixup_barcode_visualization.png
excerpt: "We propose mixup barcodes, a novel topological descriptor capturing geometric-topological interactions between point clouds, and apply it to analyze disentanglement in neural network embeddings."
permalink: /research_projects/MixupBarcodes/
---

## Abstract

We introduce **mixup barcodes**, a new geometric‐topological descriptor that enriches a standard persistence barcode with image persistent homology information to quantify how one point cloud interacts with another in the same ambient space. For two point clouds \(A\) and \(B\), the mixup barcode of the inclusion \(A \hookrightarrow A \cup B\) records, for each homological feature born in \(A\), how its lifetime shortens when \(B\) is added—capturing notions such as overlap (degree 0), encirclement (degree 1), and surrounding (degree \(n-1\)). We present a practical algorithm for computing mixup barcodes, prove its correctness under simplex-wise filtrations, and demonstrate its utility by analyzing disentanglement in intermediate embeddings of neural networks trained on MNIST and CIFAR-10.



## Methodology

1. **Filtration Setup**  
   - Given two finite point clouds \(A\) and \(B\) in \(\mathbb{R}^d\), construct Vietoris–Rips filtrations  
     \[
       \{\,\mathrm{VR}(A; r_i)\}_{i=1}^n \quad\text{and}\quad \{\,\mathrm{VR}(A \cup B; r_i)\}_{i=1}^n
     \]  
     using a common sorted sequence of radii \(r_1 \le r_2 \le \cdots \le r_n\).  
   - Denote these filtered simplicial complexes by \(L = \bigl\{L_i = \mathrm{VR}(A; r_i)\bigr\}\) and \(K = \bigl\{K_i = \mathrm{VR}(A \cup B; r_i)\bigr\}\).

2. **Mixup Barcode Definition**  
   - Compute the standard persistence barcode of \(H_k(L)\) (persistent homology of \(A\)) and the image persistence barcode of \(H_k(A)\hookrightarrow H_k(A\cup B)\).  
   - Match intervals in both barcodes by their birth index \(b\). For each matched pair \([b,d)\) (in \(H_k(L)\)) and \([b,d')\) (in image persistence), record a **mixup triple** \((b,\,d',\,d)\). Unmatched intervals \([b,d)\) become triples \((b,b,d)\).  
   - Each triple encodes:
     - **Birth** \(b\): index (or filtration value) where a homology class appears in \(A\).  
     - **Image death** \(d'\): index where that class dies in \(A\cup B\) (premature death).  
     - **True death** \(d\): index where it dies in \(A\) alone.  
   - The **mixup sub-bar** is \([d',\,d)\), whose length \(d - d'\) measures how much \(B\) shortens the lifetime of that feature.

3. **Algorithm for Computation**  
   - Form the boundary matrix \(B_K\) of \(K\), ordered by filtration index, then reorder rows so that simplices of \(L\) come before those of \(K\setminus L\).  
   - Derive \(B_L\) by zeroing out rows/columns in \(B_K\) that correspond solely to simplices in \(K\setminus L\).  
   - Apply the standard Gaussian‐elimination‐style reduction to both \(B_L\) (to recover \(\mathrm{PH}(A)\)) and \(B_K\) (to recover image persistence of \(A\hookrightarrow A\cup B\)).  
   - For each \(k\)-simplex \(\sigma\in L\) that births a homology class in \(A\), identify indices \(\tau\) and \(\tau'\) of the simplices that kill that class in \(A\) and in \(A\cup B\), respectively. Record \((\mathrm{birth}=f(\sigma),\,\mathrm{death}'=f(\tau'),\,\mathrm{death}=f(\tau))\).  
   - This yields the mixup barcode in degree \(k\).

4. **Statistical Summaries**  
   - **Mixup** of a triple \((b,d',d)\) is \(\;d - d'\), the length of its mixup sub-bar.  
   - **Total mixup** of \(A\hookrightarrow A\cup B\) is \(\sum_{(b,d',d)} (d - d')\).  
   - **Mixup percentage** of triple \(t\) is  
     \[
       \text{mixup\%}(t) \;=\; \frac{d - d'}{\,d - b\,}\;\in [0,1].
     \]  
   - **Mean mixup percentage** is the average of mixup\% over all triples, giving a scale-invariant measure.

5. **Application to Neural Network Disentanglement**  
   - Train a 5-layer Multi-Layer Perceptron (MLP) on either MNIST (digits 0,1,2) or CIFAR-10 (classes airplane, car, bird) using ReLU activations and MSE loss.  
   - At each training epoch \(t\) and for each hidden layer \(k\), collect the intermediate embeddings of the test set, separately for each label class \(X_{k}^{(q)}\).  
   - For each label \(q\), let  
     \[
       A = X_{k}^{(q)} \quad\text{and}\quad B = \bigcup_{r\ne q} X_{k}^{(r)},
     \]  
     and compute the mixup barcode in degree 0 (connectivity) and degree 1 (loops).  
   - Record the **mixup profile**:  
     \[
       P_{k,t} \;=\; \max_{q}\Bigl\{\text{mean-mixup\%}\bigl(X_{k}^{(q)},\,\bigcup_{r\ne q}X_{k}^{(r)}\bigr)\Bigr\}.
     \]  
   - Subsample \(A\) (500 points) and \(B\) (100 points) via \(k\)-medoids to keep computation tractable while preserving outliers.

## Results

- **MNIST (Digits 0,1,2)**  
  - Pairwise mean mixup percentages in degree 0 are all below 0.01, confirming almost perfect linear separability of digit classes.  
  - The mixup barcode between the “4” and “9” samples (highest among all pairs) shows many short mixup sub-bars, indicative of slight overlaps along shallow interfaces.  
  - **Mixup profiles** across layers and epochs (degree 0 and degree 1) drop rapidly: after a few training steps, all class embeddings become almost entirely disentangled.  

  ![MNIST Mixup Profile (deg 0)](/assets/images/mixup_mnist_deg0.png)  
  _Degree 0 mixup profile on MNIST: the maximum mean-mixup\% across labels falls near zero by layer 3._

  ![MNIST Mixup Profile (deg 1)](/assets/images/mixup_mnist_deg1.png)  
  _Degree 1 mixup profile on MNIST: capturing loops, which also shrink to zero as training progresses._

- **CIFAR-10 (Airplane, Car, Bird)**  
  - Pairwise mean mixup percentages in degree 0 are an order of magnitude higher (up to 0.09 between airplane and deer), reflecting greater topological overlap.  
  - The mixup barcode between “airplane” and “deer” samples reveals longer mixup sub-bars, consistent with more entangled manifolds.  
  - **Mixup profiles** remain high throughout training: degree 0 mixup plateaus near 0.05–0.10, and degree 1 mixup stays nontrivial even after 50 epochs, correlating with the model’s lower test accuracy (~76%).

  ![CIFAR Mixup Profile (deg 0)](/assets/images/mixup_cifar_deg0.png)  
  _Degree 0 mixup profile on CIFAR-10: plateauing at higher values than MNIST, indicating persistent overlaps._

  ![CIFAR Mixup Profile (deg 1)](/assets/images/mixup_cifar_deg1.png)  
  _Degree 1 mixup profile on CIFAR-10: nonzero loops remain, suggesting unresolved entanglements._

- **Key Observations**  
  - **MNIST**: Low mixup in both degrees → embeddings disentangle quickly → high test accuracy.  
  - **CIFAR-10**: Significantly higher mixup → persistent entanglements → lower test accuracy.  
  - Mixup barcodes capture interactions that standard persistence alone would miss (since each class by itself may have nontrivial topology, but entanglement is only revealed when comparing two classes).

## Code & Data

- **Implementation**  
  - The mixup barcode algorithm is implemented within the [Ripserer](https://github.com/Ripserer) framework (extension by Čufar et al.).  
  - Core repository (private until publication):  
    - MATLAB scripts for Vietoris–Rips filtration and boundary matrix construction.  
    - Python/Julia modules wrapping Ripserer for standard and image persistence.  
    - Subsampling via \(k\)-medoids (using scikit-learn’s `KMedoids`).  

- **Experimental Notebooks**  
  - **MNIST Analysis**: Jupyter notebook showing data loading, network training, intermediate embedding extraction, subsampling, and mixup barcode computation.
  - **CIFAR-10 Analysis**: Similar pipeline adapted to CIFAR-10 images 

- **Data**  
  - Original datasets:  
    - MNIST (digits 0,1,2)—preprocessed, available from [Yann LeCun’s repository](http://yann.lecun.com/exdb/mnist/).  
    - CIFAR-10 (classes airplane, car, bird)—available at [https://www.cs.toronto.edu/~kriz/cifar.html](https://www.cs.toronto.edu/~kriz/cifar.html).  
  - Processed point clouds and subsamples are stored in `/data/mixup/{mnist,cifar}/` with separate folders for each layer and epoch.  

## Publication

Wagner, H., Arustamyan, N., Wheeler, M., & Bubenik, P. “Mixup Barcodes: Quantifying Geometric‐Topological Interactions between Point Clouds.” Submitted to **SoCG 2024**; arXiv:2402.15058v2 (December 2024).  
[PDF on arXiv](https://arxiv.org/abs/2402.15058v2)  

---

**Acknowledgments**  
We thank Hubert Wagner for supervision and Matja Čufar for guidance on Ripserer integration. This work was partly supported by NSF Grant DMS-XXXXXXX.
