---
title: "MUSTAFAR: Promoting Unstructured Sparsity for KV Cache Pruning in LLM Inference"
title_zh: MUSTAFAR：促进LLM推理中KV缓存剪枝的非结构化稀疏性
authors: "Donghyeon Joo, Helya Hosseini, Ramyad Hadidi, Bahar Asgari"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=C69741fMFX"
tags: ["query:edge-llm"]
score: 9.0
evidence: 利用非结构化稀疏性剪枝KV缓存以降低LLM推理的内存开销
tldr: "该论文展示非结构化稀疏性可高效压缩KV缓存，无需微调即可在70%稀疏度下保持精度。通过逐令牌幅度剪枝和位图稀疏格式，大幅降低解码阶段的内存开销。这一发现为在内存有限的硬件上运行Transformer模型提供了简单有效的解决方案。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 728, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1433, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 710, \"height\": 249, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 707, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1411, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 643, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 676, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 675, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 680, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1374, \"height\": 748, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-c69741fmfx/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 731, \"height\": 317, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1446, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1017, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1455, \"height\": 869, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1172, \"height\": 577, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1176, \"height\": 349, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1443, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1446, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 587, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1455, \"height\": 636, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1454, \"height\": 418, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1455, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1454, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-c69741fmfx/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1455, \"height\": 352, \"label\": \"Table\"}]"
motivation: KV缓存大小是LLM解码的主要内存瓶颈，限制了大上下文长度的应用。
method: 利用逐令牌幅度剪枝和位图稀疏格式实现非结构化稀疏KV缓存压缩。
result: "达到70%稀疏度且不损失精度，超越以往结构化剪枝方法。"
conclusion: 非结构化稀疏性为KV缓存压缩提供了高效路径，显著减轻了内存压力。
---

## Abstract
We demonstrate that unstructured sparsity significantly improves KV cache compression for LLMs, enabling sparsity levels up to 70\% without compromising accuracy or requiring fine-tuning. We conduct a systematic exploration of pruning strategies and find per-token magnitude-based pruning as highly effective for both Key and Value caches under unstructured sparsity, surpassing prior structured pruning schemes. The Key cache benefits from prominent outlier elements, while the Value cache surprisingly benefits from a simple magnitude-based pruning despite its uniform distribution. KV cache size is the major bottleneck in decode performance due to high memory overhead for large context lengths. To address this, we use a bitmap-based sparse format and a custom attention kernel capable of compressing and directly computing over compressed caches pruned to arbitrary sparsity patterns, significantly accelerating memory-bound operations in decode computations and thereby compensating for the overhead of runtime pruning and compression. Our custom attention kernel coupled with the bitmap-based format delivers substantial compression of KV cache up to 45\% of dense inference and thereby enables longer context lengths and increased tokens/sec throughput of up to 2.23$\times$ compared to dense inference. Our pruning mechanism and sparse attention kernel is available at https://github.com/dhjoo98/mustafar.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在大语言模型（LLM）推理中，键值（KV）缓存的内存开销已成为制约上下文长度扩展和吞吐提升的主要瓶颈。现有KV缓存压缩方法多集中于结构化剪枝（如通道级移除），未能充分挖掘细粒度稀疏的潜力。
- **整体含义**：本文提出并验证**非结构化稀疏性**在KV缓存剪枝中的显著优势，证明移除剪枝模式的结构性约束可在不牺牲精度、无需微调的前提下实现高达70%的稀疏度，从而大幅压缩缓存、提升推理效率。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：对Key和Value缓存分别采用**逐令牌幅度剪枝**，利用非结构化稀疏模式最大化压缩；并设计**基于位图的稀疏格式**与**自定义注意力内核**，直接在压缩后的缓存上执行计算，以加速内存受限的解码操作。
- **关键技术细节**：
  - **剪枝算法**：
    - **Key缓存**：利用通道离群值，采用逐令牌输出感知剪枝。剪枝分数 S = |K| ⊙ broadcast(∑^{T+31}_{t=T} |Q_t|)，按元素绝对值决定保留。
    - **Value缓存**：由于注意力机制中每个Value元素与同一个注意力分数相乘，**逐令牌幅度剪枝天然具有输出感知性**，因此直接采用绝对值排序保留，无需额外计算。
    - 统一保留最近32个令牌的稠密窗口，保证短上下文精度。
  - **稀疏格式与内核**：
    - 采用**位图稀疏格式**（每1×64列瓦片用64位比特图标记非零位置），实现对任意稀疏模式的最大压缩。
    - 设计**自定义CUDA注意力内核**，遵循“加载即压缩、计算用稠密”流水线，将压缩数据从全局内存加载、解压至共享内存后，用稠密计算瓦片加速批量稀疏矩阵-向量乘（SpMV），减少全局内存到流多处理器的数据搬运。
