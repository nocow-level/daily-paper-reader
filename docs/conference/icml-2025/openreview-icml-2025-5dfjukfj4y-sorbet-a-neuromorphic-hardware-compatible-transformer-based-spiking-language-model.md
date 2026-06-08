---
title: "Sorbet: A Neuromorphic Hardware-Compatible Transformer-Based Spiking Language Model"
title_zh: Sorbet：一种神经形态硬件兼容的基于Transformer的脉冲语言模型
authors: "Kaiwen Tang, Zhanglu Yan, Weng-Fai Wong"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=5dFJukfj4y"
tags: ["query:edge-llm"]
score: 9.0
evidence: 面向边缘语言模型的神经形态硬件兼容Transformer
tldr: 针对边缘设备上语言模型的能效需求，Sorbet提出了一种神经形态硬件兼容的Transformer脉冲语言模型。通过引入基于移位的softmax和硬件友好的层归一化，解决了关键操作在神经形态硬件上的实现难题。该方法使Transformer模型能够部署在低功耗神经形态芯片上，在保护隐私的同时实现高效的边缘语言处理。实验验证了其能效优势。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-5dfjukfj4y/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1351, \"height\": 683, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5dfjukfj4y/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 840, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5dfjukfj4y/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 838, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-5dfjukfj4y/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1359, \"height\": 1631, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 854, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 855, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1768, \"height\": 651, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1445, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 654, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 695, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 986, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-5dfjukfj4y/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 949, \"height\": 253, \"label\": \"Table\"}]"
motivation: 边缘端语言模型需要高能效，但神经形态硬件上Transformer的softmax和层归一化难以实现。
method: 提出Sorbet，采用新型移位softmax和兼容的层归一化，构建神经形态硬件兼容的脉冲语言模型。
result: Sorbet实现了在神经形态硬件上高效运行Transformer语言模型。
conclusion: Sorbet为边缘能效语言模型提供了神经形态硬件部署的解决方案。
---

