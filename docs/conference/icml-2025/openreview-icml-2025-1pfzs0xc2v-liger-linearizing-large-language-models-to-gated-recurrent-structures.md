---
title: "Liger: Linearizing Large Language Models to Gated Recurrent Structures"
title_zh: Liger：将大型语言模型线性化为门控循环结构
authors: "Disen Lan, Weigao Sun, Jiaxi Hu, Jusen Du, Yu Cheng"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=1PfZs0xC2v"
tags: ["query:edge-llm"]
score: 10.0
evidence: 将预训练LLM线性化为高效门控循环结构，实现恒定内存部署
tldr: Liger将预训练大型语言模型转化为门控线性循环结构，从而在不重新训练的情况下实现恒定内存推理，显著降低了部署门槛。该方法克服了现有线性化方法依赖特征图模块和微调的局限，在保持性能的同时大幅提升了在资源受限设备上的运行效率。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-1pfzs0xc2v/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 828, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1pfzs0xc2v/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1668, \"height\": 755, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1pfzs0xc2v/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 786, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1pfzs0xc2v/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 858, \"height\": 351, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1517, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1767, \"height\": 639, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1776, \"height\": 694, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1690, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 549, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1750, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1141, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1588, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1809, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1pfzs0xc2v/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1821, \"height\": 404, \"label\": \"Table\"}]"
motivation: 从头预训练线性循环模型成本高，现有线性化方法需大量微调且忽略门控。
method: 提出Liger，将预训练LLM线性化为门控循环结构，无需额外特征图模块。
result: 实现恒定内存推理，在多任务上保持与原始模型相当的性能。
conclusion: Liger为LLM的高效部署提供了一种即插即用的线性化方案。
---

## Abstract
Transformers with linear recurrent modeling offer linear-time training and constant-memory inference. Despite their demonstrated efficiency and performance, pretraining such non-standard architectures from scratch remains costly and risky. The linearization of large language models (LLMs) transforms pretrained standard models into linear recurrent structures, enabling more efficient deployment. However, current linearization methods typically introduce additional feature map modules that require extensive fine-tuning and overlook the gating mechanisms used in state-of-the-art linear recurrent models. To address these issues, this paper presents \textbf{Liger}, short for \underline{\textbf{Li}}nearizing LLMs to \underline{\textbf{g}}at\underline{\textbf{e}}d \underline{\textbf{r}}ecurrent structures. Liger is a novel approach for converting pretrained LLMs into gated linear recurrent models without adding extra parameters. It repurposes the pretrained key matrix weights to construct diverse gating mechanisms, facilitating the formation of various gated recurrent structures while avoiding the need to train additional components from scratch. Using lightweight fine-tuning with Low-Rank Adaptation (LoRA), Liger restores the performance of the linearized gated recurrent models to match that of the original LLMs. Additionally, we introduce Liger Attention, an intra-layer hybrid attention mechanism, which significantly recovers 93\% of the Transformer-based LLM performance at 0.02\% pre-training tokens during the linearization process, achieving competitive results across multiple benchmarks, as validated on models ranging from 1B to 8B parameters.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **背景**：基于 Transformer 的大型语言模型（LLM）因其 softmax 注意力机制的平方复杂度，在长序列训练和推理时面临巨大的计算与内存瓶颈。线性循环模型（如线性注意力，状态空间模型）虽提供线性时间训练和恒定内存推理，但从头预训练这类非标准架构成本极高、风险大。
- **现存问题**：现有方法通过“线性化”将预训练 Transformer 转为线性循环结构，以实现高效部署。然而，这些方法普遍存在以下弊端：
  - 需要引入额外的特征映射（feature map）模块并进行大量微调，无法直接复用预训练参数。
  - 忽视了当前先进线性循环模型中至关重要的门控（gating）机制，导致架构差异大，难以有效逼近原始 softmax 注意力。
- **研究动机**：亟需一种无需新增参数、能充分融合门控机制的线性化方法，以极低成本将预训练 LLM 转换为高性能的门控线性循环模型，实现恒定内存推理。

## 2. 论文提出的方法论

- **核心思想**：**参数重利用**。不引入任何额外可训练参数，而是将预训练 Transformer 中冗余的 Key 投影矩阵 \(W_K\) 重用于构造门控机制，从而将标准注意力替换为门控循环结构。

- **关键技术细节**：
  - **门控构建（Key Projection + Pooling）**  
    利用原有 Key 投影计算 \(k_t = x_t W_K\)，再通过参数自由的池化（Pooling）操作和激活函数（如 \(\sigma\), \(\exp(-\text{softplus})\)）生成门控 \(G_t\)。该策略可适配多种现有门控线性循环模型（如 GLA、Mamba2、HGRN2、RWKV6 等）。
  - **线性化递归形式**  
    查询、键、值向量均来自预训练权重：  
    \(q_t, k_t, v_t = x_t W_Q, x_t W_K, x_t W_V\)。  
    状态更新：\(S_t = G_t \odot S_{t-1} + \phi(k_t)^\top v_t\)，输出：\(o_t = \phi(q_t) S_t\)。  
    特征映射 \(\phi(\cdot)\) 无需训练额外网络，直接使用简单的 **Softmax 归一化**，有效维持了与原始注意力分布的一致。
  - **轻量微调策略**  
    只对 \(W_Q, W_K, W_V\) 插入 **LoRA（Low-Rank Adaptation）** 低秩矩阵（秩设为 8），冻结其余全部参数。使用自回归交叉熵损失进行端到端微调，无需多阶段训练（如注意力蒸馏）。
  - **Liger Attention（层内混合注意力）**  
    提出一种层内混合机制，将门控循环建模（GRM）与滑动窗口 softmax 注意力（SWA，窗口大小 \(w=64\)）加权融合：  
    \(o_t = \alpha \cdot \text{GRM}(q_t, k_t, v_t) + \beta \cdot \text{SWA}(q_t, k_t, v_t)\)，其中 \(\alpha + \beta = 1\)（默认各为 0.5）。该设计保留了关键的非线性，同时整体计算复杂度维持在 \(O(T W D + T D^2)\)。
  - **层间混合架构**：可选择每隔若干层 Liger block 插入一个标准 softmax 注意力块，构成层间混合模型。

