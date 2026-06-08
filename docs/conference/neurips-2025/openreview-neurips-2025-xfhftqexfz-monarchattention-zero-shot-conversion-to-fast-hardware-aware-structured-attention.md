---
title: "MonarchAttention: Zero-Shot Conversion to Fast, Hardware-Aware Structured Attention"
title_zh: MonarchAttention：零样本转化为快速硬件感知的结构化注意力
authors: "Can Yaras, Alec S Xu, Pierre Abillama, Changwoo Lee, Laura Balzano"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=XfHfTqeXfZ"
tags: ["query:edge-llm"]
score: 9.0
evidence: 用Monarch矩阵逼近注意力以降低复杂度，支持有限内存下的推理
tldr: MonarchAttention针对Transformer注意力二次复杂度问题，提出基于Monarch矩阵的近似方法，将计算复杂度降至O(N√N d)且内存仅为O(Nd)。该方法支持零样本转换，即插即用，在几乎不损失精度的情况下实现快速、硬件友好的推理，为Transformer在资源受限设备上的部署扫清了主要障碍。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1441, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1434, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1434, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1512, \"height\": 1432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1415, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1444, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1517, \"height\": 1160, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xfhftqexfz/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1146, \"height\": 669, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-xfhftqexfz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1475, \"height\": 438, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xfhftqexfz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1355, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xfhftqexfz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 143, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xfhftqexfz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1433, \"height\": 138, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xfhftqexfz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1310, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xfhftqexfz/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1319, \"height\": 179, \"label\": \"Table\"}]"
motivation: Transformer注意力机制导致序列长度二次方复杂度，阻碍其在资源受限设备上的应用。
method: 利用Monarch矩阵对softmax注意力做变分近似，设计高效优化算法计算近似投影。
result: 达到O(N√N d)计算复杂度和O(Nd)内存，实现零样本迁移且性能损失极小。
conclusion: MonarchAttention为Transformer提供了一种即插即用的高效注意力替代方案，显著降低了硬件门槛。
---

## Abstract
Transformers have achieved state-of-the-art performance across various tasks, but suffer from a notable quadratic complexity in sequence length due to the attention mechanism. In this work, we propose MonarchAttention -- a novel approach to sub-quadratic attention approximation via Monarch matrices, an expressive class of structured matrices. Based on the variational form of softmax, we describe an efficient optimization-based algorithm to compute an approximate projection of softmax attention onto the class of Monarch matrices with $\Theta(N\sqrt{N} d)$ computational complexity and $\Theta(Nd)$ memory/IO complexity. Unlike previous approaches, MonarchAttention is both (1) transferable, yielding minimal performance loss with no additional training, even when replacing every attention layer of the transformer, and (2) hardware-efficient, utilizing the highest-throughput tensor core units on modern GPUs. With optimized kernels, MonarchAttention achieves substantial speed-ups in wall-time over FlashAttention-2: $1.4\times$ for shorter sequences $(N=256)$, $4.5\times$ for medium-length sequences $(N=4K)$, and $8.2\times$ for longer sequences $(N=16K)$. We demonstrate the quality of MonarchAttention on diverse tasks and architectures in vision and language problems, showing that it flexibly and accurately approximates softmax attention in a variety of contexts.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化总结。

---

### 1. 论文的核心问题与整体含义

-   **核心问题**：Transformer 模型的核心——注意力机制的计算复杂度与序列长度 \( N \) 成平方关系 \( \Theta(N^2 d) \)，这成为处理长序列时的关键瓶颈。
-   **现有解决方案的不足**：
    -   **低秩/稀疏近似方法**：虽然理论上降低了复杂度，但往往不可迁移，需要从头训练或微调；或者因与 GPU 硬件不兼容，在实践中无法实现真正的加速。
-   **整体含义**：本文提出了 **MonarchAttention**，一种新型的次二次方注意力近似方法。它能作为“即插即用”的组件（零样本迁移）直接替换预训练 Transformer 中的注意力层，在几乎不损失性能的前提下，利用现代 GPU 的硬件特性实现显著的推理加速。

### 2. 论文提出的方法论

-   **核心思想**：将软最大化注意力的计算视为一个受限于 Monarch 矩阵类的优化问题，通过最大化软最大值的变分形式来寻找最接近真实注意力的结构化矩阵。
-   **关键技术细节**：
    -   **Monarch 矩阵**：一种具有高度表达性的分块秩-1矩阵。用其近似注意力矩阵，可将存储和矩阵乘法复杂度均降低至 \( \Theta(N \sqrt{N} d) \)。
    -   **变分优化**：利用 softmax 的变分形式 \( \text{softmax}(z) = \arg \max_{a \in \Delta^N} \langle a, z \rangle + H(a) \)，将寻找注意力矩阵 \( A \) 转化为在 Monarch 矩阵约束下优化目标函数 \( f(A; Q, K) \)。
    -   **交替最大化算法**：
        -   将 Monarch 矩阵 \( M \) 分解为因子 \( L \) 和 \( R \)。当固定一个因子时，目标函数对另一个因子是凹的，可得到闭合形式的解，构成单次更新步骤。
        -   通过约束因子 \( L, R \) 的切片位于概率单纯形上，来保证最终的注意力矩阵 \( M \) 满足概率分布约束。
        -   求解过程被转化为一系列小批量矩阵乘法运算，可在 GPU 张量核心上高效执行。
