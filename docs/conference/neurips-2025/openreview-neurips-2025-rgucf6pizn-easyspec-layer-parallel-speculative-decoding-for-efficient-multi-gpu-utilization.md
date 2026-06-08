---
title: "EasySpec: Layer-Parallel Speculative Decoding for Efficient Multi-GPU Utilization"
title_zh: EasySpec：面向高效多GPU利用的层并行推测解码
authors: "Yize Wu, KE GAO, Ling Li, Yanjun Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=RGUcF6pIZN"
tags: ["query:edge-llm"]
score: 8.0
evidence: 提出层并行推测解码技术在多GPU系统上加速LLM推理
tldr: 现有推测解码在多GPU系统中因小模型的层间顺序依赖导致GPU闲置，EasySpec提出层并行推测策略，通过打破层间顺序执行，使草稿模型和基础模型的各层能并行处理，从而提升多GPU利用率，加速LLM推理。实验显示该策略有效提高了吞吐量。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-rgucf6pizn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1430, \"height\": 1393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rgucf6pizn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1113, \"height\": 683, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rgucf6pizn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 727, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rgucf6pizn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1382, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-rgucf6pizn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1140, \"height\": 588, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1260, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1396, \"height\": 1702, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1387, \"height\": 429, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 819, \"height\": 226, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1440, \"height\": 877, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1251, \"height\": 322, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 701, \"height\": 418, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 861, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1412, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-rgucf6pizn/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1443, \"height\": 2039, \"label\": \"Table\"}]"
motivation: 多GPU推测解码中，小模型草稿阶段因层顺序执行导致GPU闲置，硬件利用率低。
method: 提出层并行推测策略，打破层间顺序依赖，使草稿和验证阶段各层可并行执行。
result: 实验表明该方法显著提升了多GPU系统的LLM推理吞吐量。
conclusion: 层并行推测解码有效解决了多GPU推测解码的利用效率问题，为LLM高效推理提供了新思路。
---

## Abstract
Speculative decoding is an effective and lossless method for Large Language Model (LLM) inference acceleration. It employs a smaller model to generate a draft token sequence, which is then verified by the original base model. In multi-GPU systems, inference latency can be further reduced through tensor parallelism (TP), while the optimal TP size of the draft model is typically smaller than that of the base model, leading to GPU idling during the drafting stage. We observe that such inefficiency stems from the sequential execution of layers, which is seemingly natural but actually unnecessary. Therefore, we propose EasySpec, a layer-parallel speculation strategy that optimizes the efficiency of multi-GPU utilization. EasySpec breaks the inter-layer data dependencies in the draft model, enabling multiple layers to run simultaneously across multiple devices as ``fuzzy'' speculation. After each drafting-and-verification iteration, the draft model’s key-value cache is calibrated in a single forward pass, preventing long-term fuzzy-error accumulation at minimal additional latency. EasySpec is a training-free and plug-in method. We evaluated EasySpec on several mainstream open-source LLMs, using smaller versions of models from the same series as drafters. The results demonstrate that EasySpec can achieve a peak speedup of 4.17x compared to vanilla decoding, while preserving the original distributions of the base LLMs. Specifically, the drafting stage can be accelerated by up to 1.62x with a maximum speculation accuracy drop of only 7\%. The code is available at https://github.com/Yize-Wu/EasySpec.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将使用中文、以Markdown形式，对该论文进行结构化、深入、客观的总结。

### 1. 核心问题与研究背景

*   **研究问题**：现有的推测解码（Speculative Decoding）方法在多GPU系统中，利用张量并行（Tensor Parallelism, TP）加速大模型（Base Model）推理时，存在严重的GPU资源浪费问题。
*   **问题背景**：
    *   推测解码使用一个小模型（Draft Model）串行生成“草稿”令牌序列，再由大模型并行验证，以实现无损加速。
    *   在多GPU系统中，大模型和小模型的最优张量并行度（TP Size）不同。大模型适合用多个GPU进行张量并行加速，而小模型因计算量小、通信开销大，往往在单个GPU上运行最快。
    *   这导致了在小模型的“草稿”阶段，分配给大模型的其他GPU处于空闲状态，整体硬件利用率低下。
