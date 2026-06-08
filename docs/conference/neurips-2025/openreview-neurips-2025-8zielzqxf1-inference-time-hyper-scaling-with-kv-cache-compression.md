---
title: Inference-Time Hyper-Scaling with KV Cache Compression
title_zh: 基于KV缓存压缩的推理时超缩放
authors: "Adrian Łańcucki, Konrad Staniszewski, Piotr Nawrot, Edoardo Ponti"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=8ZiElzQxf1"
tags: ["query:edge-llm"]
score: 8.0
evidence: 压缩KV缓存以在相同计算预算下生成更多token
tldr: 提出动态内存稀疏化方法，通过对KV缓存进行压缩，可在相同计算预算下生成更多token，仅需1000步训练即可实现8倍压缩，显著提升Transformer LLM推理效率。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 634, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 598, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1412, \"height\": 1872, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1432, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1323, \"height\": 739, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1419, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1415, \"height\": 1855, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1355, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8zielzqxf1/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1331, \"height\": 1507, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1446, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 642, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1320, \"height\": 430, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 971, \"height\": 1010, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 981, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 918, \"height\": 848, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1365, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1370, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1371, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1296, \"height\": 635, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1295, \"height\": 636, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1081, \"height\": 634, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 970, \"height\": 300, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8zielzqxf1/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 865, \"height\": 119, \"label\": \"Table\"}]"
motivation: Transformer LLM推理成本受KV缓存大小限制。
method: 提出动态内存稀疏化（DMS）方法，稀疏化KV缓存以压缩并加速推理。
result: 仅需1K训练步数即可实现8倍压缩，提升推理时超缩放的准确性。
conclusion: DMS在保持准确性的同时大幅降低KV缓存内存占用，使超缩放实用化。
---

## Abstract
Inference-time scaling trades efficiency for increased reasoning accuracy by generating longer or more parallel sequences. However, in Transformer LLMs, generation cost is bottlenecked by the size of the key–value (KV) cache, rather than the number of generated tokens. Hence, we explore inference-time hyper-scaling: by compressing the KV cache, we can generate more tokens within the same compute budget and further improve the accuracy of scaled inference. The success of this approach, however, hinges on the ability of compression methods to preserve accuracy even at high compression ratios. To make hyper-scaling practical, we introduce Dynamic Memory Sparsification (DMS), a novel method for sparsifying KV caches that only requires 1K training steps to achieve 8× compression, while maintaining better accuracy than training-free sparse attention. Instead of prematurely discarding cached tokens, DMS delays token eviction, implicitly merging representations and preserving critical information. We demonstrate the effectiveness of inference-time hyper-scaling with DMS on multiple families of LLMs, showing that it boosts accuracy for comparable inference latency and memory load. For instance, we enhance Qwen-R1 32B by 9.1 points on AIME 24, 7.6 on GPQA, and 9.6 on LiveCodeBench on average for an equivalent number of memory reads.

---

## 论文详细总结（自动生成）

# 论文总结：推理时超缩放与KV缓存压缩（Inference-Time Hyper-Scaling with KV Cache Compression）

## 1. 研究动机与核心问题
- Transformer大语言模型（LLM）在推理时通过生成更长或更多并行思维链来提升准确性，即“推理时缩放”（inference-time scaling）。
- 然而，推理过程的瓶颈并非生成的token数量，而是**键值（KV）缓存的大小**。缓存随生成的token线性增长，成为内存占用和延迟的主要来源。
- 论文提出“**推理时超缩放**（inference-time hyper-scaling）”概念：通过压缩KV缓存，在相同算力（内存读取、峰值内存）预算下生成更多token，从而进一步提升缩放后的推理准确率。
- 实现超缩放的关键在于：压缩方法必须在高压缩比下仍能保持模型原有准确率。现有训练无关的稀疏注意力方法在高压缩比下性能下降明显，而后训练压缩方法如DMC（Dynamic Memory Compression）虽效果好，但训练成本高。

## 2. 方法论：动态内存稀疏化（Dynamic Memory Sparsification, DMS）
### 核心思想
- DMS是一种**可训练的KV缓存稀疏化方法**，将预训练LLM改造为自适应、低成本的token驱逐策略，兼具训练无关方法和训练方法的优点。
- 与DMC不同，DMS**仅执行token驱逐（eviction），不做合并（merging）**，且驱逐决策与执行时间分离。
- 仅需约**1000步训练即可达到8倍压缩比**，且准确率保持优于训练无关稀疏注意力。

### 关键技术细节
- **驱逐决策**
  - 在每步推理时，基于当前隐藏状态通过可学习的线性投影预测一个二进制决策 \(\alpha_t\in\{0,1\}\)，决定是否驱逐对应的KV对。
  - 训练中使用**Gumbel-sigmoid重参数化**以保持可微性，并设置低温度和初始偏置，防止训练初期的灾难性遗忘。
  - 构造一个加性注意力掩码 \(M_\alpha\)，将预计驱逐的token对应的注意力权重置为 \(-\infty\)，弱化但仍允许访问中间状态。
- **延迟驱逐与滑动窗口**
  - 驱逐决策在时刻 \(t\) 做出，但实际驱逐延迟至 \(t+w\) ，\(w\) 为窗口大小（默认256）。
  - 延迟窗口使模型在丢弃前能整合被驱逐token的信息，避免过早丢失关键上下文。
  - 消融实验表明，**立即驱逐会导致精度快速崩塌**，而延迟驱逐能稳定训练并大幅减少所需训练token数。
