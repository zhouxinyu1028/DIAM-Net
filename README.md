<h1 align="center" style="font-size: 42px;">RAID-Net</h1>

<h2 align="center" style="font-size: 28px;">Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation</h2>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Under%20Review-orange?style=flat-square&logo=github&logoColor=white" alt="Status"/>
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/PyTorch-2.3+-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/Datasets-ISIC%202018%20%7C%20Synapse-8A2BE2?style=flat-square" alt="Datasets"/>
  <img src="https://img.shields.io/badge/Task-Medical%20Segmentation-1A73E8?style=flat-square" alt="Task"/>
</p>

---

<h3 style="font-size: 28px;">📌 Introduction</h3>

This repository corresponds to the paper:

**RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation**

We propose **RAID-Net**, a novel dual-path network for accurate and robust medical image segmentation, addressing key challenges including **boundary ambiguity**, **large scale variations**, and **background interference**.

Unlike conventional single-path networks that couple local visual details with high-level structural semantics in the same information flow, RAID-Net constructs two complementary streams:

- **Semantic Feature Path** — captures local visual details, textures, and boundaries
- **Semantic State Path** — models structural context and cross-layer semantics

By introducing **reliability-aware interaction**, **adaptive multi-scale relation fusion**, and **semantic-guided decoding**, RAID-Net effectively suppresses unreliable feature propagation and improves segmentation accuracy in complex medical scenarios.

---

<h3 style="font-size: 28px;">🎯 Key Contributions</h3>

- **Semantic-Aware Reliability Interaction (SARI)** — Dynamically gates cross-path information based on path confidence, regional uncertainty, and cross-path response conflicts, suppressing unreliable feature propagation.

- **Adaptive Multi-Scale Relation Fusion (AMRF)** — Models dependencies across local, regional, contextual, and global scales with content-adaptive scale selection.

- **Semantic-Guided Decoding Enhancement (SGDE)** — Leverages structural semantics to guide decoding and suppress background noise.

- **State-of-the-Art Performance** — Achieves **91.60% Dice** on ISIC 2018 and **84.50% Dice / 13.22 mm HD95** on Synapse with only **9.59M parameters** and **1.95G FLOPs**.

---

<h3 style="font-size: 28px;">🏗️ Network Architecture</h3>

The overall architecture of the proposed RAID-Net framework is illustrated in Figure 1.

The model consists of three core components:

- Semantic-Aware Reliability Interaction (SARI)
- Adaptive Multi-Scale Relation Fusion (AMRF)
- Semantic-Guided Decoding Enhancement (SGDE)

---

**Figure 1. Overall architecture of the proposed RAID-Net framework, including the dual-path encoder, SARI, AMRF, and SGDE modules.**

<p align="center">
<img width="1379" height="622" alt="image1" src="https://github.com/user-attachments/assets/29fada49-f2e1-4691-8e2d-931869eb61ec" />
</p>

---

<h3 style="font-size: 28px;">📊 Quantitative Comparison with State-of-the-Art Methods</h3>

<h4 style="font-size: 24px;">ISIC 2018 — Skin Lesion Segmentation</h4>

<table align="center">
  <thead>
    <tr>
      <th align="center">Methods</th>
      <th align="center">Dice (%)</th>
      <th align="center">IoU (%)</th>
      <th align="center">ACC (%)</th>
      <th align="center">Spe (%)</th>
      <th align="center">Sen (%)</th>
      <th align="center">Params (M)</th>
      <th align="center">FLOPs (G)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">U-Net</td>
      <td align="center">86.12</td>
      <td align="center">75.66</td>
      <td align="center">92.22</td>
      <td align="center">95.00</td>
      <td align="center">87.69</td>
      <td align="center">31.04</td>
      <td align="center">36.92</td>
    </tr>
    <tr>
      <td align="center">AttU-Net</td>
      <td align="center">86.64</td>
      <td align="center">76.78</td>
      <td align="center">92.38</td>
      <td align="center">95.65</td>
      <td align="center">88.37</td>
      <td align="center">31.39</td>
      <td align="center">42.76</td>
    </tr>
    <tr>
      <td align="center">Swin-Unet</td>
      <td align="center">89.24</td>
      <td align="center">81.28</td>
      <td align="center">94.45</td>
      <td align="center">96.35</td>
      <td align="center">91.09</td>
      <td align="center">27.17</td>
      <td align="center">6.16</td>
    </tr>
    <tr>
      <td align="center">I²U-Net</td>
      <td align="center">89.64</td>
      <td align="center">82.14</td>
      <td align="center">95.69</td>
      <td align="center">96.98</td>
      <td align="center">91.37</td>
      <td align="center">7.03</td>
      <td align="center">2.74</td>
    </tr>
    <tr>
      <td align="center">SVMB-Net</td>
      <td align="center">90.86</td>
      <td align="center">84.24</td>
      <td align="center">97.32</td>
      <td align="center">96.73</td>
      <td align="center">91.95</td>
      <td align="center">28.60</td>
      <td align="center">7.95</td>
    </tr>
    <tr>
      <td align="center"><b>RAID-Net (Ours)</b></td>
      <td align="center"><b>91.60</b></td>
      <td align="center"><b>85.19</b></td>
      <td align="center"><b>97.64</b></td>
      <td align="center"><b>97.02</b></td>
      <td align="center"><b>92.15</b></td>
      <td align="center">9.59</td>
      <td align="center"><b>1.95</b></td>
    </tr>
  </tbody>
