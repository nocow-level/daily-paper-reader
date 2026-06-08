---
title: "CateKV: On Sequential Consistency for Long-Context LLM Inference Acceleration"
title_zh: CateKV：基于顺序一致性的长上下文大模型推理加速
authors: "Haoyun Jiang, Haolin li, jianwei zhang, Fei Huang, Qiang Hu, Minmin Sun, Shuai Xiao, Yong Li, Junyang Lin, Jiangchao Yao"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=u7dlwgKstN"
tags: ["query:edge-llm"]
score: 9.0
evidence: 混合KV缓存方法仅保留一致头中的关键token，以减少长上下文推理的内存和计算负担
tldr: 针对长上下文推理中KV缓存内存占用大的问题，发现部分注意力头具有顺序一致性，据此提出CateKV，对一致头仅保留关键token信息，动态头保留更多信息，混合缓存压缩有效减小内存并加速推理，为Transformer模型在资源受限硬件上的运行提供了新方法。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 711, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 827, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 751, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 826, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1742, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 853, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1695, \"height\": 837, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1580, \"height\": 2362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 749, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-u7dlwgkstn/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 750, \"height\": 408, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1774, \"height\": 940, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 859, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1695, \"height\": 837, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1195, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1732, \"height\": 1162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1606, \"height\": 1078, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-u7dlwgkstn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1740, \"height\": 566, \"label\": \"Table\"}]"
motivation: 长上下文导致巨大内存需求和推理延迟，现有压缩方法可能丢失信息。
method: 利用系数变异识别顺序一致的注意力头，设计混合KV缓存策略保留关键信息。
result: 缩减KV缓存大小和计算开销，同时保持高精度。
conclusion: CateKV通过选择性地压缩缓存，有效平衡效率与准确性。
---

## Abstract
Large language models (LLMs) have demonstrated strong capabilities in handling long-context tasks, but processing such long contexts remains challenging due to the substantial memory requirements and inference latency. In this work, we discover that certain attention heads exhibit sequential consistency in their attention patterns, which can be persistently identified using a coefficient-of-variation-based algorithm. Inspired by this observation, we propose CateKV, a hybrid KV cache method that retains only critical token information for consistent heads, thereby reducing KV cache size and computational overhead, while preserving the majority of KV pairs in adaptive heads to ensure high accuracy. We show the unique characteristics of our algorithm and its extension with existing acceleration methods. Comprehensive evaluations on long-context benchmarks show that, while maintaining accuracy comparable to full attention, CateKV reduces memory usage by up to $2.72\times$ and accelerates decoding by $2.18\times$ in single-sample inputs, and boosts throughput by $3.96\times$ in batch scenarios.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化、深入、客观的中文总结。

### 论文核心问题与整体含义
本研究聚焦于长上下文大语言模型推理中的高内存占用和延迟问题。随着上下文长度增加，存储和处理所有键值缓存所需的资源急剧增长，成为推理加速的关键瓶颈。论文的核心发现是，部分注意力头在预填充和解码阶段展现出**顺序一致性**的注意力模式，即始终关注少数固定 token；而另一些头则展现出动态变化的**自适应**模式。基于此，作者提出通过差异化地缓存不同注意力头的 KV 对，在维持精度的前提下大幅降低内存和计算开销，从而加速长上下文推理。

### 方法论：CateKV 的核心思想与关键技术
CateKV 是一种混合 KV 缓存加速方法，其核心在于利用预填充阶段的信息指导解码阶段的稀疏化。方法流程分为三步：

1.  **注意力头分类：**
    *   ​**观测矩阵构建**：在预填充阶段，选取输入序列末尾的 `L_obs` 个查询 token 作为观测窗口，计算它们对所有键的注意力分数矩阵 `A`。
    *   ​**系数变异评分**：首先，通过百分位阈值 `k` 和缩放因子 `α` 对矩阵 `A` 进行二值化处理，得到矩阵 `B`。然后，沿观察窗口维度求和，得到每个 token 被识别为关键的频率向量 `C`。最后，计算 `C` 的变异系数作为该注意力头的**CV 分数**。高 CV 分数意味着注意力高度集中于少数 token，且模式稳定。
    *   ​**静态分类**：利用一个参考数据集，根据 CV 分数和预设的自适应头比例 `r`，将模型的注意力头一次性、静态地划分为 **一致性头** 和 **自适应头**。实验发现不同样本的分类结果高度一致，使得静态分类可行。

2.  ​**差异化 KV 缓存策略：**
    *   ​**一致性头**：仅保留由观测窗口识别出的极少数最关键 token 的 KV 对。稀疏预算 `b` 很小。
    *   ​**自适应头**：保留大部分的 KV 对，其保留比例由 `η` 控制。选择依据仍是预填充阶段的注意力权重。

