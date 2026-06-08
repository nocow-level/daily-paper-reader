---
title: Mixture of Lookup Experts
title_zh: 混合查找专家
authors: "Shibo Jie, Yehui Tang, Kai Han, Yitong Li, Duyu Tang, Zhi-Hong Deng, Yunhe Wang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=wUEp13rqXP"
tags: ["query:edge-llm"]
score: 9.0
evidence: 通过将专家重新参数化为查找表减少显存占用
tldr: 为解决混合专家模型（MoE）因需要加载全部专家导致的显存占用大和延迟高的问题，提出MoLE架构，在推理前将专家重新参数化为查找表，直接检索输出。该方法显著降低了通信和显存开销，使得大规模MoE模型能够在资源有限的设备上高效部署。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-wuep13rqxp/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 848, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wuep13rqxp/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1760, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wuep13rqxp/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 828, \"height\": 412, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1642, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1763, \"height\": 704, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1738, \"height\": 918, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1749, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1748, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1756, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1727, \"height\": 390, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1719, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wuep13rqxp/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 778, \"height\": 783, \"label\": \"Table\"}]"
motivation: MoE模型因需要加载全部专家导致显存占用大，卸载加载则增加延迟。
method: 提出MoLE，专家训练时为前馈网络，推理前重新参数化为查找表，实现低显存和低通信。
result: MoLE降低了通信和显存开销，实现了高效部署。
conclusion: MoLE为MoE模型在资源受限环境中的部署提供了新思路，显著提升效率。
---

## Abstract
Mixture-of-Experts (MoE) activates only a subset of experts during inference, allowing the model to maintain low inference FLOPs and latency even as the parameter count scales up. However, since MoE dynamically selects the experts, all the experts need to be loaded into VRAM. Their large parameter size still limits deployment, and offloading, which load experts into VRAM only when needed, significantly increase inference latency. To address this, we propose Mixture of Lookup Experts (MoLE), a new MoE architecture that is efficient in both communication and VRAM usage. In MoLE, the experts are Feed-Forward Networks (FFNs) during training, taking the output of the embedding layer as input. Before inference, these experts can be re-parameterized as lookup tables (LUTs) that retrieves expert outputs based on input ids, and offloaded to storage devices. Therefore, we do not need to perform expert computations during inference. Instead, we directly retrieve the expert's computation results based on input ids and load them into VRAM, and thus the resulting communication overhead is negligible. Experiments show that, with the same FLOPs and VRAM usage, MoLE achieves inference speeds comparable to dense models and significantly faster than MoE with experts offloading, while maintaining performance on par with MoE. Code: https://github.com/JieShibo/MoLE.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将以 Markdown 格式为您提供对该论文的结构化、深入、客观的总结。

### 1. 研究动机与核心问题

*   **核心问题**：混合专家模型（MoE）虽然通过稀疏激活专家保持了较低的计算量（FLOPs），但其庞大的总参数量导致推理时必须将**所有专家加载到显存（VRAM）中**，这对硬件部署构成了严峻挑战。
*   **现有方案的局限**：将专家参数卸载（Offloading）到CPU内存或硬盘等外部存储，并在需要时加载的方法，虽然节约了显存，但会引入巨大的**参数传输延迟**。此外，批处理场景下，不同样本可能激活不同专家，需加载的专家数量激增，进一步加剧了通信瓶颈和显存占用。
*   **研究动机**：本文旨在解决MoE模型在推理时的**显存占用与通信延迟**之间的矛盾，提出一种既能保持MoE性能优势，又能实现低显存、低延迟推理的新型架构。
*   **整体含义**：本文提出“混合查找专家”（MoLE），其核心思想是通过**改变专家输入来源**，使其在推理前能被重参数化为**零计算、可卸载的查找表（LUT）**，从而将专家计算转化为简单的查找操作，根本上消除了加载大量专家参数的需求。

### 2. 方法论：核心思想与关键技术细节

