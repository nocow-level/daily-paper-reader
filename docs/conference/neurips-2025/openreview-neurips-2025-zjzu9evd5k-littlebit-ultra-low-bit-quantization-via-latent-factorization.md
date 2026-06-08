---
title: "LittleBit: Ultra Low-Bit Quantization via Latent Factorization"
title_zh: "LittleBit: 基于潜在分解的超低位量化"
authors: "Banseok Lee, Dongkyu Kim, Youngcheon you, Young-Min Kim"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=zJzu9evD5K"
tags: ["query:edge-llm"]
score: 10.0
evidence: 通过潜在因子分解实现0.1比特极端量化，内存缩减31倍，助力端侧部署
tldr: 为应对大语言模型部署中的庞大内存需求，本文提出LittleBit框架，采用低秩因子分解将权重表示为二值化因子，并结合多尺度补偿策略，实现低至0.1比特每参数的极端压缩。实验表明，该方法可将Llama2-13B压缩至0.9GB以下，内存缩减约31倍，同时保持模型质量，为在边缘设备上高效运行LLM提供了可行的压缩技术。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1286, \"height\": 687, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1224, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1304, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1436, \"height\": 811, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 690, \"height\": 222, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1014, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1457, \"height\": 786, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zjzu9evd5k/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1325, \"height\": 556, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1303, \"height\": 685, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1304, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1386, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 591, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1011, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1457, \"height\": 786, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1013, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1297, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 808, \"height\": 706, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 723, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1461, \"height\": 848, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1460, \"height\": 777, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1317, \"height\": 670, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1446, \"height\": 818, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zjzu9evd5k/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1012, \"height\": 318, \"label\": \"Table\"}]"
motivation: 大语言模型部署受限于巨大的内存和计算需求，极端低位量化面临保真度挑战。
method: 提出LittleBit框架，通过低秩潜在因子分解表示权重并二值化，配合多尺度补偿机制。
result: 将Llama2-13B压缩至不足0.9GB，约31倍内存缩减，在极低位宽下保持模型性能。
conclusion: 该方法突破了极低位量化极限，为LLM在资源受限边缘设备上的部署开辟了新途径。
---

## Abstract
The deployment of large language models (LLMs) is frequently hindered by prohibitive memory and computational requirements. While quantization mitigates these bottlenecks, maintaining model fidelity in the sub-1-bit regime remains a persistent challenge. In this paper, we introduce LittleBit, a novel framework for extreme LLM compression. We target quantization rates as low as $0.1$ bits per weight (BPW), achieving a memory reduction of approximately $31\times$, which effectively compresses Llama2-13B to under $0.9$ GB. We represent weights via low-rank latent matrix factorization and subsequently binarize the resulting factors. To counteract the information loss inherent to such drastic precision reduction, we integrate a multi-scale compensation mechanism that learns importance parameters across row, column, and latent dimensions. Two primary contributions enable effective training: Dual Sign-Value-Independent Decomposition (Dual-SVID) for quantization-aware training (QAT) initialization, and Residual Compensation to minimize approximation errors. Extensive experiments confirm the superiority of LittleBit in the sub-1-bit domain; for instance, our method at $0.1$ BPW surpasses the performance of leading techniques operating at $0.7$ BPW on Llama2-7B. We establish a new size-performance trade-off---unlocking a potential $11.6\times$ inference speedup relative to FP16---and render powerful LLMs practical for resource-constrained environments. Our code is available at https://github.com/SamsungLabs/LittleBit.

---

## 论文详细总结（自动生成）

好的，作为资深学术论文分析助手，我将根据您提供的论文内容，以 Markdown 格式生成一份结构化、深入且客观的中文总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**: 大语言模型（LLM）的部署受限于高昂的内存和计算需求。现有的量化技术虽然能缓解这一问题，但在低于1比特的超低位宽（sub-1-bit）领域，尤其是在0.1比特/权重（BPW）这种极端压缩率下，维持模型性能（保真度）仍然是一个巨大的挑战。
*   **研究动机**: 即使是1比特模型也难以在极度资源受限的设备上运行。因此，研究工作旨在突破子比特量化的极限，探索在0.1 BPW级别实现有效压缩的方法，以大幅缩减模型内存占用。
*   **整体含义**: 该研究不仅提出了一种极端的模型压缩技术，更开创了一种新的模型尺寸与性能的权衡关系。这意味着可以在几乎不牺牲模型基本能力的前提下，将其体积缩小数十倍，使得强大的LLM在消费级或边缘设备上的实际部署成为可能。

