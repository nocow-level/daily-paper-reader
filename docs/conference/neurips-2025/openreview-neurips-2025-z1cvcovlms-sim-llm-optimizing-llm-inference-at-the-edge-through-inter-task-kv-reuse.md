---
title: "Sim-LLM: Optimizing LLM Inference at the Edge through Inter-Task KV Reuse"
title_zh: Sim-LLM：通过任务间KV重用优化边缘LLM推理
authors: "Ruikun Luo, Changwei Gu, Qiang He, Feifei Chen, Song Wu, Hai Jin, Yun Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=z1Cvcovlms"
tags: ["query:edge-llm"]
score: 10.0
evidence: 通过任务间KV缓存重用优化边缘LLM推理，降低资源受限节点的内存和计算开销。
tldr: 边缘计算节点资源有限，LLM的KV缓存随任务增加导致GPU内存消耗巨大。Sim-LLM提出利用任务相似性实现KV缓存的跨任务重用，避免重复计算和冗余存储。通过识别相似任务并共享KV对，该方法在保持推理精度的同时显著降低了内存占用和计算开销，使得边缘服务器能够更高效地部署和运行大语言模型。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 642, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 861, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 428, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 881, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1421, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1199, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 713, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1343, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 721, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 721, \"height\": 329, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 703, \"height\": 314, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z1cvcovlms/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 853, \"height\": 267, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-z1cvcovlms/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 749, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-z1cvcovlms/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 955, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-z1cvcovlms/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1441, \"height\": 898, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-z1cvcovlms/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1446, \"height\": 506, \"label\": \"Table\"}]"
motivation: 边缘节点上LLM的KV缓存内存占用大，现有压缩方法计算昂贵，不适用于资源受限环境。
method: 提出Sim-LLM机制，利用任务相似性识别并重用KV缓存，减少重复存储与计算。
result: 实验表明Sim-LLM有效降低边缘LLM推理的GPU内存消耗，提升吞吐量。
conclusion: Sim-LLM通过任务相似性重用KV缓存，为资源受限边缘环境下的LLM推理提供了高效方案。
---

## Abstract
KV cache technology, by storing key-value pairs, helps reduce the computational overhead incurred by *large language models* (LLMs). It facilitates their deployment on resource-constrained edge computing nodes like edge servers. However, as the complexity and size of tasks increase, KV cache usage leads to substantial GPU memory consumption. Existing research has focused on mitigating KV cache memory usage through sequence length reduction, task-specific compression, and dynamic eviction policies. However, these methods are computationally expensive for resource-constrained edge computing nodes. To tackle this challenge, this paper presents Sim-LLM, a novel inference optimization mechanism that leverages task similarity to reduce KV cache memory consumption for LLMs. By caching KVs from processed tasks and reusing them for subsequent similar tasks during inference, Sim-LLM significantly reduces memory consumption while boosting system throughput and increasing maximum batch size, all with minimal accuracy degradation. Evaluated on both A40 and A100 GPUs, Sim-LLM achieves a system throughput improvement of up to 39.40\% and a memory reduction of up to 34.65%, compared to state-of-the-art approaches. Our source code is available at https://github.com/CGCL-codes/SimLLM.

---

## 论文详细总结（自动生成）

好的，这是对论文《Sim-LLM: Optimizing LLM Inference at the Edge through Inter-Task KV Reuse》的详细中文总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：在资源受限的边缘计算节点（如边缘服务器）上部署大型语言模型（LLM）时，**键值（KV）缓存**的内存消耗随任务数量和序列长度的增加而急剧膨胀，成为主要的性能瓶颈。现有的KV缓存压缩或驱逐方法（如H2O、StreamingLLM）虽然有效，但它们通常是基于层或基于令牌的细粒度操作，**计算开销大**，并不适用于资源本就紧张的边缘环境。

