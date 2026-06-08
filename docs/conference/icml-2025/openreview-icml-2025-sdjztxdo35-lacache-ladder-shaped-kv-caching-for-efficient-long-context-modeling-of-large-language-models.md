---
title: "LaCache: Ladder-Shaped KV Caching for Efficient Long-Context Modeling of Large Language Models"
title_zh: LaCache：用于大型语言模型高效长上下文建模的梯形KV缓存
authors: "Dachuan Shi, Yonggan Fu, Xiangchi Yuan, Zhongzhi Yu, Haoran You, Sixu Li, Xin Dong, Jan Kautz, Pavlo Molchanov, Yingyan Celine Lin"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=SDjZtxDo35"
tags: ["query:edge-llm"]
score: 8.0
evidence: 梯形KV缓存用于高效长上下文LLM推理
tldr: 为解决LLM在长上下文推理中的KV缓存爆炸和内存溢出问题，LaCache提出一种训练无关的梯形缓存优化范式。它通过分层选择策略，在保持长程建模能力的同时防止OOM，支持连续生成。该方法无需重新训练即可提升推理效率，特别适用于内存有限的边缘设备，为端侧LLM的长文本处理提供了实用解决方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1755, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 878, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 728, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 852, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 733, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 773, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1769, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 838, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 837, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sdjztxdo35/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 842, \"height\": 933, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-sdjztxdo35/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1786, \"height\": 563, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sdjztxdo35/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 874, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sdjztxdo35/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1590, \"height\": 1015, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sdjztxdo35/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 962, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sdjztxdo35/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1780, \"height\": 172, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sdjztxdo35/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 170, \"label\": \"Table\"}]"
motivation: LLM长上下文推理中KV缓存占用内存过大，易引发OOM，限制连续生成。
method: 提出训练无关的梯形KV缓存策略LaCache，分层管理缓存以同时保障长程能力和内存效率。
result: 实现长上下文建模且避免内存溢出。
conclusion: LaCache为LLM的高效长文本生成提供了一种无额外训练的缓存优化方法。
---

## Abstract
Recent advancements in Large Language Models (LLMs) have spurred interest in numerous applications requiring robust long-range capabilities, essential for processing extensive input contexts and continuously generating extended outputs. As sequence lengths increase, the number of Key-Value (KV) pairs in LLMs escalates, creating a significant efficiency bottleneck.
In this paper, we propose a new KV cache optimization paradigm called LaCache, a training-free method for efficient and accurate generative inference of LLMs. LaCache enables LLMs to simultaneously address both of the critical challenges in long-range modeling: robust long-range capabilities and continuous generation without running out-of-memory (OOM). Specifically, LaCache integrates two key innovations: (1) a ladder-shaped KV cache pattern that stores KV pairs not only sequentially (left-to-right within each layer) but also across layers (from shallow to deep), providing an extended span for capturing long-range dependencies under a fixed storage budget, thereby boosting long-range capabilities; and (2) an iterative compaction mechanism that progressively compresses older caches, freeing up space for new tokens within a fixed cache size. This token distance-based dynamic compression enables more effective continuous generation under constrained cache budgets.
Experiments across various tasks, benchmarks, and LLM models consistently validate LaCache's effectiveness in enhancing LLMs' long-range capabilities. Our code is available at https://github.com/GATECH-EIC/LaCache.

---

## 论文详细总结（自动生成）

# 论文总结：LaCache——用于高效长上下文建模的梯形 KV 缓存

## 1. 核心问题与整体含义
- **背景**：大语言模型（LLM）在长上下文生成任务中需要缓存大量的 Key-Value（KV）状态，随着序列长度增长，KV 缓存内存开销线性增加，极易引发**显存溢出（OOM）**，阻碍连续生成。
- **矛盾**：现有 KV 缓存优化方法难以同时满足两个关键需求：（1）**强健的长程建模能力**；（2）**持续生成且不 OOM**。
  - 基于近因（recency-based）的方法（如 StreamingLLM）可以支持无限长生成，但损失长程信息，准确率衰减严重。
  - 基于检索的方法（如 Quest）保留了全部 KV 缓存，精度高但缓存随序列无限增长，最终 OOM。
  - 基于注意力分数的重要性方法（如 H2O）虽然减少缓存，但与高效注意力实现（FlashAttention）不兼容，实际吞吐较低。