### 2. 论文提出的方法论

LittleBit 框架的核心思想是**将低秩矩阵分解与二值化相结合，并辅以多尺度补偿机制**来对抗极端压缩带来的信息损失。

*   **核心技术思想**:
    *   **低秩分解与二值化**: 利用LLM权重矩阵具有低秩特性的观察，首先将原始权重矩阵 $W$ 近似表示为两个小矩阵的乘积 $W \approx UV^\top$。然后，对分解后的因子 $U$ 和 $V$ 进行二值化处理（$U_{sign} = \text{sign}(U), V_{sign} = \text{sign}(V)$），将其存储为 $\pm 1$。
    *   **多尺度补偿机制**: 为了弥补二值化造成的巨大信息损失，框架引入了一组可学习的、全精度（FP16）的缩放因子。这超越了常规的行、列缩放，额外地引入了**一个潜在维度缩放因子 $\ell$**，用于学习 $r$ 个潜在维度的相对重要性。
    *   **初始化与误差修正**:
        *   **Dual-SVID 初始化**: 提出一种基于奇异值分解（SVD）的初始化方法，能够将原始权重的符号和幅度信息有效地映射到 LittleBit 的可学习参数（$U, V, h, g, \ell$）上，为量化感知训练（QAT）提供稳定且逼近原始权重的起点。
        *   **残差补偿**: 引入一个与主路径结构平行的辅助路径，专门用于学习并补偿主路径近似产生的残差误差。最终的等效权重是两条路径输出之和：$\widehat{W} = \widehat{W}_{pri} + \widehat{W}_{res}$。这种方法在不增加总参数预算的情况下，能有效提升模型精度。
*   **算法流程/公式**:
    *   **等效权重构建**: 主路径的等效权重通过下式隐式构建，无需显式存储：
        $\widehat{W}_{pri} = \text{diag}(h)U_{sign}\text{diag}(\ell)V_{sign}^\top\text{diag}(g)$
    *   **高效前向传播**: 对于输入 $X$，前向计算 $Y = X\widehat{W}_{pri}^\top$ 可以被高效地分解为小规模二值矩阵乘法和逐元素缩放操作，避免了使用巨大的全精度矩阵乘法（GEMM）：
        $Y = ((((X \odot g)V_{sign}) \odot \ell)U_{sign}^\top) \odot h$
    *   **训练**: 使用量化感知训练（QAT）和知识蒸馏（KD）对整个框架进行优化，目标损失函数结合了输出 KL 散度损失和中间层 MSE 损失。

### 3. 实验设计

*   **数据集与场景**:
    *   **语言建模**: 使用 `WikiText-2` 作为主要验证集评估困惑度（PPL），并在 `C4` 和 `PTB` 数据集上进行了泛化性测试。
    *   **零样本推理**: 在 7 个常识推理基准上评估零样本准确率，包括 `WinoGrande`, `OBQA`, `HellaSwag`, `BoolQ`, `ARC-e`, `ARC-c`, `PIQA`。
*   **基准模型（Backbone）**: 实验覆盖了多种主流 LLM 架构和规模，包括 `OPT` (1.3B)、`Llama` (7B)、`Llama2` (7B, 13B)、`Llama3` (8B)、`Phi-4` (14.7B) 和 `QwQ` (32B)。
*   **对比方法**: 与多个 SOTA 量化方法进行了全面比较，覆盖了不同范式：
    *   **后训练量化（PTQ）**: `RTN`, `GPTQ`, `OmniQuant`, `BiLLM`, `STBLLM`。
    *   **量化感知训练（QAT）**: `OneBit`, `BinaryMoS`。
    *   **对比位宽**: 重点在子比特领域（0.1 到 1.0 BPW）进行比较，尤其与 `STBLLM` 在 0.8, 0.7, 0.55, 0.3 BPW 进行了直接对标。

### 4. 资源与算力

*   **训练硬件**:
    *   对于大部分模型（OPT-1.3B 到 Phi-4-14.7B），使用了 **4块NVIDIA H100 GPU**（表示为 $1 \times 4$）。
    *   对于最大的 QwQ-32B 模型，使用了 **32块NVIDIA A100 GPU**（表示为 $4 \times 8$，即4个节点，每节点8卡）。
