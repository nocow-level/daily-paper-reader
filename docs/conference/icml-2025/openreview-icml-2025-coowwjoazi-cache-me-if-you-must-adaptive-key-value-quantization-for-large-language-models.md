---
title: "Cache Me If You Must: Adaptive Key-Value Quantization for Large Language Models"
title_zh: 缓存随需应变：大语言模型的自适应键值量化
authors: "Alina Shutova, Vladimir Malinovskii, Vage Egiazarian, Denis Kuznedelev, Denis Mazur, Surkov Nikita, Ivan Ermakov, Dan Alistarh"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=COowwJOAZi"
tags: ["query:edge-llm"]
score: 9.0
evidence: 自适应键值缓存量化以减少内存占用
tldr: 针对大语言模型键值缓存占用大量设备内存的问题，提出自适应键值量化方法，利用跨层依赖性进行压缩，在保持生成质量的同时减少内存占用。该方法有助于在边缘设备上高效运行长上下文LLM，缓解内存瓶颈。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-coowwjoazi/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-coowwjoazi/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-coowwjoazi/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 858, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-coowwjoazi/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1707, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-coowwjoazi/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1701, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-coowwjoazi/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1721, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-coowwjoazi/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1718, \"height\": 698, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 795, \"height\": 1093, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1719, \"height\": 561, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 676, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 675, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 779, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 701, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 719, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1744, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1820, \"height\": 1916, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1670, \"height\": 575, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1668, \"height\": 576, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1669, \"height\": 572, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1632, \"height\": 489, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1630, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 645, \"height\": 725, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1466, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 577, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1526, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1527, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1525, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-coowwjoazi/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1526, \"height\": 453, \"label\": \"Table\"}]"
motivation: KV缓存高达数十GB，严重限制大模型的部署。
method: 利用键值跨层依赖性和高压缩内部网络方法，提出自适应KV量化压缩。
result: 方法在保持质量前提下有效降低内存占用。
conclusion: 自适应量化是解决LLM部署内存瓶颈的关键技术，提升长上下文推理效率。
---

## Abstract
Efficient real-world deployments of large language models (LLMs) rely on Key-Value (KV) caching for processing and generating long outputs, reducing the need for repetitive computation. For large contexts, Key-Value caches can take up tens of gigabytes of device memory, as they store vector representations for each token and layer. Recent work has shown that the cached vectors can be compressed through quantization, pruning or merging, but these techniques often compromise quality towards higher compression rates. In this work, we aim to improve Key \& Value compression by exploiting two observations: 1) the inherent dependencies between keys and values across different layers, and 2) the existence of high-compression methods for internal network states (e.g. attention Keys \& Values). We propose AQUA-KV, an adaptive quantization for Key-Value caches that relies on compact adapters to exploit existing dependencies between Keys and Values, and aims to "optimally" compress the information that cannot be predicted. AQUA-KV significantly improves compression rates, while maintaining high accuracy on state-of-the-art LLM families. On Llama 3.2 LLMs, we achieve near-lossless inference at 2-2.5 bits per value with under $1\%$ relative error in perplexity and LongBench scores. AQUA-KV is one-shot, simple, and efficient: it can be calibrated on a single GPU within 1-6 hours, even for 70B models.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容撰写的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **研究动机与背景：**
    *   **内存瓶颈：** 大语言模型（LLM）在生成长文本时，用于缓存先前计算的键（Key）和值（Value）向量（KV Cache）会占用巨大的设备内存。例如，Llama 3.1 70B模型处理一个最长上下文时，其16位精度的缓存就可能占用约43GB内存，甚至超过模型本身。
    *   **效率需求：** 这种内存消耗不仅增加了部署成本，还使推理过程受限于内存带宽，降低了速度。因此，高效压缩KV Cache对于在实际应用中部署LLM至关重要。
    *   **现有局限：** 现有压缩技术（如量化、剪枝）在追求高压缩率时，往往会显著牺牲模型精度。论文旨在解决这一折衷问题，实现更高的压缩率而不损失性能。

### 2. 论文提出的方法论

*   **核心思想：**
    *   利用KV Cache中**层间**和**层内**向量之间的内在依赖关系来改进压缩。具体来说，论文观察到相邻层的键和值向量以及同一层的键值向量之间存在很强的可预测性。

*   **关键技术细节：**
    *   **AQUA-KV框架：** 该框架并非直接量化原始的键和值，而是训练紧凑的线性预测器，利用前一层的键或值来“猜测”当前层的键或值，然后只对**预测残差**（即无法被预测的信息）进行量化存储。
    *   **预测器配置：**
        1.  使用前一层的重建**键**来预测当前层的**键**。
        2.  使用前一层的重建**值**和当前层已重建的**键**来预测当前层的**值**。
    *   **算法流程（单次校准）：**
        1.  运行模型通过少量校准数据，获取每层的KV Cache。
        2.  从第一层开始，逐层训练线性回归预测器。训练时，预测器的输入是上一层经过量化和反量化后的**重建**向量，以模拟推理时的实际情况。
        3.  计算当前层真实KV向量与预测值之间的残差。
        4.  使用一个可插拔的量化器（Q）量化该残差并存储。
        5.  对后续的所有Transformer层重复此过程。
    *   **与量化器的兼容性：** AQUA-KV是一个与量化方法无关的框架，可以使用简单的均匀量化、QuaRot或HIGGS等向量量化方法作为其“骨干”量化器来压缩残差。

