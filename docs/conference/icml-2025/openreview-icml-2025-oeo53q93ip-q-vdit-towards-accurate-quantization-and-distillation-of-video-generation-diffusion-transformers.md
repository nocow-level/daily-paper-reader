---
title: "Q-VDiT: Towards Accurate Quantization and Distillation of Video-Generation Diffusion Transformers"
title_zh: Q-VDiT：面向视频生成扩散Transformer的精确量化与蒸馏
authors: "Weilun Feng, Chuanguang Yang, Haotong Qin, Xiangqi Li, Yu Wang, Zhulin An, Libo Huang, Boyu Diao, Zixiang Zhao, Yongjun Xu, Michele Magno"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Oeo53q93iP"
tags: ["query:edge-llm"]
score: 9.0
evidence: 用于在边缘设备上部署视频扩散Transformer的量化与蒸馏框架
tldr: 针对视频生成扩散Transformer参数量大、计算复杂难以在边缘设备部署的问题，提出Q-VDiT框架，结合量化与蒸馏，解决量化信息损失和优化目标与视频生成需求不一致两大挑战，实现高效边缘推理。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1757, \"height\": 639, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 715, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 853, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 890, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 848, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1779, \"height\": 822, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1779, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1781, \"height\": 817, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1781, \"height\": 824, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1779, \"height\": 824, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1780, \"height\": 824, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1778, \"height\": 825, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1780, \"height\": 825, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oeo53q93ip/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1782, \"height\": 819, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-oeo53q93ip/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1786, \"height\": 1199, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oeo53q93ip/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1734, \"height\": 1201, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oeo53q93ip/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1733, \"height\": 987, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oeo53q93ip/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1724, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oeo53q93ip/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 862, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oeo53q93ip/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1864, \"height\": 553, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oeo53q93ip/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1505, \"height\": 205, \"label\": \"Table\"}]"
motivation: 现有图像生成模型量化方法无法直接用于视频DiT，面临信息损失和优化目标不匹配问题。
method: 设计专门针对视频DiT的量化框架，并引入蒸馏策略克服上述挑战。
result: 在多个视频基准上实现了与全精度模型相当的生成质量，同时显著降低计算和存储需求。
conclusion: Q-VDiT为视频生成模型在边缘设备上的实用化应用铺平道路。
---

## Abstract
Diffusion transformers (DiT) have demonstrated exceptional performance in video generation. However, their large number of parameters and high computational complexity limit their deployment on edge devices. Quantization can reduce storage requirements and accelerate inference by lowering the bit-width of model parameters.
Yet, existing quantization methods for image generation models do not generalize well to video generation tasks. We identify two primary challenges: the loss of information during quantization and the misalignment between optimization objectives and the unique requirements of video generation. To address these challenges, we present **Q-VDiT**, a quantization framework specifically designed for video DiT models. From the quantization perspective, we propose the *Token aware Quantization Estimator* (TQE), which compensates for quantization errors in both the token and feature dimensions. From the optimization perspective, we introduce *Temporal Maintenance Distillation* (TMD), which preserves the spatiotemporal correlations between frames and enables the optimization of each frame with respect to the overall video context. Our W3A6 Q-VDiT achieves a scene consistency score of 23.40, setting a new benchmark and outperforming the current state-of-the-art quantization methods by **1.9$\times$**.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义
- **研究背景与动机**：  
  视频生成扩散 Transformer（DiT）在视频生成任务中表现卓越，但其参数量大（可达数十亿）且计算复杂度高，难以在边缘设备上部署。量化技术通过降低模型参数的位宽来减少存储和加速推理，是一种有效的压缩手段。然而，现有的扩散模型量化方法大多面向图像生成任务，直接迁移到视频生成时会导致严重的性能退化。
- **核心挑战**：  
  ① **量化信息损失**：视频生成需同时建模空间和时间维度，信息密度远高于图像生成，低位宽量化造成的信息丢失更为严重。  
  ② **优化目标不匹配**：现有方法仅依靠均方误差（MSE）对齐逐帧输出，忽视了帧间的时空相关性，无法从整体视频视角优化量化过程。  
- **本文目标**：提出专用于视频生成 DiT 的量化框架 **Q‑VDiT**，在低位宽下保持视频生成质量，缩小与全精度模型的差距。

## 2. 方法论
Q‑VDiT 框架由两个核心技术组成：

### 2.1 Token‑aware Quantization Estimator（TQE）
- **核心思想**：  
  基于信息熵理论（量化误差的熵 ≤ 原权重的熵），利用极少的额外参数对权重的量化误差进行低秩近似补偿，并感知激活量化的 token 维度差异。
- **技术细节**：
  - 将权重量化误差 Δ 近似为两个低维向量 α（特征维度）和 β（输出维度）的乘积，额外参数从权重矩阵尺寸 dout×din 降至 dout+din。
  - 考虑视频潜在表示在 token 维度的信息分布差异，引入动态 token 缩放因子 M（每个视频帧一个标量），对量化后的激活进行重新标定，以补偿不同帧及不同 token 的量化信息损失。
  - M 的初始化结合了激活量化前后序列的余弦相似度和 token 显著性测量。
- **公式概览**（文字描述）：  
  量化前向过程改写为：  
  `X W^T ≈ ˆQ(X) ˆQ(W)^T + (M ⊙ ˆQ(X)) α β^T`，  
  其中 M 为 token‑wise 缩放因子，α, β 为低秩补偿项。

### 2.2 Temporal Maintenance Distillation（TMD）
- **核心思想**：  
  仅使用 MSE 优化单帧输出忽略了帧间关联。通过知识蒸馏，让量化模型学习全精度模型输出的帧间关系分布，从而保持时序一致性。
