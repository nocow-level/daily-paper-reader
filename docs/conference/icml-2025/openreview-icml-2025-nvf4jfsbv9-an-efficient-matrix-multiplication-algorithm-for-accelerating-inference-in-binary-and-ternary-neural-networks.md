---
title: An Efficient Matrix Multiplication Algorithm for Accelerating Inference in Binary and Ternary Neural Networks
title_zh: 一种加速二进制与三进制神经网络推理的高效矩阵乘法算法
authors: "Mohsen Dehghankar, Mahdi Erfanian, Abolfazl Asudeh"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Nvf4jFsbv9"
tags: ["query:edge-llm"]
score: 9.0
evidence: 为二进制/三进制网络提出高效矩阵乘法算法，加速推理并减少内存
tldr: 针对深度神经网络推理效率低下问题，特别是大型语言模型，提出面向二值/三值权重矩阵的高效矩阵乘法算法，通过权重预处理压缩存储，加速推理并降低内存需求，推动了低精度网络在边缘设备上的实际应用。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1771, \"height\": 720, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 776, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 829, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1762, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 595, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 802, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 838, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1769, \"height\": 668, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1761, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 752, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 771, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nvf4jfsbv9/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 845, \"height\": 584, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nvf4jfsbv9/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 668, \"height\": 113, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nvf4jfsbv9/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 856, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nvf4jfsbv9/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 858, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nvf4jfsbv9/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nvf4jfsbv9/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 888, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nvf4jfsbv9/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 883, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nvf4jfsbv9/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1246, \"height\": 708, \"label\": \"Table\"}]"
motivation: 深度神经网络推理计算和内存开销大，限制其在资源受限设备上的应用。
method: 利用权重矩阵不变性，预处理创建索引，对数级压缩存储，优化矩阵乘法。
result: 降低了存储需求和计算复杂度，加速了二值/三值网络推理。
conclusion: 低精度网络结合专用算法能大幅提升推理效率，适用于边缘部署。
---

## Abstract
Despite their tremendous success and versatility, Deep Neural Networks (DNNs) such as Large Language Models (LLMs) suffer from inference inefficiency and rely on advanced computational infrastructure.
To address these challenges and make these models more accessible and cost-effective, in this paper, we propose algorithms to improve the inference time and memory efficiency of DNNs with binary and ternary weight matrices.
Particularly focusing on matrix multiplication as the bottleneck operation of inference, we observe that, once trained, the weight matrices of a model no longer change. This allows us to preprocess these matrices and create indices that help reduce the storage requirements by a logarithmic factor while enabling our efficient inference algorithms.
Specifically, for a $n\times n$ weight matrix, our efficient algorithm guarantees a time complexity of $O(\frac{n^2}{\log n})$, a logarithmic factor improvement over the standard vector-matrix multiplication.
Besides theoretical analysis, we conduct extensive experiments to evaluate the practical efficiency of our algorithms. Our results confirm the superiority of our approach both with respect to time and memory, as we observed a reduction in the multiplication time up to 29x and memory usage up to 6x. When applied to LLMs, our experiments show up to a 5.24x speedup in the inference time.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将以 Markdown 形式对该论文进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体意义

*   **研究动机与背景**：深度神经网络（DNN）和大语言模型（LLM）虽然在许多领域取得了巨大成功，但其推理过程计算效率低下，严重依赖昂贵的、专用的计算基础设施（如高端GPU）。这导致了高延迟、高能耗和高运营成本，限制了这些模型在普通消费设备上的部署和普及，并带来了网络依赖、隐私泄露等问题。
*   **核心问题**：为了解决上述挑战，研究聚焦于提高具有**二值（{0,1}）和三值（{-1,0,1}）权重**的量化神经网络的推理效率。这类量化模型（如1.58-bit LLM）在保持精度的同时，为计算加速提供了新的可能。
*   **整体意义**：本文旨在通过算法创新，从根本上提升二值/三值网络中最核心、最耗时的操作——**向量-矩阵乘法**的性能和内存效率，从而使先进模型能够更经济、更广泛地部署在资源受限的设备上。

### 2. 论文提出的方法论

核心思想是利用训练后权重矩阵**固定不变**这一特性，在推理前进行一次性的预处理，构造索引来压缩存储并加速推理时的矩阵乘法计算。

*   **预处理阶段：构建索引**
    *   **问题转化**：首先，将三值矩阵（A）分解为两个二值矩阵（B¹, B²）的差，即 `A = B¹ - B²`，从而将向量-三值矩阵乘法问题简化为向量-二值矩阵乘法问题。
    *   **三步构建索引**：
        1.  **列分块 (Column Blocking)**：将原始 n×n 的二值权重矩阵 B 划分为若干个更小的 `n × k` 的子矩阵（称为k-列块）。
        2.  **行置换 (Row Permutation)**：对每个列块，根据其行向量对应的二进制值（将长度为k的行视为二进制数）进行排序，生成一个置换索引（σ）。
        3.  **分段 (Segmentation)**：在排序后的列块中，标记具有相同二进制值的连续行区间的边界，形成一个分段索引列表（L）。一个列块的存储空间可由这些索引（σ, L）取代。
*   **推理阶段：高效向量-矩阵乘法**
    *   **RSR (Redundant Segment Reduction) 算法**：
        1.  **计算分段和 (Segmented Sum)**：对于输入的激活向量 v，根据预先计算的置换（σ）和分段（L）索引，快速计算出分段和向量 u。这相当于将 v 中对应于权重矩阵中相同行模式的部分提前求和，实现了**冗余计算复用**。
        2.  **块乘积**：计算分段和向量 u 与一个预定义的、包含所有可能二值行模式的矩阵 `Bin[k]` 的乘积。该步骤计算了小矩阵乘，而不是原始的 n×k 矩阵乘。
    *   **RSR++ 算法**：在 RSR 的基础上，进一步优化了第二步（`u · Bin[k]`）的计算。利用 `Bin[k]` 矩阵的特殊结构，通过迭代两两求和并提取奇数位和的方式，将这一步的时间复杂度从 `O(k·2^k)` 降为 `O(2^k)`。
