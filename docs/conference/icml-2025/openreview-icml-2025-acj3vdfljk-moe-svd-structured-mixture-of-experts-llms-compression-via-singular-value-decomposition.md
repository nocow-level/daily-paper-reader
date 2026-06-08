---
title: "MoE-SVD: Structured Mixture-of-Experts LLMs Compression via Singular Value Decomposition"
title_zh: MoE-SVD：基于奇异值分解的结构化混合专家大模型压缩
authors: "Wei Li, Lujun Li, Hao Gu, You-Liang Huang, Mark G. Lee, Shengjie Sun, Wei Xue, Yike Guo"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=acJ3vdFljk"
tags: ["query:edge-llm"]
score: 9.0
evidence: 基于奇异值分解的MoE专家压缩，减少内存并加速推理
tldr: 针对MoE大模型参数量和内存需求大导致部署困难的问题，提出基于奇异值分解的压缩框架MoE-SVD，通过选择性分解专家矩阵为低秩表示，在无额外训练的条件下实现模型压缩和推理加速。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1721, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1782, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1767, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 870, \"height\": 312, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1768, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 795, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 809, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-acj3vdfljk/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 810, \"height\": 457, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1775, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 1117, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1450, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1454, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 840, \"height\": 127, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 844, \"height\": 115, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 844, \"height\": 96, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 844, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1454, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1250, \"height\": 570, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-acj3vdfljk/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1453, \"height\": 267, \"label\": \"Table\"}]"
motivation: MoE-LLM的高参数和内存需求给部署带来挑战。
method: 利用SVD分解专家为低秩矩阵，并基于敏感性度量选择性分解。
result: 无需训练即可压缩模型，加速推理，节省内存。
conclusion: MoE-SVD是一种简单有效的MoE模型压缩方法，便于实际部署。
---

## Abstract
Mixture of Experts (MoE) architecture improves Large Language Models (LLMs) with better scaling, but its higher parameter counts and memory demands create challenges for deployment. In this paper, we present MoE-SVD, a new decomposition-based compression framework tailored for MoE LLMs without any extra training. By harnessing the power of Singular Value Decomposition (SVD), MoE-SVD addresses the critical issues of decomposition collapse and matrix redundancy in MoE architectures.   Specifically, we first decompose experts into compact low-rank matrices, resulting in accelerated inference and memory optimization. In particular, we propose selective decomposition strategy by measuring sensitivity metrics based on weight singular values and activation statistics to automatically identify decomposable expert layers. Then, we share a single V-matrix across all experts and employ a top-k selection for U-matrices. This low-rank matrix sharing and trimming scheme allows for significant parameter reduction while preserving diversity among experts.  Comprehensive experiments on Mixtral, Phi-3.5, DeepSeek, and Qwen2 MoE LLMs show MoE-SVD outperforms other compression methods, achieving a 60\% compression ratio and 1.5× faster inference with minimal performance loss.

---

## 论文详细总结（自动生成）

好的，这是根据您提供的论文内容生成的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景与动机**：混合专家（MoE）架构通过稀疏激活机制，在提升大语言模型（LLM）能力的同时控制了计算成本，因此被广泛采用。然而，MoE模型通常拥有巨大的参数量和更高的内存需求，这给其在资源受限环境下的部署带来了严峻挑战。
*   **核心问题**：现有的MoE压缩方法（如专家剪枝）在高压缩率下会导致显著的性能下降，且往往需要昂贵的重新训练；部分方法依赖于特定硬件，加速效果有限。直接应用针对稠密模型的SVD分解技术到MoE模型上，会导致严重的性能崩溃（困惑度飙升）。
*   **整体含义**：本文旨在开辟一条新的技术路线，提出一个无需额外训练、不依赖特定硬件、且能保持模型性能的MoE模型结构化压缩框架，以实现高效的模型部署。

### 2. 论文提出的方法论

论文提出了一个名为**MoE-SVD**的压缩框架，其核心思想是利用奇异值分解（SVD）将MoE中的专家层分解为低秩矩阵，并通过一系列创新策略解决直接应用SVD导致的性能崩溃和专家冗余问题。

**关键技术细节与流程：**

*   **SVD专家分解**：首先，对每个专家层的权重矩阵 \( W_i \) 应用激活感知的SVD，即 \( W_i = U_i \Sigma_i V_i^T \)。通过截断较小的奇异值，将原始矩阵近似为低秩矩阵 \( U_i \Sigma_i V_i^T \)，从而减少参数量。
*   **选择性分解策略**：为解决不同专家层对分解敏感度不同的问题，提出一个综合敏感度度量指标，用于自动识别哪些层可以被分解。
    *   **敏感度指标 \( S_L \)**：对于一个包含 \( N \) 个专家的层，其敏感度 \( S_L = \sum_{i=1}^N f_i \cdot p_i \cdot a_i \)，其中：
        *   \( f_i \)：专家 \( i \) 的路由采样频率。
        *   \( p_i \)：专家 \( i \) 权重矩阵SVD分解后奇异值的主秩（重要成分的数量）。
        *   \( a_i \)：专家 \( i \) 中激活值离群点（outliers）的比例。
    *   **策略**：设定一个阈值 \( \tau \)，仅对敏感度 \( S_L < \tau \) 的层进行SVD分解，而保留敏感度高的层（通常是首尾层），以此维持模型整体性能。