## 3. 实验设计

- **微调数据**：清洗后的 **Alpaca** 数据集（52K 条指令样本），总计约 0.02B tokens。
- **评测基准**：覆盖常识推理与知识理解的 6 个标准任务——**PiQA， ARC-easy， ARC-challenge， HellaSwag， WinoGrande， MMLU**，使用 `lm-evaluation-harness` 统一评测。
- **主要对比方法**：
  - 线性化方法：**SUPRA**， **MambaInLlama**， **LoLCATs**（包含两阶段变体）。
  - 预训练 Transformer：Mistral-7B， Llama-3-8B。
  - 从头预训练的线性/亚线性模型：Mamba-7B， RWKV-6-7B， Hawk-7B， Griffin-7B 等。
  - 混合模型：StripedHyena-Nous-7B， Zamba-7B， Zamba2-7B。
- **实验模型尺寸**：包括 Llama-3.2-1B， Llama-3.2-3B， Mistral-7B， Llama-3-8B。

## 4. 资源与算力

- **硬件**：所有实验均在 **单块 NVIDIA A800 80GB GPU** 上完成。
- **训练开销**（以 8B 模型为例）：微调采用 batch size=1、梯度累积步数=8，训练 2 个 epoch 的端到端线性化总耗时约 **4 小时**，GPU 显存占用约 **27 GB**。
- **推理效率评测**：同样在单张 A800 GPU 上，测试解码长度从 1K 至 32K，batch size=16 时的延迟与显存。

## 5. 实验数量与充分性

实验覆盖全面，主要包括：
1. **主线性化对比实验**（2个模型，多个基线，表2），验证 Liger 以极低 token 开销超越已有线性化方法。
2. **与预训练模型综合对比**（表3），展示其性能可媲美甚至超过部分从头预训练模型。
3. **可扩展性分析**（1B/3B/8B，表4），证明方法在不同规模模型上的一致性。
4. **多种门控结构适配**（GLA， HGRN2， GSA，表5），验证框架通用性。
5. **消融研究**（表6），专门分析门控构造方式、特征映射、LoRA 微调、混合注意力各组件的作用。
6. **效率分析**（图4），实测解码延迟与 GPU 内存，确认线性复杂度和恒定内存特性。
7. **辅助分析**：权重变化幅度对比（表7）、门控来源（Q/K/V）对比（表8）。

以上实验设置统一，对比基线多样，消融细致，总体较为**充分、客观、公平**。

## 6. 论文的主要结论与发现

- **高效性能恢复**：Liger 仅使用 **0.02B tokens**（即 0.02% 预训练量）的 LoRA 微调，就能恢复原始 Llama-3-8B 约 **93%** 的平均性能，在多个基准上显著超越 SUPRA、LoLCATs 等先前方法。
- **恒内存、线性时间推理**：线性化后的模型，解码延迟与显存占用随序列长度呈近线性增长且内存恒定（32K 序列仍为 16.37GB），无 OOM 问题。
- **门控重用的有效性**：直接基于 Key 投影构造的门控能有效替代额外可训练模块，且参数变化幅度小，减轻灾难性遗忘。
- **混合注意力的收益**：Liger Attention 进一步加速了线性化过程，并保持了输出分布逼近原始注意力。

## 7. 优点

- **参数零增量**：完全重用预训练权重，不引入任何新的特征映射或门控参数，架构简洁。
- **极低微调成本**：仅需训练 LoRA 低秩参数，在单卡 4 小时内完成 8B 模型的线性化，远超其他方案。
- **端到端流水线**：无需多阶段训练（如注意力迁移、再适配），直接端到端优化。
- **通用性与灵活性**：构建的门控方案可适配 GLA、HGRN2、GSA 等多种先进循环结构，且支持层内/层间混合架构。
- **理论与实践支撑**：利用 Key 矩阵冗余性构建门控，与记忆索引原理吻合，并通过实验充分验证。

## 8. 不足与局限

- **知识密集型任务仍存差距**：在 MMLU 等需要深层知识的任务上，线性化模型性能（43.4）相较原始 Transformer（65.3）有明显跌落。
- **实验规模有限**：仅在最大 8B 参数模型上验证，更大规模（如 70B， 405B）的线性化效果未知。
- **微调数据单一**：仅使用 Alpaca 指令数据，缺乏代码、数学、多语言等多样数据的验证，可能引入微调分布偏差。
- **超参数敏感性未充分探索**：滑动窗口大小（64）、混合权重（0.5）等关键超参数未进行系统的敏感性分析或自适应机制研究。
- **长上下文任务评测缺失**：虽验证了推理效率，但未专门评估线性化模型在长文档摘要、长对话等实际长序列任务上的能力。

（完）