*   **根本原因**：论文将上述空等问题的根本原因归结为小模型内部的“层间数据依赖性”，即必须前一层计算完毕，后一层才能开始，这种严格的串行执行阻碍了跨GPU的并行。

### 2. 核心方法论

论文的核心思想是打破草稿模型内部的层间串行依赖，提出了一种名为**EasySpec**的层并行推测策略，包含两个关键技术：模糊推测（Fuzzy Speculation）和奖励校准（Bonus Calibration）。

*   **核心思想与“模糊推测”（Fuzzy Speculation）**
    *   **动机**：草稿模型的输出不需要绝对精确，因为它仅用于生成候选序列，最终结果由验证阶段的大模型保证。因此，可以用一种“模糊”但更快的方式执行草稿模型。
    *   **具体操作**：打破传统Transformer中层与层的顺序依赖。具体来说，对于一组连续的注意力（Attention）层，它们不再等待上一层的输出作为输入，而是**都使用同一份最早的隐藏状态 `h1` 作为输入**，并行计算。如下图所示，原本串行的 `Attn1(h1) -> Attn2(h2)...` 被改为 `Attn1(h1), Attn2(h1)...` 同时进行。
        
        > Figure 1（示意）: 传统推测解码（左）中，草稿模型的N层是顺序执行的。EasySpec（右）中，多个注意力层以同一个底层输出作为输入并行执行（模糊推测），之后再通过一次顺序前向传递进行KV缓存的奖励校准。

    *   **可行性基础**：论文观察到，相邻层的隐藏状态 `hi` 和 `hi+1` 具有极高的余弦相似度。因此，用 `h1` 近似 `hi` 作为所有注意力层的输入是可行的。
    *   **并行策略**：将草稿模型的中间层（排除对误差更敏感的第一层和最后一层）分组，每组包含N个注意力层，组内层并行执行。MLP层仍保持顺序执行。
*   **“奖励校准”（Bonus Calibration）**
    *   **动机**：模糊推测会引入近似误差，尤其是草稿模型的KV缓存（Key-Value Cache）误差会随着生成过程逐步累积，严重降低推测准确率。
    *   **具体操作**：在每一轮“草稿-验证”迭代开始时，利用上一轮验证阶段产生的“奖励令牌”（Bonus Token），执行一次高效的校准。
        1.  **丢弃**：完全丢弃上一轮草稿阶段产生的所有“模糊”的KV缓存项。
        2.  **重建**：将上一轮被验证通过的令牌序列和奖励令牌拼接，进行一次**标准的顺序前向传递**，在草稿模型中重建出精确的KV缓存。
    *   **效率保证**：此校准步骤利用了令牌级并行（Token-Level Parallelism），类似于验证阶段。一次处理多个令牌的延迟，几乎等同于处理单个令牌的延迟，因此额外开销极小，但能有效阻止误差累积，大幅提升接受率。

### 3. 实验设计

*   **基准模型与草稿模型**：
    *   **基础模型**：Llama-3-70B-Instruct, Qwen2-72B-Instruct, Llama-3.3-70B-Instruct。
    *   **任务特定模型**：Qwen2-Math-72B-Instruct, Qwen2.5-Coder-32B-Instruct。
    *   **草稿模型**：使用同系列的小版本模型，如Llama-3-8B, Qwen2-7B, Llama-3.2-1B等。
*   **评估基准（Benchmarks）**：使用了覆盖多种任务的基准数据集进行评测：
    *   MMLU（语言理解）
    *   HumanEval（代码生成）
    *   MATH（数学推理）
    *   IFEval（指令遵循）
    *   MGSM（多语言数学）
    *   Spec-Bench（推测解码性能专项基准，用于对比EAGLE-2）
*   **对比方法**：
    *   **Vanilla Decoding**：纯串行解码（基础）。
    *   **TP**：仅使用张量并行。
    *   **\+SD (Speculative Decoding)**：张量并行 + 标准推测解码。
    *   **\+Tree**：在`+SD`基础上加入树形注意力（Tree Attention）机制。
    *   **EAGLE-2**：一种需要训练的、使用极浅层草稿模型的推测解码方法。
