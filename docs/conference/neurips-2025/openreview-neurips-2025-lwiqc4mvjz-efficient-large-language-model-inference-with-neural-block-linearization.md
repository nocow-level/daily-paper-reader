---
title: Efficient Large Language Model Inference with Neural Block Linearization
title_zh: 基于神经块线性化的高效大语言模型推理
authors: "Mete Erdogan, Francesco Tonin, Volkan Cevher"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=lwIQC4MVJZ"
tags: ["query:edge-llm"]
score: 9.0
evidence: 通过线性近似替代自注意力层加速Transformer模型推理
tldr: 提出神经块线性化方法，利用线性最小均方误差估计器替代自注意力层来加速LLM推理，无需微调即可在保持性能的同时实现显著加速。该方法通过典型相关分析确定线性化误差上界，选择误差最小的层进行替换，从而降低计算需求，适用于资源受限设备的部署。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-lwiqc4mvjz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 907, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-lwiqc4mvjz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1418, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-lwiqc4mvjz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 685, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-lwiqc4mvjz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1423, \"height\": 1627, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 767, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1456, \"height\": 790, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1456, \"height\": 793, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1452, \"height\": 571, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1451, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 626, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 896, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1110, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1179, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1177, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1176, \"height\": 439, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1177, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1439, \"height\": 1347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 707, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 910, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 709, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 732, \"height\": 514, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1449, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 811, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 812, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1448, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1450, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1449, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1457, \"height\": 1847, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-lwiqc4mvjz/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1383, \"height\": 335, \"label\": \"Table\"}]"
motivation: Transformer架构的LLM推理计算需求高，阻碍部署。
method: 采用线性最小均方误差估计器线性近似自注意力层，通过典型相关分析选择误差最小的层进行替换。
result: 在实验中实现了显著的计算加速，同时保持了模型性能。
conclusion: NBL框架为预训练LLM的高效推理提供了无需微调的加速方案。
---

## Abstract
The high inference demands of transformer-based Large Language Models (LLMs) pose substantial challenges in their deployment. To this end, we introduce *Neural Block Linearization* (NBL), a novel framework for accelerating transformer model inference by replacing self-attention layers with linear approximations derived from Linear Minimum Mean Squared Error estimators. NBL leverages Canonical Correlation Analysis to compute a theoretical upper bound on the approximation error. Then, we use this bound as a criterion for substitution, selecting the LLM layers with the lowest linearization error. NBL can be efficiently applied to pre-trained LLMs without the need for fine-tuning. In experiments, NBL achieves notable computational speed-ups while preserving competitive accuracy on multiple reasoning benchmarks. For instance, applying NBL to 12 self-attention layers in *DeepSeek-R1-Distill-Llama-8B* increases the inference speed by 32% with less than 1% accuracy trade-off, making it a flexible and promising solution to improve the inference efficiency of LLMs.

---

## 论文详细总结（自动生成）

好的，我将基于提供的论文内容，为您生成一份详细的中文总结。

---

# 高效LLM推理：神经块线性化方法 (Neural Block Linearization)

## 1. 研究背景与核心问题

-   **动机与挑战**：基于 Transformer 的大型语言模型（LLM）推理时计算需求极高，这严重阻碍了它们在资源受限或成本敏感场景下的实际部署。
-   **现有局限**：现有加速方法（如剪枝、量化、推测解码等）虽有效果，但直接移除自注意力层等结构化剪枝方法常导致显著的性能下降；而面向线性注意力的方法则通常需要大规模重训练。
-   **核心问题**：如何在不进行重训练的情况下，高效地识别并替换 Transformer 中冗余的自注意力层，以在保持原有性能的同时实现显著的推理加速。

## 2. 方法论

-   **核心思想**：提出 **神经块线性化（NBL）** 框架。该框架并非直接移除自注意力层，而是利用 **线性最小均方误差（LMMSE）** 估计器，用计算高效的线性变换来近似替代那些表现出高度线性冗余的自注意力层。
-   **关键技术：基于典型相关分析的误差约束与层选择**
    -   **问题建模**：将自注意力层的输入 $X$ 和输出 $Y$ 视为随机向量，目标是找到一个线性估计器 $\hat{Y} = WX + b$，以最小化均方误差（MSE）。
    -   **闭式解求解**：根据 LMMSE 理论，最优的权重 $W$ 和偏置 $b$ 具有闭式解：$W = C_{YX} C_{XX}^{-1}$， $b = \mathbb{E}[Y] - W\mathbb{E}[X]$。这允许直接从前向传播的统计量中计算线性层参数，无需梯度优化。
    -   **冗余量化与选择**：利用 **典型相关分析（CCA）** 衡量输入与输出之间的线性关系强弱。论文推导出线性近似误差（归一化均方误差，NMSE）的一个理论上界：
        $\text{NMSE}(Y, \hat{Y}) \le \sum_{i=1}^{h} (1 - \rho_i^2)$。
        其中 $\rho_i$ 是 $X$ 与 $Y$ 之间的典型相关系数。该上界越小，表明该层输出越能由输入线性预测，即冗余度越高。
    -   **算法流程**：
        1.  **校准**：使用少量校准数据集 $D$ 传入预训练 LLM，提取每层自注意力模块的输入 $X$ 和输出 $Y$。
        2.  **评估与排序**：对每一层，计算其 CCA 误差上界。该值越低，说明该层越适合被线性化。
        3.  **选择性替换**：选择分数最低（即最冗余）的 $m$ 个注意力层，用计算好的线性层（权重 $W$，偏置 $b$）进行替换。

