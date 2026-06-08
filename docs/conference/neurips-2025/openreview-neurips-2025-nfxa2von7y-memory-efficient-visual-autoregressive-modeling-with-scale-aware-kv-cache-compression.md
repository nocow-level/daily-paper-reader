---
title: Memory-Efficient Visual Autoregressive Modeling with Scale-Aware KV Cache Compression
title_zh: 具有尺度感知KV缓存压缩的高效内存视觉自回归建模
authors: "Kunjun Li, Zigeng Chen, Cheng-Yen Yang, Jenq-Neng Hwang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=NFxA2Von7y"
tags: ["query:edge-llm"]
score: 4.0
evidence: 视觉自回归模型的KV缓存压缩，一种神经网络压缩技术
tldr: 提出ScaleKV框架，针对视觉自回归模型进行尺度感知的KV缓存压缩，但该技术与LLM端侧部署关联较弱。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1374, \"height\": 643, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1428, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1457, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1427, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1342, \"height\": 760, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1455, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1433, \"height\": 376, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1450, \"height\": 797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1452, \"height\": 1934, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1456, \"height\": 1945, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1436, \"height\": 1803, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-nfxa2von7y/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1437, \"height\": 1802, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-nfxa2von7y/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1441, \"height\": 660, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-nfxa2von7y/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1441, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-nfxa2von7y/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 977, \"height\": 346, \"label\": \"Table\"}]"
motivation: 视觉自回归模型推理时KV缓存呈指数增长，内存消耗大。
method: 根据层和尺度差异设计尺度感知KV缓存压缩。
result: 显著减少内存和计算冗余，同时保持生成质量。
conclusion: 该方法为视觉生成模型高效推理提供新思路，但与LLM端侧部署间接相关。
---

## Abstract
Visual Autoregressive (VAR) modeling has garnered significant attention for its innovative next-scale prediction approach, which yields substantial improvements in efficiency, scalability, and zero-shot generalization. Nevertheless, the coarse-to-fine methodology inherent in VAR results in exponential growth of the KV cache during inference, causing considerable memory consumption and computational redundancy. To address these bottlenecks, we introduce ScaleKV, a novel KV cache compression framework tailored for VAR architectures. ScaleKV leverages two critical observations: varying cache demands across transformer layers and distinct attention patterns at different scales. Based on these insights, ScaleKV categorizes transformer layers into two functional groups: drafters and refiners. Drafters exhibit dispersed attention across multiple scales, thereby requiring greater cache capacity. Conversely, refiners focus attention on the current token map to process local details, consequently necessitating substantially reduced cache capacity. ScaleKV optimizes the multi-scale inference pipeline by identifying scale-specific drafters and refiners, facilitating differentiated cache management tailored to each scale. Evaluation on the state-of-the-art text-to-image VAR model family, Infinity, demonstrates that our approach effectively reduces the required KV cache memory to 10% while preserving pixel-level fidelity.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

*   **研究背景**：视觉自回归（VAR）模型因其创新的“下一尺度预测”模式而备受关注，该模式在生成效率、可扩展性和零样本泛化能力上均有显著提升。不同于传统的逐token生成，VAR模型一次性生成整个token图，随后逐步细化到更高分辨率。
*   **核心问题**：VAR模型的“由粗到细”（coarse-to-fine）生成流程导致其键值（KV）缓存大小呈指数级增长，造成了巨大的显存消耗和计算冗余。例如，使用Infinity-8B模型生成1024x1024的图像时，批量大小为8的KV缓存可能占用高达85 GB的显存。
*   **整体含义**：本文旨在解决VAR模型在推理阶段面临的内存瓶颈，提出一种针对其多尺度特性的KV缓存压缩框架，以实现在显著降低内存占用的同时，保持高保真度的图像生成质量，从而推动该类模型在资源受限环境中的实际部署。

### 2. 论文提出的方法论

论文的核心思想是**ScaleKV**，一个尺度感知的KV缓存压缩框架，其关键流程如下：

*   **核心观察**：
    1.  **层间缓存需求差异**：不同的Transformer层表现出截然不同的注意力模式。一些层（称为**绘图者/草稿层，Drafters**）的注意力分散在多个历史尺度上，需要大的缓存容量；另一些层（称为**细化层/精炼层，Refiners**）的注意力则高度集中于当前的token图，处理局部细节，缓存需求极低。
    2.  **尺度间注意力模式差异**：随着生成尺度的增加，草稿层的注意力变得更加分散以整合全局上下文，而精炼层的注意力则变得更加集中。