- **技术细节**：
  - 计算全精度模型输出中任意两帧特征序列的相似度，构建时序关系矩阵 T，并经 softmax 得到每帧与所有帧的关系分布 D^FP。
  - 同样计算量化模型的 D^Q，使用 KL 散度最小化两者差异，形成时序保持损失 L_temporal。
  - 梯度推导显示，单帧的优化受到所有其他帧的联合影响，实现了整体视频视角的优化。
- **训练总损失**：L_total = L_task (MSE) + γ L_temporal，其中 γ 为超参数。

## 3. 实验设计
- **模型与数据集**：
  - **Open‑SORA**：文本到视频生成模型，使用 Open‑SORA prompt set（10 个 prompt 生成 10 个视频）进行多指标评估，同时在 VBench 基准（93+72+86 个提示）上进行综合评分。
  - **Latte**：在 UCF‑101 数据集上做类别条件视频生成评估。
- **评估维度**：
  - **VBench 8 大维度**：Imaging Quality、Aesthetic Quality、Motion Smoothness、Dynamic Degree、Background Consistency、Subject Consistency、Scene Consistency、Overall Consistency。
  - **多指标**：CLIPSIM、CLIP‑Temp、VQA‑Aesthetic、VQA‑Technical、Δ Flow Score、Warping Error，以及 UCF‑101 上的 FVD、FVD‑FP16、Temporal Flickering。
- **比较方法**：
  - LLM 量化方法：SmoothQuant，Quarot  
  - 扩散模型量化方法：EfficientDM，SVDQuant  
  - DiT 专用量化方法：Q‑DiT，PTQ4DiT，ViDiT‑Q
- **量化设置**：主要测试低比特（W4A6、W3A8、W3A6），也覆盖高比特（W8A8、W6A6、W4A8）。校准数据使用 10 个 prompt 均匀采样的 50 个扩散步骤。

## 4. 资源与算力
- **训练成本**（W8A8，Open‑SORA）：
  - GPU 内存：Q‑VDiT 约 **18,770 MB**，与 ViDiT‑Q（16,600 MB）等相当，稍高于无校准的 ViDiT‑Q，但明显低于 EfficientDM。
  - 训练时间：约 **12.9 小时**（GPU 型号未明确说明），较 ViDiT‑Q 仅增加约 3% 的时间开销。
- **注**：原文未提供 GPU 型号、数量等具体硬件信息，仅给出了内存和时间对比。

## 5. 实验数量与充分性
- **实验规模**：
  - 三套比特配置（W4A6, W3A8, W3A6）的 benchmark 评估（表 1），多指标评估（表 2）。
  - 高比特实验（表 3）以展示通用性。
  - 消融实验（表 4）：逐步增加 TQE（不含 M）、TQE（含 M）、TMD，验证各模块贡献。
  - 超参数敏感性：不同 γ 值的对比（图 6）。
  - 跨模型验证：Latte 模型在 UCF‑101 上的结果（表 6）。
  - 定性比较：大量生成视频帧的可视化（图 7‑15）。
- **充分性与公平性**：
  - 覆盖了主流的视频生成量化基线，所有方法均在同一条件下重跑以保证公平。
  - 消融实验明确展示了各个组件的累加效果，超参数选择也有敏感性分析。
  - 实验设计较为全面，能有力支撑论文结论。

## 6. 主要结论与发现
- **关键发现**：
  - Q‑VDiT 在视频 DiT 的低位宽量化中大幅超越现有方法。在 W3A6 设置下，场景一致性从 12.04 提升至 23.40，提升近一倍（表 1）。
  - 多指标评估中，W3A6 的 VQA‑Technical 从 29.58 提升到 59.10，CLIPSIM 从 0.1768 提升到 0.1785（表 2）。
  - 在 W4A8 下，VQA‑Aesthetic 甚至超过了全精度模型，显示出量化与蒸馏结合的优势。
  - Q‑VDiT 在 Latte 模型上也表现一致，证明方法具有通用性。
- **结论**：提出的 TQE 有效补偿了量化误差，TMD 保证了时序连贯性，二者结合使视频生成 DiT 在极低位宽下仍能生成高质量、有意义的视频。

## 7. 优点
- **问题针对性**：首次系统解决视频 DiT 量化中的信息损失和帧间依赖问题，而非简单移植图像量化方法。
- **方法巧妙性**：
  - TQE 利用低秩估计和 token 维动态缩放，以极少参数恢复量化误差。
  - TMD 通过帧间分布对齐，将单帧优化与整体视频关联起来，理论梯度分析扎实。
- **实验全面**：多比特、多模型、多维度评估，消融实验和定性结果充分，与多家 SOTA 方法公平对比。
- **实用性强**：训练成本可控，量化后内存和延迟均有显著下降（W4A8 下内存减少 2.4×，提速 1.35×），且 TQE 可以在专用 Kernel 中融合，额外延迟很小。

## 8. 不足与局限
- **模型与数据局限性**：仅在 Open‑SORA 和 Latte 上验证，未涉及更大规模、更先进的视频生成模型（如类 Sora 模型），推广性有待进一步检验。
- **校准数据依赖**：校准过程依赖 10 个 prompt 生成的视频片段，可能对 prompt 质量和多样性敏感，缺乏无数据校准能力的讨论。
- **硬件细节缺失**：未透露 GPU 型号及具体测试平台，难以精确评估在不同边缘设备上的实际推理加速效果。
- **超参数 γ 选择**：虽说不敏感，但仍需手动调整，未提供自适应或启发式选择方法。
- **比特专用性**：方案主要针对 3‑4 bit 权重，激活量化仅到 6‑8 bit，未涉及权重/激活更极端的 1‑2 bit 量化。

（完）
