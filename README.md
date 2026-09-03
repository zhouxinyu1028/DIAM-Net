# RAID-Net: Reliability-Aware Interactive Dual-Path Network for Medical Image Segmentation

> **面向医学图像分割的可靠性感知交互与自适应多尺度关系融合双路径网络**

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.3.1-ee4c2c.svg)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 📌 Overview

RAID-Net is a novel dual-path network for medical image segmentation, addressing key challenges such as **boundary ambiguity**, **large scale variations**, and **background interference**. It introduces three core modules:

- **SARI**: Semantic-Aware Reliability Interaction — dynamically gates cross-path information flow based on path confidence, regional uncertainty, and cross-path response conflicts.
- **AMRF**: Adaptive Multi-scale Relation Fusion — models dependencies across local, regional, contextual, and global scales, with content-adaptive scale selection.
- **SGDE**: Semantic-Guided Decoding Enhancement — leverages structural semantics from the state path to guide the decoding process and suppress background noise.

RAID-Net achieves **91.60% Dice** on ISIC 2018 and **84.50% Dice / 13.22 mm HD95** on Synapse, with only **9.59M parameters** and **1.95G FLOPs**, balancing accuracy, boundary recovery, and efficiency.

---

## 🧠 Architecture Overview

![RAID-Net Overall Architecture](./docs/fig1_architecture.png)

*Figure 1: Overall architecture of RAID-Net. It consists of a dual-path encoder (Semantic Feature Path & Semantic State Path), a bottleneck with AMRF, and a decoder enhanced by SGDE.*

---

## 🔧 Core Modules

### 1. Semantic-Aware Reliability Interaction (SARI)

SARI estimates path reliability, models cross-path conflicts, and applies gated bidirectional updates to suppress unreliable feature propagation.

![SARI Module](./docs/fig2_sari.png)

*Figure 2: SARI module structure.*

### 2. Adaptive Multi-scale Relation Fusion (AMRF)

AMRF constructs four scale sources (Local, Regional, Context, Global), models their correlations, and adaptively fuses them based on input content.

![AMRF Module](./docs/fig3_amrf.png)

*Figure 3: AMRF module structure.*

### 3. Semantic-Guided Decoding Enhancement (SGDE)

SGDE uses high-level structural semantics to modulate decoder features via detail, shape, and context branches, with residual gating for selective enhancement.

![SGDE Module](./docs/fig4_sgde.png)

*Figure 4: SGDE module structure.*

---

## 📊 Results

### ISIC 2018 (Skin Lesion Segmentation)

| Method       | Dice (%) | IoU (%) | ACC (%) | Spe (%) | Sen (%) | Params (M) | FLOPs (G) |
|--------------|----------|---------|---------|---------|---------|------------|-----------|
| U-Net        | 86.12    | 75.66   | 92.22   | 95.00   | 87.69   | 31.04      | 36.92     |
| Swin-Unet    | 89.24    | 81.28   | 94.45   | 96.35   | 91.09   | 27.17      | 6.16      |
| I²U-Net      | 89.64    | 82.14   | 95.69   | 96.98   | 91.37   | 7.03       | 2.74      |
| SVMB-Net     | 90.86    | 84.24   | 97.32   | 96.73   | 91.95   | 28.60      | 7.95      |
| **RAID-Net** | **91.60**| **85.19**| **97.64**| **97.02**| **92.15**| 9.59      | **1.95**  |

![ISIC 2018 Performance-Complexity](./docs/fig5_isic_complexity.png)

*Figure 5: Performance vs. complexity on ISIC 2018.*

![ISIC 2018 Visualization](./docs/fig6_isic_vis.png)

*Figure 6: Visualization comparisons on ISIC 2018.*

---

### Cross-Dataset Generalization

| Train → Test     | Method       | Dice (%) | IoU (%) |
|------------------|--------------|----------|---------|
| ISIC2018 → 2017  | SVMB-Net     | 91.64    | 84.38   |
|                  | **RAID-Net** | **92.18**| **85.29** |
| ISIC2018 → PH2   | SVMB-Net     | 91.99    | 84.86   |
|                  | **RAID-Net** | **92.23**| **85.22** |

![ISIC 2017 Visualization](./docs/fig7_isic2017_vis.png)
![PH2 Visualization](./docs/fig8_ph2_vis.png)

*Figures 7 & 8: Visualization on ISIC 2017 and PH2.*

---

### Synapse (Multi-Organ Segmentation)

| Method       | Dice (%) | HD95 (mm) | Params (M) | FLOPs (G) |
|--------------|----------|-----------|------------|-----------|
| TransUNet    | 77.48    | 31.69     | 105.28     | 24.73     |
| Swin-Unet    | 79.13    | 21.55     | 27.17      | 6.16      |
| I²U-Net      | 83.22    | 16.82     | 7.03       | 2.74      |
| PSCT-Net     | 84.67    | 13.42     | 68.88      | 17.25     |
| MS-GBANet    | 84.01    | 13.26     | 54.80      | 14.70     |
| **RAID-Net** | **84.50**| **13.22** | 9.59       | **1.95**  |

![Synapse Organ-wise Dice Heatmap](./docs/fig9_synapse_heatmap.png)

*Figure 9: Organ-wise Dice heatmap on Synapse.*

![Synapse Performance-Complexity](./docs/fig10_synapse_complexity.png)

*Figure 10: Performance vs. complexity on Synapse.*

![Synapse Visualization](./docs/fig11_synapse_vis.png)

*Figure 11: Visualization comparisons on Synapse.*

---

## 🧪 Ablation Studies

### Module Contributions (ISIC 2018 / Synapse)

| SARI | AMRF | SGDE | ISIC Dice | ISIC IoU | Synapse Dice | Synapse HD95 |
|------|------|------|-----------|----------|--------------|---------------|
| ✗    | ✗    | ✗    | 89.64     | 82.14    | 83.22        | 16.82         |
| ✓    | ✗    | ✗    | 90.86     | 84.01    | 83.94        | 14.76         |
| ✓    | ✓    | ✓    | **91.60** | **85.19**| **84.50**    | **13.22**     |

![SARI Mechanism Visualization](./docs/fig12_sari_vis.png)
![AMRF Scale Selection](./docs/fig13_amrf_vis.png)
![SGDE Error Maps](./docs/fig14_sgde_vis.png)
![Grad-CAM Analysis](./docs/fig15_gradcam.png)

*Figures 12–15: Ablation visualizations for SARI, AMRF, SGDE, and Grad-CAM analysis.*

---

## 🚀 Getting Started

### Installation

```bash
git clone https://github.com/yourusername/RAID-Net.git
cd RAID-Net
pip install -r requirements.txt
