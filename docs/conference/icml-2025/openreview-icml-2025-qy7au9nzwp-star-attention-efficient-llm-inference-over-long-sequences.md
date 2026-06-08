---
title: "Star Attention: Efficient LLM Inference over Long Sequences"
title_zh: Star Attention：长序列上的高效大模型推理
authors: "Shantanu Acharya, Fei Jia, Boris Ginsburg"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=QY7Au9nZwp"
tags: ["query:edge-llm"]
score: 8.0
evidence: 块稀疏注意力近似跨主机分片，最多减少11倍内存和时间
tldr: 针对Transformer长序列推理成本高的问题，提出Star Attention，采用两阶段块稀疏注意力，将上下文分片并行处理，大幅降低内存需求和推理时间，同时与原模型性能相当，为边缘多设备协同推理提供了高效策略。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 682, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 968, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 371, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1769, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1698, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1763, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 806, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qy7au9nzwp/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1773, \"height\": 486, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1353, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 958, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1771, \"height\": 348, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1334, \"height\": 740, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1450, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 605, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 812, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1310, \"height\": 807, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 756, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qy7au9nzwp/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1209, \"height\": 666, \"label\": \"Table\"}]"
motivation: 自注意力二次复杂度导致长序列推理昂贵且缓慢。
method: 设计两阶段块稀疏注意力，第一阶段分块局部并行处理，第二阶段全局注意力。
result: "内存和推理时间减少高达11倍，准确率保持97-100%。"
conclusion: 稀疏注意力机制在不损失精度的前提下显著加速推理，适用于资源受限环境。
---

## Abstract
Inference with Transformer-based Large Language Models (LLMs) on long sequences is both costly and slow due to the quadratic complexity of the self-attention mechanism. We introduce Star Attention, a two-phase block-sparse approximation that improves computational efficiency by sharding attention across multiple hosts while minimizing communication overhead. In the first phase, the context is processed using blockwise-local attention across hosts, in parallel. In the second phase, query and response tokens attend to all prior cached tokens through sequence-global attention. Star Attention integrates seamlessly with most Transformer-based LLMs trained with global attention, reducing memory requirements and inference time by up to 11x while preserving 97-100% of accuracy.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **核心问题**：Transformer 大模型在长序列推理时，自注意力机制的二次复杂度导致计算成本高、内存占用大、推理速度慢。
- **研究动机**：现有长上下文推理方法要么仍需完整注意力矩阵（如 Ring Attention），要么需要额外微调或引入新模块，难以即插即用。
- **整体含义**：论文提出 **Star Attention**，一种两阶段、块稀疏的注意力近似算法。它能够在不修改模型结构、无需微调的前提下，将注意力计算分布到多台设备上，大幅降低长序列推理的内存和时间开销，同时保持 97-100% 的原始精度，为资源受限环境（如多设备协同推理）提供高效策略。

### 2. 方法论

Star Attention 将推理过程分为两个阶段：

