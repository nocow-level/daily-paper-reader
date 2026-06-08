---
title: "Q-Palette: Fractional-Bit Quantizers Toward Optimal Bit Allocation for Efficient LLM Deployment"
title_zh: Q-Palette：面向高效LLM部署的最优比特分配分数比特量化器
authors: "Deokjae Lee, Hyun Oh Song"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=l4F50jpiVH"
tags: ["query:edge-llm"]
score: 10.0
evidence: 权重的训练后量化对减少LLM推理内存占用和延迟至关重要，尤其适用于边缘设备上的小批量个性化推理
tldr: 研究LLM的权重量化，提出Q-Palette分数比特量化器，信息论最优比特分配，旨在降低内存占用和延迟，特别适用于边缘设备上的个性化推理。通过旋转变换等技巧处理权重分布中的离群值，实现高压缩比下的精度保持。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-l4f50jpivh/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1463, \"height\": 617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l4f50jpivh/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 621, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l4f50jpivh/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 619, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l4f50jpivh/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1431, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l4f50jpivh/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1435, \"height\": 641, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1304, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1399, \"height\": 684, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1402, \"height\": 707, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1389, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1449, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1399, \"height\": 685, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1275, \"height\": 668, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1297, \"height\": 530, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l4f50jpivh/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1212, \"height\": 359, \"label\": \"Table\"}]"
motivation: LLM权重分布存在重尾离群值，传统量化误差大，阻碍边缘部署。
method: 推导信息论最优比特分配，设计分数比特量化器，结合旋转变换改善权重分布。
result: 在边缘设备的个性化推理场景中，实现了更低的内存占用和延迟。
conclusion: Q-Palette为LLM在边缘设备上的高效量化部署提供了理论最优的方案。
---

## Abstract
We study weight-only post-training quantization (PTQ), which quantizes the weights of a large language model (LLM) without retraining, using little or no calibration data. Weight-only PTQ is crucial for reducing the memory footprint and latency of LLM inference, especially in memory-bound, small-batch inference scenarios, such as personalized inference on edge devices. Despite its importance, irregular weight distributions with heavy-tailed outliers in LLMs complicate quantization, recently motivating rotation-based methods that transform weights into near-Gaussian distributions, which are more regular with fewer outliers, thereby reducing quantization error. In this work, we first derive the information-theoretically optimal bit allocation for Gaussianized weights under given bit budgets, revealing that fine-grained fractional-bit quantizers approaching the Gaussian distortion-rate bound are essential to achieve near-optimal quantization performance. To bridge this theoretical insight and practical implementation, we introduce Q-Palette, a versatile collection of fractional-bit quantizers that range from trellis-coded quantizers offering near-optimal distortion to simpler vector and scalar quantizers optimized for faster inference, all efficiently implemented with optimized CUDA kernels across various bitwidths. Furthermore, leveraging Q-Palette as a foundational component, we propose a novel mixed-scheme quantization framework, jointly optimizing quantizer choices and layer fusion decisions given resource constraints. The code is available at https://github.com/snu-mllab/Q-Palette.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

*   **背景与动机**：大语言模型（LLM）在资源有限的边缘设备（如笔记本、手机）上部署时，内存带宽往往成为推理瓶颈，尤其是在小批量（small-batch）解码场景下。仅对权重进行训练后量化（Weight-only PTQ）能有效降低模型内存占用并提升推理速度，且无需昂贵重训练或大量校准数据。
*   **核心挑战**：LLM 的权重分布通常呈现不规则的重尾特性并包含离群值，直接量化会引入较大误差。
*   **已有工作**：近期研究通过旋转变换（如随机 Hadamard 变换）对权重矩阵进行“不相干处理”，将权重分布高斯化，从而抑制离群值并减小量化误差。
*   **本文目标**：基于高斯化后的权重，研究在给定内存预算下如何达到信息论上的最优比特分配，并设计一族能够逼近理论界且实际推理高效的分数比特量化器。

### 2. 论文提出的方法论

*   **理论推导（最优比特分配）**：
    *   基于“线性定理”，量化引起的性能下降可近似为各层归一化量化误差的加权和。
    *   将高斯化后的权重量化问题建模为高斯信源编码，利用率失真理论推导出理想高斯量化器下的最优分数比特分配闭式解（定理 3.1），核心是平衡各层梯度与维度，用注水法分配比特。
    *   进一步分析量化最优性差距，指出差距来源于实际量化器与理想失真界的差异（失真差距）以及可用比特宽度与理论最优分配的偏差（比特分配差距）。这引出对细粒度分数比特量化器的需求。

