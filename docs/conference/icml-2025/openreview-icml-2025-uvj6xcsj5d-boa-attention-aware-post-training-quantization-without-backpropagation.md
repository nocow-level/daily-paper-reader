---
title: "BoA: Attention-aware Post-training Quantization without Backpropagation"
title_zh: BoA：无需反向传播的注意力感知后训练量化
authors: "Junhan Kim, Ho-young Kim, Eulrang Cho, Chungman Lee, Joonyoung Kim, Yongkweon Jeon"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Uvj6XcSJ5d"
tags: ["query:edge-llm"]
score: 10.0
evidence: 用于在资源受限设备上部署大语言模型的后训练量化算法
tldr: 针对大语言模型后训练量化中梯度优化计算量大的问题，提出无需反向传播的BoA算法，通过考虑层间依赖性来优化量化权重，在资源受限设备上高效部署LLMs且保持准确度。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-uvj6xcsj5d/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 734, \"height\": 305, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uvj6xcsj5d/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 856, \"height\": 239, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uvj6xcsj5d/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1058, \"height\": 678, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 831, \"height\": 304, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 509, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1639, \"height\": 1353, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 860, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 838, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1730, \"height\": 1428, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1761, \"height\": 1428, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1488, \"height\": 762, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1470, \"height\": 1045, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1717, \"height\": 2148, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1729, \"height\": 1427, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1705, \"height\": 1558, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1464, \"height\": 968, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1464, \"height\": 968, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uvj6xcsj5d/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1464, \"height\": 963, \"label\": \"Table\"}]"
motivation: 现有后训练量化方法要么依赖反向传播计算量大，要么忽略层间交互导致精度损失。
method: 提出注意力感知的不需反向传播的PTQ算法，通过建模层间依赖性优化量化权重。
result: 在多种LLM模型上实现了与基于梯度方法相当的量化精度，且计算开销明显降低。
conclusion: BoA为大规模LLM的高效量化部署提供了实用解决方案。
---

## Abstract
Post-training quantization (PTQ) is a promising solution for deploying large language models (LLMs) on resource-constrained devices. 
Early methods developed for small-scale networks, such as ResNet, rely on gradient-based optimization, which becomes impractical for hyper-scale LLMs with billions of parameters.
While recently proposed backpropagation-free or transformation-based methods alleviate this issue, they ignore inter-layer interactions or use the naive nearest-rounding-based quantized weight assignment to save the heavy computational cost of weight optimization.
In this paper, we introduce a novel backpropagation-free PTQ algorithm that optimizes quantized weights by considering inter-layer dependencies. 
The key innovation is the development of attention-aware Hessian matrices that capture inter-layer interactions within the attention module. 
Extensive experiments demonstrate that our approach not only outperforms existing weight quantization methods but also shows good synergy with conventional methods to suppress activation outliers, leading to state-of-the-art weight-activation quantization performance.
The code will be available at https://github.com/SamsungLabs/BoA.

---

## 论文详细总结（自动生成）

好的，这是对您提供的论文《BOA: Attention-aware Post-training Quantization without Backpropagation》的结构化、深入、客观的总结。

### 1. 核心问题与研究意义

*   **研究背景**：后训练量化是部署大语言模型到资源受限设备的关键技术。然而，早期针对小网络设计的PTQ方法依赖耗时的梯度优化，难以应用于拥有数十亿参数的LLMs。
*   **现存问题**：近期出现两类方法试图解决此问题：
    *   **免反向传播方法**：基于Hessian矩阵优化权重，但假设层与层之间相互独立，忽略了Transformer中关键的层间交互。
    *   **基于变换的方法**：通过平滑、旋转等操作使模型更抗量化，但在权重赋值上仍采用简单的最近舍入，导致性能受限。
*   **核心动机**：如何在不依赖反向传播的前提下，有效地将层间依赖关系建模到LLM的权重优化过程中，从而以可接受的计算成本实现更高的量化精度。

### 2. 方法论

本文提出了一种名为 **BOA** 的新型、免反向传播的PTQ算法，其核心在于利用注意力模块内的层间依赖关系来优化量化权重。

*   **核心思想**：**注意力感知的Hessian矩阵**
    *   传统方法（如GPTQ）的Hessian矩阵近似仅基于单层输入(`2XX^T ⊗ I`)，忽略了其他层的影响。
    *   BOA创新性地使用**注意力重建误差**替代层级重建误差来近似Hessian矩阵。这使得为查询、键、值和输出投影权重推导出的Hessian矩阵（见表1）不仅包含输入，还包含了其他层的的信息。例如，查询权重`W_Q`的Hessian为`2XX^T ⊗ K^T_h K_h`，它通过`K_h`（键）引入了层间依赖。

