---
title: "LowRA: Accurate and Efficient LoRA Fine-Tuning of LLMs under 2 Bits"
title_zh: LowRA：2比特以下精确高效的LoRA大模型微调
authors: "Zikai Zhou, Qizheng Zhang, Hermann Kumbong, Kunle Olukotun"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Fm0nDMKBwC"
tags: ["query:edge-llm"]
score: 8.0
evidence: "实现低于2比特的LoRA微调，内存使用量最多减少50%"
tldr: 针对大模型微调资源开销大的问题，提出LowRA，支持1.15比特的超低位LoRA微调，通过精细量化优化和高效CUDA内核，在几乎不损失性能的情况下将内存占用减半，为边缘设备上的模型快速适配提供了可能。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1708, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 841, \"height\": 284, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 826, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 833, \"height\": 909, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1338, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1280, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1769, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1766, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1770, \"height\": 781, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1732, \"height\": 1505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fm0ndmkbwc/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1670, \"height\": 1497, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1773, \"height\": 1256, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 742, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 619, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 708, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 868, \"height\": 727, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1772, \"height\": 738, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1423, \"height\": 647, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1460, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1002, \"height\": 1340, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 909, \"height\": 728, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 900, \"height\": 677, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1012, \"height\": 1581, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fm0ndmkbwc/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1517, \"height\": 311, \"label\": \"Table\"}]"
motivation: 大模型规模扩大，甚至参数高效微调如LoRA也内存密集，限制边缘设备适配。
method: 设计LowRA，优化细粒度量化过程，包括映射、阈值和精度分配，并利用CUDA内核加速。
result: "在1.15比特下仍保持与高精度微调相当的性能，内存减少高达50%。"
conclusion: 超低位量化是可行的，大幅降低了微调资源需求，适用于资源受限场景。
---

## Abstract
Fine-tuning large language models (LLMs) is increasingly costly as models scale to hundreds of billions of parameters, and even parameter-efficient fine-tuning (PEFT) methods like LoRA remain resource-intensive.
We introduce LowRA, the first framework to enable LoRA fine-tuning below 2 bits per parameter with minimal performance loss.
LowRA optimizes fine-grained quantization—mapping, threshold selection, and precision assignment—while leveraging efficient CUDA kernels for scalable deployment.
Extensive evaluations across 4 LLMs and 4 datasets show that LowRA achieves a superior performance–precision trade-off above 2 bits and remains accurate down to 1.15 bits, reducing memory usage by up to 50\%. 
Our results highlight the potential of ultra-low-bit LoRA fine-tuning for resource-constrained environments.

---

## 论文详细总结（自动生成）

好的，这是对论文《LowRA: Accurate and Efficient LoRA Fine-Tuning of LLMs under 2 Bits》的结构化深度总结。

### 1. 论文的核心问题与整体含义

*   **研究动机与背景**：随着大语言模型（LLM）规模扩大到数千亿参数，即使是参数高效微调（PEFT）方法（如 LoRA）也变得资源密集，其内存开销仍可能超过单 GPU 的限制。尽管量化 LoRA（如 QLoRA、LoftQ）能缓解此问题，但现有方法存在三个根本局限，限制了其在超低位宽（低于 2 比特）下的应用：
    *   **L1 - 粗粒度精度分配**：对整个权重矩阵或层应用统一的量化精度，未能考虑到参数的细粒度敏感性差异。
    *   **L2 - 固定数据分布的假设**：依赖假设模型权重遵循固定全局分布（如正态分布）的量化格式，忽略了不同层甚至不同通道间分布的显著差异。
    *   **L3 - 缺乏高效系统支持**：大多依赖模拟量化，缺少针对低位宽和混合精度的 LoRA 微调优化的高性能 CUDA 内核，导致实际部署中内存节省和加速效果有限。
*   **核心问题**：如何突破 2 比特的量化极限，实现低于 2 比特的、几乎无性能损失的 LoRA 微调，从而将大模型适配能力扩展到资源极度受限的嵌入式或移动设备。
*   **整体含义**：论文提出了 LowRA 框架，这是首个能够在低于 2 比特每参数下实现精确 LoRA 微调的方案。它通过精细化的量化优化和高效系统实现，在保持精度的同时，将内存占用降低高达 50%，为在极端资源受限环境下的 LLM 部署和适配开辟了道路。

### 2. 论文提出的方法论