#### 2.1 第一阶段：上下文编码（Context Encoding）
- **分块与锚定块（Anchor Block）**：将长上下文 \(c\) 均匀分割为 \(n\) 个连续块 \(c=[c_1,c_2,\dots,c_n]\)。除第一个块 \(c_1\) 外，每个块 \(c_i\) 前都拼接上 \(c_1\) 作为锚定块，形成扩充块 \(c'_i = (c_1, c_i)\)。
- **分布式局部注意力**：扩充块被分配到不同主机上，各自主机独立对其负责的块（含锚定块）执行自注意力计算。
- **缓存策略**：每台主机仅保留当前上下文块 \(c_i\) 的键-值（KV）向量，丢弃锚定块部分。这使得注意力复杂度从序列长度的平方降至线性（与序列长度和块数成比例）。
- **锚定块的作用**：处理“注意力汇”（attention sinks）现象。若不加锚定块，每个独立块会在起始位置产生各自的注意力尖峰，破坏原始全局注意力分布。使用首个块作为锚定块可把注意力尖峰集中到锚定token上，丢弃这些KV后，局部注意力的分布更接近全局注意力。

#### 2.2 第二阶段：查询编码与令牌生成（Query Encoding & Token Generation）
- **查询广播**：查询被复制到所有主机，每台主机利用本地的 KV 缓存计算查询 \(Q\) 的局部注意力输出 \(A_h\) 和局部 softmax 分母 \(s_h\)（即指数和）。
\[
A_h = \left( \frac{\exp(QK_h^\top/\sqrt{d})}{\sum_{k=1}^{l_k}\exp(QK_{h,k}^\top/\sqrt{d})} \right) V_h
\]
\[
s_h = \sum_{k=1}^{l_k}\exp\left(\frac{QK_{h,k}^\top}{\sqrt{d}}\right)
\]
- **全局聚合**：指定一台“查询主机”收集所有主机的 \(A_h\) 和 \(s_h\)，计算全局 softmax 分母 \(s_{\text{global}} = \sum_h s_h\)，然后用加权和得到全局注意力：
\[
A_{\text{global}} = \sum_{h} \frac{s_h}{s_{\text{global}}} A_h
\]
- **在线 Softmax 与 Flash Attention**：实际实现中结合在线 softmax（log-sum-exp 技巧）保证数值稳定性，并利用 Flash Attention 加速各主机的局部注意力计算。
- **令牌生成与缓存更新**：只有查询主机根据 \(A_{\text{global}}\) 生成新令牌，并更新其 KV 缓存。该过程自回归重复，通信量仅涉及每个主机传递一个标量 \(s_h\) 和一个向量 \(A_h\)（每个令牌），通信开销极小。

### 3. 实验设计

#### 3.1 使用模型
- **Llama-3.1-8B**（基础版与指令版），上下文长度 128K；
- **Llama-3.1-70B**（指令版）；
- **gradientai-Llama-3-8B-Instruct**（支持 262K 和 1048K 上下文，用于测试超长序列）。

#### 3.2 对比基线
- **Ring Attention**：分布式全局块状注意力，用于速度对比（均为分布式方案）。
- **StreamingLLM**：基于注意力汇的滑动窗口注意力（带 1000 全局 token + 8000 滑动窗口）。
- **MInference**：动态稀疏注意力，离线选择最佳稀疏模式。
- **Full (Global) Attention**：在单机或 Ring Attention 设置下的全局注意力，用于精度上限。

#### 3.3 评测基准
- **RULER**：13 个合成任务，涵盖 Needle-in-a-Haystack（检索）、多跳追踪、聚合、问答四类。
- **BABILong**：5 个需要跨多事实推理的长上下文任务。
- **InfiniteBench**：10 个包含真实与合成任务，覆盖摘要、多语言问答、代码调试、检索等，评估通用长上下文理解能力。

#### 3.4 评测指标
- 精度：准确率（%），与全局注意力的绝对差值 \(\Delta\)；
- 速度：相对于 Ring Attention 的加速比（\(\times\)），以及每样本推理时间。

### 4. 资源与算力

- **硬件**：所有实验均使用 **NVIDIA A100 GPU**，精度为 **bfloat16**。
- **GPU 数量**（表 7）：
  - Llama-3.1-8B：16K~128K 序列用 **8 卡**，256K~512K 用 **16 卡**，1M 用 **32 卡**。
  - Llama-3.1-70B：16K~32K 用 **8 卡**，64K 用 **16 卡**，128K 用 **32 卡**。
- **软件**：基于 HuggingFace Transformers 和 NVIDIA TRT-LLM 实现。
- **训练时长**：Star Attention **无需训练或微调**，所有实验均为推理评测。

### 5. 实验数量与充分性

- **主要实验组数**：
  - 多模型 × 多序列长度（16K~128K 甚至 1M）× 多基准（RULER, BABILong, InfiniteBench）× 不同块大小（1/4 序列长度等）。
  - 消融实验：锚定块位置、内容（常数、随机、打乱）、大小（0 到等于上下文块），以及有无锚定块的对比。
  - 与三种稀疏/分布式方法的精度对比，与 Ring Attention 的速度对比。
- **充分性评估**：
  - 覆盖了合成与真实任务，从 16K 到 1M 长度。
  - 充分探讨了锚定块机制、块大小与精度的权衡。
  - 基线选择具有代表性，包括了分布式方法和稀疏方法。
  - 使用标准基准，且与全局注意力直接对比，实验公平、客观。未发现明显的偏差风险。

### 6. 主要结论与发现

- **速度大幅提升**：Star Attention 相较于 Ring Attention 可实现最高 **11×** 推理加速，在超长序列（1M tokens）甚至达到 **16.9×**。
- **精度保持良好**：在多数任务中，精度损失控制在 **0-3%**，部分任务（如聚合）甚至超过全局注意力。
- **任务适应性**：在检索、问答、聚合任务上表现接近全局注意力；在多跳追踪任务上因缺乏跨块通信而有所退化。
- **锚定块的核心作用**：
  - 内容至关重要（必须使用序列开头的真实 token），位置（位置 ID）影响很小。
  - 锚定块大小需与上下文块大小相当，否则性能大幅下降。
  - 无锚定块时，精度会大幅崩塌（如 NIAH 任务下降 25-40%）。
- **块大小权衡**：块大小取序列长度约 **1/4** 时，可获得最佳精度-速度平衡。超长序列固定 32K 块可在加速与精度之间取得较好折中。

### 7. 优点

- **即插即用**：无需模型微调，直接兼容大多数用全局注意力训练的 Transformer LLM。
- **极低的通信开销**：第二阶段仅需传递标量指数和与局部注意力向量，远优于 Ring Attention 的 KV 缓存全传输。
- **分布式友好**：通过锚定块机制，各主机在上下文编码阶段完全并行、无通信，适合多设备协同推理。
- **精度稳健**：在多种任务和模型规模下均能保持极高精度，尤其适合检索和聚合类任务。
- **可结合现有优化**：能与 Flash Attention、KV 缓存压缩等方法正交结合，进一步提升效率。

### 8. 不足与局限

- **跨块交互受限**：上下文编码阶段的局部注意力无法建模跨块依赖，导致多跳推理任务精度下降明显。
- **锚定块大小要求严格**：锚定块需与上下文块等大才能获得最佳精度，原因尚不明确，增加了内存占用。
- **块大小敏感**：当上下文块过小时，精度退化较明显，在超长序列上尤为突出。
- **任务覆盖尚可扩展**：主要实验基座为 Llama 系列，其他模型架构（如非自回归、MOE 等）的效果待验证；真实的长上下文对话、多轮交互场景也未涉及。
- **仅限推理**：方法设计专为推理优化，无法直接应用于训练阶段。

（完）