*   **Q-Palette 量化器族**：
    *   **非均匀标量量化 (NUQ)**：通过 k-means 对高斯样本聚类构建非均匀查找表（LUT），每个权重独立量化。
    *   **向量量化 (VQ)**：实现 2D VQ，将权重分组为二维向量，利用大小为 2 的幂次的码本实现分数比特编码（如 1.5 比特）。
    *   **网格编码量化 (TCQ)**：基于 QTIP 扩展，利用比特移位方案实现高分维度量化，达到接近最优的失真率。
    *   **Half-TCQ**：一种 TCQ 变体，按行将权重矩阵分为两半，分别用不同比特宽度的 TCQ 量化（如 2.5 和 3.0 比特），实现中间分数比特（如 2.75 比特），并提供融合内核。
    *   **旋转开销优化**：仅沿输入维度进行旋转变换，并在具有相同输入的线性层（如 query/key/value）间共享旋转矩阵，大幅减少在线旋转次数。

*   **混合方案量化框架 (MSQ)**：
    *   将资源约束下的量化器选择问题形式化为多选背包问题 (MCKP)，目标是最小化由线性定理估计的总体损失，约束为内存或延迟。
    *   **融合感知 MSQ**：进一步联合优化层融合（如将 Q、K、V 投影合并为一个矩阵乘法）与量化器选择。引入指示变量表示可融合层组与量化器的选择，通过整数线性规划联合求解，在降低内存访问和内核启动次数的同时优化性能-延迟权衡。

*   **高效 CUDA 内核实现**：
    *   提供 Tensor Core 和 CUDA Core 两种类型内核，支持 NUQ、VQ、TCQ 及 Half-TCQ 的广泛分数比特宽度（如 1.5 到 5.0 比特）。
    *   扩展了 QTIP 的单批次内核到分数比特宽度，并优化了较大批次（如 batch size 8）下的实现：直接加载并解量化权重，利用共享内存缓存激活。

### 3. 实验设计

*   **模型与数据集**：
    *   评估模型：LLaMA 3 系列（3.1-8B, 70B, 3.2-1B, 3B）、LLaMA 2 系列（7B, 13B）、Qwen 2.5-7B。
    *   主要测评基准：WikiText2 困惑度，以及五个零样本下游任务的平均准确率（ARC-easy, ARC-challenge, HellaSwag, PiQA, WinoGrande）。
    *   延迟测评硬件：NVIDIA RTX 4090 和 RTX 3090 GPU。

*   **对比方法**：
    *   **数据无关 (Data-free) 基线**：HQQ（均匀量化）、NormalFloat (NUQ) w/ FLUTE 内核、HIGGS-Single (VQ)、数据无关的 QTIP (TCQ) 以及混合精度 MSQ 基线 HIGGS-MSQ。
    *   **数据感知 (Data-aware) 基线**：QTIP（无重训练）。
    *   **本文方法**：Ours-TCQ-x（单方案 TCQ 量化）、Ours-MSQ-Mem（内存约束 MSQ，使用 TCQ 量化器集）、Ours-MSQ-Lat（延迟约束的融合感知 MSQ，使用全部 Q-Palette 量化器）。

*   **实验场景**：
    *   **数据无关设定**：使用随机生成 Token 结合 KL 散度估计层敏感系数，利用预测的高斯失真构建损失项。
    *   **数据感知设定**：使用 RedPajama 数据集的验证集实际困惑度增加作为损失项。块 LDLQ 方式更新权重。

### 4. 资源与算力

*   **实验硬件**：
    *   主要延迟实验在单个 NVIDIA RTX 4090 GPU（云环境）和 RTX 3090 GPU（本地）上进行。
    *   未具体说明训练 (retraining) 时长，因为本文聚焦于训练后量化 (PTQ)，不涉及重训练。唯一可能的计算开销是，在数据无关设定下用 128K 随机 Token 估计层敏感系数，文中指出这可以并行进行，属于一次性开销。

### 5. 实验数量与充分性