*   **核心思想**：将MoE中计算密集的专家模块（FFN），在推理阶段转变为计算无关的查找表。通过在训练阶段限制专家的输入为**离散、有限的嵌入token**，使得可以预计算所有可能输入与专家输出的映射，从而构建LUT。
*   **训练阶段**：
    *   **结构差异**：与常规MoE不同，MoLE层中的**路由专家（Routed Experts）的输入不是中间层特征，而是来自嵌入层的输出**（`e = Embedding(i)`）。共享专家（Shared Expert）仍以中间特征为输入。
    *   **全激活策略**：为解决因输入信息受限（无上下文信息）导致的性能损失，MoLE在训练时激活**所有**路由专家，以最大化模型容量。
    *   **公式化表示**：MoLE层的计算可表示为 `h' = Σ_{j=1}^N g_j * FFN_j(e) + FFN_shared(h) + h`，其中 `g_j` 是路由器的SoftMax输出，`e` 是嵌入token。
    *   **训练稳定性**：由于所有专家均被激活，模型是端到端可微的，无需像传统稀疏MoE那样为了防止负载不均或路由坍塌而引入额外的辅助损失（如负载均衡损失）。
*   **推理阶段**：
    *   **重参数化为LUT**：对于每个可能的输入token ID `i` 和每个路由专家 `FFN_j`，预先计算其输出向量 `v_{ij} = FFN_j(Embedding(i))`。所有层、所有专家、所有词汇的 `v_{ij}` 集合构成了LUT `{{ {v_{ij}}^N_{j=1} }}^{|V|}_{i=1}`。
    *   **计算流程**：推理时，MoLE层的计算变为 `h' = Σ_{j=1}^N g_j * v_{ij} + FFN_shared(h) + h`，即直接根据输入ID从LUT中**检索**专家输出，无需进行FFN计算。
    *   **卸载与通信**：体积庞大的LUT可以被整个卸载到外部存储（如CPU内存、硬盘）。每一步推理只需根据输入ID从LUT中检索出对应的 `N` 个输出向量（每个维度为 `d`，总计 `dN` 个参数）并加载进显存。这个通信量远小于加载原始专家参数（`2dNDr` 量级）。
*   **复杂度分析（查表1）**：MoLE的FLOPs与保持相同激活参数的稠密模型一致。关键优势在于，其每次推理需加载的参数数量（LoadParam）为 `dN`，仅为MoE专家卸载方案（最坏情况下 `2dkD_r`）的数百分之一甚至数千分之一。

### 3. 实验设计

*   **模型规模与架构**：在**160M、410M、1B**三个激活参数规模下进行实验，遵循Pythia的设置。比较了稠密模型（Dense）、不同专家数量组合的MoE（10E, 34E）和MoLE（4E, 16E）模型。为确保公平，所有模型在推理时具有相同的激活参数量，MoLE的FLOPs也与同等规模的稠密模型和MoE模型对齐。
*   **训练数据与Tokenizer**：所有模型使用从去重Pile数据集中抽取的**1000亿（100B）token**子集进行训练，使用与Pythia相同的GPT-NeoX tokenizer，词表大小约为50k。
*   **评估基准**：使用**lm-evaluation-harness**框架在多个零样本（zero-shot）下游任务上进行评估，包括：**ARC-C, ARC-E, BoolQ, HellaSwag, PIQA, RACE, SIQA, LAMBADA**。
*   **对比方法与设置**：
    *   **稠密模型**：不进行任何卸载。
    *   **MoE + 专家卸载**：将所有专家卸载，仅在需要时加载。显存中仅保留激活的专家和所有非专家参数。
    *   **MoLE + LUT卸载**：将重参数化的LUT卸载，其他参数保留在显存中。这两种卸载策略确保了比较时所有模型的显存占用等同于稠密模型。

### 4. 资源与算力

*   **训练细节**：论文未明确提及训练使用的GPU型号、数量及具体训练时长。只提供了超参数设置（学习率、批次大小、优化器等）和训练的Token数量（100B）。
*   **推理效率测试**：在**NVIDIA V100 GPU**上测量了410M激活参数模型的每步解码延迟，并使用最大PCIe带宽（16GB/s）来模拟参数加载延迟。

### 5. 实验数量与充分性

