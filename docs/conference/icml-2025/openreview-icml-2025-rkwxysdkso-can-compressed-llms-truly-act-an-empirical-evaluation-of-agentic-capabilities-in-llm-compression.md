---
title: Can Compressed LLMs Truly Act? An Empirical Evaluation of Agentic Capabilities in LLM Compression
title_zh: 压缩后的LLM能否真正行动？对LLM压缩中智能体能力的实证评估
authors: "Peijie Dong, Zhenheng Tang, Xiang Liu, Lujun Li, Xiaowen Chu, Bo Li"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=rkwXYSDKso"
tags: ["query:edge-llm"]
score: 6.0
evidence: 评估训练后压缩对LLM智能体能力的影响以支持资源高效部署
tldr: ACBench评估了压缩后的LLM在智能体任务上的表现，发现压缩会损害工具使用和长上下文推理等能力，这一基准为在资源受限设备上部署压缩LLM提供了重要参考，确保压缩模型在保持效率的同时不丧失关键的智能体功能。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1763, \"height\": 655, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1741, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 845, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 740, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1778, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1426, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1770, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1516, \"height\": 725, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1516, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 857, \"height\": 193, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 857, \"height\": 194, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 856, \"height\": 190, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 853, \"height\": 192, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 852, \"height\": 194, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 854, \"height\": 192, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1776, \"height\": 895, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1776, \"height\": 899, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1771, \"height\": 980, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rkwxysdkso/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1771, \"height\": 977, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1776, \"height\": 1007, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 738, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1773, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1777, \"height\": 436, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1777, \"height\": 465, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1424, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 636, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1776, \"height\": 1681, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1768, \"height\": 1002, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rkwxysdkso/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1776, \"height\": 1038, \"label\": \"Table\"}]"
motivation: 现有压缩基准忽略智能体能力，无法指导真实场景部署。
method: 构建ACBench基准，包含12项任务评估压缩对4类智能体能力的影响。
result: 4位量化会显著影响LLM的智能体表现，尤其是工具调用能力。
conclusion: ACBench揭示了压缩对LLM智能体能力的负面影响，为部署提供指导。
---

## Abstract
Post-training compression reduces the computational and memory costs of large language models (LLMs), enabling resource-efficient deployment. However, existing compression benchmarks focus narrowly on language modeling (e.g., perplexity) and natural language understanding tasks (e.g., GLUE accuracy), ignoring the agentic capabilities—workflow, tool use/function call, long-context understanding and real-world application. We introduce the Agent Compression Benchmark (ACBench), the first comprehensive benchmark for evaluating how compression impacts LLMs' agentic abilities. ACBench spans (1) 12 tasks across 4 capabilities (e.g., WorfBench for workflow generation, Needle-in-Haystack for long-context retrieval), (2) 4-bit quantization (GPTQ, AWQ) and 50% pruning (Wanda, SparseGPT), and (3) 15 models, including small (Gemma-2B), standard (Qwen2.5-7B), and distilled reasoning LLMs (DeepSeek-R1-Distill). Our experiments reveal compression tradeoffs: 4-bit quantization preserves workflow generation and tool use (1%--3% drop) but degrades real-world application accuracy by 10%--15%. We introduce ERank, Top-k Ranking Correlation and Energy to systematize analysis. ACBench provides actionable insights for optimizing LLM compression in agentic scenarios, bridging the gap between algorithmic efficiency and real-world applicability.

---

## 论文详细总结（自动生成）

好的，这是根据您提供的论文内容生成的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **研究动机与背景**：现有的大型语言模型（LLM）压缩技术评估基准（如 WikiText-2 和 GLUE）仅关注单轮语言建模和自然语言理解能力，忽略了模型在智能体场景下的关键能力。
*   **核心问题**：论文首次系统性地探究了训练后压缩（量化和剪枝）是否以及如何影响 LLM 的智能体能力，例如工作流生成、工具使用、长上下文理解和真实世界应用。
*   **整体含义**：该研究揭示了当前压缩方法在提升效率与保留高级智能体能力之间的复杂权衡，强调在部署面向真实应用的压缩LLM时，必须超越传统指标，全面评估其“行动”能力。