*   **实验组数**：
    *   跨三个模型系列（LLaMA 2、LLaMA 3、Qwen）和多个参数规模（1B 到 70B）及比特宽度（2.0 到 4.25 比特，以及图中的更宽范围）进行了大量对比实验。
    *   包含数据无关和数据感知两种设定下的 MSQ 与单方案量化对比。
    *   针对延迟，对比了不同 batch size（1 和 8）下的吞吐量-PPL 权衡。
    *   进行了详细的消融实验：层融合与 CUDA Core 内核的影响；数据感知 MSQ 中不同损失项（线性 vs 实际）的影响；MSQ 方法与不相干处理（IP）结合前后的效果；还比较了 QTIP 等特定比特宽度。

*   **充分性与公平性**：
    *   实验设计严谨，考虑了最相关的 SOTA 基线。比较了多种比特宽度和模型，并报告了准化困惑度和零样本精度，以及实测延迟和吞吐量，评估全面。
    *   消融实验充分分析了框架中各个组件（融合、内核类型、损失项类型）的贡献。对于数据感知基线，采用了 QTIP 论文中使用的相同代理 Hessian。对比公平，均在不进行重训练的前提下进行。

### 6. 论文的主要结论与发现

*   Q-Palette 的细粒度分数比特量化器集（特别是 TCQ 和 Half-TCQ）能显著降低实际量化与理论最佳高斯失真之间的差距。
*   基于 Q-Palette 的混合方案量化（MSQ-Mem 和 MSQ-Lat）在同等内存/延迟预算下，持续超越基于 NormalFloat、HQQ、HIGGS 和 QTIP 的单方案或混合精度基线，取得了更优的 WikiText2 困惑度和相当或更好的零样本精度。
*   提出的融合感知 MSQ 通过联合优化量化器和层融合，能够在不增加甚至改善延迟和吞吐的同时，进一步降低困惑度，大幅扩展了准确率-推理效率的帕累托前沿。
*   优化的 CUDA 内核在批量推理（batch size 8）时相比 QTIP 有高达 4 倍以上的吞吐量提升，并矫正了“TCQ 等复杂量化器在批量大于 1 时计算效率低下”的误解。
*   即使在不用 Incoherence Processing (IP)的环境下，利用线性定理和高斯失真预测的 MSQ 仍然有效，并能提升量化性能。

### 7. 优点

*   **理论与实践的紧密结合**：从信息论最优比特分配的理论分析出发，明确指出了需要什么样的量化器，并实现了相应的分数比特量化器族来弥合理论和实践的差距。
*   **系统性量化器设计**：Q-Palette 不仅仅是一个量化器，而是一个兼顾精度、延迟和比特宽度的量化器族工具箱，为下游 MSQ 框架提供了灵活的搜索空间。
*   **创新的融合感知优化**：首次提出融合感知 MSQ，将编译器级别的层融合优化与量化算法选择进行联合优化，这是一个新的维度，并取得了实际增益。
*   **扎实的工程实现**：提供了高质量、支持多种分数比特宽度和更大批处理量的 CUDA 内核，显著提升了复杂量化方案（如 TCQ）的实际可用性。
*   **实验全面扎实**：覆盖了数据无关/感知、多模型规模、多比特宽度、多硬件和多 batch size 的评估，消融实验深入，结论有说服力。

### 8. 不足与局限

*   **一次性优化开销**：数据无关 MSQ 依赖敏感系数估计，需要 `O(L)` 次 KL 散度计算，虽然可并行化且系数可复用，但对超大型模型仍是一笔非负可的开销，可能限制在评估预算有限时的复用性。
*   **PTQ 范畴局限**：框架和 Q-Palette 设计针对 PTQ 场景，未涉及量化感知训练（QAT）等需要更大计算和数据预算的设定，没有探索 Q-Palette 在可重训练场景下的潜力。
*   **权重-激活量化拓展未评估**：论文仅聚焦于权重仅量化 (W-only)，这对于内存受限的小批量推理有效。但对于需要整数 GEMM 的硬件加速器（如 NPU），可能需要激活量化，而论文未评估将方法拓展到 W-A 量化的方案，仅提出了未来方向。
*   **损失项依赖 Hessian 近似**：在数据感知设定下，虽然使用了 QTIP 的代理 Hessian，但实际实现依赖于对 Hessian 的良好近似，不同的数据或近似方法可能会影响最终优化结果。
*   **实验公平性细节**：文中提到一些基线（如 HIGGS-Single 的 VQ 配置）可能使用非 2 的幂次的码本大小，在现实中不易高效实现，但依然作为精度对比基线，但这不影响本文方法公平性的结论。

（完）
