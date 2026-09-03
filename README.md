# RAID-Net

## Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation

<p>
  <img src="https://img.shields.io/badge/Status-Under%20Review-orange?style=flat-square&logo=github&logoColor=white" alt="Status"/>
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/PyTorch-2.3+-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/Datasets-ISIC%202018%20%7C%20Synapse-8A2BE2?style=flat-square" alt="Datasets"/>
  <img src="https://img.shields.io/badge/Task<img width="1379" height="622" alt="image1" src="https://github.com/user-attachments/assets/c29b9924-7d19-423b-ad42-9ddbc942f5f4" />
-Medical%20Segmentation-1A73E8?style=flat-square" alt="Task"/>
</p>

---

## Introduction

This repository corresponds to the paper:

**RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation**

We propose **RAID-Net**, a novel dual-path network for accurate and robust medical image segmentation, addressing key challenges including **boundary ambiguity**, **large scale variations**, and **background interference**.

Unlike conventional single-path networks that couple local visual details with high-level structural semantics in the same information flow, RAID-Net constructs two complementary streams:

- **Semantic Feature Path** — captures local visual details, textures, and boundaries
- **Semantic State Path** — models structural context and cross-layer semantics

By introducing **reliability-aware interaction**, **adaptive multi-scale relation fusion**, and **semantic-guided decoding**, RAID-Net effectively suppresses unreliable feature propagation and improves segmentation accuracy in complex medical scenarios.

---

## Key Contributions

- **Semantic-Aware Reliability Interaction (SARI)** — Dynamically gates cross-path information based on path confidence, regional uncertainty, and cross-path response conflicts, suppressing unreliable feature propagation.

- **Adaptive Multi-Scale Relation Fusion (AMRF)** — Models dependencies across local, regional, contextual, and global scales with content-adaptive scale selection.

- **Semantic-Guided Decoding Enhancement (SGDE)** — Leverages structural semantics to guide decoding and suppress background noise.

- **State-of-the-Art Performance** — Achieves **91.60% Dice** on ISIC 2018 and **84.50% Dice / 13.22 mm HD95** on Synapse with only **9.59M parameters** and **1.95G FLOPs**.

---

## Network Architecture

The overall architecture of the proposed RAID-Net framework is illustrated in Figure 1.

The model consists of three core components:

- Semantic-Aware Reliability Interaction (SARI)
- Adaptive Multi-Scale Relation Fusion (AMRF)
- Semantic-Guided Decoding Enhancement (SGDE)

---

**Figure 1. Overall architecture of the proposed RAID-Net framework, including the dual-path encoder, SARI, AMRF, and SGDE modules.**

<p align="center">
  <img width="1379" height="622" alt="image1" src="https://github.com/user-attachments/assets/cd57bcbf-d15c-45b1-af6c-7f75895ef6f4" />
</p>

---

## Quantitative Comparison with State-of-the-Art Methods

### ISIC 2018 — Skin Lesion Segmentation

| Methods | Dice (%) | IoU (%) | ACC (%) | Spe (%) | Sen (%) | Params (M) | FLOPs (G) |
|:--------|---------:|--------:|--------:|--------:|--------:|-----------:|----------:|
| U-Net | 86.12 | 75.66 | 92.22 | 95.00 | 87.69 | 31.04 | 36.92 |
| AttU-Net | 86.64 | 76.78 | 92.38 | 95.65 | 88.37 | 31.39 | 42.76 |
| Swin-Unet | 89.24 | 81.28 | 94.45 | 96.35 | 91.09 | 27.17 | 6.16 |
| I²U-Net | 89.64 | 82.14 | 95.69 | 96.98 | 91.37 | 7.03 | 2.74 |
| SVMB-Net | 90.86 | 84.24 | 97.32 | 96.73 | 91.95 | 28.60 | 7.95 |
| **RAID-Net (Ours)** | **91.60** | **85.19** | **97.64** | **97.02** | **92.15** | 9.59 | **1.95** |

**Table 1. Quantitative comparison on ISIC 2018 dataset.**

---

### Qualitative Results — ISIC 2018

**Figure 2. Qualitative segmentation comparisons on ISIC 2018.**

<p align="center">
 <img width="1201" height="693" alt="image6" src="https://github.com/user-attachments/assets/a6592c6a-58a6-4a5b-aa1b-c32850985eae" />
</p>

---

### Cross-Dataset Generalization — ISIC 2017 & PH2

| Train → Test | Methods | Dice (%) | IoU (%) |
|:-------------|:--------|---------:|--------:|
| ISIC 2018 → ISIC 2017 | SVMB-Net | 91.64 | 84.38 |
| | **RAID-Net** | **92.18** | **85.29** |
| ISIC 2018 → PH2 | SVMB-Net | 91.99 | 84.86 |
| | **RAID-Net** | **92.23** | **85.22** |

**Table 2. Cross-dataset generalization performance.**

---

### Synapse — Multi-Organ Segmentation

| Methods | Dice (%) | HD95 (mm) | Params (M) | FLOPs (G) |
|:--------|---------:|----------:|-----------:|----------:|
| TransUNet | 77.48 | 31.69 | 105.28 | 24.73 |
| Swin-Unet | 79.13 | 21.55 | 27.17 | 6.16 |
| I²U-Net | 83.22 | 16.82 | 7.03 | 2.74 |
| PSCT-Net | 84.67 | 13.42 | 68.88 | 17.25 |
| MS-GBANet | 84.01 | 13.26 | 54.80 | 14.70 |
| **RAID-Net (Ours)** | **84.50** | **13.22** | 9.59 | **1.95** |

**Table 3. Quantitative comparison on Synapse dataset.**

---

### Qualitative Results — Synapse

**Figure 3. Qualitative segmentation comparisons on Synapse.**

<p align="center">
<img width="1233" height="899" alt="image11" src="https://github.com/user-attachments/assets/cc60ed81-f08b-41e3-917b-2a7f2f81e323" />
</p>

---

## Code & Data Availability

The source code of **RAID-Net** is available upon reasonable request.

The released implementation includes:

- Semantic-Aware Reliability Interaction (SARI)
- Adaptive Multi-Scale Relation Fusion (AMRF)
- Semantic-Guided Decoding Enhancement (SGDE)
- Network construction, loss functions, training and evaluation pipeline

### Datasets

Experiments are conducted on:

- **ISIC 2018** — Skin lesion segmentation
- **ISIC 2017 / PH2** — Cross-dataset generalization
- **Synapse** — Multi-organ abdominal CT segmentation

Due to dataset license restrictions, the original medical images are not redistributed in this repository. Researchers should obtain the datasets from the official sources and follow the corresponding access policies.

---

## Code & Data Request

For research collaboration and code/data access, please contact:

📧 **zhouxinyu2025@hunnu.edu.cn**

Please include your **name**, **institution**, and **intended use** in the email.

---

## Notes

- This project is released for **academic research and non-commercial use only**.
- Redistribution of the datasets is prohibited.
- Please cite our work when using this code.
- Issues and suggestions are welcome.

---

## Citation

If you use this repository in your research, please cite:

```bibtex
@article{zhou2026raidnet,
  title={RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation},
  author={Zhou, Xinyu and ...},
  journal={arXiv preprint},
  year={2026}
}
