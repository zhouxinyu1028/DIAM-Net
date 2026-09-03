# RAID-Net

> Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation

**面向医学图像分割的可靠性感知交互与自适应多尺度关系融合双路径网络**

---

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.3.1-ee4c2c.svg)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

| 指标 | 数值 |
|------|------|
| 参数量 | 9.59M |
| FLOPs | 1.95G |
| ISIC 2018 Dice | **91.60%** |
| Synapse Dice | **84.50%** |
| Synapse HD95 | **13.22 mm** |

---

## 📬 数据和代码申请

**联系邮箱：** [zhouxinyu2025@hunnu.edu.cn](mailto:zhouxinyu2025@hunnu.edu.cn)

请发送邮件标题为"RAID-Net 数据/代码申请"，并附上您的姓名、单位和用途说明。

---

## 📌 概述

RAID-Net 是一种面向医学图像分割的新型双路径网络，通过构建**语义特征路径**和**语义状态路径**两条互补信息流，分别建模局部视觉细节与结构上下文。

**三个核心模块：**

- **SARI** — 语义感知可靠性交互：基于路径置信度、区域不确定性和跨路径响应差异动态调节信息传递
- **AMRF** — 自适应多尺度关系融合：联合建模局部、区域、上下文和全局尺度，根据输入内容动态选择有效尺度
- **SGDE** — 语义引导解码增强：利用语义状态信息引导解码过程，抑制背景噪声

---

## 🧠 网络架构

### 图1：RAID-Net 整体架构

<img width="1379" height="622" alt="image1" src="https://github.com/user-attachments/assets/4ff758a4-43c5-4464-a83d-01d1e5c6981b" />


### 图2：SARI 模块

![SARI 模块](docs/fig2_sari.png)

*可靠性感知的双路径交互*

### 图3：AMRF 模块

![AMRF 模块](docs/fig3_amrf.png)

*自适应多尺度关系融合*

### 图4：SGDE 模块

![SGDE 模块](docs/fig4_sgde.png)

*语义引导解码增强*

---

## 📊 实验结果

### ISIC 2018 皮肤病灶分割

| Method | Dice (%) | IoU (%) | ACC (%) | Spe (%) | Sen (%) | Params (M) | FLOPs (G) |
|--------|----------|---------|---------|---------|---------|------------|-----------|
| U-Net | 86.12 | 75.66 | 92.22 | 95.00 | 87.69 | 31.04 | 36.92 |
| AttU-Net | 86.64 | 76.78 | 92.38 | 95.65 | 88.37 | 31.39 | 42.76 |
| Swin-Unet | 89.24 | 81.28 | 94.45 | 96.35 | 91.09 | 27.17 | 6.16 |
| I²U-Net | 89.64 | 82.14 | 95.69 | 96.98 | 91.37 | 7.03 | 2.74 |
| SVMB-Net | 90.86 | 84.24 | 97.32 | 96.73 | 91.95 | 28.60 | 7.95 |
| **RAID-Net** | **91.60** | **85.19** | **97.64** | **97.02** | **92.15** | 9.59 | **1.95** |

### 图5：ISIC 2018 性能-复杂度对比

![ISIC 性能-复杂度](docs/fig5_isic_complexity.png)

### 图6：ISIC 2018 可视化对比

![ISIC 可视化](docs/fig6_isic_vis.png)

---

### Synapse 多器官分割

| Method | Dice (%) | HD95 (mm) | Params (M) | FLOPs (G) |
|--------|----------|-----------|------------|-----------|
| TransUNet | 77.48 | 31.69 | 105.28 | 24.73 |
| Swin-Unet | 79.13 | 21.55 | 27.17 | 6.16 |
| I²U-Net | 83.22 | 16.82 | 7.03 | 2.74 |
| PSCT-Net | 84.67 | 13.42 | 68.88 | 17.25 |
| MS-GBANet | 84.01 | 13.26 | 54.80 | 14.70 |
| **RAID-Net** | **84.50** | **13.22** | 9.59 | **1.95** |

### 图7-11：Synapse 实验结果可视化

| 图7：器官热力图 | 图8：性能-复杂度 |
|:---:|:---:|
| ![热力图](docs/fig9_synapse_heatmap.png) | ![性能-复杂度](docs/fig10_synapse_complexity.png) |

![Synapse 可视化](docs/fig11_synapse_vis.png)

---

## 🔬 消融实验与可解释性

| 图12：SARI 可视化 | 图13：AMRF 尺度选择 |
|:---:|:---:|
| ![SARI](docs/fig12_sari_vis.png) | ![AMRF](docs/fig13_amrf_vis.png) |

| 图14：SGDE 误差图 | 图15：Grad-CAM |
|:---:|:---:|
| ![SGDE](docs/fig14_sgde_vis.png) | ![Grad-CAM](docs/fig15_gradcam.png) |

---

## 📝 引用

```bibtex
@article{RAIDNet2026,
  title={RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation},
  author={Zhou, Xinyu and ...},
  journal={arXiv preprint},
  year={2026}
}
