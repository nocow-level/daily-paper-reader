---
title: "Polar Sparsity: High Throughput Batched LLM Inferencing with Scalable Contextual Sparsity"
title_zh: 极稀疏性：通过可扩展的上下文稀疏性实现高吞吐量批处理LLM推理
authors: "Susav Shrestha, Bradley Settlemyer, Nikoli Dryden, A. L. Narasimha Reddy"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=cg2S1qqNSq"
tags: ["query:edge-llm"]
score: 7.0
evidence: 注意力头的可扩展稀疏性加速批处理LLM推理，利于高效部署
tldr: 针对上下文稀疏性在大批次下失效的问题，Polar Sparsity提出将稀疏化重心从MLP转移至注意力层，利用注意力头稀疏性的批次不变特性，实现了可扩展的高吞吐量批处理LLM推理。该方法为大规模LLM在线服务提供了新的效率优化维度。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1438, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1441, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1435, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1443, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1443, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1438, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1433, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1447, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1430, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1442, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1442, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1442, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-cg2s1qqnsq/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1445, \"height\": 603, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-cg2s1qqnsq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1450, \"height\": 702, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-cg2s1qqnsq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1044, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-cg2s1qqnsq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1457, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-cg2s1qqnsq/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1450, \"height\": 439, \"label\": \"Table\"}]"
motivation: 现有上下文稀疏性在增大批次时因神经元激活并集快速膨胀而退化为稠密计算。
method: 聚焦于注意力头的稀疏性，利用其批次稳定性设计可扩展的稀疏计算方案。
result: 在保持稀疏加速的同时实现了大批次下的高吞吐量推理。
conclusion: 极稀疏性为批处理LLM推理提供了一种新颖的稀疏化策略，突破了批次规模限制。
---

## Abstract
Accelerating large language model (LLM) inference is critical for real-world deployments requiring high throughput and low latency. Contextual sparsity, where each token dynamically activates only a small subset of the model parameters, shows promise but does not scale to large batch sizes due to union of active neurons quickly approaching dense computation. We introduce Polar Sparsity, highlighting a key shift in sparsity importance from MLP to Attention layers as we scale batch size and sequence length. While MLP layers become more compute-efficient under batching, their sparsity vanishes. In contrast, attention becomes increasingly more expensive at scale, while their head sparsity remains stable and batch-invariant. We develop Selective Head Attention with hardware-efficient, sparsity-aware GPU kernels, delivering up to \(2.2\times\) end-to-end speedups for models like OPT, LLaMA-2 \& 3, Qwen, Mistral across various batch sizes and sequence lengths without compromising accuracy. To our knowledge, this is the first work to demonstrate that contextual sparsity can scale effectively to large batch sizes, delivering substantial inference acceleration with minimal changes, making Polar Sparsity practical for large-scale, high-throughput LLM deployment systems.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现代大语言模型（LLM）推理中，上下文稀疏性（Contextual Sparsity）是一种有前景的加速技术，即每个 token 仅动态激活一小部分神经元。然而，当使用批处理（Batching）提升吞吐量时，不同序列的激活神经元并集（Union Activations）迅速膨胀，导致稀疏性退化、计算量趋近于稠密模型，使得现有稀疏方法在规模化部署时效果急剧下降。
- **整体含义**：论文揭示了一个关键现象——随着批大小（Batch Size）和序列长度（Sequence Length）的增加，稀疏性的重要性从 **MLP 层**转移到了 **注意力层**。MLP 层的稀疏性会因批处理而消失，而注意力头的稀疏性却保持稳定且不受批次影响。基于此洞察，提出了 **Polar Sparsity（极稀疏性）**，通过将稀疏化重心从 MLP 迁移至注意力头，实现了在大规模批处理推理中仍然有效、可扩展的加速，将上下文稀疏性从单查询引向了高吞吐场景。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：Polar Sparsity 利用注意力头稀疏性的 **批次不变（Batch-Invariant）** 特性，在批处理解码时仅对每个请求最重要的注意力头进行计算。同时，对 MLP 层仍保留动态稀疏化，但采用适用于批处理的动态 top-k 策略和融合内核，以补偿稀疏性退化带来的影响。
- **MLP 层动态稀疏化与内核**：
  - **路由器**：为每个 Transformer 层设计一个轻量级两层前馈网络（瓶颈维度 1024），预测神经元激活。训练时用真实激活作为监督信号，损失为二元交叉熵。
  - **动态 top-k 策略**：根据目标召回率（99%），离线逐层贪心地选择最小的 top-k 神经元数量，以适应不同层和批大小的动态激活变化。
  - **Selective GEMM 内核**：将索引与矩阵乘法融合，避免单独的 Gather/Scatter 操作，支持批处理 GEMM，在 A100 上取得最高 5.5 倍加速。