*   **低秩矩阵共享与裁剪**：为解决专家间矩阵冗余的问题，在分解后进一步压缩。
    *   **V矩阵共享**：所有被分解的专家共享一个V矩阵 \( V_s \)。该矩阵选择自路由采样频率最高的专家，因为其输出变换最具代表性。更新后的专家表示为 \( E_i \approx U_i \Sigma_i V_s^T \)。
    *   **U矩阵裁剪**：对U矩阵进行基于频率的Top-k选择。具体来说，对于专家 \( i \)，从其采样频率更高的专家中，选择频率最高的 \( k \) 个U矩阵（文中 \( k=2 \)）组合作为其新的U矩阵。最终专家函数为 \( E_i(x) = (U_{i,1}\Sigma_{i,1} + U_{i,2}\Sigma_{i,2})V_s^T x \)。此方法在保证专家多样性的同时，极大减少了参数。

### 3. 实验设计

*   **数据集/场景**：
    *   **语言建模数据集**：WikiText-2, PTB, C4（以困惑度PPL为评价指标）。
    *   **常识推理数据集**（零样本设置）：OpenbookQA, ARC-e, ARC-c, WinoGrande, HellaSwag, PIQA, MathQA（以准确率为评价指标）。
    *   **Benchmark工具**：使用LM-Evaluation-Harness框架进行评估。
*   **模型**：在Mixtral-8×7B, Mixtral-8×22B, Phi-3.5-MoE, DeepSeekMoE-16B, Qwen2-57B-A14B等多个主流MoE大模型上进行了验证。
*   **对比方法**：
    *   **通用LLM压缩方法**：Wanda (剪枝), SparseGPT (剪枝), LoSparse (低秩+稀疏)。
    *   **MoE特定压缩方法**：MC-SMoE (合并后压缩), MoE-I2 (搜索+丢弃+分解), MoE-Compression (剪枝+层丢弃)。
    *   **SVD系列方法**：ASVD, SVD-LLM。

### 4. 资源与算力

论文的“实验设置”部分提到所有实验均在**NVIDIA H800 GPU**上进行，但未明确说明使用的GPU具体数量以及整个实验过程的总训练/压缩时长。对于结合LoRA微调的实验（MoE-SVD †），也未说明微调的详细算力开销和时间。

### 5. 实验数量与充分性

实验设计**相当全面和充分**，具体体现在：
*   **多模型验证**：在5个不同规模的MoE模型上进行了主实验和泛化性实验。
*   **多比率对比**：在20%到60%的多个压缩比率下进行了性能对比。
*   **多维度评估**：综合评估了语言建模能力（PPL）和下游推理任务能力（准确率）。
*   **细粒度消融研究**：对核心组件（选择性分解、V矩阵共享、U矩阵裁剪）进行了消融，验证了每个设计的有效性。还分析了敏感度指标中各因子的贡献、不同裁剪数量（k值）的影响、以及校准数据来源和数量的影响。
*   **效率分析**：专门评估了压缩后的推理加速（吞吐量）和内存占用减少情况。
*   **可扩展性探讨**：结合4-bit/3-bit量化技术（GPTQ）进行了实验，展示了方法与其他技术的正交性。
*   **客观公平性**：对比方法涵盖了SVD、剪枝、MoE特定压缩等多种流派，且统一使用256个WikiText-2样本作为校准数据，对比条件公平。

### 6. 论文的主要结论与发现

*   **关键发现**：直接应用SVD到MoE模型会失败，原因在于：1）不同专家层对分解的敏感性差异巨大；2）用于稠密模型的激活统计量在MoE上存在偏差；3）专家间的V矩阵高度相似，存在显著冗余。
*   **方法有效性**：MoE-SVD在多种压缩率下均显著优于其他压缩方法，能在保持极小性能损失的情况下实现高压缩比。例如，在Mixtral-8×7B上以20%压缩率仅损失2%性能，在60%压缩率下其他SVD方法困惑度破千，而MoE-SVD仍保持较低水平。
*   **加速与内存节省**：MoE-SVD能实现1.2倍至1.5倍的推理加速，并将模型内存占用降低至原来的40%左右。
*   **泛化能力**：该方法在不同架构（Mixtral, Phi, DeepSeek, Qwen）的MoE模型上均表现良好，证明其具有良好的通用性。
*   **可组合性**：可以与LoRA微调和量化技术结合，进一步提升性能或降低内存占用。

### 7. 优点

*   **方法创新性强**：首次系统性地探索了SVD在MoE模型压缩上的应用，并针对其失败原因提出了高度定制化的解决方案，包括选择性分解、V矩阵共享和U矩阵裁剪，形成了一个完整的框架。
*   **无需训练，效率高**：作为一种后训练压缩方法，避免了昂贵和耗时的重新训练过程，压缩过程本身耗时较短（文中案例为44分钟）。
*   **硬件友好，加速显著**：不依赖特定的稀疏硬件支持，可实现通用加速，且是直接减少激活专家的计算量，加速效果明确。
*   **性能保持优秀**：在极高压缩比下，相比同类方法能更好地保持模型原有效果，实现了性能与效率的良好平衡。
*   **实验扎实**：评估维度全面（语言建模+下游任务），对比基线丰富，消融实验细致，结论令人信服。

### 8. 不足与局限

*   **通信开销**：论文在局限性部分承认，SVD分解方法在张量并行场景下会引入额外的通信开销，尽管计算量的显著减少最终优化了总时间。
*   **压缩成本**：尽管无需训练，但压缩过程本身（激活值收集与SVD分解）需要一定的时间和计算资源，其计算复杂度可能随模型规模扩大而增加。
*   **校准数据依赖性**：方法的性能依赖于少量校准数据的选择，不同数据分布可能对结果有一定影响。
*   **长序列和复杂生成任务未评估**：评估主要集中在语言建模困惑度和常识推理任务上，缺少在长文本生成、代码生成、数学推理等更复杂和更具挑战性任务上的表现评估。
*   **超参数敏感性未深度探索**：虽然做了消融，但对于阈值 \( \tau \)、敏感度指标中权重分配等超参数选择的通用原则和自动化方法，未进行更深入的探讨。

（完）