- **动机**：提出一种**无需训练**、**与 FlashAttention 兼容**、能同时保障**长程能力**与**连续生成**的 KV 缓存优化范式。

## 2. 方法论
LaCache 包含两个核心创新：**梯形 KV 缓存模式（ladder-shaped pattern）** 和 **迭代压缩机制（iterative compaction）**。

### 2.1 梯形 KV 缓存模式
- **核心思想**：不同层不必缓存完全相同的 Token 集合。浅层保留较早 Token 的 KV，深层逐步转向较晚 Token，形成“阶梯状”覆盖。
- **存储方式**：对于每层，保留一段连续 Token 的 KV 状态，相邻层之间保留的 Token 窗口向后移动，整体呈现左侧高、右侧低的“梯子”形状。
- **两个可调超参数**：
  - **跨度 S**：同一个 Token 被多少层保留其 KV。
  - **重叠度 O**：相邻层保留的 Token 集合之间的重叠数量。
- **优势分析**：
  - 同等缓存预算下，梯形结构能覆盖更长的上下文范围，提升了信息保留的下界，不依赖注意力分数即可保留可能重要的 Token。
  - 相邻 Token 之间的语义关联性通过重叠平滑过渡，自然语言中常见的局部相关性得到保留。
  - 作者通过随机生成 1500+ 种缓存模式并评估 PPL，发现梯形模式处于帕累托前沿，印证了其合理性。

### 2.2 迭代压缩（支持连续无限长生成）
- **触发条件**：当已用 LaCache 压缩过的 KV 缓存再次达到容量上限时，再次应用梯形压缩。
- **压缩策略**：对新缓存中的早期 Token 采用更大压缩比（丢弃更多），对后期 Token 压缩更温和，逐步为新 Token 腾出空间。
- **结果**：缓存大小保持恒定，模型可以无限制地持续生成，同时优先保留近期上下文。

### 2.3 实现细节
- LaCache 是完全**训练无关的**，仅需在推理时修改 KV 缓存的存储与丢弃策略。
- 与 FlashAttention 完全兼容，因为 KV 状态的丢弃发生在注意力计算之前或之后，不会干扰 FlashAttention 的算子级别优化。

## 3. 实验设计
### 3.1 数据集与场景
- **语言建模（长上下文建模）**：
  - **Wikitext-2-raw-v1**：拼接后以 token 级别逐位生成评估困惑度（PPL），解码长度从 1K 到 16K。
  - **PG19**：100 本书拼接为超长序列（约 1000 万 tokens），采用滑动窗口评估长程建模，并测试生成至 600K 甚至 1000 万 token 的能力。
- **长上下文理解**：
  - **LongBench**：21 个双语长上下文理解子任务（问答、摘要、少样本学习、合成任务、代码补全等），平均输入长度 5K–15K。
  - **Needle-In-A-Haystack**：检索隐藏在极长上下文中的特定信息，上下文长度可达 128K。
  - **RULER**：合成基准，包含 13 个任务（单键/多键检索、多跳追踪、聚合、问答等），检验长上下文理解鲁棒性。

### 3.2 对比方法
- **完全缓存**（全 KV 缓存，作为上界）
- **Static/Naïve 方法**：StreamingLLM（基于近因，固定窗口保留初始 Token 和最近 Token）
- **重要性驱动方法**：H2O、TOVA、PyramidInfer、SnapKV（依赖注意力图进行令牌选择）

### 3.3 评价指标
- 语言建模：**困惑度（Perplexity, PPL）**
- 理解任务：**准确率/F1/得分**（LongBench 各类任务得分）
- 效率：**生成吞吐量**（tokens/s），分数-吞吐权衡（Pareto 曲线）

## 4. 资源与算力
- 论文中提到实验使用 **单张 NVIDIA A100 GPU** 进行测试（例如 PG19 实验在 A100 上遇到 160K 时 OOM）。也提到使用 **NVIDIA H200** 评估吞吐量。
- **未明确说明**所用 GPU 总数、总实验时长或训练所需算力；因方法是训练无关的，只有推理评估，所以未报告训练算力。
- 由于仅在推理时修改缓存策略，LaCache 不引入额外大型计算，但实验量较大（多个模型、多个数据集），推测推理评测使用若干 GPU 进行即可。

