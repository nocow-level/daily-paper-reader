---
title: Dynamic Sparse Training of Diagonally Sparse Networks
title_zh: 对角稀疏网络的动态稀疏训练
authors: "Abhishek Tyagi, Arjun Iyer, William H Renninger, Christopher Kanan, Yuhao Zhu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=bAUVnNc0Ky"
tags: ["query:edge-llm"]
score: 8.0
evidence: 结构化稀疏训练和自定义CUDA内核加速
tldr: 针对非结构化稀疏无法在现代硬件上实现实际加速的问题，提出DynaDiag对角结构化稀疏训练方法，在训练中保持对角线稀疏模式，并通过自定义CUDA内核加速计算。实验表明其性能与密集模型相当，且实现硬件友好的高效推理，有助于在资源受限设备上部署稀疏神经网络。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 860, \"height\": 609, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 824, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1739, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 835, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 1167, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 845, \"height\": 1231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1227, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1089, \"height\": 863, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bauvnnc0ky/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1765, \"height\": 561, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1231, \"height\": 1372, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 860, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 884, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 740, \"height\": 674, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1622, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 697, \"height\": 1027, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1441, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1233, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1605, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1427, \"height\": 1415, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1425, \"height\": 517, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1747, \"height\": 608, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1232, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1578, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1583, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bauvnnc0ky/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1578, \"height\": 881, \"label\": \"Table\"}]"
motivation: 非结构化稀疏难以转化为现代硬件上的实际加速。
method: 提出DynaDiag，一种对角结构化稀疏训练方法，在训练中保持对角线稀疏并进行稀疏计算，利用自定义CUDA内核加速。
result: 在性能上与非结构化稀疏相当，并实现硬件友好的加速。
conclusion: DynaDiag提供了一种适用于硬件的高效稀疏训练方案，推动了稀疏模型在推理加速中的应用。
---

## Abstract
Recent advances in Dynamic Sparse Training (DST) have pushed the frontier of sparse neural network training in structured and unstructured contexts, matching dense-model performance while drastically reducing parameter counts to facilitate model scaling. However, unstructured sparsity often fails to translate into practical speedups on modern hardware. To address this shortcoming, we propose DynaDiag, a novel structured sparse-to-sparse DST method that performs at par with unstructured sparsity. DynaDiag enforces a diagonal sparsity pattern throughout training and preserves sparse computation in forward and backward passes. We further leverage the diagonal structure to accelerate computation via a custom CUDA kernel, rendering the method hardware-friendly. Empirical evaluations on diverse neural architectures demonstrate that our method maintains accuracy on par with unstructured counterparts while benefiting from tangible computational gains. Notably, with 90\% sparse linear layers in ViTs, we observe up to a 3.13x speedup in online inference without sacrificing model performance and a 1.59x speedup in training on a GPU compared to equivalent unstructured layers.

---

## 论文详细总结（自动生成）

好的，以下是基于所提供论文《Dynamic Sparse Training of Diagonally Sparse Networks》的详细中文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：深度神经网络规模日益庞大，训练和推理成本高昂。动态稀疏训练（DST）旨在通过训练稀疏网络来降低计算和存储开销，同时保持模型性能。
*   **核心矛盾**：非结构化稀疏虽然在极高稀疏度下能保持模型精度，但由于其权重的随机分布模式，无法在现代硬件（如GPU）上有效地转化为实际的推理和训练加速。现有的结构化稀疏方法（如块稀疏、N:M稀疏）虽然对硬件友好，但在高稀疏度下往往会出现显著的性能下降，且多数方法在训练阶段无法实现加速。
*   **研究目标**：本文旨在提出一种新的结构化稀疏模式与训练方法，在性能上比肩非结构化稀疏，同时在训练和推理阶段均能实现真实的硬件加速，从而突破当前结构化稀疏方法的瓶颈。

### 2. 论文提出的方法论

核心思想是通过一种受“小世界网络”启发的**对角稀疏模式（Diagonal Sparsity）** 和配套的动态训练算法**DynaDiag**来解决问题。

*   **对角稀疏模式的数学表示**：
    *   一个权重矩阵 \( W \in \mathbb{R}^{M \times N} \) 被表示为多个对角线的和：\( W_K = \sum_{j=1}^K \tilde{\alpha}_j P_j \text{diag}(V_j) \)。
    *   \( K \) 是由目标稀疏度决定的对角线数量。
    *   \( P_j \) 是一个置换矩阵，定义了第 \( j \) 条对角线的位置（偏移量）。
    *   \( V_j \) 是一个值向量，包含了该对角线上的可训练参数。
    *   \( \tilde{\alpha}_j \) 是该对角线的可学习重要性权重。

*   **关键技术细节——动态对角选择算法**：
    *   **可微 Top-K 选择**：引入一个可学习的全局重要性向量 \( \alpha \)。在每个训练步骤中，通过一个带温度参数 \( T \) 的可微 softmax-TopK 函数，选择出当前最重要的 \( K \) 条对角线参与前向传播。温度系数 \( T \) 遵循余弦退火，从高值（探索）平滑过渡到低值（利用）。
    *   **稀疏正则化**：通过对 \( \alpha \) 施加 \( \ell_1 \) 正则化来鼓励其稀疏性，确保最终只保留少数关键对角线。
    *   **前后向加速**：在对角线模式被确定后，将其高效地转换为**块压缩稀疏行（BCSR）格式**。这种转换优化了两个目标：最小化块数量、最大化块内密度。利用自定义 CUDA 内核直接对 BCSR 格式的矩阵进行稀疏矩阵乘法，加速前向和反向传播计算。核心优势在于，对角稀疏矩阵及其转置结构相似，因此反向传播时无需额外开销即可转换回 BCSR 格式进行加速。

