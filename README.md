# Pcd-SSM + Clustering for Population-level Hemodynamics

[![Paper](https://img.shields.io/badge/Paper-CMPB%202025-blue)](https://doi.org/10.1016/j.cmpb.2025.108924)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Official implementation of the **deep learning–based Point Cloud Statistical Shape Modeling (Pcd-SSM)** and **unsupervised clustering framework** described in:

> **Expanding point cloud statistical shape model applications: Generalized vascular modeling for population-level hemodynamic simulations**  
> *Yao Zeng, Zheng Sun, Mengfei Wang, Zhuo Li, Ao Liu, Meixiu Pan, Haifeng Zhao, Yuehua Li*  
> *Computer Methods and Programs in Biomedicine, 2025*  
> [DOI:10.1016/j.cmpb.2025.108924](https://doi.org/10.1016/j.cmpb.2025.108924)

---

## 🚀 Overview

Population-scale hemodynamic research often struggles with a trade-off between **computationally expensive patient-specific CFD** and **overly simplified cylindrical models**.  
This repository implements a **tier-and-cluster generalization framework** that integrates:

- **Deep learning Point2SSM** for automatic point correspondence  
- **Point cloud statistical shape modeling (Pcd-SSM) + PCA** for compact shape space  
- **HDBSCAN clustering** to extract geometric subtypes  
- **Cluster mean models** to replace case-by-case CFD in moderate-scale (Tier-2) cohorts  
- **Statistical validation** (MSE, Bootstrap-FDR, Bland–Altman)  

This approach reduces per-case CFD computation by ~**65×** while maintaining **77–95% accuracy** compared with individual simulations.

---

## 🧩 Workflow

<p align="center">
  <img src="docs/figures/paper_02.png" alt="Workflow" width="80%">
</p>

1. **Data preprocessing**  
   - TOF-MRA → segmentation & 3D reconstruction  
   - Export vessel surfaces (STL/point cloud)  
2. **Point2SSM training**  
   - Deep learning model for unsupervised point-to-point correspondences  
3. **Pcd-SSM construction**  
   - PCA-based low-dimensional shape space  
4. **Unsupervised clustering (HDBSCAN)**  
   - Extract cluster mean models representing major geometric subtypes  
5. **CFD simulation**  
   - Steady-state ANSYS Fluent (non-Newtonian Carreau model)  
6. **Statistical analysis**  
   - MSE vs individual CFD, Bootstrap-FDR significance test, Bland–Altman plots  

---

## 📂 Repository Structure