### 2. 论文提出的方法论

*   **核心思想**：论文的核心贡献并非提出新的压缩算法，而是构建了一个全面的评估基准和一套分析工具，用于衡量压缩对LLM智能体能力的影响。
*   **评估基准与框架**：
    *   **ACBench（智能体压缩基准）**：首个综合性基准，将智能体能力划分为四个核心维度，并在12项任务上进行评估。
        1.  **行动执行**：评估函数调用与工具使用能力（如 T-Eval 数据集）。
        2.  **工作流生成**：评估将复杂任务分解为可执行步骤序列的能力（如 WorfBench 基准）。
        3.  **长上下文理解**：评估处理长文本的能力（如 LongBench、LongGenBench 和 Needle-in-Haystack 测试）。
        4.  **真实世界应用**：评估在具体环境中的实操能力（如 AgentBoard 框架中的 ScienceWorld 和 Jericho 游戏）。
*   **分析工具**：为了系统化分析，论文引入了三种新颖的度量：
    1.  **高效秩 (ERank, Efficient Rank)**：通过分析模型 logit 矩阵的奇异值分布，量化压缩导致的结构复杂性损失，揭示模型决策过程的内部变化。
        *   **公式原理**：`eRank(A) = exp(-∑ (σi / ∑σj) * log(σi / ∑σj))`，其中 `σ` 是矩阵 `A` 的奇异值。ERank 值下降意味着信息丢失。
    2.  **Top-K 排名相关性 (Top-k Ranking Correlation)**：衡量压缩前后模型对前 K 个最可能 token 预测排名的一致性，使用 Jaccard 相似度计算。此指标解释了为何压缩后模型在下游任务中性能会下降。
        *   **公式原理**：`Jk = |T(o)_k ∩ T(c)_k| / |T(o)_k ∪ T(c)_k|`，其中 `T(o)_k` 和 `T(c)_k` 分别是原始模型和压缩模型预测的前 K 个 token 集合。
    3.  **能量分析 (Energy-based Analysis)**：借鉴分布外（OOD）检测思想，计算模型 logit 输出的能量分数，评估压缩前后模型置信度分布的偏移。
        *   **公式原理**：能量函数 `E(x; f) = -T * log(∑ e^(fi(x)/T))`，比较 `ΔE = |E(x; f(o)) - E(x; f(c))|`。`ΔE` 越小表示置信度模式保留越好。

### 3. 实验设计

*   **数据集与场景**：实验覆盖了用于评估四项智能体能力的多个基准数据集，具体如上文方法论所述。
*   **基准模型**：评估了15个 LLM，分为三类：
    *   中型模型 (7B)：InternLM-2.5-7B, Qwen2.5-7B, Mistral-7B 等。
    *   知识蒸馏模型：DeepSeek-R1-Distill 系列（基于 Qwen 和 LLaMA）。
    *   高效小模型 (<7B)：Phi-3.5, MiniCPM-4B, Gemma-2B, Megrez-3B 等。
*   **对比方法**：聚焦于与推理框架 vLLM 兼容的训练后压缩方法。
    *   量化：GPTQ 和 AWQ（主要对比4-bit，也包含8-bit）。
    *   剪枝：SparseGPT 和 Wanda（采用非结构化 50% 和半结构化 2:4 稀疏模式），同时对比了简单的幅度剪枝。

### 4. 资源与算力

*   论文未明确提及进行这些基准测试所使用 GPU 的型号、数量或总运行时长。其评估重点是压缩后模型的性能指标，而非压缩过程或推理的算力开销。

### 5. 实验数量与充分性

