<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>RAID-Net: 医学图像分割双路径网络</title>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        /* ===== 全局重置 ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Roboto, system-ui, -apple-system, sans-serif;
            background: #f8fafc;
            color: #0f172a;
            line-height: 1.6;
            padding: 2rem 1.5rem;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: #ffffff;
            border-radius: 2rem;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.08);
            padding: 2.5rem 3rem;
        }
        @media (max-width: 768px) {
            body { padding: 1rem; }
            .container { padding: 1.5rem; }
        }

        /* ===== 头部 ===== */
        .header {
            text-align: center;
            padding-bottom: 2rem;
            border-bottom: 2px solid #eef2f6;
        }
        .header h1 {
            font-size: 2.6rem;
            font-weight: 700;
            background: linear-gradient(135deg, #1e293b, #3b82f6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: -0.02em;
        }
        .header .subtitle {
            font-size: 1.2rem;
            color: #475569;
            margin-top: 0.3rem;
            font-weight: 400;
        }
        .header .chinese {
            font-size: 1.0rem;
            color: #64748b;
            margin-top: 0.2rem;
        }
        .badges {
            margin-top: 1rem;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 0.6rem;
        }
        .badge {
            background: #eef2f6;
            padding: 0.3rem 1rem;
            border-radius: 30px;
            font-size: 0.85rem;
            font-weight: 500;
            color: #1e293b;
            display: inline-flex;
            align-items: center;
            gap: 0.4rem;
        }
        .badge i { color: #3b82f6; }

        /* ===== 申请入口 ===== */
        .apply-box {
            background: linear-gradient(135deg, #eff6ff, #dbeafe);
            border: 2px dashed #3b82f6;
            border-radius: 1.2rem;
            padding: 1.2rem 2rem;
            margin: 1.8rem 0 2rem 0;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
        }
        .apply-box .left {
            display: flex;
            align-items: center;
            gap: 1rem;
        }
        .apply-box .left i {
            font-size: 2rem;
            color: #2563eb;
        }
        .apply-box .left span {
            font-weight: 600;
            font-size: 1.05rem;
        }
        .apply-box .left small {
            display: block;
            color: #475569;
            font-weight: 400;
            font-size: 0.9rem;
        }
        .apply-box .right {
            display: flex;
            align-items: center;
            gap: 1rem;
        }
        .apply-box .right .email {
            background: white;
            padding: 0.5rem 1.2rem;
            border-radius: 40px;
            font-weight: 500;
            color: #1e293b;
            box-shadow: 0 2px 8px rgba(0,0,0,0.04);
        }
        .apply-btn {
            background: #1e293b;
            color: white;
            border: none;
            padding: 0.6rem 1.8rem;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.2s;
            font-size: 0.95rem;
        }
        .apply-btn:hover {
            background: #0f172a;
            transform: scale(1.02);
        }

        /* ===== 通用 ===== */
        h2 {
            font-size: 1.8rem;
            font-weight: 600;
            margin: 2.5rem 0 1.2rem 0;
            padding-bottom: 0.5rem;
            border-bottom: 3px solid #e2e8f0;
            display: flex;
            align-items: center;
            gap: 0.6rem;
        }
        h2 i { color: #3b82f6; }
        h3 {
            font-size: 1.3rem;
            font-weight: 600;
            margin: 1.8rem 0 0.8rem 0;
            color: #1e293b;
        }
        .highlight {
            background: #f1f5f9;
            padding: 0.1rem 0.5rem;
            border-radius: 6px;
            font-weight: 600;
            color: #0f172a;
        }

        /* ===== 图片区 ===== */
        .figure-block {
            background: #fafbfc;
            border-radius: 1.2rem;
            padding: 1.5rem;
            margin: 1.5rem 0;
            text-align: center;
            border: 1px solid #e9edf2;
        }
        .figure-block img {
            max-width: 100%;
            height: auto;
            border-radius: 0.8rem;
            box-shadow: 0 4px 16px rgba(0,0,0,0.05);
        }
        .figure-block .caption {
            margin-top: 0.6rem;
            font-size: 0.95rem;
            color: #475569;
        }
        .figure-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1.5rem;
        }
        @media (max-width: 768px) {
            .figure-grid { grid-template-columns: 1fr; }
        }

        /* ===== 表格 ===== */
        .table-wrap {
            overflow-x: auto;
            margin: 1.2rem 0;
            border-radius: 1rem;
            border: 1px solid #e9edf2;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.9rem;
        }
        th {
            background: #f1f5f9;
            font-weight: 600;
            padding: 0.7rem 0.8rem;
            text-align: center;
            border-bottom: 2px solid #d1d9e6;
        }
        td {
            padding: 0.6rem 0.8rem;
            text-align: center;
            border-bottom: 1px solid #e9edf2;
        }
        tr:last-child td { border-bottom: none; }
        .highlight-row td {
            background: #eff6ff;
            font-weight: 600;
        }
        .highlight-row td:first-child {
            border-left: 4px solid #3b82f6;
        }

        /* ===== 页脚 ===== */
        .footer {
            margin-top: 3rem;
            padding-top: 1.5rem;
            border-top: 2px solid #eef2f6;
            text-align: center;
            color: #94a3b8;
            font-size: 0.9rem;
        }
        .footer a {
            color: #3b82f6;
            text-decoration: none;
        }

        /* ===== 响应式 ===== */
        @media (max-width: 640px) {
            .apply-box {
                flex-direction: column;
                align-items: stretch;
                gap: 1rem;
            }
            .apply-box .right {
                flex-wrap: wrap;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
<div class="container">

    <!-- ===== HEADER ===== -->
    <header class="header">
        <h1>RAID-Net</h1>
        <div class="subtitle">
            Reliability-Aware Interactive Dual-Path Network<br/>
            with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation
        </div>
        <div class="chinese">
            <i class="fas fa-language"></i> 面向医学图像分割的可靠性感知交互与自适应多尺度关系融合双路径网络
        </div>
        <div class="badges">
            <span class="badge"><i class="fas fa-microchip"></i> 9.59M Params</span>
            <span class="badge"><i class="fas fa-bolt"></i> 1.95G FLOPs</span>
            <span class="badge"><i class="fas fa-heartbeat"></i> 91.60% Dice (ISIC 2018)</span>
            <span class="badge"><i class="fas fa-brain"></i> 84.50% Dice (Synapse)</span>
            <span class="badge"><i class="fas fa-code-branch"></i> PyTorch 2.3.1</span>
        </div>
    </header>

    <!-- ===== 数据/代码申请 ===== -->
    <div class="apply-box">
        <div class="left">
            <i class="fas fa-envelope-open-text"></i>
            <div>
                <span>📬 数据和代码申请</span>
                <small>论文尚未正式发表，欢迎学术交流</small>
            </div>
        </div>
        <div class="right">
            <span class="email"><i class="fas fa-at"></i> zhouxinyu2025@hunnu.edu.cn</span>
            <button class="apply-btn" onclick="window.location.href='mailto:zhouxinyu2025@hunnu.edu.cn?subject=RAID-Net 数据/代码申请&body=姓名：%0A单位：%0A用途：%0A'">
                <i class="fas fa-paper-plane"></i> 发送申请
            </button>
        </div>
    </div>

    <!-- ===== 1. 概述 ===== -->
    <h2><i class="fas fa-flag"></i> Overview</h2>
    <p>
        <strong>RAID-Net</strong> 是一种面向医学图像分割的新型双路径网络，通过构建
        <span class="highlight">语义特征路径</span> 和 <span class="highlight">语义状态路径</span>
        两条互补信息流，分别建模局部视觉细节与结构上下文。
        它引入三个核心模块：
    </p>
    <ul style="margin: 0.8rem 0 0 1.8rem; color: #334155;">
        <li><strong>SARI</strong> — 语义感知可靠性交互：基于路径置信度、区域不确定性和跨路径响应差异动态调节信息传递。</li>
        <li><strong>AMRF</strong> — 自适应多尺度关系融合：联合建模局部、区域、上下文和全局尺度，根据输入内容动态选择有效尺度。</li>
        <li><strong>SGDE</strong> — 语义引导解码增强：利用语义状态信息引导解码过程，抑制背景噪声。</li>
    </ul>

    <!-- ===== 2. 架构 ===== -->
    <h2><i class="fas fa-sitemap"></i> Architecture</h2>
    <div class="figure-block">
        <img src="docs/fig1_architecture.png" alt="RAID-Net整体架构" />
        <div class="caption"><strong>图1：</strong> RAID-Net 整体网络结构（U形编码-瓶颈-解码框架）</div>
    </div>

    <div class="figure-grid">
        <div class="figure-block">
            <img src="docs/fig2_sari.png" alt="SARI模块" />
            <div class="caption"><strong>图2：</strong> SARI 模块结构</div>
        </div>
        <div class="figure-block">
            <img src="docs/fig3_amrf.png" alt="AMRF模块" />
            <div class="caption"><strong>图3：</strong> AMRF 模块结构</div>
        </div>
        <div class="figure-block" style="grid-column: 1 / -1;">
            <img src="docs/fig4_sgde.png" alt="SGDE模块" />
            <div class="caption"><strong>图4：</strong> SGDE 模块结构</div>
        </div>
    </div>

    <!-- ===== 3. 实验结果 ===== -->
    <h2><i class="fas fa-chart-bar"></i> Experimental Results</h2>

    <h3>📌 ISIC 2018 皮肤病灶分割</h3>
    <div class="table-wrap">
        <table>
            <thead><tr>
                <th>Method</th><th>Dice (%)</th><th>IoU (%)</th><th>ACC (%)</th><th>Spe (%)</th><th>Sen (%)</th><th>Params (M)</th><th>FLOPs (G)</th>
            </tr></thead>
            <tbody>
                <tr><td>U-Net</td><td>86.12</td><td>75.66</td><td>92.22</td><td>95.00</td><td>87.69</td><td>31.04</td><td>36.92</td></tr>
                <tr><td>AttU-Net</td><td>86.64</td><td>76.78</td><td>92.38</td><td>95.65</td><td>88.37</td><td>31.39</td><td>42.76</td></tr>
                <tr><td>Swin-Unet</td><td>89.24</td><td>81.28</td><td>94.45</td><td>96.35</td><td>91.09</td><td>27.17</td><td>6.16</td></tr>
                <tr><td>I²U-Net</td><td>89.64</td><td>82.14</td><td>95.69</td><td>96.98</td><td>91.37</td><td>7.03</td><td>2.74</td></tr>
                <tr><td>SVMB-Net</td><td>90.86</td><td>84.24</td><td>97.32</td><td>96.73</td><td>91.95</td><td>28.60</td><td>7.95</td></tr>
                <tr class="highlight-row"><td><strong>RAID-Net</strong></td><td><strong>91.60</strong></td><td><strong>85.19</strong></td><td><strong>97.64</strong></td><td><strong>97.02</strong></td><td><strong>92.15</strong></td><td>9.59</td><td><strong>1.95</strong></td></tr>
            </tbody>
        </table>
    </div>

    <div class="figure-grid">
        <div class="figure-block">
            <img src="docs/fig5_isic_complexity.png" alt="ISIC 性能-复杂度" />
            <div class="caption"><strong>图5：</strong> ISIC 2018 性能与模型复杂度对比</div>
        </div>
        <div class="figure-block">
            <img src="docs/fig6_isic_vis.png" alt="ISIC 可视化" />
            <div class="caption"><strong>图6：</strong> ISIC 2018 分割可视化对比</div>
        </div>
    </div>

    <h3>📌 Synapse 多器官分割</h3>
    <div class="table-wrap">
        <table>
            <thead><tr>
                <th>Method</th><th>Dice (%)</th><th>HD95 (mm)</th><th>Params (M)</th><th>FLOPs (G)</th>
            </tr></thead>
            <tbody>
                <tr><td>TransUNet</td><td>77.48</td><td>31.69</td><td>105.28</td><td>24.73</td></tr>
                <tr><td>Swin-Unet</td><td>79.13</td><td>21.55</td><td>27.17</td><td>6.16</td></tr>
                <tr><td>I²U-Net</td><td>83.22</td><td>16.82</td><td>7.03</td><td>2.74</td></tr>
                <tr><td>PSCT-Net</td><td>84.67</td><td>13.42</td><td>68.88</td><td>17.25</td></tr>
                <tr><td>MS-GBANet</td><td>84.01</td><td>13.26</td><td>54.80</td><td>14.70</td></tr>
                <tr class="highlight-row"><td><strong>RAID-Net</strong></td><td><strong>84.50</strong></td><td><strong>13.22</strong></td><td>9.59</td><td><strong>1.95</strong></td></tr>
            </tbody>
        </table>
    </div>

    <div class="figure-grid">
        <div class="figure-block">
            <img src="docs/fig9_synapse_heatmap.png" alt="Synapse 热力图" />
            <div class="caption"><strong>图9：</strong> Synapse 各器官 Dice 热力图</div>
        </div>
        <div class="figure-block">
            <img src="docs/fig10_synapse_complexity.png" alt="Synapse 性能-复杂度" />
            <div class="caption"><strong>图10：</strong> Synapse 性能与模型复杂度对比</div>
        </div>
        <div class="figure-block" style="grid-column: 1 / -1;">
            <img src="docs/fig11_synapse_vis.png" alt="Synapse 可视化" />
            <div class="caption"><strong>图11：</strong> Synapse 多器官分割可视化</div>
        </div>
    </div>

    <!-- ===== 4. 消融 & 可解释性 ===== -->
    <h2><i class="fas fa-flask"></i> Ablation & Interpretability</h2>

    <div class="figure-grid">
        <div class="figure-block">
            <img src="docs/fig12_sari_vis.png" alt="SARI 可视化" />
            <div class="caption"><strong>图12：</strong> SARI 可靠性交互机制可视化</div>
        </div>
        <div class="figure-block">
            <img src="docs/fig13_amrf_vis.png" alt="AMRF 尺度选择" />
            <div class="caption"><strong>图13：</strong> AMRF 内容自适应多尺度选择</div>
        </div>
        <div class="figure-block">
            <img src="docs/fig14_sgde_vis.png" alt="SGDE 误差图" />
            <div class="caption"><strong>图14：</strong> SGDE 解码增强误差图</div>
        </div>
        <div class="figure-block">
            <img src="docs/fig15_gradcam.png" alt="Grad-CAM" />
            <div class="caption"><strong>图15：</strong> Grad-CAM 可解释性分析</div>
        </div>
    </div>

    <!-- ===== 5. 引用 ===== -->
    <h2><i class="fas fa-quote-right"></i> Citation</h2>
    <div style="background: #f1f5f9; padding: 1.2rem 1.8rem; border-radius: 1rem; font-family: monospace; font-size: 0.9rem; white-space: pre-wrap; word-break: break-all;">
@article{RAIDNet2026,
  title={RAID-Net: Reliability-Aware Interactive Dual-Path Network with Adaptive Multi-Scale Relation Fusion for Medical Image Segmentation},
  author={Zhou, Xinyu and ...},
  journal={arXiv preprint},
  year={2026}
}
    </div>

    <!-- ===== 6. 页脚 ===== -->
    <div class="footer">
        <p>
            <i class="fas fa-code"></i> 代码与数据将逐步开放 ·
            联系邮箱: <a href="mailto:zhouxinyu2025@hunnu.edu.cn">zhouxinyu2025@hunnu.edu.cn</a> ·
            <i class="fas fa-university"></i> 湖南师范大学
        </p>
        <p style="margin-top:0.4rem; font-size:0.8rem;">
            <i class="fas fa-exclamation-triangle" style="color:#eab308;"></i>
            论文尚未正式发表，所有结果仅供学术交流参考。
        </p>
    </div>

</div>
</body>
</html>