### 3. 实验设计

*   **数据集与场景**：
    *   **计算机视觉**：在CIFAR-10, CIFAR-100 和 ImageNet-1K 数据集上进行图像分类任务。
    *   **自然语言处理**：在 WikiText-103 数据集上进行语言建模任务，评估困惑度（Perplexity, PPL）。
*   **基准模型**：
    *   **视觉**：视觉Transformer（ViT-S/16, ViT-B/16, ViT-L/16, ViT-H/14）和 MLP-Mixer（Mixer-S/16）。
    *   **语言**：GPT-2 Small 和 GPT-2 Medium。
*   **对比方法**：
    *   **非结构化动态稀疏训练**：RigL, SET, MEST, CHT, CHTs.
    *   **结构化动态稀疏训练**：SRigL (N:M sparsity), DSB (Block sparsity), PixelatedBFly (Butterfly sparsity).
    *   **对角稀疏的启发式基线**：DiagHeur. (使用 RigL 的幅度增长-衰减策略，但限制在对角模式内).
    *   **剪枝方法**：Wanda (仅在比较时用于提供性能上界).
*   **评估指标**：
    *   **性能**：视觉任务的 Top-1 准确率，语言任务的困惑度。使用配对渐进麦克尼马尔检验衡量方法间差异是否显著。
    *   **效率**：在 GPU 上测量训练和推理的墙钟时间加速比。

### 4. 资源与算力

*   **硬件配置**：所有实验均在 NVIDIA Tesla A100 80GB GPU 上进行。
*   **算力细节**：论文详细报告了 ViT-Base 模型在不同稀疏度下的**训练和推理加速比（墙钟时间）**，例如在 90% 稀疏度下，DynaDiag 相比非结构化稀疏实现了 3.13 倍推理加速和 1.59 倍训练加速。但是，论文**并未明确报告**所有实验的总 GPU 卡数、总训练时长（如 GPU 时）等具体算力消耗。

### 5. 实验数量与充分性

实验设计**较为全面和充分**，具体体现在：
*   **多维度覆盖**：覆盖了计算机视觉和自然语言处理两大领域，测试了 MLP、Transformer 等多种架构，并在多个模型尺度（Small、Base、Large、Huge）上进行了验证。
*   **多稀疏度比较**：系统性地在从 40% 到 95% 乃至极端稀疏度（99.99%）的宽广范围内测试了所有对比方法，充分展现了各方法在不同压力下的表现差异。
*   **公平性保证**：
    *   所有对比方法的实验设置（如训练轮数、优化器）均与原论文保持一致或进行公平调整。
    *   对于性能比较，使用了严格的统计显著性检验（McNemar's test）来判断差异是真实存在还是随机波动。
    *   对于速度比较，使用墙钟时间，并针对每种方法的稀疏模式选择了最适合的加速库（如 RigL 用 cuSPARSE，块稀疏用 Triton 库，对角稀疏用自研 CUDA 内核），实验设计客观。

### 6. 论文的主要结论与发现

*   **性能领先**：DynaDiag 在所有测试的计算机视觉与自然语言处理任务上，均**在结构化动态稀疏训练方法中取得了最佳性能**，尤其在 90% 及以上的高稀疏度下，其优势更为显著。
*   **比肩非结构化**：DynaDiag 在多数稀疏度下与顶尖的非结构化稀疏方法（如 RigL, CHT）相比，性能**没有统计上的显著差异**，成功弥补了结构化稀疏的性能短板。
*   **真实加速**：与非结构化稀疏相比，DynaDiag 在 GPU 上实现了显著的训练和推理加速。例如，在 90% 稀疏的 ViT-Base 上，推理加速 3.13 倍，训练加速 1.59 倍。
*   **潜力巨大**：实验表明，通过轻量级的微调方法（如 LoRA-FA），DynaDiag 的性能甚至可以**超越非结构化稀疏的上限**。

### 7. 优点

*   **理论与实践结合**：从“小世界网络”获得灵感，设计出结构化稀疏模式，并提供了理论证明其对全输入输出覆盖和通用逼近性质的保证。
*   **全流程加速**：与大多数仅在推理时加速的结构化稀疏方法不同，DynaDiag 通过保留转置不变性的对角模式，实现了训练和推理的双重硬件加速。
*   **实现高效**：将新颖的对角稀疏模式转换为业界成熟的 BCSR 格式，并利用自定义 CUDA 内核，巧妙地平衡了算法创新与工程实现，降低了落地门槛。
*   **实验扎实**：实验覆盖了多领域、多模型、多稀疏度，并使用了统计检验确保结论的可靠性。

### 8. 不足与局限

*   **CNN 适用性未验证**：论文明确指出，由于 CNN 的卷积核在通道维度上搜索对角模式的巨大开销，DynaDiag 目前在 CNN 架构上的应用面临挑战，主要验证范围限于 Transformer 和 MLP。
*   **极端稀疏性探索有限**：虽然提到了在小世界连接假设下，矩阵在极端稀疏度（如 99.9999%）仍可能有效，但承认未找到好的示例模型来验证此假设。
*   **性能天花板**：在常规稀疏度（>90%）下，纯 DynaDiag 的性能依然略逊于顶尖的非结构化方法，需要借助微调才能超越。
*   **工程优化潜力**：论文提到其 PyTorch 实现未能完全利用 CUDA 内核优化，暗示报告的加速比仍有提升空间，当前实现可能不是最优的。
*   **算力详情缺失**：未能提供完整的训练算力报告，使得其他研究者难以精确估量其方法的训练成本。

（完）