- **注意力层选择性头部注意力（Selective Head Attention）**：
  - **注意力路由器**：使用单层全连接网络，根据输入 hidden state 预测每个注意力头的激活分数（依据输出 L2 范数），选出 top-k 个最重要的头。
  - **Selective FlashAttention 解码内核（算法1）**：在 FlashAttention 的基础上，融入批次头索引（batch_head_index）张量。每个 CUDA 线程块或 Triton 程序只针对激活的注意力头进行 Q、K、V 的读取和计算，大幅减少内存 I/O 和计算量。
  - **组查询注意力（GQA）适配**：对于使用 GQA 的模型，采用组稀疏性（Group Sparsity），即同一组内的 query 头共享 KV cache，一起被激活或跳过。
- **计算流程**：对于 OPT 模型同时应用 MLP 和注意力头稀疏；对于 LLaMA 等不使用 ReLU 的模型，仅应用注意力头稀疏（因其 MLP 稀疏化不理想）。路由器在推理时与对应模块并行或顺序执行，以隐藏部分延迟。

### 3. 实验设计：使用了哪些数据集/场景，它的 benchmark 是什么，对比了哪些方法
- **模型与架构**：预训练模型包括 OPT（6.7B, 30B, 66B）、LLaMA-2（7B, 13B）、LLaMA-3.1（70B）、Mistral（7B）；指令微调模型包括 LLaMA-3.1-8B-Instruct、Mistral-7B-Instruct、Qwen-2.5-14B-Instruct。
- **下游任务 Benchmark**：九个零样本任务：COPA、OpenBookQA、PIQA、RTE、WinoGrande、HellaSwag、MMLU、ARC-Easy、ARC-Challenge；指令微调模型额外评估 MMLU-PRO 和 LongBench。使用 `lm-eval-harness` 框架测量准确率。
- **对比方法**：与稠密基线（Dense）对比不同注意力头激活密度下的准确率；吞吐量与延迟对比了 **Deja Vu 风格的激活稀疏性**（使用 Selective GEMM 替换稀疏 GEMV 以适配批处理）以及稠密基线。在 LLaMA-2-7B 上，还与 ProbePruning、ReLUfication、ProSparse、CATS、TEAL、GRIFFIN、R-Sparse 等近年稀疏化方法进行了精度对比。
- **实验场景**：测试覆盖多种批大小（1 到 512，直至显存上限）、多种序列长度（OPT: 1920, LLaMA-2: 3968, LLaMA-3: 8192），并利用流水线并行（Pipeline Parallelism）和张量并行（Tensor Parallelism）进行吞吐测试。内核性能在 A5000、A100、H100 上均有验证。

### 4. 资源与算力
- **硬件**：所有实验在 **NVIDIA DGX A100 80GB GPU 节点**服务器上完成；内核性能测试额外使用了 A5000 和 H100。
- **路由器训练**：使用来自 Wikitext-2 训练集的 **400,000 个 token 样本**。训练配置：batch size 64，学习率 1e-4，AdamW 优化器，最多 20 个 epoch 并采用 early stopping。**论文未明确给出训练所需的总 GPU 时数或单个 GPU 的具体训练耗时**。
- **推理测量**：使用 CUDA Graphs 进行解码吞吐量与延迟测量，以获取稳定且低波动结果。

