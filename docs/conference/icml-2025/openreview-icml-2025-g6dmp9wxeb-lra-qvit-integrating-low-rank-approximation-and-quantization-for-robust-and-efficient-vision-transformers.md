---
title: "LRA-QViT: Integrating Low-Rank Approximation and Quantization for Robust and Efficient Vision Transformers"
title_zh: LRA-QViT：集成低秩近似和量化以实现鲁棒高效的视觉Transformer
authors: "Beom Jin Kang, NamJoon Kim, Hyun Kim"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=G6DmP9wxeB"
tags: ["query:edge-llm"]
score: 8.0
evidence: 针对边缘设备的视觉Transformer低秩近似与量化压缩
tldr: 为应对视觉Transformer在边缘设备部署时的参数和计算挑战，LRA-QViT提出结合低秩近似与量化的联合压缩方法。通过分解高维权重矩阵并降低数值精度，在减少模型大小的同时保持或提升鲁棒性。该方法展示了压缩技术在视觉模型上的有效性，对边缘端Transformer推理具有普适参考价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-g6dmp9wxeb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1671, \"height\": 867, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g6dmp9wxeb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 846, \"height\": 748, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g6dmp9wxeb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g6dmp9wxeb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1066, \"height\": 740, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g6dmp9wxeb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1740, \"height\": 315, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1532, \"height\": 760, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1595, \"height\": 903, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1732, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1497, \"height\": 398, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1151, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 867, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 732, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 871, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 894, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1155, \"height\": 466, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g6dmp9wxeb/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1477, \"height\": 251, \"label\": \"Table\"}]"
motivation: 视觉Transformer参数众多，难以在边缘移动设备上部署。
method: 集成低秩近似和量化技术，对视觉Transformer进行联合压缩，提升鲁棒性和效率。
result: 实现了在资源受限环境下的高效视觉Transformer部署。
conclusion: LRA-QViT为视觉模型在边缘设备的部署提供了一种压缩加速方案。
---

## Abstract
Recently, transformer-based models have demonstrated state-of-the-art performance across various computer vision tasks, including image classification, detection, and segmentation. However, their substantial parameter count poses significant challenges for deployment in resource-constrained environments such as edge or mobile devices. Low-rank approximation (LRA) has emerged as a promising model compression technique, effectively reducing the number of parameters in transformer models by decomposing high-dimensional weight matrices into low-rank representations. Nevertheless, matrix decomposition inherently introduces information loss, often leading to a decline in model accuracy. Furthermore, existing studies on LRA largely overlook the quantization process, which is a critical step in deploying practical vision transformer (ViT) models. To address these challenges, we propose a robust LRA framework that preserves weight information after matrix decomposition and incorporates quantization tailored to LRA characteristics. First, we introduce a reparameterizable branch-based low-rank approximation (RB-LRA) method coupled with weight reconstruction to minimize information loss during matrix decomposition. Subsequently, we enhance model accuracy by integrating RB-LRA with knowledge distillation techniques. Lastly, we present an LRA-aware quantization method designed to mitigate the large outliers generated by LRA, thereby improving the robustness of the quantized model. To validate the effectiveness of our approach, we conducted extensive experiments on the ImageNet dataset using various ViT-based models. Notably, the Swin-B model with RB-LRA achieved a 31.8\% reduction in parameters and a 30.4\% reduction in GFLOPs, with only a 0.03\% drop in accuracy. Furthermore, incorporating the proposed LRA-aware quantization method reduced accuracy loss by an additional 0.83\% compared to naive quantization.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：视觉 Transformer（ViT）在图像分类、检测等任务上性能出色，但参数量和计算量巨大，难以直接部署到资源受限的移动或边缘设备上。
- **研究动机**：现有低秩近似（LRA）压缩方法会因矩阵分解产生信息损失，导致精度下降；同时，大多数 LRA 研究忽略了量化——这一实际部署中必不可少的技术。两者简单叠加会引发严重的精度衰减。
- **整体含义**：本文旨在设计一种将鲁棒的低秩近似与面向 LRA 特性的量化有机融合的压缩框架，使 ViT 在大幅降低存储和计算开销的同时，保持高精度，从而推动 ViT 在边缘端的实用化。

## 2. 论文提出的方法论

### 2.1 可重参数化分支的低秩近似（RB‑LRA）与权重重构（WR）
- **基础低秩近似**：利用 SVD 将全连接层的权重矩阵 \(W\) 分解为两个低秩矩阵 \(V'\) 和 \(U'\)，只保留前 \(r\) 个奇异值以实现压缩。但直接丢弃小奇异值会损失信息。
- **RB‑LRA 核心思想**：用可重参数化的残差分支补偿 LRA 引入的误差。前向传播时，输出可以表示为 \(y = V'(U'^T X) + \tilde{E}X\)，其中误差矩阵 \(\tilde{E}\) 被设计为低秩结构 \((V' + \tilde{V})(U'^T + \tilde{U}^T) - V'U'^T\)。通过重参数化，训练后将两个分支合并为一个等效低秩矩阵，推理时不增加参数。
- **权重重构初始化**：\(\tilde{V}\) 分支利用 LRA 中丢弃的奇异值子矩阵 \(S_{del}V_{del}\) 进行初始化，\(\tilde{U}\) 从零初始化，从而显著减小初始信息损失，并加速微调收敛。

### 2.2 块级知识蒸馏（Block‑Level KD）
- 以原始完整模型作为教师，RB‑LRA 压缩后的模型作为学生，对每个编码器块的输出特征计算 MSE 损失，引导压缩模型恢复教师表征。
- 最终损失函数：\(L = \alpha L_{ce} + \beta L_{kd}\)（\(\alpha=\beta=1\)）。