### 3. 实验设计

*   **数据集与场景：**
    *   **校准数据：** 从RedPajama数据集中随机抽取256个长度为8192个Token的序列，其中224个用于训练，32个用于验证。
    *   **评估基准：**
        *   **困惑度：** WikiText-2数据集，在基础（非指令微调）模型上评估。
        *   **长文本任务：** LongBench v1基准测试，包含14个英语任务（如问答、摘要），在指令微调模型上评估。
        *   **其他任务（部分模型）：** GSM8K（数学推理）、MMLU-Pro（通用推理）、IFEval（指令遵循）和HumanEval（编程）。
*   **对比方法：**
    *   **骨干量化器对比：** 在AQUA-KV框架内，对比了Quanto、QuaRot和HIGGS三种不同的量化方案。
    *   **外部基线对比：** 与专门的KV缓存量化方法进行了比较，包括KIVI和KVQuant。
    *   **相关策略对比：** 与层间KV缓存共享方法KVSharer，以及动态剪枝方法H2O进行了对比。

### 4. 资源与算力

*   **校准成本：** 论文明确指出AQUA-KV是一种高效的“单次”校准方法。对于一个Llama-3.1-70B模型，其完整的预测器校准过程可以在**单个GPU**上、在**1到6个小时**内完成，且最多占用16GB显存。
*   **推理硬件：** 推理速度基准测试在**NVIDIA A100 GPU**上执行（3B模型用单卡，70B模型用2张A100）。

### 5. 实验数量与充分性

*   **实验数量：** 实验设计丰富且系统，包含以下主要方面：
    *   **消融实验：** 在Llama 3.2 3B模型上进行了非常详尽的消融研究，包括不同骨干量化器、预测器架构（线性、降秩回归、MLP）、首层量化精度、注意力汇的处理、不同预测输入源等。
    *   **规模扩展：** 在5个不同规模和家族的模型（Llama 3.x 3B/8B/70B， Qwen 2.5 3B/7B）上评估了2/3/4比特等多种位宽下的表现。
    *   **基准覆盖：** 评估指标覆盖语言建模质量（困惑度）和多种下游任务能力（LongBench, GSM8K, MMLU-Pro等）。
    *   **兼容性验证：** 额外进行了与剪枝技术（H2O）结合的实验，验证了AQUA-KV的正交兼容性。
*   **客观性与公平性：** 实验对比公平。例如，为了公平比较，AQUA-KV和基线方法都保留了前几个不受压缩的注意力汇（attention sinks）和最近的Token。对比方法均遵循其原论文建议的设置。

### 6. 论文的主要结论与发现

*   **KV缓存存在强依赖性：** 邻近层的键和值之间存在很高的可预测性，这种依赖性是AQUA-KV方法有效的基础。
*   **大幅提升量化性能：** AQUA-KV能显著提高KV缓存的压缩率同时保持高精度。特别是在极端的2比特量化下，使用AQUA-KV的2比特量化效果大致相当于不使用的3比特量化效果。
*   **近乎无损的推理：** 在Llama 3.2模型上，仅用2-2.5比特/值，就能在困惑度和LongBench分数上实现相对误差低于1% 的近乎无损推理。
*   **通用性与兼容性：** AQUA-KV与多种量化方法和剪枝策略兼容，且校准成本低，具有很好的实用性。

### 7. 优点

*   **方法新颖有效：** 创新性地将KV缓存的层间依赖性用于构建预测-残差压缩框架，在压缩率与精度之间取得了极佳的平衡，尤其在低位宽下优势明显。
*   **通用性强：** “量化器无关”的设计使其可以灵活地与不同的先进量化技术结合，并可以与剪枝等正交技术共存。
*   **资源开销小：** 训练和推理的额外计算与内存开销很小，预测器参数远少于模型本身。校准过程资源友好，单GPU即可在几小时内完成对大模型的压缩设置。
*   **实验详尽：** 论文提供了非常全面的消融实验和多维度评估，有力地支撑了其核心论点。

### 8. 不足与局限

*   **推理延迟：** 尽管节省了内存，论文也指出AQUA-KV引入了额外的预测计算步骤，导致生成单个Token的延迟比不压缩的BF16基线高出约18%。其设计主要面向内存优化场景，而非纯推理加速。
*   **校准依赖：** 方法需要少量校准数据来训练预测器，不完全是一种“免校准”（calibration-free）方案，尽管其数据需求很低。
*   **静态位宽：** 当前方法对所有层和Token使用统一的位宽进行压缩，作者也指出未来可以探索动态调整不同组件位宽的潜力。
*   **根本原因未解：** 论文发现了LLM中KV表示的可预测性这一现象并加以利用，但并未解释为何LLM会学到这样具有“冗余”的表示，这仍是一个待探究的开放问题。

（完）