## Abstract
For reasons such as privacy, there are use cases for language models at the edge. This has given rise to small language models targeted for deployment in resource-constrained devices where energy efficiency is critical. Spiking neural networks (SNNs) offer a promising solution due to their energy efficiency, and there are already works on realizing transformer-based models on SNNs. However, key operations like softmax and layer normalization (LN) are difficult to implement on neuromorphic hardware, and many of these early works sidestepped them. To address these challenges, we introduce Sorbet, a transformer-based spiking language model that is more neuromorphic hardware-compatible. Sorbet incorporates a novel shifting-based softmax called PTsoftmax and a BitShifting-based PowerNorm (BSPN), both designed to replace the respective energy-intensive operations. By leveraging knowledge distillation and model quantization, Sorbet achieved a highly compressed binary weight model that maintains competitive performance while achieving $27.16\times$ energy savings compared to BERT. We validate Sorbet through extensive testing on the GLUE benchmark and a series of ablation studies, demonstrating its potential as an energy-efficient solution for language model inference.  Our code is publicly available at [https://github.com/Kaiwen-Tang/Sorbet](https://github.com/Kaiwen-Tang/Sorbet)

---

## 论文详细总结（自动生成）

# 论文详解：Sorbet — 面向神经形态硬件的 Transformer 脉冲语言模型

## 1. 研究动机与核心问题
- **边缘端隐私与能效需求**：出于数据隐私和连接限制，越来越多的语言模型需要本地部署在资源受限的边缘设备上，因此对能效提出了极高要求。
- **脉冲神经网络 (SNN) 的潜力**：SNN 模仿生物神经元的脉冲通信，具有事件驱动、无乘法计算的特性，是提高能效的天然方案。
- **Transformer 在神经形态硬件上的障碍**：虽然已有将 Transformer 转换为 SNN 的工作，但 `softmax` 和 `layer normalization` (LN) 依赖除法、指数、开方等复杂运算，难以部署在仅支持脉冲和累加的神经形态芯片上。以往的工作大多绕过这些操作，未从根本上解决兼容性问题。
- **论文目标**：提出 **Sorbet**，第一个完全神经形态硬件兼容的、面向自然语言理解的 Transformer 脉冲语言模型，通过硬件友好的算子替换，实现高能效推理并保持竞争力性能。

## 2. 方法论与技术细节
### 2.1 整体架构：量化与脉冲化
- 以 BERT‑base 为教师模型，通过多步知识蒸馏训练一个**二值权重 (1‑bit)**、**4‑bit 激活**的学生模型。
- 采用平均积分发放 (ASG) 脉冲神经元，将矩阵乘法转换为对脉冲事件的累加，杜绝所有乘法运算。
- 架构对应 BERT 的自注意力和前馈网络，但将 `softmax` 替换为 PTsoftmax、`LayerNorm` 替换为 BSPN，并使用 ReLU‑SN 产生脉冲。

### 2.2 PTsoftmax：基于 2 的幂次移位 softmax
- **运算简化**：先将传统 softmax 的 `exp(x)` 替换为 `2^x` 得到 base‑2 softmax，再将分母近似为最接近的 2 的整数次幂 (`2^k`)，最终输出 `2^{⌈z_i⌉ - k}`。
- **硬件实现**：所有操作仅需上取整、查表取对数、右移位，无需乘除。
- **理论保证**：误差被约束在常数因子内 (`1/(2√2) ≤ PTsoftmax / base‑2 softmax ≤ 2√2`)，不影响概率分布功能。

### 2.3 BSPN：位移式 PowerNorm
- **动机**：PowerNorm 中的 RMSLN 仍含平方和开方，硬件不友好。BSPN 首先在通道分组内计算 L1 范数，并将其近似为最近的 2 的幂次，用右移代替除法；最后接 PowerNorm 的“零均值松弛 BN”步骤。
- **硬件友好特性**：全部操作为绝对值、加法、取对数查表、移位。归一化统计量在训练中滑动平均，推理时无需重复计算方差。
- **理论性质**：
  - **梯度有界**：在输入分布的 L1 范数对数值非负的温和假设下，BSPN 的梯度范数不增大 PowerNorm 的梯度界。
  - **Lipschitz 常数受控**：BSPN 不放大 PowerNorm 的损失 Lipschitz 常数，通常还更小，有利于训练稳定。

### 2.4 训练流程
1. 全精度 BERT 作为教师。
2. 逐步量化并替换算子：
   - 量化为 1‑bit 权重 / 4‑bit 激活（使用弹性二值化，分母改为 2 的幂次移位）。
   - 将 softmax 替换为 PTsoftmax。
   - 将 LN 替换为 BSPN。
3. 每一步都用 KL 散度 + 中间激活蒸馏进行知识蒸馏 (`L_logits + L_reps`)。
4. 最终将量化 ANN 模型转换为脉冲 SNN（Sorbet）。

## 3. 实验设计
### 3.1 评估基准
- **GLUE 基准**中的 7 个任务：QQP（问题对等价）、MNLI‑m（自然语言推理）、SST‑2（情感分类）、QNLI（问答推理）、RTE（文本蕴含）、MRPC（语义相似度）、STS‑B（语义相似度回归）。

### 3.2 对比方法
- **ANN 变压器**：BERT‑base、DistilBERT、TinyBERT、Q2BERT、BiT（二值化 BERT）。
- **脉冲变压器**：SpikingFormer、SpikingBERT、SpikeLM，特别比较了它们的 1‑bit 量化版本。
- 所有模型均在 GLUE 上报告准确率（STS‑B 为 Spearman 相关系数）。

### 3.3 能量分析
- 对比 BERT（32‑bit FP、16‑bit FP）以及 SpikeLM 的推理能耗。
- 计算原理：将 SNN 的累加能耗（基于发火率和时间步）与 ANN 的乘加能耗对比。
- 还对 PTsoftmax 和 BSPN 分层运算进行独立能量计算（45nm 工艺下，DIV、EXP、SHIFT 等单元能量）。

## 4. 资源与算力
- **明确说明**：所有实验均在 **3 块 Nvidia RTX A100‑80GB GPU** 上运行。
- **未提供信息**：训练总时长、批大小、学习率、收敛 epoch 数等超参数细节在正文中未明确给出，但可通过开源代码获取。

## 5. 实验充分性与客观性
- **数据任务覆盖**：涵盖 GLUE 中 7 个不同类型的数据集，较全面。
- **对比基线丰富**：包括全精度、蒸馏压缩、各类 SNN 以及专门的二值化 BERT。
- **消融实验**：
  - 在全精度 BERT 上逐步替换 softmax→PTsoftmax、LN→BSPN，观察性能下降（约 2‑4 个百分点）。
  - 在 4‑bit 和 1‑bit 量化模型上再次验证算子替换的影响（精度损失很小，在 0.6‑1.4% 范围内）。
  - 量化位宽与时间步长消融，展示 SNN 转换损失。
- **能量评估**：用多组发火率（SST‑2 约 0.13，STS‑B 约 0.15）计算能耗，结果有可比性。
- **公平性**：所有模型皆基于 BERT‑base 蒸馏，且对比时保持相似的权重位宽，比较基准合理。

## 6. 主要结论与发现
- **首创性**：Sorbet 是第一个移除 softmax 和 LN 且完全兼容神经形态硬件的 Transformer 脉冲语言模型。
- **性能竞争力**：在 GLUE 上的平均表现与同等规模的二值化网络（如 BiT）及现有脉冲模型（SpikeLM）相当，例如 Sorbet 在 SST‑2 达到 90.4%，整体在 77‑90% 区间。
- **能耗大幅降低**：
  - 对比 BERT‑base 实现 **27.16×** 能耗节省。
  - 对比 SpikeLM 实现 **3.16×** 能耗节省。
  - PTsoftmax 比传统 softmax 能效高 **27.62×**，BSPN 比 LN 能效高 **12.4×**。
- **理论支撑**：PTsoftmax 和 BSPN 都有对应的误差界和梯度稳定性证明，确保替换合理。

## 7. 优点与亮点
- **完整解决兼容性难题**：首次同时处理了 Transformer 中 softmax 和 LN 这两个关键操作在神经形态硬件上的实现。
- **算子设计巧妙**：利用“2 的幂次”和位移动代替除法和指数，几乎是 SNN 硬件天然的适配。
- **理论与实验结合**：给出了 BSPN 的有界梯度、Lipschitz 性质证明，以及 PTsoftmax 的误差界，增强了方法的可解释性。
- **训练流程系统化**：多步知识蒸馏 + 渐进替换策略，有效保证了量化模型的精度。
- **开源代码**：提供了完整实现，便于复现和后续改进。

## 8. 不足与局限
- **未在真实芯片上验证**：虽在 Loihi 框架仿真和 22nm 综合上评估能效，但缺少实际硬件的端到端延迟和功耗数据，实际影响（如芯片噪声、时序约束）未知。
- **性能仍落后于全精度模型**：与 BERT‑base 相比，平均性能有约 8‑10% 的绝对差距，部分任务（RTE、STS‑B）退化较明显。
- **发火率依赖**：能耗节省高度依赖发火率；在部分数据集上发火率未知，极端情况下能耗优势可能缩小。
- **任务范围有限**：仅评估了 GLUE 基准的自然语言理解任务，未涉及生成、长文本、多语言等更复杂的 NLP 场景。
- **架构限制**：使用固定时间步 ASG 脉冲神经元，可能不如动态脉冲编码灵活。
- **依赖教师模型**：需要全精度 BERT 教师进行蒸馏，无法从头训练。

（完）
