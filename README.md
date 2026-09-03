# RAID-Net

> **R**eliability-**A**ware **I**nteractive **D**ual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/PyTorch-2.3.1-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License"/>
  <img src="https://img.shields.io/badge/Paper-Not%20Published-yellow?style=for-the-badge" alt="Paper Status"/>
</p>

<p align="center">
  <a href="#-architecture">Architecture</a> •
  <a href="#-results">Results</a> •
  <a href="#-code--data-request">Code & Data</a> •
  <a href="#-citation">Citation</a>
</p>

---

## 📌 Highlights

| Metric | Value |
|:-------|------:|
| **Parameters** | 9.59M |
| **FLOPs** | 1.95G |
| **ISIC 2018 Dice** | **91.60%** |
| **Synapse Dice** | **84.50%** |
| **Synapse HD95** | **13.22 mm** |

---

## 📬 Code & Data Request

For research collaboration and code/data access, please contact:

<p align="center">
  <a href="mailto:zhouxinyu2025@hunnu.edu.cn?subject=RAID-Net%20Code%20%26%20Data%20Request&body=Name:%0AInstitution:%0APurpose:%0A">
    <img src="https://img.shields.io/badge/Email-zhouxinyu2025@hunnu.edu.cn-1A73E8?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/>
  </a>
</p>

> 📝 Please include your **name**, **institution**, and **intended use** in the email.

---

## 🧠 Overview

RAID-Net is a novel **dual-path network** for medical image segmentation that constructs two complementary information streams:

- **Semantic Feature Path** — captures local visual details, textures, and boundaries
- **Semantic State Path** — models structural context and cross-layer semantics

### Core Modules

| Module | Full Name | Function |
|:-------|:----------|:---------|
| **SARI** | Semantic-Aware Reliability Interaction | Dynamically gates cross-path information based on path confidence, regional uncertainty, and cross-path response conflicts |
| **AMRF** | Adaptive Multi-Scale Relation Fusion | Models dependencies across local, regional, contextual, and global scales with content-adaptive scale selection |
| **SGDE** | Semantic-Guided Decoding Enhancement | Leverages structural semantics to guide decoding and suppress background noise |

---

## 🏗️ Architecture

### Overall Network Architecture

<p align="center">
  <img width="100%" alt="RAID-Net Architecture" src="https://github.com/user-attachments/assets/4ff758a4-43c5-4464-a83d-01d1e5c6981b" />
</p>

<p align="center">
  <i>Figure 1: Overall architecture of RAID-Net with dual-path encoder, AMRF bottleneck, and SGDE-enhanced decoder.</i>
</p>

---

## 📊 Results

### ISIC 2018 — Skin Lesion Segmentation

| Method | Dice ↑ | IoU ↑ | ACC ↑ | Spe ↑ | Sen ↑ | Params ↓ | FLOPs ↓ |
|:-------|-------:|------:|------:|------:|------:|---------:|--------:|
| U-Net | 86.12 | 75.66 | 92.22 | 95.00 | 87.69 | 31.04 | 36.92 |
| AttU-Net | 86.64 | 76.78 | 92.38 | 95.65 | 88.37 | 31.39 | 42.76 |
| Swin-Unet | 89.24 | 81.28 | 94.45 | 96.35 | 91.09 | 27.17 | 6.16 |
| I²U-Net | 89.64 | 82.14 | 95.69 | 96.98 | 91.37 | 7.03 | 2.74 |
| SVMB-Net | 90.86 | 84.24 | 97.32 | 96.73 | 91.95 | 28.60 | 7.95 |
| **RAID-Net (Ours)** | **91.60** | **85.19** | **97.64** | **97.02** | **92.15** | 9.59 | **1.95** |

### ISIC 2018 — Visualization

<p align="center">
  <img width="100%" alt="ISIC 2018 Visualization" src="https://github.com/user-attachments/assets/ec1d24a0-0680-4259-89f5-5c82ac7a2bcf" />
</p>

<p align="center">
  <i>Figure 2: Qualitative segmentation results on ISIC 2018 dataset.</i>
</p>

---

### Synapse — Multi-Organ Segmentation

| Method | Dice ↑ | HD95 ↓ | Params ↓ | FLOPs ↓ |
|:-------|-------:|-------:|---------:|--------:|
| TransUNet | 77.48 | 31.69 | 105.28 | 24.73 |
| Swin-Unet | 79.13 | 21.55 | 27.17 | 6.16 |
| I²U-Net | 83.22 | 16.82 | 7.03 | 2.74 |
| PSCT-Net | 84.67 | 13.42 | 68.88 | 17.25 |
| MS-GBANet | 84.01 | 13.26 | 54.80 | 14.70 |
| **RAID-Net (Ours)** | **84.50** | **13.22** | 9.59 | **1.95** |

### Synapse — Visualization

<p align="center">
  <img width="100%" alt="Synapse Visualization" src="https://github.com/user-attachments/assets/699134db-2c89-4802-9cc3-766850fd4f51" />
</p>

<p align="center">
  <i>Figure 3: Qualitative segmentation results on Synapse multi-organ dataset.</i>
</p>

---

## 📝 Citation

If you find this work useful, please cite:

```bibtex
@article{RAIDNet2026,
  title={RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation},
  author={Zhou, Xinyu and ...},
  journal={arXiv preprint},
  year={2026}
}
