---
title: "RetrievalAttention: Accelerating Long-Context LLM Inference via Vector Retrieval"
title_zh: RetrievalAttention：通过向量检索加速长上下文LLM推理
authors: "Di Liu, Meng Chen, Baotong Lu, Huiqiang Jiang, Zhenhua Han, Qianxi Zhang, Qi Chen, Chengruidong Zhang, Bailu Ding, Kai Zhang, Chen Chen, Fan Yang, Yuqing Yang, Lili Qiu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=8z3cOVER4z"
tags: ["query:edge-llm"]
score: 8.0
evidence: 通过近邻搜索技术将KV缓存索引存放在CPU内存，降低GPU内存消耗并加速长上下文LLM推理。
tldr: 长上下文LLM推理面临KV缓存占用GPU内存过大、速度慢的问题。RetrievalAttention提出一种免训练方法，将固定上下文的KV向量预建索引于CPU内存，通过近似最近邻检索融入注意力计算，并针对查询和键向量的分布偏移设计了适应性的索引策略，显著降低GPU内存占用并加速解码，使长上下文推理更高效可行。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 728, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1250, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1420, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1458, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 494, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 681, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 541, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 438, \"height\": 315, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 596, \"height\": 300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 696, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 545, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 632, \"height\": 399, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-8z3cover4z/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1165, \"height\": 457, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 626, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1266, \"height\": 757, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 360, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 818, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 388, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1221, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1438, \"height\": 1017, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 804, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1433, \"height\": 120, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1306, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1156, \"height\": 144, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-8z3cover4z/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 866, \"height\": 113, \"label\": \"Table\"}]"
motivation: 长上下文场景下，KV缓存导致GPU内存消耗过高、推理速度缓慢，限制LLM应用。
method: 采用免训练方法，在CPU内存预构建KV向量索引，利用近似最近邻搜索融入注意力机制。
result: 实验显示该方法大幅降低GPU内存占用，同时提升长上下文推理速度，且保持模型精度。
conclusion: RetrievalAttention为长上下文LLM在资源有限设备上的高效推理提供了实用方案。
---

## Abstract
Transformer-based Large Language Models (LLMs) have become increasingly important. However, scaling LLMs to longer contexts incurs slow inference speed and high GPU memory consumption for caching key-value (KV) vectors. This paper presents RetrievalAttention, a training-free approach to both accelerate the decoding phase and reduce GPU memory consumption by pre-building KV vector indexes for fixed contexts and maintaining them in CPU memory for efficient retrieval. Unlike conventional KV cache methods, RetrievalAttention integrate approximate nearest neighbor search (ANNS) indexes into attention computation. We observe that off-the-shelf ANNS techniques often fail due to the out-of-distribution (OOD) nature of query and key vectors in attention mechanisms. RetrievalAttention overcomes this with an attention-aware vector index. Our evaluation shows RetrievalAttention achieves near full attention accuracy while accessing only 1-3\% of the data, significantly reducing inference costs. Remarkably, RetrievalAttention enables LLMs with 8B parameters to handle 128K tokens on a single NVIDIA RTX4090 (24GB), achieving a decoding speed of 0.107 seconds per token.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义
* **研究动机**：随着大语言模型（LLMs）支持的上下文长度急剧增长（可达千万Token），推理效率成为瓶颈。Key-Value (KV) 缓存的内存占用和注意力计算的延迟随上下文长度线性增长，导致在资源受限的设备（如本地或边缘设备）上部署长上下文LLMs极为困难。
* **核心问题**：本文旨在解决长上下文LLM推理中解码阶段的**高GPU显存消耗**和**低速推理**问题，尤其是针对包含大量固定前缀（如系统提示、文档库）的请求场景。

### 论文提出的方法论
* **核心思想**：**RetrievalAttention** 提出一种免训练方法，将近似最近邻搜索（ANNS）融入注意力计算，通过动态稀疏注意力机制，仅检索与当前查询最相关的少量关键Token，从而绕过全量KV缓存的计算。
* **关键技术细节**：
    * **注意力感知的向量索引**：首次发现查询向量（Q）和键向量（K）存在**分布外（OOD）** 问题，即现成的ANNS索引因两者分布不匹配而失效。为此，该方法利用少量预采样查询向量，建立其与精准最近邻键向量的连接，再通过投影技术将连接关系转移到键向量自身上，构建出能有效弥合分布差距的图索引。
    * **CPU-GPU协同执行**：固定上下文的KV缓存及索引离线构建并存储在CPU内存中。解码时，采用CPU-GPU并行策略：
        1.  将静态激活的Token（如开头的注意力汇聚点Token和局部窗口Token）持久化在GPU上作部分注意力计算。
        2.  同时，在CPU端通过注意力感知索引快速检索出动态的关键Token，并计算另一部分注意力。
        3.  最后，将两部分注意力输出合并，得到近似的全注意力输出。