3.  ​**理论分析：**
    *   论文通过引理和定理，从理论上分析了影响 token 保留准确率下限的三个关键因素：表征 token 相关性度量的有效性、预算控制的合理性以及分类准确率。

该方法可与 KV 检索等方法无缝集成：在自适应头中可进一步应用如 Quest 等检索算法，以在保留的 KV 对中进行高效查询。

### 实验设计
*   **数据集与基准测试：**
    *   `RULER`：在 128K 长度的多种合成任务上评估。
    *   `LongBench`：在超过 4096 token 的样本上评估 21 个任务的平均性能。
    *   `Needle in a Haystack (NIAH)`：测试从 20K 到 1M token 上下文中提取信息的能力。
*   **测试模型：** LLaMA-3-8B-Instruct-1048K, Phi-3-Mini-128K, LLaMA-3.1-8B, Yi-9B-200K, Qwen2.5-7B。
*   **对比方法：**
    *   ​KV 驱逐方法：StreamingLLM, SnapKV, PyramidKV。
    *   ​KV 检索方法：Quest, ShadowKV。
    *   ​基于头分类的方法：DuoAttention, MInference。

### 资源与算力
论文明确指出，所有实验均在**单个 NVIDIA A100-80G GPU** 上完成。未提及特定实验的具体运行时间。

### 实验数量与充分性
实验设计**非常充分且客观**。
*   ​**广泛验证**：在 5 个主流长上下文 LLM 和 3 个权威基准上进行了评估，覆盖了从 8K 到 1M 的上下文长度。
*   ​**多维对比**：对比了驱逐、检索、头分类三大类方法。在与驱逐和头分类方法对比时，保持相同 KV 缓存大小；与检索方法对比时，保持相同计算预算，确保了**公平性**。
*   ​**全面消融**：对三个核心超参数（自适应头比例 `r`、自适应头保留率 `η`、一致性头稀疏预算）进行了详细的消融研究。
*   ​**兼容性验证**：额外实验证明了 CateKV 与 DuoAttention、MInference 等方法的可组合性，能带来进一步性能提升。
*   ​**实测效率**：不仅报告了准确性，还实测了单样本和批处理场景下的内存占用、解码延迟和吞吐量提升。

### 主要结论与发现
1.  ​**现象验证**：大规模语言模型中普遍存在具有顺序一致性注意力模式的“一致性头”。
2.  ​**性能优异**：CateKV 在仅保留约 40% KV 缓存的情况下，在 RULER、LongBench 和 NIAH 等长上下文基准上，达到了与全量注意力相媲美的准确性。
3.  ​**效率显著**：在单样本推理中，最高实现了 **2.72倍** 内存占用减少和 **2.18倍** 解码加速；在批处理推理中，吞吐量最高提升 **3.96倍**。
4.  ​**兼容性强**：该方法作为一个即插即用模块，可以有效集成到现存的 KV 检索（如 Quest）和预填充加速（如 MInference）方法中，在不牺牲精度的情况下，进一步降低其内存消耗或整体延迟。

### 优点
*   ​**洞察新颖**：首次系统地利用跨预填充和解码阶段的“顺序一致性”来指导长上下文推理加速，区别于单纯基于预填充或解码阶段的方法。
*   ​**方法优雅且实用**：基于 CV 分数的静态头分类方式，避免了运行时动态分类的开销，可直接用于模型部署，普适性强。
*   ​**实验扎实**：评估覆盖模型广、基准全、对比公平，理论与实证结合，证明了方法的有效性和鲁棒性。
*   ​**效率-精度平衡佳**：相比于 KV 驱逐方法，精度损失极小；相比于 KV 检索方法，解决了其内存占用高的问题，找到了一个很好的平衡点。

### 不足与局限
*   ​**依赖参考数据集**：静态分类需要预先在一个参考数据集上运行，虽然文中验证了其稳定性，但若模型或任务分布发生剧烈变化，预定义的分类结果可能不再最优。
*   ​**GQA 模型处理简化**：对于分组查询注意力模型，观测矩阵直接取组内平均，可能掩盖了组内不同头的差异。
*   ​**加速局限于解码阶段**：CateKV 主要加速解码阶段的注意力计算，预填充阶段的计算开销（尽管可以和 MInference 结合）并未减少。
*   ​**超参数敏感性**：虽然进行了消融实验，但自适应头比例 `r` 和保留率 `η` 存在临界阈值，低于阈值性能会骤降，实际部署对超参数调优有一定要求。

（完）