*   **评估指标**：
    *   **吞吐量（Token Throughput）**：单批次推理的令牌生成速度，核心性能指标。
    *   **分阶段耗时**：分别测量草稿阶段和验证阶段的耗时。
    *   **接受率（Acceptance Rate, α）**：草稿令牌被大模型接受的比率，衡量推测准确度。

### 4. 资源与算力

*   **硬件平台**：所有实验均在 **8 × NVIDIA A100 GPU** 的服务器上进行。
*   **软件配置**：论文未提及具体的CUDA或深度学习框架版本，但提到了与vLLM推理引擎的结果进行交叉验证。
*   **训练需求**：论文强调EasySpec是**无需训练（training-free）的即插即用方法**，因此没有额外的训练算力开销。

### 5. 实验充分性

*   **实验数量**：论文进行了非常详尽的实验，包括：
    *   **多模型/多任务评测**：在至少3个主流通用模型、2个任务特定模型、5个数据集上进行了性能测试。
    *   **不同温度系数测试**：分别在Temperature=0和0.8的设置下评估，证实其稳定性。
    *   **多草稿模型组合**：测试了多种不同规格的草稿模型和大模型的组合。
    *   **消融研究（Ablation Study）**：系统地分析了“树宽度”、“层并行尺寸(N)”、“是否使用奖励校准”这三个关键组件对吞吐量和接受率的影响。
    *   **与其他方法对比**：将EasySpec与另一高水平的、需要训练的推测解码方法EAGLE-2在Spec-Bench上进行对比，并从性能和方差角度分析了其泛化优势。
*   **公平客观性**：全文对比设置清晰，基准线选择合理（从Vanilla到+SD、+Tree）。还通过对比EasySpec（使用训练好的同系小模型）和EAGLE-2（训练一个极浅模型）展示其免训练和强泛化的优势，实验维度上非常公平。

### 6. 主要结论与发现

*   **显著加速**：EasySpec在各种模型和数据集上均能实现远超基准的推理加速。相比基础的张量并行解码，**最高可实现4.17倍加速**。
*   **有效解决瓶颈**：通过对草稿阶段的加速，最高可将**草稿阶段耗时降低1.62倍**，有效解决了该阶段成为多GPU系统新瓶颈的问题。
*   **高精度保持**：层并行（模糊推测）带来的**推测准确率下降不超过7%**，且“奖励校准”是维持高接受率的关键，实现了推理速度与准确率的良好平衡。
*   **强泛化能力**：作为一种免训练方法，EasySpec的表现稳定。在与需要训练的EAGLE-2的对比中，展现出更低的性能方差，尤其在跨模型泛化时优势巨大，证明了使用同系列小模型作为草稿器的可行性与高效性。

### 7. 优点与亮点

*   **新颖性**：首次提出从打破层间依赖的角度解决多GPU推测解码的利用率问题，视角独特。
*   **即插即用\&无需训练**：这是极大的优势，无需任何额外的训练或微调，可直接应用于任何已有的同系列模型。这降低了部署门槛，提高了实用性。
*   **理论与工程的巧妙结合**：利用隐藏状态的高余弦相似度这一理论观察，设计了高效的“模糊推测”；又在不增加显著延迟的前提下，利用令牌并行设计了“奖励校准”，工程实现精巧。
*   **详尽的实验验证**：实验覆盖模型广、任务多，并包含充分的消融实验，对方法的各个设计点进行了清晰论证。

### 8. 不足与局限

*   **硬件平台局限性**：所有实验基于8×A100 GPU。虽然论文作者认为在更快硬件上问题会更突出，但不同GPU架构（如H100）上的通信特性可能不同，其最优配置和加速比可能会有变化。
*   **层并行策略固定**：当前的层并行策略（如排除首尾层、固定分组大小N=4）是基于经验的手工规则。虽然有效，但是否对不同模型和任务是最优的，尚存疑问。论文也承认可能存在更优策略。
*   **草稿模型依赖**：该方法依赖于同一系列中存在合适的、更小的模型版本。如果某个模型系列没有小模型，EasySpec的直接应用会受限。
*   **理论分析深度不足**：论文对为什么“层并行”作用于注意力层而不是MLP层，以及为什么首尾层更敏感，仅给出了经验解释和现象观察，缺乏更深入的理论分析。

（完）