* **公式与算法流程（文字说明）**：近似注意力公式为 $\boldsymbol{o}_t \approx \sum_{i \in I_{t,\epsilon}} \tilde{a}_{t,i} \cdot \boldsymbol{v}_i$，其中$I_{t,\epsilon}$是被选中的高注意力权重Token索引子集。算法流程上，固定上下文的KV向量及索引离线构建在CPU内存；在线推理时，GPU处理静态Token注意力，CPU并行执行基于索引的动态KV检索与计算，最终通过类似FlashAttention的机制合并输出。

### 实验设计
* **数据集与基准**：使用了三个具有代表性的长上下文评测基准：
    * **RULER**：包含检索、聚合和问答等多种任务。
    * **∞-Bench**：平均值上下文长度超过100K Token的综合性基准。
    * **Needle-in-a-haystack**：测试在长文本中检索特定信息的能力。
* **对比方法**：将RetrievalAttention与多类免训练方法进行了对比：
    * 基于静态/启发式Token选择的方法：StreamingLLM、SnapKV、Quest。
    * 基于动态块检索的方法：InfLLM。
    * 基于哈希检索的方法：MagicPIG。
    * 基于推测性预取的方法：InfiniGen。
    * 传统ANNS方法（Faiss库）：精确KNN (Flat) 和聚类索引 (IVF)。

### 资源与算力
* **推理环境**：主要在一台配备**单张NVIDIA RTX4090 GPU**（24GB显存）、Intel i9-10900X CPU（10核）和128GB系统内存的服务器上进行了端到端实验。此外，还在**NVIDIA A100 GPU**上进行了补充延迟测试。
* **离线索引构建成本**：文中汇报了对10万Token上下文构建索引的耗时（如Llama-3-8B模型耗时约788秒），并明确指出这是离线完成的，不影响在线推理延迟。

### 实验数量与充分性
* **实验规模**：实验设计**非常充分且严格**。
* **多维度评测**：
    * **模型多样性**：在**三个**不同系列和规模的模型上进行评测（Llama-3-8B-Instruct-262k, Yi-9B-200K, Yi-6B-200K）。
    * **任务多样性**：覆盖了**三个**主流长上下文基准，并在其中细分任务上进行了详细分析。
    * **上下文长度**：评估了从4K、8K、16K到128K，甚至高达1000K的多种上下文长度。
    * **消融与微架构分析**：包含了对比实验（如投影技术的有效性）和参数敏感性分析（如静态模式大小、检索预算分配策略）。
    * **资源与延迟分析**：在不同用户输入长度下测试了预填充和解码阶段的延迟变化，并分析了吞吐量随批次大小的扩展性，还给出了详细的延迟分解。
* **客观性与公平性**：所有对比方法均为免训练，且在相同的硬件环境下测试，通过多个终端任务指标（准确率、解码延迟）进行客观衡量，设置了公平的比较基线。

### 论文的主要结论与发现
* **近乎无损的模型精度**：在RULER和∞-Bench等复杂长上下文任务上，RetrievalAttention取得了与全量注意力几乎相同的准确率（平均性能下降通常低于2.2%），显著优于其他动态稀疏或KV缓存压缩方法。
* **显著的推理加速与显存节省**：Accessing仅 **1-3%** 的KV缓存数据即可实现高精度。与精确KNN和传统IVF索引相比，在128K上下文下解码延迟分别降低了**7.93倍**和**2.80倍**。
* **边缘部署可行性**：首次实现了在**单张24GB显存的RTX4090 GPU**上，以可接受的延迟（0.109秒/Token）运行8B参数模型处理128K Token上下文，无需牺牲模型准确率。

### 优点
* **问题发现深刻**：首次系统性识别并量化了注意力机制中查询向量和键向量之间的**分布外（OOD）** 挑战，为将高性能ANNS应用于自注意力计算点明了关键障碍。
* **解决方案创新有效**：提出的**注意力感知索引**通过建立查询到键的映射并投影，巧妙地解决了OOD问题，设计新颖且效果显著。
* **工程系统设计完整**：**CPU-GPU协同架构**充分利用了两者的优势，将海量低活跃度缓存置于CPU并在其上完成检索和部分计算，极大降低了GPU负载和PCIe通信开销，具有很强的实用价值。
* **评估系统且客观**：实验设计涵盖了多个模型、基准和上下文长度，并与代表性方法进行了全面、公平的比较，结论说服力强。

### 不足与局限
* **适用场景特定**：当前设计明确聚焦于**固定前缀被大量复用**的场景，索引的离线构建是其前提。对于每次都是全新、动态变化的上下文，其构建索引的开销会抵消加速效果，通用性受限。
* **训练阶段未优化**：该方法主要加速解码阶段，**未涉及训练或长上下文预填充**的优化（预填充是通过复用缓存来加速TTFT）。
* **索引构建成本较高**：离线索引构建时间较长（近千秒级），这可能限制了其在需要频繁、快速构建索引的动态场景下的应用。
* **理论分析缺失**：论文未提供关于向量检索准确率或索引搜索复杂度的理论保证，结论主要基于系统的实证分析。

（完）