*   **训练时长**: 论文未明确提及每个实验的具体训练时长，但说明了所有实验均训练 **5个 Epoch**。

### 5. 实验数量与充分性

*   **实验组数**: 实验设计相当充分和全面。
    *   **模型覆盖度**: 在 6 种不同规模和家族的 LLM（从 1.3B 到 32B）上进行了验证。
    *   **位宽覆盖度**: 在从 0.1 BPW 到 1.0 BPW 的多个位宽级别进行了测试。
    *   **任务多样性**: 涵盖了语言建模（困惑度）和零样本推理（7项任务），并进行了全精度、0.55 BPW 和 0.3 BPW 条件下的对比。
*   **消融实验**: 提供了多项消融实验来验证关键设计的有效性，包括：
    *   残差补偿模块的有效性（附录 B.1）。
    *   `SmoothSign` 与 `STE` 梯度估计器的对比（附录 B.2）。
    *   针对分组查询注意力（GQA）机制模型的潜在秩调整策略（附录 B.3）。
    *   剪枝 vs SVD 基线的对比（附录 E）。
*   **客观性与公平性**: 与多种公开的 SOTA 基准方法（PTQ 和 QAT）在标准数据集和评估协议下进行了直接比较，实验结果具有说服力和客观性。

### 6. 论文的主要结论与发现

*   **极低位宽性能领先**： LittleBit 在子比特量化领域，尤其是低于 0.5 BPW 的极端压缩场景下，性能显著优于先前最先进的 STBLLM 等方法，后者在 0.3 BPW 时性能已严重下降甚至崩溃。
*   **开辟新的性能边界**： 该方法成功将 Llama2-13B 压缩至 0.9 GB 以下（约 31倍压缩），并在 0.1 BPW 下保持了模型的可用性，其表现甚至超越了某些方法在更高位宽（0.7 BPW）下的结果。
*   **关键技术的有效性**： Dual-SVID 和 Residual Compensation 是实现稳定且高效 QAT 训练的关键，保证了模型在极致压缩下的学习动态。
*   **计算加速潜力**： 通过自定义CUDA内核验证，LittleBit 的架构有潜力实现相对于 FP16 高达 11.6 倍的推理延迟加速。
*   **KV缓存压缩**： 该方法还会自然地压缩 KV Cache，其存储量可减少达 21.3 倍。

### 7. 优点

*   **创新的架构**： 将低秩分解、二值化和多维度缩放补偿创造性地结合，为极端量化提供了一个强大且高效的框架。
*   **技术深度与完整性**： 不仅提出了架构，还配套设计了精妙的初始化（Dual-SVID）和误差修正（Residual Compensation）策略，形成了一套完整的训练方案。
*   **极致的性能**： 在 0.1 BPW 这种前所未有的低位宽下证明了模型可用性，显著推动了该领域的边界。
*   **全面的实验验证**： 在多种模型、多个位宽和不同任务上进行了详尽的评估和消融研究，结论坚实可靠。
*   **出色的工程价值**： 内存缩减31倍、推理加速11.6倍、KV缓存压缩，这些指标直接体现了巨大的部署价值。

### 8. 不足与局限

*   **训练成本高昂**： 必须使用 QAT 是其主要限制之一，对于数十亿参数的模型，即便是使用4块H100或32块A100，训练开销依然非常大，难以扩展到超大规模模型（如 70B 以上）。
*   **词表头部未压缩**： 当前的压缩主要针对 Transformer 块，语言模型头（`lm_head`）未被同等压缩。在极端压缩率下，`lm_head` 会成为新的存储瓶颈。
*   **推理延迟的优化空间**： 虽然自研内核展示了加速潜力，但其与高度优化的库（如 cuBLAS）相比仍有优化空间，端到端加速比（约2.46倍）低于内核层面的理论收益（11.6倍），表明存在内存访问等瓶颈。
*   **生成文本的质量退化**： 附录中的生成样本分析显示，模型在极低位宽（如 0.1 BPW）下虽然能维持语法结构，但事实准确性和逻辑连贯性会严重下降，可能出现幻觉。
*   **未报告误差棒**： 由于计算成本所限，实验结果是基于单次运行的报告，这符合该领域惯例，但无法评估随机性带来的统计差异。

（完）