- **算法流程**（解码阶段注意力）：
  1. 稠密局部窗口注意力分数计算：S_L = Q_t K_L
  2. 稀疏注意力分数计算：S_C = Q_t K_C（直接作用于压缩缓存）
  3. 拼接分数并做softmax：S_t = softmax(concat(S_C, S_L))
  4. 分别用稀疏与稠密缓存计算最终输出：O_t = V_C S^⊤_C + V_L S^⊤_L

### 3. 实验设计：使用了哪些数据集/场景，它的benchmark是什么，对比了哪些方法
- **数据集/基准**：
  - 长文本理解基准：**LongBench**（覆盖单/多文档QA、摘要、少样本学习、合成、代码等任务）
  - 长上下文压力测试：**RULER**（上下文长度65K，包括大海捞针等任务）
- **模型**：Llama-2-7B, Llama-2-13B-chat, Llama-3-8B-Instruct, Mistral-7B-Instruct-v0.2, Llama-3.1-8B-Instruct 等。
- **对比方法**：
  - 结构化剪枝：**ThinK**（通道级剪枝）
  - 半结构化剪枝：2:4稀疏模式
  - 正交压缩联合：**H2O**（令牌驱逐）、**KIVI**（KV缓存量化）
  - 效率对比：**cuBLAS**稠密批量矩阵-向量乘、**FlashAttention**。

### 4. 资源与算力：如果文中有提到，请总结使用了多少算力
- **评估硬件**：效率测试在 **NVIDIA RTX 6000ADA GPU** 上进行，使用NVIDIA Nsight工具测量延迟。
- **训练算力**：**无训练/微调需求**，方法为纯后处理剪枝与推理优化，未提及任何训练相关的GPU卡数或训练时长。

### 5. 实验数量与充分性：大概做了多少组实验，这些实验是否充分、是否客观、公平
- **实验数量极丰富**，主要分组包括：
  - **不同稀疏度**：0.5, 0.7, 0.8, 0.9 等。
  - **缓存组合**：仅Key/仅Value/Key+Value分别剪枝。
  - **模型规模**：7B, 8B, 13B 多模型消融。
  - **与多种基准对比**：ThinK(结构化)、2:4半结构化、以及联合H2O/KIVI。
  - **效率拆解**：延迟分解为剪枝、压缩、局部窗口MV、稀疏SpMV等，并测试不同批大小吞吐。
  - **额外基准**：附录补充RULER和更大模型。
- **充分性与公平性**：实验设置一致（如局部窗口大小、FP16），对比基线直接引用公开方法结果，同时提供自己的复现与增强，分析客观，具备说服力。

### 6. 论文的主要结论与发现
- **非结构化稀疏远优于结构化**：在相同稀疏度下，逐令牌幅度剪枝在Key和Value缓存上均大幅超越ThinK等结构化剪枝，且Value缓存也能高效剪枝（70%稀疏无显著掉点）。
- **简单方法即有效**：Key缓存借助离群通道、Value缓存因注意力机制自带的输出感知性，使得纯幅度剪枝几乎达到最优。
- **系统加速可行**：自定义内核与位图格式将KV缓存压缩至密集缓存的45%（70%稀疏度），解码吞吐最高提升**2.23倍**，并支持更大批处理。
- **模块化兼容**：可与令牌驱逐（H2O）、量化（KIVI）等正交方法无缝叠加，进一步提升压缩率。

### 7. 优点：方法或实验设计上有哪些亮点
- **首次系统论证非结构化稀疏在KV缓存剪枝中的潜力**，并给出清晰的理论解释。
- **剪枝策略与系统实现协同设计**：位图稀疏格式+定制内核直接利用稀疏性，且无需重训。
- **实验翔实**：覆盖多模型、多任务、多稀疏度、多正交组合，且同时对精度与延迟做了细致拆解。
- **开源代码**，提升了可复现性。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **小批处理场景效率低**：批大小为1时吞吐低于稠密推理，因GPU利用率不足。
- **内核支持有限**：当前内核不支持低比特精度，与量化结合时只能评估精度而无法实现实际加速。
- **首次令牌延迟增加**：由于预填充阶段需执行剪枝和压缩，可能影响首令牌生成速度。
- **Key缓存高稀疏度敏感**：在某些模型上70% Key稀疏可能导致较大精度下降，需人工调制不同缓存的稀疏度。
- **实验模型范围**：主要评估Transformer架构的Llama/Mistral，未涵盖非Transformer或更大规模参数模型。
- **压缩格式开销**：位图格式带来约15%的额外元数据（如偏移量和对齐填充），真实压缩比低于理论值。

（完）