### 2.3 LRA 感知的量化方法
- **问题分析**：应用 RB‑LRA 后，某些通道和 token 上出现大幅度离群值，导致常规量化误差陡增。
- **激活平滑方法 (WADS)**：引入可学习的通道缩放向量 \(\alpha\)，对激活按通道缩放，同时调整对应权重以保持数学等效性，从而平滑离群值。缩放向量的优化目标同时考虑激活量化误差和权重量化误差，避免权重离群化。
- **细粒度量化策略**：针对 token 维度离群值，提出对激活采用逐 token（per‑token）量化，对权重采用逐通道（per‑channel）量化。最终将 WADS 与 per‑token 量化结合，有效降低精度损失。

## 3. 实验设计

- **数据集与任务**：
  - 图像分类：ImageNet‑1k；
  - 下游任务：MSCOCO 上的目标检测和实例分割（Mask R‑CNN）、人体姿态估计（ViTPose）；
  - 跨模态验证：语言建模（GPT‑2 Medium on Wikitext‑103）和语音识别（Conformer‑L on LibriSpeech）。
- **基准模型**：DeiT‑T、DeiT‑B、Swin‑T、Swin‑B、ViTPose‑B、GPT‑2 Medium、Conformer‑L。
- **对比方法**：
  - LRA 方向：朴素 SVD LRA、PELA、AAFM+GFM；
  - 量化方向：SmoothQuant、Repq‑ViT、QADS、FQ‑ViT、APQ‑ViT、AdaLog、IGQ‑ViT 等；
  - 联合压缩框架与 SOTA 方法的整体对比（如 PTQ4ViT、QDrop、I&S‑ViT 等）。

## 4. 资源与算力

- **硬件配置**：所有实验均在**单块 NVIDIA A100 GPU** 上完成。
- **训练开销**：文中未详细给出每个模型的全部训练时间，但在附录中提及 DeiT‑B 上的 RB‑LRA 微调 + WADS 优化总耗时约 **5 小时 56 分**（含知识蒸馏训练）。这一成本相比纯 PTQ 方法更高，但换取了明显的精度提升。
- **推理延迟测试**：分别在 Android 手机（Cortex‑X3 大核）和 NVIDIA Jetson Xavier 上测试，以验证边缘部署的真实加速效果。

## 5. 实验数量与充分性

- **实验维度丰富**：
  - 在 4 种 ViT 模型（DeiT‑T/B、Swin‑T/B）上进行压缩实验，展示 RB‑LRA 的有效性（表1）。
  - 不同量化配置下的消融（WADS、per‑token 量化组合效果，表2、表9）。
  - 与当前 SOTA LRA 和量化方法在多模型、多压缩比下的对比（表3、表10）。
  - 跨任务（检测、分割、姿态估计）验证（表5、6）。
  - 跨模态（语言、语音）的泛化实验（表8）。
  - 分支初始化方法的影响分析（表7）及理论误差分析（附录）。
- **评价维度全面**：涵盖参数量、GFLOPs、Top‑1 准确率、模型大小、推理延迟、训练时间、量化误差可视化等。
- **公平性**：实验对比时均采用各方法的原始基线准确率计算精度退化，并尽可能统一 8‑bit 量化设置进行横向比较；与 4‑bit 方法的对比也通过模型大小维度进行公平讨论。

## 6. 论文的主要结论与发现

- RB‑LRA + 块级 KD 能够在显著压缩模型（Swin‑B 减少 31.8% 参数、30.4% GFLOPs）的同时，几乎不损失精度（仅下降 0.03%）。
- 联合应用 LRA 和量化时，常规量化会因 LRA 产生的激活离群值而严重衰退；所提出的 **WADS + per‑token 量化**可大幅缓解该问题，在 DeiT‑B 和 Swin‑B 上相较朴素量化分别提升 0.94% 和 0.83% 准确率。
- 整合 LRA 与 8‑bit 量化后，模型尺寸可压缩至原 FP32 的约 1/5～1/8，并在实际移动和边缘设备上获得 1.5×～3.2× 的推理加速。
- 该方法不仅在计算机视觉任务上有效，在 NLP 和语音任务上也展现出良好的通用性，证明其作为通用 Transformer 压缩策略的潜力。

## 7. 优点

- **方法创新**：首次将可重参数化分支与 SVD 丢弃权重重构引入 ViT 压缩，从信息损失角度改善 LRA。
- **联合压缩视角**：系统研究 LRA 与量化的相互影响，并提出针对性的离群值处理方案，优于简单叠加两技术。
- **实验扎实**：覆盖多模型、多任务、多模态，有丰富的消融和可视化分析，并实测了真实设备延迟。
- **性能优越**：在同等压缩率下，相比主流 PTQ 方法和 LRA 方法取得更优的精度‑效率平衡。

## 8. 不足与局限

- **训练成本较高**：RB‑LRA 需要额外微调（含 KD），相比纯 PTQ 方法耗时更长，对快速部署场景不够友好。
- **压缩粒度相对固定**：文中主要对全连接层施加统一的秩压缩，未探讨层自适应秩选择或结构化剪枝的潜在增效。
- **量化位宽限制**：主要验证了 8‑bit 量化，与部分 SOTA 4‑bit PTQ 的对比虽在模型大小上相近，但极低位宽下的组合效果未深入探讨。
- **离群值处理的特化**：WADS 和 per‑token 量化专门针对 RB‑LRA 后的异常分布设计，若更换其他 LRA 方法或网络结构，可能需要重新适配。

（完）