LowRA 是一个端到端框架，其核心思想在于通过三个关键组件系统性地解决现有量化 LoRA 方法的三大局限，实现超低位宽的精确微调。
*   **核心思想**：采用数据无关的一次性后训练量化，对预训练权重进行**细粒度、自适应的量化**，包含为每个输出通道学习独特的量化映射和阈值，并为其分配最优位宽。随后使用吸收量化误差的低秩矩阵初始化策略，并用定制的高效 CUDA 内核进行实际部署。
*   **关键技术细节**：
    1.  **映射与阈值学习器（L2 解决方案）**：
        *   **方法**：将每个输出通道的量化映射和阈值搜索问题形式化为一个**加权 Lloyd-Max 问题**。
        *   **流程**：以 QLoRA 的 NormalFloat 格式的初始阈值和映射为起点，迭代执行两步操作：
            *   **M 步**：根据分配的数据，重新计算量化映射值（作为加权后的聚类中心）。
            *   **E 步**：重新计算量化阈值（作为相邻映射值的中点）。
        *   **加权策略**：将每个 64 元素分组的最大绝对值（absmax，用于缩放）作为该组的权重。这使得算法更关注数值范围大的组，以最小化整体均方误差（MSE）。
    2.  **精度分配器（L1 解决方案）**：
        *   **方法**：提出一种**基于层次整数线性规划（ILP）的混合精度分配策略**，在给定总比特预算下，最小化所有通道的量化误差总和（SSE）。
        *   **预处理**：首先计算每个输出通道在 {1, 2, 4} 比特下的量化 MSE。然后按参数数量对通道进行分组，并在每组内基于 MSE 特征进行 K-Means 聚类（共 128 个簇）。
        *   **簇级 ILP**：决定每个簇内分别有多少通道被分配为 1、2 或 4 比特，以满足该组的比特预算并最小化总误差。
        *   **簇内 ILP**：在簇内部的通道间，依据预计算的 MSE 值，精准地将指定的比特数分配给具体的通道，实现最低的局部量化误差。
    3.  **高效 CUDA 量化原语（L3 解决方案）**：
        *   设计了支持细粒度和混合精度的 **量化与反量化 CUDA 内核**。
        *   量化时，内核根据通道的位宽和决策边界进行归一化和打包存储。
        *   反量化时，内核根据位宽解包，利用每个通道专属的查找表进行解码，并乘以分组的 absmax 恢复到浮点值。
*   **算法流程**：
    1.  输入预训练权重。
    2.  **学习映射/阈值**：映射与阈值学习器为每个输出通道生成优化的映射和阈值。
    3.  **分配精度**：两步 ILP 精度分配器根据用户定义的整体压缩比，为每个输出通道分配最优的 `{1, 2, 4}` 比特位宽。
    4.  **量化并初始化**：使用定制内核量化权重，计算量化误差，并利用 **LoftQ** 算法初始化低秩适配器以吸收该误差。
    5.  **微调**：量化后的权重冻结，仅训练低秩适配器，在训练过程中使用定制的反量化内核恢复基础权重。

### 3. 实验设计

*   **数据集与场景**：使用 4 个涵盖不同 NLP 任务的标准数据集进行评估：
    *   **WikiText-2**：语言建模任务。
    *   **OpenAssistant**：多轮对话任务。
    *   **XSUM** 和 **CNN/DailyMail**：长文本摘要任务。
*   **基准模型**：在 4 个不同规模的 LLM 上进行验证：
    *   LLaMA-2-7B、LLaMA-2-13B、BART-large，以及用于测试极限的 LLaMA-33B 和 LLaMA-65B。
*   **对比方法**：
    *   **QLoRA**：作为最早且广泛使用的量化 LoRA 方法，基线为 4 比特，将其适配到低于 4 比特进行对比。
    *   **LoftQ**：一种结合了混合精度量化和联合权重/适配器初始化的先进方法。

### 4. 资源与算力

*   **硬件平台**：所有评估实验均在单个 **NVIDIA A100 80GB** GPU 上进行，部分时序基准测试使用了 RTX A5000 和 RTX 3080。
*   **训练时长**：论文主要关注性能与内存权衡，未报告具体完整微调时长，但提供了单次迭代的运行时开销分析。
*   **预处理开销（明确的）**：
    *   **映射/阈值学习器**：在 A100 上，处理 BART-large/LLaMA2-7B/13B 分别耗时约 111/310/465 秒。
    *   **ILP 精度分配器**：在 2x Intel Xeon Gold 6342 CPU 服务器上，使用 8 个线程，处理上述模型分别耗时约 49/319/666 秒。
    *   这两部分均为离线一次性开销，对在线微调无影响。