- **训练目标**
  - 蒸馏损失：使用原始LLM作为教师，用logit蒸馏训练DMS模型，降低对原始训练数据的依赖。
  - 辅助压缩损失：单边 ℓ1 损失，驱动模型平均 \(\alpha\) 趋近目标压缩比（\(\alpha^* = 1 - 1/CR\)）。
  - 总损失：\(L = L_D + L_{\text{aux}}\)。
- **推理时实现**
  - 决策离散化，α 取整为 0/1。
  - 可利用PagedAttention等已有框架，将驱逐的token简单覆盖，不引入额外读写。
  - 不增加模型参数（复用query头的一个神经元输出α）。

## 3. 实验设计
### 模型与任务
- **推理模型**：Qwen 2.5 1.5B/7B/32B（蒸馏自DeepSeek R1）、Qwen3-8B（蒸馏自Qwen3-235B-A22B）。
- **消融与通用模型**：Llama 3.2 1B Instruct。
- **推理任务**：AIME 24、MATH-500（数学）；GPQA Diamond（科学）；LiveCodeBench（编程）。
- **额外多任务评估**：GSM8K、MMLU、HellaSwag、Needle-in-a-Haystack（NIAH）、Variable Tracking（VT）等。

### 对比方法
- 原始Transformer（无压缩，Vanilla）。
- 训练无关稀疏注意力：**TOVA**、**H2O**（驱逐）；**Quest**（选择性页提取，不减内存）。
- 可训练压缩：**DMC**（动态内存压缩）。

### 评估指标与场景
- **效率指标**：KV缓存总读取数（proxy 延迟）、峰值内存占用、吞吐量（最大batch size下的examples/min）。
- **推理时超缩放配置**：组合不同最大生成长度（L）、并行链数（W）和压缩比（CR），形成多个(W, L, CR)点，绘制准确率-效率的**帕累托前沿**。
- 对比各方法在同一预算下的准确率优势，以及DMS在通用任务上等token生成量时的准确率保持。

## 4. 资源与算力
- **训练硬件**：NVIDIA H100 SXM GPU，使用Megatron-LM框架，bfloat16精度。
- **训练规模**：不同模型和压缩比阶段的训练成本详见表3。例如，Llama 3 1B每增加1倍CR需10 GPU小时；Qwen-R1 32B每增加1倍CR需345 GPU小时。整体训练极轻量（如Qwen-R1 32B达到CR8总计约700步）。
- **推理延迟测量**：在NVIDIA H100上使用HuggingFace Transformers + FlashAttention实现。

## 5. 实验充分性
- **多模型、多任务、多指标**：覆盖1.5B~32B参数，4个推理基准 + 多个通用任务，从延迟、内存、吞吐量三个维度评估。
- **大规模消融实验**：研究了延迟驱逐 vs. 立即驱逐、不同窗口大小的影响，以及训练数据量（对数亿token）对DMS与DMC的影响，证明DMS数据效率提升8倍。
- **帕累托前沿分析**：在多个预算配置下绘制前沿线，定量计算平均提升（如AIME 24 DMS vs Vanilla 平均提升10.6~15.0点）。
- **统计显著性**：附录G提供了部分结果的误差区间，评估多次运行的标准误。
- **公平性**：对比方法均采用公开实现，Quest按原设计保留完整缓存（内存不减）仍不及DMS，说明对比公平且DMS优势显著。

## 6. 主要结论与发现
- **KV缓存压缩能有效实现推理时超缩放**：在相同延迟或内存预算下，压缩模型通过扩大token预算获得更高准确率，且帕累托前沿全面优于原始模型。
- **DMS在保持准确率的同时实现高压缩比**：以极低训练成本（~1K步）达到8×压缩，并在推理时缩放中显著超越原始LLM和其他压缩基线（TOVA、H2O、Quest、DMC）。
- **延迟驱逐是核心设计**：延迟驱逐大幅提升训练稳定性与数据效率，是DMS成功的关键。
- **通用部署能力**：在等token长度下，DMS 8× 模型准确率与原始模型接近（如Qwen3-8B各项基准维持在原始水平的±2%以内），且在某些长上下文任务（如NIAH）上甚至超过原始模型，体现通用部署价值。
- **吞吐量提升**：在实际多用户服务场景中，DMS可提供高达5×的吞吐量提升而准确率不降。

## 7. 优点
- **方法新颖且高效**：提出“推理时超缩放”新框架，将KV压缩与推理时计算扩展系统结合。
- **训练成本极低**：仅需少量训练步数（~1K）和蒸馏数据，无需原始预训练数据。
- **即插即用**：复用注意力头现有神经元，无额外参数；支持PagedAttention等现成框架。
- **帕累托最优**：在延迟、内存、吞吐量三种效率维度上均全面优于已有方法。
- **良好的通用性和可扩展性**：在推理、非推理、长上下文任务上均验证有效，且压缩比可灵活配置。

## 8. 不足与局限
- **模型规模与上下文长度受限**：当前验证集中在≤32B参数、≤32K上下文长度、≤8×压缩比，更大模型和更长上下文的扩展性未充分验证。
- **注意力变体未探索**：仅在标准GQA注意力上验证，与MLA（Multi-head Latent Attention）等新架构的兼容性未知。
- **与PRM等验证器结合的扩展**：文章提到超缩放可扩展至过程奖励模型（PRM）验证场景，但未进行实验。
- **长上下文外推限制**：DMS在超过训练上下文长度后性能有所下降（附录F），虽优于DMC，但仍可能不稳定。
- **无开源代码**：论文未提供完整可复现代码，仅描述方法实现细节，可能增加复现门槛。
- **潜在社会风险**：虽无新风险，但增强推理能力可能放大LLM已有的误用风险。

（完）