## 5. 实验数量与充分性
- **模型数量**：至少 6 种（Llama2-7B/13B/7B-Chat/13B-Chat，Llama3-8B，Llama3.2-3B-Instruct，SmolLM2-1.7B-Instruct，LongChat-7b-v1.5），覆盖不同规模与功能。
- **数据集**：语言建模 2 个，长上下文理解 3 个（LongBench 含 21 子任务，RULER 含 13 子任务），总计上千种实验条件组合。
- **缓存预算**：如 512、256、80（对应压缩比 2×、4×、1% 预训练长度）等，多档设置。
- **消融实验**：
  - 在 1500+ 随机缓存模式中对比梯形模式（图 3），验证模式选择的帕累托最优性。
  - 调整超参数 Span S 和 Overlap O 对 PPL 和任务得分的影响（表 6，图 10）。
  - 对比不同任务类型（QA vs. 合成任务）对 Overlap 的不同需求。
- **对比公平性**：所有方法在相同硬件、相同模型、相同缓存预算下比较，LaCache 与 StreamingLLM 皆保持恒定缓存大小；重要性方法因需维护额外数据结构或计算，吞吐量对比时公平反映了实际效率。

综上，实验极其充分，系统地覆盖了不同模型、任务、缓存预算，并进行了超参数和模式选择的合理性消融。

## 6. 主要结论与发现
- LaCache 在**同等固定缓存预算**下，**长程建模能力远优于 StreamingLLM**。例如在 Wikitext-2，512 缓存下 LaCache 相较全缓存 PPL 劣化仅约 5%，而 StreamingLLM 劣化约 35%。
- 在 **1000 万 token 的超长 PG19** 上，LaCache 支持连续生成且无 OOM，同时保持合理 PPL，而全缓存迅速 OOM。
- 在极低缓存（仅 1% 预训练长度，80 个 token）下仍显著优于 StreamingLLM。
- 在 **LongBench** 21 个任务上，相同缓存预算下，LaCache 平均得分损失约为 StreamingLLM 的一半；与 H2O 等重要性方法相比，**分数-吞吐 Pareto 曲线上更优**，因为其兼容 FlashAttention，实际推理速度更快。
- 在 **Needle-In-A-Haystack** 测试中，LaCache 将 128K 上下文的检索准确率从 54.54% 提升至 99.16%（50% 缓存预算），几乎翻倍。
- 在 **RULER** 的 13 个合成任务上，平均得分提升约 5 个百分点，多值、变量追踪等任务提升显著。
- 消融表明，Span 过大或过小都会降低性能，Overlap 对不同类型的任务影响不同（更大 O 有助于需要全局信息的合成任务，更小 O 有利于局部信息型 QA 任务）。

## 7. 优点
- **训练无关**：无需任何微调，直接应用于预训练 LLM，部署成本极低。
- **固定缓存，无 OOM**：通过迭代压缩支持理论上无限长的连续生成，保证恒定显存占用。
- **兼容 FlashAttention**：不依赖注意力图来计算重要性，可与 SOTA 高效注意力框架共同工作，实际吞吐高。
- **简单且有效**：仅需定义每层保留的 Token 范围，规则简便，易于实现。
- **广泛验证**：在多种模型、多个权威基准上一致优于同类方法，可信度强。
- **模式解释性强**：梯形覆盖与自然语言序列相邻语义关联的假设相吻合，且经过随机搜索验证位于帕累托前沿。

## 8. 不足与局限
- **模式并非全局最优**：固定的梯形结构不一定对所有输入和所有层都是最优的，某些情况可能需要非均匀、数据依赖的模式。
- **未利用注意力信息**：虽然避开了与 FlashAttention 的冲突，但也放弃了注意力图中可能蕴含的更精细的重要性信息，在极端压缩比下可能不如 token 选择方法。
- **超参数依赖任务类型**：Span 和 Overlap 需要根据任务特性调整（如语言建模 vs. 长上下文理解），缺少自动化选择机制。
- **未涉及微调适配**：训练无关是一种优势，但也可能是局限，微调或许能在固定模式下进一步提升质量，目前未探索。
- **评估局限于生成与理解基准**：未在真实对话系统或多轮交互等更复杂场景下测试。
- **算力报告不够详尽**：未明确给出实验所需的 GPU 总小时数，对成本评估略显模糊。

（完）
