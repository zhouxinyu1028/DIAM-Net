# RAID-Net

## Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation

<p align="center">
  <img src="https://img.shields.io/badge/Status-Available%20Upon%20Request-2ea44f?style=for-the-badge&logo=github&logoColor=white" alt="Status"/>
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/PyTorch-2.3+-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/Datasets-ISIC%202018%20%7C%20Synapse-8A2BE2?style=for-the-badge" alt="Datasets"/>
  <img src="https://img.shields.io/badge/Task-Medical%20Segmentation-1A73E8?style=for-the-badge" alt="Task"/>
  <img src="https://img.shields.io/badge/Framework-PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="Framework"/>
  <img src="https://img.shields.io/badge/Paper-Not%20Published-yellow?style=for-the-badge" alt="Paper Status"/>
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

## Key Metrics

<p align="center">
  <img src="https://img.shields.io/badge/Params-9.59M-007EC6?style=for-the-badge" alt="Params"/>
  <img src="https://img.shields.io/badge/FLOPs-1.95G-FF6B6B?style=for-the-badge" alt="FLOPs"/>
  <img src="https://img.shields.io/badge/ISIC%202018%20Dice-91.60%25-2ea44f?style=for-the-badge" alt="ISIC Dice"/>
  <img src="https://img.shields.io/badge/Synapse%20Dice-84.50%25-2ea44f?style=for-the-badge" alt="Synapse Dice"/>
  <img src="https://img.shields.io/badge/Synapse%20HD95-13.22%20mm-FF6B6B?style=for-the-badge" alt="Synapse HD95"/>
</p>

---

## Network Architecture

The overall architecture of the proposed RAID-Net framework is illustrated in Figure 1.

The model consists of three core components:

- **Semantic-Aware Reliability Interaction (SARI)**
- **Adaptive Multi-Scale Relation Fusion (AMRF)**
- **Semantic-Guided Decoding Enhancement (SGDE)**

---

**Figure 1. Overall architecture of the proposed RAID-Net framework, including the dual-path encoder, SARI, AMRF, and SGDE modules.**

<p align="center">
  <img width="100%" alt="RAID-Net Architecture" src="https://github.com/user-attachments/assets/4ff758a4-43c5-4464-a83d-01d1e5c6981b" />
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

**Table 1. Quantitative comparison on ISIC 2018 dataset.** RAID-Net achieves the highest Dice, IoU, ACC, Spe, and Sen scores with the lowest FLOPs, demonstrating superior segmentation accuracy and computational efficiency.

---

### Qualitative Results — ISIC 2018

**Figure 2. Qualitative segmentation comparisons on ISIC 2018.** RAID-Net demonstrates improved boundary consistency and more accurate lesion recovery, particularly in ambiguous and low-contrast regions.

<p align="center">
  <img width="100%" alt="ISIC 2018 Visualization" src="https://github.com/user-attachments/assets/ec1d24a0-0680-4259-89f5-5c82ac7a2bcf" />
</p>

---

### Cross-Dataset Generalization — ISIC 2017 & PH2

| Train → Test | Methods | Dice (%) | IoU (%) |
|:-------------|:--------|---------:|--------:|
| ISIC 2018 → ISIC 2017 | SVMB-Net | 91.64 | 84.38 |
| | **RAID-Net** | **92.18** | **85.29** |
| ISIC 2018 → PH2 | SVMB-Net | 91.99 | 84.86 |
| | **RAID-Net** | **92.23** | **85.22** |

**Table 2. Cross-dataset generalization performance.** RAID-Net achieves consistent improvements across different data distributions.

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

**Table 3. Quantitative comparison on Synapse dataset.** RAID-Net achieves the lowest HD95 with competitive Dice and significantly lower model complexity.

---

### Qualitative Results — Synapse

**Figure 3. Qualitative segmentation comparisons on Synapse.** RAID-Net demonstrates improved organ boundary consistency and better recovery of small organs.

<p align="center">
  <img width="100%" alt="Synapse Visualization" src="https://github.com/user-attachments/assets/699134db-2c89-4802-9cc3-766850fd4f51" />
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

## 📬 Code & Data Request

For research collaboration and code/data access, please contact:

<p align="center">
  <a href="mailto:zhouxinyu2025@hunnu.edu.cn?subject=RAID-Net%20Code%20%26%20Data%20Request&body=Name:%0AInstitution:%0APurpose:%0A">
    <img src="https://img.shields.io/badge/📧%20Email-zhouxinyu2025@hunnu.edu.cn-1A73E8?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/>
  </a>
</p>

> 📝 Please include your **name**, **institution**, and **intended use** in the email.

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
