<img width="1201" height="693" alt="image6" src="https://github.com/user-attachments/assets/213b9813-96ae-4ba0-929f-26626d4222b3" /># RAID-Net

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

### RAID-Net 整体架构

<img width="1379" height="622" alt="image1" src="https://github.com/user-attachments/assets/4ff758a4-43c5-4464-a83d-01d1e5c6981b" />


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



### ISIC 2018 可视化对比

<img width="1201" height="693" alt="image6" src="https://github.com/user-attachments/assets/ec1d24a0-0680-4259-89f5-5c82ac7a2bcf" />

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

### Synapse 实验结果可视化
<img width="1233" height="899" alt="image11" src="https://github.com/user-attachments/assets/699134db-2c89-4802-9cc3-766850fd4f51" />

---


## 📝 引用

```bibtex
@article{RAIDNet2026,
  title={RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation},
  author={Zhou, Xinyu and ...},
  journal={arXiv preprint},
  year={2026}
}