### 5. 实验数量与充分性：大概做了多少组实验，这些实验是否充分、客观、公平
- **实验规模丰富**：涵盖了 **5 个模型家族、9+ 种下游任务**，贯穿从 6.7B 到 70B 的多种参数规模。系统性能测试覆盖多种批大小和序列长度，并展示了流水线并行与张量并行场景下的结果。
- **消融与深入分析**：
  - 分析了 MLP 层神经元和注意力头的激活模式（含热力图）。
  - 测量了路由器及稀疏内核各自的延迟，并研究路由器延迟的隐藏效果。
  - 验证了 Selective MLP 和 Selective Attention 内核在不同 GPU 架构上的线性加速特性。
  - 对比了不同稀疏方法在 LLaMA-2-7B 上的零样本精度，保证对比的公平性。
- **充分性与客观性**：实验设计遵循标准的学术流程，对比基线均基于公开模型和已有工作，展示了标准偏差或通过 CUDA Graphs 保证了测量的可靠性。稀疏阈值设定基于准确率下降不超过 1% 的“临界阈值”，逻辑清晰且可复现。

### 6. 论文的主要结论与发现
- **批次不变的头稀疏性**：在批处理解码中，注意力头的稀疏性几乎不受批次规模影响，而 MLP 层的并集稀疏性随批大小快速退化，这为规模化稀疏推理指明了新方向。
- **高效加速**：Polar Sparsity 在 **大带宽场景** 下，端到端解码吞吐量最高达到稠密基线的 **2.2 倍**（OPT-66B），且比传统激活稀疏方法高出 2 倍；在 LLaMA-3.1-70B 上也取得 1.51 倍加速。
- **精度保持**：在临界注意力密度下，预训练模型的 **平均准确率下降在 1% 以内**，指令微调模型在 LongBench 等生成式基准上也保持竞争力，证明该方法几乎不牺牲模型质量。
- **内核有效性**：提出的 Selective GEMM 和 Selective FlashAttention 内核能随稀疏度线性加速，将理论稀疏性真正转化为 wall-clock 速度收益。

### 7. 优点：方法或实验设计上有哪些亮点
- **首次实现**：首次证明上下文稀疏性能够有效扩展到大批量推理，突破了以往的瓶颈。
- **方法论新颖**：提出“极稀疏性”概念，明确区分 MLP 与 Attention 在不同推理规模下的稀疏性适用性，并将优化重心转移到注意力头。
- **硬件友好**：专门设计的高效 GPU 内核（Selective FlashAttention、Selective GEMM）对稀疏性敏感，可在多代 GPU（A5000/A100/H100）上线性加速，为实际部署扫清了障碍。
- **模型无关**：仅需训练轻量级路由器，无需修改原模型参数，适用于多种架构（OPT、LLaMA、Mistral、Qwen），包括没有 ReLU 激活的模型（仅稀疏注意力）。
- **潜力巨大**：头稀疏性与 token 稀疏性正交，可进一步结合；且推理难度感知的路由器有望实现无损的动态稀疏推理。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **小规模场景收益有限**：小批量和短序列下，GPU 工作负载本身较低，稀疏化的加速效果不明显，甚至会因路由器开销影响延迟。
- **静态 top-k 策略**：每层激活的注意力头数量仍是固定的，缺乏依据输入难度动态调整的机制，可能无法同时达到最优精度和效率。
- **未与 token 稀疏整合**：当前工作仅聚焦头稀疏性，与 token 级稀疏的结合未探索，潜在乘法收益待挖掘。
- **上下文长度局限**：实验中的序列长度最长仅 8192，未覆盖新一代模型百万级 token 的“长上下文”场景，稀疏模式是否仍稳定尚待验证。
- **GQA 模型略逊**：组查询注意力（GQA）模型的组稀疏性本质上弱于单头稀疏性，可能导致重要头被整组遗漏，因此精度退化对稀疏度更敏感，加速比相对有限。
- **解码策略局限**：仅评估贪婪解码，束搜索和投机解码下的有效性未知。
- **微小精度损失**：尽管平均误差很低，部分困难任务（如 RTE、MMLU）对头稀疏更敏感，仍有细微准确率下降，文中提到可通过微调恢复。

（完）