*   **实验数量**：论文包含了较为全面的实验，主要包括：
    *   **主要结果对比（表3）**：在3个模型规模、2种专家数量配置下，系统比较了Dense、MoE和MoLE在下游任务上的表现和效率，共约5组主要对比。
    *   **效率分析（图3）**：测量了不同批大小（1, 8, 32）下的解码延迟。
    *   **消融实验**：设计了多个消融实验来考察关键设计选择的影响。
        *   **训练损失（表4）**：对比仅用LM损失与加入MoE辅助损失的效果。
        *   **专家尺寸与数量（表5、表6）**：探索路由专家隐藏层维度（`Dr`）和专家个数（`N`）对性能的影响。
        *   **架构演进（表7）**：追踪了从MoE到MoLE关键步骤（全激活、重配置、嵌入输入、重参数化）的逐项性能变化。
        *   **后训练量化（表8）**：对LUT进行NF4、NF3量化以压缩体积。
*   **充分性与公平性**：实验设计充分且公平。
    *   **公平性**：严格控制了训练数据量、训练Token数、激活参数量和推理FLOPs，并在同等显存约束下进行比较。
    *   **充分性**：从性能、效率、设计选择等多个维度进行了验证。消融实验清晰地阐明了各设计成分的贡献，特别是解释了“以嵌入为输入”带来的性能损失能被“全激活”所带来的增益弥补。

### 6. 主要结论与发现

1.  **性能持平或更优**：在同等计算量和显存占用下，MoLE在下游任务上的平均准确率与MoE基本持平，甚至在多数对比组中略优于MoE，并显著优于稠密模型。
2.  **推理延迟极低**：MoLE的推理速度与稠密模型相当，并且显著快于使用专家卸载的MoE。在批处理增大时，MoE的延迟因加载专家数量增加而急剧上升，而MoLE的延迟几乎不变，展现了出色的Batch-generation友好性。
3.  **有效部署方案**：MoLE完美解决了MoE模型在显存受限场景下的部署难题。它通过将计算替换为查找，将庞大的参数卸载负担转化为微乎其微的通信开销（每次仅加载`dN`个参数），使得大参数模型在边缘设备或低层级存储上的高效运行成为可能。
4.  **设计选择验证**：消融实验表明，MoLE仅需标准的语言模型损失即可稳定训练；增加专家数量可以持续提升性能，展现了一定可扩展性；LUT可通过后量化进一步压缩而不显著损失精度。

### 7. 优点（亮点）

*   **范式创新**：提出了一种颠覆性的MoE推理范式，将“计算”转化为“查找”，从根本上解耦了专家参数规模与推理延迟，创意新颖且实用性强。
*   **解决核心矛盾**：精准地解决了MoE部署中显存占用、通信延迟和批处理扩展性这三大难题。
*   **部署友好**：其推理框架非常简单，无需复杂的缓存、预取或资源调度策略，即可实现高效推理。
*   **可扩展性**：LUT的大小虽然巨大但可卸载，其加载量微小且恒定，使其能够利用廉价的、大容量的存储设备，展现了良好的硬件可扩展性。
*   **实验严谨**：通过系统性的对比和消融实验，逻辑清晰地论证了从标准MoE演进到MoLE每一步的必要性与收益。

### 8. 不足与局限

*   **存储成本**：尽管推理时通信开销小，但生成的LUT体积庞大。虽然论文认为存储空间相对充裕，但在极端受限的环境下（如手机），LUT的存储仍可能是一个瓶颈。虽然初步探索了量化，但仍值得进一步研究。
*   **专家损失的上下文信息**：将专家输入限制为无上下文信息的嵌入token，虽然在论文中被“全激活”策略所弥补，但这在理论上限制了专家处理依赖上下文细微差别的任务的能力。这种设计在更复杂、更深层语言理解任务中的深度影响有待挖掘。
*   **训练与推理架构不一致**：模型在训练和推理时结构不同（FFN vs. LUT），这要求额外的重参数化步骤，引入了工程复杂性。
*   **缺乏大规模验证**：实验规模止步于1B激活参数，相较于当前工业界的7B、70B乃至更大参数模型，MoLE在大规模LLM上的效果和可扩展性仍有待验证。

（完）