</table>

<p align="center"><b>Table 1. Quantitative comparison on ISIC 2018 dataset.</b></p>

---

<h4 style="font-size: 24px;">🖼️ Qualitative Results — ISIC 2018</h4>

**Figure 2. Qualitative segmentation comparisons on ISIC 2018.**

<p align="center">
<img width="1201" height="693" alt="image6" src="https://github.com/user-attachments/assets/b77f4bab-1835-4a04-b980-2a1e6bb6d5bf" />
</p>

---

<h4 style="font-size: 24px;">🔄 Cross-Dataset Generalization — ISIC 2017 & PH2</h4>

<table align="center">
  <thead>
    <tr>
      <th align="center">Train → Test</th>
      <th align="center">Methods</th>
      <th align="center">Dice (%)</th>
      <th align="center">IoU (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" align="center" valign="middle"><b>ISIC 2018 →<br>ISIC 2017</b></td>
      <td align="center">SVMB-Net</td>
      <td align="center">91.64</td>
      <td align="center">84.38</td>
    </tr>
    <tr>
      <td align="center"><b>RAID-Net (Ours)</b></td>
      <td align="center"><b>92.18</b></td>
      <td align="center"><b>85.29</b></td>
    </tr>
    <tr>
      <td rowspan="2" align="center" valign="middle"><b>ISIC 2018 →<br>PH2</b></td>
      <td align="center">SVMB-Net</td>
      <td align="center">91.99</td>
      <td align="center">84.86</td>
    </tr>
    <tr>
      <td align="center"><b>RAID-Net (Ours)</b></td>
      <td align="center"><b>92.23</b></td>
      <td align="center"><b>85.22</b></td>
    </tr>
  </tbody>
</table>

<p align="center"><b>Table 2. Cross-dataset generalization performance.</b></p>

---

<h4 style="font-size: 24px;">🧬 Synapse — Multi-Organ Segmentation</h4>

<table align="center">
  <thead>
    <tr>
      <th align="center">Methods</th>
      <th align="center">Dice (%)</th>
      <th align="center">HD95 (mm)</th>
      <th align="center">Params (M)</th>
      <th align="center">FLOPs (G)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">TransUNet</td>
      <td align="center">77.48</td>
      <td align="center">31.69</td>
      <td align="center">105.28</td>
      <td align="center">24.73</td>
    </tr>
    <tr>
      <td align="center">Swin-Unet</td>
      <td align="center">79.13</td>
      <td align="center">21.55</td>
      <td align="center">27.17</td>
      <td align="center">6.16</td>
    </tr>
    <tr>
      <td align="center">I²U-Net</td>
      <td align="center">83.22</td>
      <td align="center">16.82</td>
      <td align="center">7.03</td>
      <td align="center">2.74</td>
    </tr>
    <tr>
      <td align="center">PSCT-Net</td>
      <td align="center">84.67</td>
      <td align="center">13.42</td>
      <td align="center">68.88</td>
      <td align="center">17.25</td>
    </tr>
    <tr>
      <td align="center">MS-GBANet</td>
      <td align="center">84.01</td>
      <td align="center">13.26</td>
      <td align="center">54.80</td>
      <td align="center">14.70</td>
    </tr>
    <tr>
      <td align="center"><b>RAID-Net (Ours)</b></td>
      <td align="center"><b>84.50</b></td>
      <td align="center"><b>13.22</b></td>
      <td align="center">9.59</td>
      <td align="center"><b>1.95</b></td>
    </tr>
  </tbody>
</table>

<p align="center"><b>Table 3. Quantitative comparison on Synapse dataset.</b></p>

---

<h4 style="font-size: 24px;">🖼️ Qualitative Results — Synapse</h4>

**Figure 3. Qualitative segmentation comparisons on Synapse.**

<p align="center">
<img width="1233" height="899" alt="image11" src="https://github.com/user-attachments/assets/96d16e04-56ad-4af3-a5ac-a5ccfd51a338" />
</p>

---

<h3 style="font-size: 28px;">💻 Code & Data Availability</h3>

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

<h3 style="font-size: 28px;">📬 Code & Data Request</h3>

For research collaboration and code/data access, please contact:

📧 **zhouxinyu2025@hunnu.edu.cn**

Please include your **name**, **institution**, and **intended use** in the email.

---

<h3 style="font-size: 28px;">📝 Notes</h3>

- This project is released for **academic research and non-commercial use only**.
- Redistribution of the datasets is prohibited.
- Please cite our work when using this code.
- Issues and suggestions are welcome.

---

<h3 style="font-size: 28px;">📄 Citation</h3>

If you use this repository in your research, please cite:

```bibtex
@article{zhou2026raidnet,
  title={RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation},
  author={Zhou, Xinyu and ...},
  journal={arXiv preprint},
  year={2026}
}