*   **整体含义**：本文旨在提出一种**更轻量、更高效**的LLM推理优化方法。其核心洞察是，在边缘计算场景中，由于服务范围和地理分布有限，LLM接收到的**推理任务之间存在着广泛的相似性**。Sim-LLM正是利用这一特性，通过**跨任务重用相似任务的KV缓存**，从任务层面大幅减少重复的KV计算和内存存储，从而在几乎不影响模型精度的前提下，提升系统吞吐量、降低内存占用。

### 2. 论文提出的方法论

Sim-LLM的方法论围绕三个核心挑战展开，即相似任务识别、处理不相似任务以及跨节点KV共享。

####   **核心思想**
通过缓存已完成任务的键值（KV）对，并在处理新任务时，识别并重用与之语义相似的历史任务的KV缓存，从而避免重复计算，节省GPU内存和计算时间。

####   **关键技术细节与算法流程**

*   **相似任务识别 (Semantic Similarity Identification)**
    *   **度量标准**：采用**余弦相似度**来衡量任务间的语义相似性，阈值为0.8，作为相似性判断的平衡点。
    *   **加速策略**：为了避免在小批量时穷举搜索开销过大，Sim-LLM结合了**局部敏感哈希（LSH）**。通过将任务的词嵌入映射到LSH桶中，系统能快速定位可能相似的历史任务。当批量大小较小时，直接使用余弦相似度比较；当批量较大时，则采用LSH进行快速查找。

*   **单节点KV缓存管理器 (KV\_Manager)**
    *   **只缓存顶层KV**：基于“Transformer底层关注句法信息，顶层关注语义信息”的发现，Sim-LLM仅缓存和重用**模型最顶层（top layer）**的KV对，用以替代当前任务在所有层的KV计算。这极大减少了缓存所需的内存空间。
    *   **推理流程（三明治结构）**：
        1.  **相似任务匹配成功**：新任务的查询（Query）在所有层仅与重用的顶层KV对进行注意力计算，直接跳过中间层的计算和KV生成，从底层直接跳至顶层生成输出。
        2.  **无相似任务**：对于不匹配的任务，采用"**三明治**"结构加速，即只保留并计算**底部三层**和**顶部三层**的KV，省略中间层的KV计算和存储。
    *   **缓存淘汰策略**：当缓存空间（可配置）满时，采用**最近最少使用（LRU）**策略进行淘汰，以保留最常被重用的KV。

*   **跨节点KV共享机制**
    *   **问题**：单节点内可能找不到相似任务。
    *   **解决方案**：引入**原型学习**概念。每个边缘服务器提取其处理过的任务特征，生成一个“任务原型”，并维护一个包含所有服务器原型的全局特征表。新任务到达时，其特征首先与全局特征表比较，直接定位到最可能存有相似任务的最优服务器，实现“一跳”查询，避免了向所有邻居服务器广播查询带来的网络开销和资源浪费。
    *   **数据传输优化**：当发现远程服务器有相似任务时，优先将当前任务的序列或词嵌入传输过去进行处理，而不是将庞大的KV缓存传回，以减小通信开销。

### 3. 实验设计

*   **数据集与场景**：
    *   **文本相似性分析**：使用了GLUE, SICK, SNLI, WIKI, REDDIT, MMChat, LCCC等7个数据集来展示边缘任务间的相似性。
    *   **性能基准测试**：在**OpenCompass**和**lm-eval-harness**框架下进行评估，涵盖了推理、语言、知识、考试、理解五个方面的多个基准，如CMNLI, HellaSwag, PIQA, MMLU, XSum等。
    *   **困惑度（PPL）评估**：使用了**SlimPajama**数据集的一个子集和**Wikipedia**数据集。

*   **模型**：在**TinyLlama-1.1B**, **Llama2-7B**, **Llama2-13B**以及**InternLM2-7B**（中英双语）上进行了实验，主要使用其聊天版本。

*   **对比方法**：与标准Transformer模型以及四种先进的KV缓存优化方法进行了比较：
    *   **StreamingLLM** (一种基于“注意力汇”和滑窗的缓存保留方法)
    *   **H2O** (一种基于“重击者”的累积注意力分数来保留关键KV的驱逐方法)
    *   **ZipCache** (一种识别显著令牌并结合每令牌量化压缩的方法)
    *   **ArkVale** (一种基于页面摘要，动态驱逐和召回关键KV页面的方法)

