# Pcd-SSM + HDBSCAN Clustering for Population-level Hemodynamics

[![Paper](https://img.shields.io/badge/Paper-CMPB%202025-blue)](https://doi.org/10.1016/j.cmpb.2025.108924)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Official implementation of the **deep learning–based Point Cloud Statistical Shape Modeling (Pcd-SSM)** and **unsupervised clustering framework** described in:

> **Expanding point cloud statistical shape model applications: Generalized vascular modeling for population-level hemodynamic simulations**  
> *Yao Zeng, Zheng Sun, Mengfei Wang, Zhuo Li, Ao Liu, Meixiu Pan, Haifeng Zhao, Yuehua Li*  
> *Computer Methods and Programs in Biomedicine, 2025*  
> [DOI:10.1016/j.cmpb.2025.108924](https://doi.org/10.1016/j.cmpb.2025.108924)

---

## 🚀 Overview

Population-scale hemodynamic studies face a trade-off between **computationally expensive patient-specific CFD** and **overly idealized cylindrical models**.  
This repository provides a **tier-and-cluster generalization framework** integrating:

- Deep learning **Point2SSM** for automatic point correspondence  
- **Point cloud statistical shape modeling (Pcd-SSM) + PCA** for compact shape representation  
- **HDBSCAN clustering** to extract geometric subtypes  
- **Cluster mean models** to replace case-by-case CFD in medium-scale (Tier-2) cohorts  
- **Statistical validation** (MSE, Bootstrap-FDR, Bland–Altman)

⚡ This reduces per-case CFD computation by ~**65×** while maintaining **77–95% accuracy** compared with individual simulations.

---

## 🧩 Methodology & Figures

### Tiered population paradigm — **Fig.1**

<p align="center">
  <img src="docs/figures/fig1_tier_paradigm.png" width="80%" alt="Tier-based paradigm">
</p>

Our study defines three cohort levels:
- **Tier 1:** N ≤ Ncrit (global mean model feasible)  
- **Tier 2:** Ncrit < N < 10³ (high shape heterogeneity, computationally heavy)  
- **Tier 3:** N ≥ 10³ (large-scale, often simplified cylinders)

---

### Proposed workflow — **Fig.2**

<p align="center">
  <img src="docs/figures/fig2_workflow.png" width="90%" alt="Workflow">
</p>

The full pipeline integrates:
1. TOF-MRA data preprocessing & vessel reconstruction  
2. **Point2SSM** training for unsupervised point correspondence  
3. **Pcd-SSM + PCA** to compress shape space  
4. **HDBSCAN clustering** to identify geometric subtypes  
5. **Cluster mean model** generation  
6. CFD simulation & statistical validation

---

### CFD pipeline — **Fig.6**

<p align="center">
  <img src="docs/figures/fig6_cfd_pipeline.png" width="90%" alt="CFD workflow">
</p>

We run **steady-state CFD** with:
- Carreau non-Newtonian blood model  
- Velocity inlet (0.45 m/s), zero-pressure outlet  
- ANSYS Fluent 2022 R2 (coupled solver, residual < 1e-5)

---

### Clustering results — **Fig.9**

<p align="center">
  <img src="docs/figures/fig9_clustering_results.png" width="90%" alt="Clustering results">
</p>

- Pcd-SSM produced **two robust clusters** with 66.7% data participation.  
- Traditional mesh-based SSM had more noise (only 43.3% clustered).  
- Pcd-SSM clusters clearly separate normal vs stenotic ICA morphologies.

---

### Section-wise hemodynamic validation — **Fig.11**

<p align="center">
  <img src="docs/figures/fig11_section_analysis.png" width="90%" alt="Section analysis">
</p>

- Red = Pcd-SSM cluster mean model  
- Blue = ideal cylindrical model  
- Boxplots = individual CFD results  
- Pcd-SSM nearly overlaps with individual median curves for WSS & pressure.

---

### Normal vs stenosed flow fields — **Fig.12**

<p align="center">
  <img src="docs/figures/fig12_normal_vs_stenosis.png" width="90%" alt="Normal vs stenosis">
</p>

- Stenotic cluster: higher velocity peaks (0.88 m/s), sharper pressure drop, and WSS elevation.  
- Normal cluster: smoother velocity and pressure distribution.

---

## 📂 Repository Structure