*   **关键技术细节与算法流程**：
    1.  **Hessian松弛**：为了降低计算原始Hessian矩阵（计算Softmax函数的雅可比矩阵`J_σ`会耗费巨大的内存和算力），BOA推导出一个基于上界的**松弛Hessian矩阵**，避免了直接计算`J_σ`。
    2.  **高效逆矩阵计算**：利用Kronecker积的性质，将大矩阵`( dd_h × dd_h )`的求逆和Cholesky分解，分解为两个较小矩阵`( d×d )`和`( d_h×d_h )`的对应操作，将计算复杂度从`O(d^3d^3_h)`降至`O(d^3)`。
    3.  **头式同步量化**：
        *   BOA的Hessian可对同一头内的不同行进行误差补偿。
        *   为加速处理，BOA**假设不同注意力头之间相互独立**。
        *   **量化步骤**：将所有头在同一行索引上的行堆叠成一个子矩阵，然后并行量化，类似于GPTQ。
        *   **补偿步骤**：利用推导出的特定行更新公式（命题3.1），在量化完一组行后，更新其余未量化的行以补偿误差。
        *   这种操作避免了逐行顺序量化，显著提升了处理速度（见表2，30B模型加速超40倍）。

### 3. 实验设计

*   **数据集与模型**：实验覆盖了多个主流开源LLMs，包括**OPT**、**LLaMA1**、**LLaMA2** 和 **LLaMA3**系列，模型规模从1B到30B不等。
*   **基准与评估指标**：
    *   **校准数据**：从WikiText-2中随机抽取128个长度为2048的序列。
    *   **评估指标**：WikiText-2数据集上的**困惑度**和8个零样本常识推理任务的**平均准确率**。
*   **对比方法**：
    *   **免反向传播方法**：主要对比 **GPTQ**。也对比了朴素的**最近舍入**方法。
    *   **基于变换的方法**：在权重或权重-激活量化实验中，与 **OmniQuant**、**AffineQuant**、**DuQuant**（+LWC）等前沿方法结合变换（QuaRot或SpinQuant）后的性能进行了比较。

### 4. 资源与算力

*   **硬件**：所有实验均在**单块 NVIDIA H100 GPU**上完成。
*   **处理时间**：
    *   BOA的量化速度慢于GPTQ，但远快于基于梯度优化的方法。例如，在LLaMA-7B模型上，BOA耗时0.96小时，而OmniQuant、AffineQuant分别需要1.83和4.32小时。随着模型增大，BOA的速度优势更加明显（见表5）。
    *   **内存消耗**：BOA的注意力感知Hessian矩阵需要更多内存（如30B模型需32.79 GB，GPTQ为8.27 GB），但通过“松弛BOA”（对值投影使用标准Hessian）可将内存显著降低（11.55 GB），同时保持优于GPTQ的性能（见表4）。

### 5. 实验数量与充分性

*   **实验数量**：论文进行了大量的实验，覆盖了多个模型家族、多种模型规模、多种比特宽度及多种量化配置，实验结果记录详细。
*   **充分性、客观性与公平性**：
    *   **充分**：实验设计全面，同时评估了权重仅量化和权重-激活同时量化两种场景。
    *   **公平客观**：在与基于变换的方法比较时，BOA同样对模型应用了变换，确保了比较基准的一致性。对于对比方法，论文使用其官方代码并遵循最佳实践（如激活LET、LWC选项等），结果报告客观。

### 6. 主要结论与发现

*   **性能优越**：在无变换的纯权重优化中，BOA在所有测试模型和比特宽度下，均在困惑度和零样本准确率上显著超越了 **GPTQ**。
*   **协同效应强**：当与模型变换方法结合后，BOA的性能进一步提升，不仅大幅领先结合变换的GPTQ，也超越了之前最优的、依赖梯度优化的变换方法，在多个任务上达到了**最先进的权重-激活量化性能**。
*   **效率与精度的权衡**：BOA以增加少量量化和推理时内存为代价，换取显著的精度提升，其量化处理速度相比梯度优化方法有巨大优势。

### 7. 优点

*   **创新性强**：首次实现了在免反向传播的PTQ框架内，正式建模并利用层间依赖关系来优化量化权重。
*   **工程实现巧妙**：通过Hessian松弛、利用Kronecker积性质分解计算、头式同步量化等一系列技术，有效解决了理论方案带来的高昂计算和内存开销，使其切实可行。
*   **性能突出**：在不牺牲过多速度的前提下，实现了与依赖梯度优化的SOTA方法相媲美甚至更优的量化精度。
*   **可组合性强**：该算法能与现有的模型变换类方法无缝结合，展现出优秀的通用性和协同潜力。

### 8. 不足与局限

*   **内存开销增加**：相比极简的一步式方法，BOA需要额外的内存来存储和计算Hessian信息。
*   **量化速度存在权衡**：虽然比梯度方法快，但BOA的量化过程仍慢于完全并行的GPTQ，存在一个速度与精度的权衡。
*   **头间独立性假设**：头式同步量化策略基于“不同注意力头之间相互独立”的假设，这可能是一个近似，存在理论上的精度风险。
*   **方法适用范围**：论文核心关注并只针对Transformer的**注意力模块**进行优化，对其他类型的层（如FFN）可能没有同等的优化效果。对于使用了分组查询注意力的模型，部分对比实验方法（如OmniQuant）的某些特性无法启用，虽然这并不影响对BOA自身的评估，但表明在跨模型适用性上需注意细节。

（完）