-   **硬件感知实现**：
    -   整个计算过程被重塑为类似 FlashAttention 的 I/O 感知核函数，避免显存中物化大型中间矩阵（\( L, R \)），仅维护少量状态变量，实现 \( \Theta(Nd) \) 的最优 I/O 复杂度。

### 3. 实验设计

-   **数据集与任务场景**：
    -   **图像分类**：在 ImageNet-1K 上评估 ViT-B 模型。
    -   **问答**：在 SQuAD1.1 数据集上评估 RoBERTa-B 模型。
    -   **长文本摘要**：在 BookSum-chapters 数据集上评估 BART-B 模型。
    -   **图像生成**：在 ImageNet 上评估 DiT-XL 扩散模型。
    -   **图节点分类**：在 Actor 数据集上评估 GraphGPS 模型。
-   **Benchmark**：以原始 softmax 注意力的性能作为基准。
-   **对比方法**：与多种低秩近似注意力方法进行对比，包括 Linear-Transformer/Attention、Performer、cosFormer 和 Nyströmformer。同时，在运行速度上与 FlashAttention-2 进行直接对比。

### 4. 资源与算力

-   **硬件平台**：基准测试中明确指出，使用 **NVIDIA A40 GPU** 来比较 MonarchAttention 与 FlashAttention-2 的运行速度。
-   **训练与推理**：论文强调了其**零样本**能力，主要实验均为直接替换预训练模型的注意力层并评估，**未进行额外训练**。因此不涉及大规模的训练算力开销。仅在附录的 BART 摘要任务中，进行了少量微调实验。

### 5. 实验数量与充分性

-   **实验数量**：论文进行了约 5 个大类的任务实验，涵盖视觉和语言两大领域。每个任务内部又通过调整关键参数（如迭代步数 \( T \)、块大小 \( b \) 或对比方法的秩）来描绘性能与计算量的权衡曲线或表格，形成了近十组的详细对比。
-   **实验充分性**：实验设计较为充分。
    -   **多维度评估**：不仅包含性能指标（准确率、F1、ROUGE、FID），还包含了实际的运行耗时加速比，验证了其理论优势能转化为实际收益。
    -   **消融分析**：附录中提供了收敛性分析、逐层替换分析、不同替换比例分析、微调前后性能对比等，有效支撑了其方法的有效性。
-   **客观性与公平性**：对比方法具有代表性，涵盖了主流的高效注意力机制。在零样本设定下公平对比，各方法的关键超参数均在合理范围内调整以展示其最佳权衡。

### 6. 论文的主要结论与发现

-   **性能保持优**：MonarchAttention 在多种任务和模型中，作为零样本替代方案，能在显著降低计算量（如 ViT 任务中降低 80% FLOPs）的同时，保持与原始模型高度接近的性能。
-   **计算效率高**：相比 FlashAttention-2，MonarchAttention 在中等（4K）和长序列（16K）任务上分别实现了 4.5 倍和 8.2 倍的绝对加速，在短序列（256）上亦有 1.4 倍提升。
-   **硬件友好性**：成功利用了现代 GPU 的张量核心，克服了以往结构化稀疏方法在硬件上的不兼容问题，实现了理论与实践效率的统一。
-   **处理长序列能力强**：在长文本摘要任务中，其高效的近似使得处理 8K 长度的输入变得可行，其性能甚至超越了处理 2K 长度的原始 BERT 模型。

### 7. 优点：方法或实验设计上的亮点

-   **创新的方法论**：巧妙地将注意力近似问题转化为一个具有结构约束的变分优化问题，为高效注意力设计提供了新视角。
-   **零样本可迁移性**：这是该工作最显著的亮点，无需任何额外训练即可实现高效部署，极大降低了应用成本和技术门槛。
-   **软硬件协同设计**：算法设计与 GPU 内核实现深度绑定，通过批处理矩阵乘法充分利用了硬件算力，实现了真正的“硬件感知”。
-   **全面的实验验证**：不仅在多个标准任务上验证了精度，还通过实际测速证明了加速效果，实验证据全面且扎实。

### 8. 不足与局限

-   **对自回归模型支持有限**：MonarchAttention 无法直接应用于自回归解码过程，因为在逐步生成时不存在完整的“注意力矩阵”可供近似。它更适合编码器或非自回归模型的推理，或用于加速自回归模型的计算。
-   **结构化假设的固定性**：Monarch 矩阵采用统一的分块大小，而实际注意力模式的空间分布可能不均匀，固定结构可能导致一些区域的近似不够精细。
-   **实验覆盖的局限**：尽管任务多样，但主要在中等规模模型（如 ViT-B、RoBERTa-B）上验证，其在更大规模模型上的零样本迁移效果尚未可知。
-   **仅限于 softmax**：该方法专门针对 softmax 注意力设计，并未探索对其他注意力变体（如稀疏注意力）的泛化能力。

（完）