### 5. 实验数量与充分性

*   **实验数量**：实验设计**非常充分**，包含数百个数据点。包括 4 个模型 × 4 个数据集 × （约 10 个量化位宽从 1.15 到 4.0 不等） × 3 种方法（LowRA、QLoRA、LoRA）的全方位对比，生成核心对比表（Table 2）。
*   **消融实验**：对 LowRA 的各个组件（仅精度分配器 vs. 精度分配器+映射/阈值搜索）在不同模型和数据集上进行了消融研究，验证了每个模块的贡献。
*   **内存分析**：对不同模型在不同量化位宽下的微调和推理内存占用进行了详细分解，论证了内存节省。
*   **硬件性能分析**：提供了模型加载延迟、吞吐量等端侧真实性能指标，从实践角度验证了方法的有效性。
*   **边界测试**：在 1.15 和 1.25 比特的极端设置下测试了 LLaMA-33B 和 65B 大模型，证明了方法的极限能力。
*   **客观性与公平性**：与基线方法的比较设置了相同的超参数，并专门讨论了与 LoftQ 结果存在差异的可能原因（如硬件差异、随机种子、量化实现细节等），体现了客观性。但需要注意，LoftQ 原作者未公开的部分细节（如实验种子）可能使复现不完全一致。

### 6. 论文的主要结论与发现

*   **更优的性能-精度权衡**：在相同精度下，LowRA 性能全面优于 QLoRA 和 LoftQ；在达到相同性能时，LowRA 平均可降低 0.86 比特每参数。
*   **首次实现低于 2 比特的 LoRA 微调**：LowRA 能在 1.75 比特甚至 1.15 比特下成功微调模型，而其他方法在此位宽下无法收敛或直接失败。
*   **显著的内存节省**：在微调和推理阶段，内存使用量减少 30-50%。据估计，这使得在内存为 16GB 的 NVIDIA Tesla T4 上微调 LLaMA-33B 成为可能。
*   **极低的系统开销**：其定制的 CUDA 内核引入的训练迭代开销最大仅为 8.5%，并且能执行 QLoRA 因内存不足而无法运行的配置。
*   **真实的硬件加速**：在实际 GPU 上，1.5 比特的 LowRA 比 4 比特的 QLoRA 加载速度快约 29%，并且推理吞吐量最高可提升 3.4 倍。

### 7. 优点

*   **突破性创新**：首次实现低于 2 比特的有效 LoRA 微调，突破了现有量化 LoRA 方法的极限。
*   **系统化解决方案**：从算法（精细化量化）到系统（CUDA 内核），提供了端到端的完整解决方案。
*   **精细粒度的量化设计**：将量化优化粒度下沉到输出通道级别，包括自定义的映射、阈值和位宽，设计思路合理且有效。
*   **实用性强**：设计目标明确指向资源受限的真实场景，方法具有数据无关、一次性量化、超参数无需调整的优点，易于部署。
*   **实验扎实全面**：在多种模型、数据集和任务上进行了详尽的性能、内存、烧蚀和真实硬件测试，验证力强。
*   **开源承诺**：承诺开源，有助于推动社区研究和应用。

### 8. 不足与局限

*   **LoftQ 基线比较的潜在偏差**：论文承认其 LoftQ 结果与原论文存在差异，归因于原方法的不可复现性（如未公开种子、模拟量化等）。这可能使得比较的基准并非 LoftQ 在最佳调优下的状态。
*   **精度分配的通用性**：消融实验（Table 8）显示，混合精度分配器在某些模型/任务上（如 LLaMA-7B 的 WikiText-2）带来的增益并不明显，其主要优势体现在其他场景（如 BART-large 的摘要任务）。其最佳应用场景和内在机理有待进一步阐明。
*   **ILP 预处理的可扩展性**：虽然已通过层次化 ILP 降低了复杂度，但该方法仍依赖于预量化来获取各通道的 MSE 曲线。对于参数规模极大且结构更复杂的模型，其预处理时间和 ILP 求解的扩展性仍是一个潜在挑战。
*   **未见大规模批次推理的优化验证**：论文提到该方法可适配数据中心生产环境，但目前的系统实现和评估仍侧重于资源受限的单一设备场景，对高并发批次推理情况下的计算效率提升验证不足。

（完）