*   **复杂度分析**：
    *   **存储**：与标准方法 `O(n²)` 相比，索引存储所需空间降为 `O(n² / log n)`，实现了对数级的压缩。
    *   **时间**：
        *   RSR 的推理时间复杂度为 `O(n² / (log n - log(log n)))`。
        *   RSR++ 进一步优化为 `O(n² / log n)`，相对于标准向量-矩阵乘法 `O(n²)` 实现了对数级的加速。

### 3. 实验设计

*   **场景与Benchmark**：
    *   **原生C++实现验证**：在随机生成的二值矩阵（大小从 `2¹¹` 到 `2¹⁶`）上进行向量-矩阵乘法，基准方法为标准的朴素矩阵乘法（Standard）。
    *   **Python (NumPy) 实现验证**：使用 NumPy 的 `np.dot()` 作为高性能基准，对比 RSR 算法在二值和三值随机矩阵（大小 `2¹¹` 到 `2¹⁵`）上的推理时间和内存占用。
    *   **真实LLM推理 (CPU)**：在1.58-bit量化的大语言模型（Llama3-8B, Falcon3-3B/10B）上，替换其全连接层的矩阵乘法为 RSR 算法，在包括`ShortQuestions`、`SimpleQuestions`和`TREC QA`的数据集上进行单token生成的推理时间测量。
    *   **真实LLM推理 (GPU)**：同上述LLM模型，评估在 GPU 上应用 RSR 的推理加速效果。
*   **对比方法**：
    *   在原生和NumPy实验中，主要对比标准/优化的矩阵乘法实现。
    *   在LLM实验中，对比未修改的1.58-bit基线模型与集成了 RSR 算法的模型。
    *   额外与专门优化的 **BitNet.cpp** 的CPU内核进行了性能比较。

### 4. 资源与算力

*   论文**未提及**预处理或训练阶段所需的算力（如GPU型号、数量、训练时长）。
*   对于LLM推理实验，文中明确说明了测试环境：一台配备**16核Intel Xeon CPU、NVIDIA Tesla T4 GPU、32GB RAM 和 Debian 11 操作系统**的服务器。

### 5. 实验数量与充分性

*   **实验组数**：论文进行了**多组、多维度**的实验，包括：
    *   2种实现方式（C++, Python）下的算法微观性能测试。
    *   对多种矩阵尺寸（`n` 值）的扩展性测试。
    *   2种权重类型（二值、三值）的测试。
    *   CPU和GPU两种硬件平台的推理测试。
    *   3个不同规模的真实LLM模型在3个数据集上的端到端测试。
    *   参数 `k` 的消融实验（寻找最优k值）。
*   **充分性与客观性**：实验设计**较为充分和客观**。它不仅有理论算法的微观验证，还延伸到了真实模型和硬件的宏观效果，并与高度优化的库（NumPy, PyTorch）以及专用内核（BitNet.cpp）进行了公平比较，多维度地验证了方法的有效性和实用性。

### 6. 论文的主要结论与发现

*   **理论贡献**：提出了一种通过预处理构造索引，在推理时复用冗余计算的高效矩阵乘法算法（RSR/RSR++），在理论上保证了对数级的时间复杂度改进和存储压缩。
*   **性能提升**：
    *   **微观层面**：在原生C++实现中，RSR++ 相比标准矩阵乘法实现了**最高29倍**的速度提升。
    *   **内存占用**：在NumPy实现中，预处理后的存储空间降低了**高达6倍**。
    *   **宏观应用**：在CPU上对真实1.58-bit LLM进行推理，实现了**最高5.24倍**的推理速度提升；在GPU上实现了**近2.5倍**的加速。

### 7. 优点

*   **理论坚实**：提供了清晰、严格的时间复杂度和空间复杂度分析，并得到了实验验证。
*   **方法优雅**：巧妙利用权重矩阵的静态性，通过“预处理-索引构建”将推理时的冗余计算转变为查找和分段求和，思路清晰。
*   **即插即用**：该方法无需重新训练或微调模型，可直接应用于任何已训练好的二值或三值网络。
*   **实用性强**：不仅提升了速度，还显著减少了内存占用，同时具备良好的并行化特性，对边缘计算部署极具价值。

### 8. 不足与局限

*   **实现层级限制**：论文坦诚其算法是在应用层实现的，并未充分利用底层的、硬件特定的指令优化（如PyTorch的cuBLAS、cuDNN等）。这导致其对高度优化的矩阵乘法库的加速比，不如对朴素算法的加速比显著。
*   **小矩阵效率**：对于规模较小的矩阵（如小于 2¹⁰），预处理的固定开销和算法常数项可能会抵消理论上的优势，实际收益不明显。这在真实模型中（如部分注意力头投影层）可能影响整体加速比。
*   **内存与速度的权衡**：虽然索引压缩了权重存储，但在推理时，尤其是在GPU上使用3D张量乘法的并行化方案，可能会产生额外的内存开销（如构造分段矩阵M），文中并未详细分析这种峰值内存变化。
*   **实验设备单一**：CPU实验仅在一款服务器CPU（Intel Xeon）上进行，缺乏在不同消费级CPU（如ARM架构）上的实验结果，这限制了“可在个人设备上部署”结论的普适性。

（完）