### 4. 资源与算力

*   **单节点实验**：在一台配备**单块NVIDIA A100 80GB GPU**的服务器上进行。
*   **多节点（边缘）实验**：使用**4台物理机**，每台配置**4块NVIDIA A40 40GB GPU**来模拟边缘服务器集群。
*   论文未提及模型的训练时长，因为Sim-LLM是一种**即插即用**的推理优化机制，不涉及模型训练或微调。

### 5. 实验数量与充分性

实验设计**较为充分且全面**，具体体现在：
*   **多模型验证**：在4种不同规模（1.1B, 7B, 13B）的模型上进行了验证。
*   **多维度评估**：从吞吐量、GPU内存占用、困惑度（PPL）、多种下游任务零样本准确率等维度进行综合衡量。
*   **多场景测试**：包含单节点和多节点（边缘集群）两种部署场景。
*   **细粒度消融研究**：对多个关键设计选择进行了消融实验，包括：
    *   **相似性阈值的影响**：在0.1到0.9的区间内分析了不同余弦相似度阈值对吞吐量、PPL和下游准确率的影响（图12）。
    *   **缓存大小的影响**：研究了不同的KV缓存容量对延迟、内存和PPL的影响（图8，图9）。
    *   **源层选择的影响**：对比了从底层、中层、顶层选择KV进行重用对PPL和准确率的影响（图10）。
    *   **任务相似度比例的影响**：构造了不同相似度比例的任务集来测试系统性能（图11）。
    *   **可变工作负载测试**：测试了在泊松分布（均匀）和幂律分布（突发）两种不同工作负载模式下的延迟表现（表1）。
*   **客观公平**：与多种SOTA方法进行了全面的横向对比，评估结果具有说服力。

### 6. 论文的主要结论与发现

*   **边缘LLM推理任务间存在广泛相似性**，且相似任务生成的KV缓存也具有很高的相似度（余弦相似度大多高于0.7）。
*   **Sim-LLM能显著提升性能并降低资源消耗**：与对比的SOTA方法相比，Sim-LLM实现了**最高39.40%（平均33.04%）的吞吐量提升**和**最高34.65%（平均30.05%）的内存占用降低**。
*   **精度损失极小**：在各种下游任务和PPL评估中，Sim-LLM的性能与标准模型相当，证明了其有效性。
*   **方法具有可扩展性**：跨节点共享机制能有效利用集群资源，并且在突发的工作负载下表现出良好的鲁棒性和低延迟。

### 7. 优点

*   **视角新颖**：从**任务间相似性**的宏观视角出发优化推理，区别于传统的层/令牌级优化。
*   **轻量高效**：无需修改模型结构或进行额外训练，是一种纯系统层面的即插即用式优化，计算开销小，特别适合边缘场景。
*   **跨节点协同**：设计了精巧的跨边缘服务器KV共享机制，利用原型学习实现高效的任务卸载，提升了整个边缘计算系统的资源利用率。
*   **实验扎实**：消融实验全面，对多个关键超参数和核心设计选择进行了详尽的剖析，说服力强。

### 8. 不足与局限

*   **额外的存储开销**：KV\_Manager需要存储历史任务的**顶层KV和嵌入向量**。当缓存大小设置得过大时（论文指出例如达到4096），这部分额外存储的开销可能超过节省下来的KV缓存，导致总内存消耗反而增加。
*   **模型同构性要求**：跨节点共享KV的前提是所有边缘服务器部署的**模型必须完全一致**，这限制了其在异构模型部署环境中的应用。
*   **相似性任务的依赖性**：系统性能**高度依赖于任务间的相似比例**。如果不断涌入全新的、与历史任务毫不相似的任务，Sim-LLM的性能会退化为标准推理。
*   **未报告误差棒**：作者在NeurIPS审查清单中承认，由于计算资源限制，实验结果**未报告误差棒（error bars）或统计显著性检验**。

（完）