*   **实验数量**：实验规模非常庞大和全面。
    *   **多维度覆盖**：涉及 4 个智能体能力维度、12 个具体任务、15 个不同模型、以及多种量化（不同比特数）和剪枝（不同稀疏模式）方法的组合。
    *   **深入分析**：除性能对比外，还进行了大量的统计分析（ERank、Top-K一致性、能量）和可视化（注意力模式、Logit分布）。
*   **充分性与公平性**：
    *   **充分性**：实验设计十分充分，系统地回答了压缩对不同能力、不同模型架构和不同压缩方法的影响。
    *   **客观性与公平性**：实验设置是公平和客观的。所有压缩方法均使用相同的校准数据集（Pile 验证集的 128 个样本，序列长度为 512），并将推理温度设为 0 以确保可复现性。

### 6. 论文的主要结论与发现

*   **压缩存在能力权衡**：压缩技术对不同智能体能力影响各异。
    *   **4-bit 量化**能较好地保留工作流生成和工具使用能力（性能下降 1%-3%），但显著损害真实世界应用能力（准确率下降 10%-15%）。
    *   **剪枝方法**（特别是幅度剪枝）通常比量化方法造成更严重的性能退化。
*   **量化优于剪枝**：在大多数智能体任务中，量化（尤其是 AWQ/GPTQ）在相同压缩率下是比剪枝更好的选择，能更好地维持模型性能。
*   **蒸馏模型的意外退化**：经过推理模型（DeepSeek-R1）蒸馏得到的模型，在智能体任务上的表现普遍不如其未蒸馏的基座模型。这表明当前的蒸馏过程可能无法有效保留或转移智能体能力，甚至会牺牲这些能力以换取核心推理能力的提升。
*   **模型架构与规模敏感性**：大模型（如 32B）对压缩的鲁棒性更强；而小模型（如 1.5B/3B）在经历压缩时，其本就有限的智能体能力会急剧下降。不同模型系列（如 InternLM2.5 与 Qwen2.5）对压缩的敏感度也不同。
*   **结构化输出受影响更大**：压缩对生成 JSON 等结构化格式的性能影响，显著大于对生成普通文本格式的影响。
*   **分析工具的有效性**：低比特量化会导致模型表征的 ERank 值下降、Top-K 排名一致性降低以及能量分布的偏移，这从机理层面解释了性能退化的原因。

### 7. 优点
*   **问题新颖且重要**：首次系统性地关注模型压缩对高级“智能体能力”的影响，填补了研究空白，对实际部署有重要指导意义。
*   **基准设计全面**：提出的 ACBench 覆盖了四大核心能力、多种任务、多个主流模型系列和多种压缩方法，评估体系完整。
*   **分析工具深入**：不仅给出性能结论，还通过 ERank、Top-k 相关性和能量分析等工具，从表征和决策层面深入剖析了压缩产生影响的机理。
*   **结论具有实践价值**：提供了清晰的压缩策略建议，例如推荐使用 GPTQ/AWQ 进行量化，并明确指出在智能体场景下应谨慎使用剪枝和蒸馏技术。

### 8. 不足与局限
*   **算力信息缺失**：论文未报告进行大规模基准测试所需的算力资源，这可能影响他人复现或评估其成本。
*   **压缩方法覆盖不全**：研究仅聚焦于与 vLLM 框架兼容的训练后压缩方法，未涵盖诸如 QuaRot 或量化感知训练（QAT）等前沿技术。
*   **参数设置的局限性**：所有实验均使用默认配置，未探索不同参数（如量化组大小）对结果的影响，这可能限制了结论的普适性。
*   **校准数据依赖**：所有压缩方法均使用了相同的校准数据集（Pile 子集），其结论可能受到该特定数据集分布的影响。
*   **潜在偏差风险**：评估侧重于开源模型，结论可能不完全适用于 GPT-4 等闭源模型。同时，仅使用特定版本的压缩方法实现，可能存在实现偏差。

（完）