*   **技术流程**：
    1.  **层功能分类**：提出**注意力选择性指数（Attention Selectivity Index, ASI）**，用于量化每一层在每一个尺度上的注意力模式。ASI通过综合当前尺度注意力比率和历史序列的Top-K注意力比率来计算。ASI值高表示该层更像精炼层，值低则更像草稿层。通过在一个小规模校准集上进行推理并计算每个“层-尺度”对的ASI值的Z分数，来自动将层分为草稿层和精炼层。
    2.  **缓存预算分配**：确定了草稿层和精炼层后，实施差异化的缓存预算分配策略。在总内存预算不变的情况下，为草稿层分配更大的缓存预算，而精炼层的缓存预算则随着生成尺度的增加而线性衰减，因为它们的注意力会变得越来越集中。省下的内存被重新分配给草稿层。
    3.  **KV缓存选择**：在预算确定后，为每个token图采样一个小的“观察窗口”。然后，根据窗口中每个token对剩余token的累积注意力分数，来选择最重要的KV对进行保留，其余部分则被裁剪掉。

### 3. 实验设计

*   **数据集与基准测试**：
    *   **一致性评估**：使用**MS-COCO 2017**验证集（5000张图像与描述），通过Fréchet Inception Distance (FID), Learned Perceptual Image Patch Similarity (LPIPS)和Peak Signal-to-Noise Ratio (PSNR)评估压缩模型输出与原模型的一致性。
    *   **质量评估**：使用**GenEval**和**DPG**基准测试来评估生成图像的感知质量和语义对齐度。

*   **对比方法**：与四种代表性的KV缓存压缩基线方法进行对比。
    *   **Sliding Window Attention**：仅保留最近的局部窗口token。
    *   **StreamingLLM**：保留注意力汇（初始token）和最近的token。
    *   **SnapKV**：基于注意力分数对token进行聚类和筛选。
    *   **PyramidKV**：采用固定的金字塔形层间预算分配策略。

*   **基础模型**：在两个不同规模的VAR文本生成图像模型上进行验证：**Infinity-2B** 和 **Infinity-8B**。

### 4. 资源与算力

*   **计算资源**：文中在分析推理延迟时提到，加速效果是在单个NVIDIA H20 GPU上测量得到的。
*   **算力细节**：论文没有提供关于模型训练所需的GPU型号、数量或训练时长的信息。该方法是一个后训练（post-training）的推理优化方法，其开销主要集中在少量校准数据上的层功能识别阶段，计算负担较小。

### 5. 实验数量与充分性

*   **实验数量**：论文包含了多组对比实验和消融研究，覆盖较为全面。
    *   **主对比实验**：在3个不同的内存预算（原缓存的4%, 10%, 20%）下，于两个模型（Infinity-2B, Infinity-8B）上与4个基线方法进行了对比。
    *   **质量基准测试**：在GenEval和DPG两个权威基准上测评并与当前最优模型比较。
    *   **分析实验**：对注意力分布、草稿层识别指标、精炼层预算衰减率等关键设计进行了消融研究。
    *   **效率分析**：分析了内存占用、批处理能力和推理延迟。
*   **充分性与客观性**：实验设计较为充分和客观。对比了最新的基线方法，使用了标准的评估指标和数据集，并分析了质量和效率的权衡。消融实验清晰地证明了各个设计组件的有效性。

### 6. 论文的主要结论与发现

*   ScaleKV能在只使用**原模型10%的KV缓存显存**情况下，实现几乎无损的图像生成质量。例如，Infinity-8B在使用压缩后，GenEval得分保持在0.79，DPG得分仅从86.61轻微下降到86.49。
*   该方法显著优于所有对比的KV缓存压缩基线方法，尤其是在极端的内存预算下，优势更为明显。
*   通过有效的缓存压缩，ScaleKV使得在更大约束的硬件上（如消费级显卡）和更大的批处理规模下部署VAR模型成为可能，并能实现高达1.25倍的推理加速。

### 7. 优点

*   **创新性强**：首次系统性地分析了VAR模型的尺度特异性注意力模式，并据此设计了尺度感知的KV缓存管理策略。
*   **方法论扎实**：提出的ASI指标和“草稿层/精炼层”的角色划分具有坚实的实证基础和理解深度，理论清晰。
*   **效果显著**：在极高的压缩率下（10倍），依然能保持与原始模型几乎一致的生成质量，效果远超同类通用压缩方法。
*   **实用价值高**：该方法计算开销小，易于实现，且能与现有技术兼容，可以直接应用于预训练好的模型以降低部署成本。

### 8. 不足与局限

*   **模型规模覆盖有限**：作者仅在Infinity系列模型（最大为80亿参数）上进行了实验，未能在更大规模的VAR模型上验证其可扩展性，这主要归因于更大规模开源模型的匮乏。
*   **依赖原始模型性能**：作为一个后处理的压缩方法，ScaleKV的性能上限受限于原始VAR模型。如果原始模型生成质量不佳，该方法无法改善生成质量。
*   **硬件平台单一**：推理延迟和加速比的实验仅在NVIDIA H20 GPU上进行，缺乏在其他硬件平台（如不同等级的消费级或服务器级GPU）上的普适性验证。


（完）