## 3. 实验设计

-   **数据集与基准测试**：在多个推理基准上评估，包括**MMLU**（5-shot）、**ARC-easy/ARC-challenge**、**BoolQ**、**HellaSwag**、**OpenBookQA**、**PIQA** 和 **WinoGrande**（均为0-shot）。
-   **模型**：主要针对三款不同规模的模型进行了评估：
    -   **Mistral-7B** (32层)
    -   **Llama-3.1-8B** (32层)
    -   **DeepSeek-R1-Distill-Llama-8B** (32层)
    -   **Llama-3.1-70B** (80层，量化后评估)
-   **对比方法**：与当前主流的多种训练后压缩和剪枝方法进行了比较，包括：
    -   结构化剪枝：**SliceGPT**、**PruneNet**
    -   块/层丢弃：**SLEB**、**DROP**（分别应用于 Transformer 块和注意力层）
-   **评估指标**：
    -   **性能**：各基准上的准确率平均值。
    -   **效率**：相对于基础模型的 Prefill（提示处理）速度和吞吐量（逐 token 生成）提升倍数，以及键值（KV）缓存占用减少。

## 4. 资源与算力

-   **硬件**：所有模型的推理和评价均在单张 **NVIDIA A100 GPU (80GB)** 上完成。
-   **校准成本**：NBL 的校准过程无需训练，仅需对校准数据进行一次前向传播以收集统计量，然后进行协方差矩阵计算和 SVD 分解。
    -   **Llama-3.1-8B** 模型总校准时间约 **0.23 小时**。
    -   **Llama-3.1-70B** 模型总校准时间约 **1.75 小时**。
-   **量化结合**：对于 70B 模型，为了使其能装入单张 A100 GPU，采用了 4 位激活感知权重量化（AWQ）作为基础，并在其之上应用 NBL。

## 5. 实验充分性与客观性

-   **实验数量**：论文进行了大量的实验，涵盖：
    -   **3个不同规模**的主要模型。
    -   从4层到16层不等的**多种压缩比例**。
    -   与 **5 种**不同类型的基线方法对比。
    -   包括校准数据集、层选择标准、LoRA 微调、贪婪选择等在内的多组**消融研究**。
-   **充分性与公平性**：实验设计较为全面和公平。
    -   对比方法覆盖了主流的剪枝和层丢弃策略。
    -   消融实验深入分析了 NBL 对不同因素的鲁棒性，如校准数据分布（C4 vs. WikiText-2）、层选择准则（CCA上界 vs. 余弦距离）等，验证了其理论动机的有效性。
    -   提供了性能-效率的二维对比图及误差区间，增强了结论的可靠性。

## 6. 主要结论与发现

-   **优异的性能-效率权衡**：NBL 在实现显著推理加速的同时，能够最大程度地保持甚至匹配原始模型的准确性，明显优于直接移除层的 DROP、SLEB 等方法。
-   **量化效率提升**：例如在 **DeepSeek-R1-Distill-Llama-8B** 上，替换12个自注意力层（共32层），实现 **32%** 的吞吐量加速，而平均准确率损失**不到1%**。
-   **模块化与可叠加**：NBL 可以与其他加速技术（如量化、推测解码）正交结合，实现更大的累积加速。结合 EAGLE-3 推测解码后，加速比可达 **4.07倍**。
-   **鲁棒性**：NBL 对校准数据集的分布不敏感，且 CCA 上界比直接计算 NMSE 或使用余弦距离，在指导层选择上更稳定、更有效。

## 7. 论文优点

-   **理论扎实**：提供了基于 LMMSE 估计和 CCA 的严谨理论框架，给出了可量化的近似误差上界，用于指导层选择，而非单纯的启发式方法。
-   **高效且无需微调**：整个压缩过程仅需一次前向传播和解析计算，无需任何耗时的重训练或梯度更新，部署成本极低。
-   **方法灵活**：既可替换单个注意力层，也可替换整个 Transformer 块，且能与其他推理优化技术无缝集成。
-   **性能表现强劲**：在多个主流模型和基准上，对比多种现有方法，均展现出明显的帕累托最优性，即在同等速度下准确率最高，或在同等准确率下速度最快。

## 8. 不足与局限

-   **非线性局限**：该方法基于线性假设。对于存在高度非线性转换的层，线性近似会引入较大误差。尽管 CCA 上界能筛选出适合的层，但这本质上仍是一种近似，过度使用可能导致模型退化为浅层、无历史信息的模式。
-   **校准依赖性**：虽然实验结果显示对校准数据集不敏感，但在极端领域迁移或校准数据覆盖不足时，理论上仍存在引起幻觉等不良行为的风险。
-   **优化潜力**：当前压缩的实现并未进行细致的系统级或算子融合优化，可能未完全发挥其理论加速潜力。
-   **评估范围**：对长上下文和注意力密集型任务的评估相对有限，仅在附录中的 NVIDIA RULER 基准上补充了少量实验。

（完）
