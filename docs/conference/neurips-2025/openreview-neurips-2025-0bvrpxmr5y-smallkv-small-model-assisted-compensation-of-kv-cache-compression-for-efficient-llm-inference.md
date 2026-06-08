---
title: "SmallKV: Small Model Assisted Compensation of KV Cache Compression for Efficient LLM Inference"
title_zh: SmallKV：小模型辅助的KV缓存压缩补偿以实现高效LLM推理
authors: "Yi Zhao, Yajuan Peng, Nguyen Cam-Tu, Zuchao Li, Wang Xiaoliang, hai zhao, Xiaoming Fu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=0BVrpXMr5Y"
tags: ["query:edge-llm"]
score: 9.0
evidence: 小模型辅助的KV缓存压缩用于高效长上下文LLM推理
tldr: 提出SmallKV方法，利用小语言模型辅助补偿KV缓存淘汰中的显著信息偏移和边缘信息过压缩问题，通过两个补偿机制在长上下文场景下高效节省内存，适用于资源受限的LLM推理。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1427, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 825, \"height\": 364, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 627, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1436, \"height\": 951, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 496, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 491, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1038, \"height\": 882, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-0bvrpxmr5y/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1196, \"height\": 519, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1014, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 555, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1446, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1163, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1160, \"height\": 140, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1175, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1322, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-0bvrpxmr5y/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 842, \"height\": 137, \"label\": \"Table\"}]"
motivation: 现有KV缓存淘汰方法忽略解码中注意力模式的动态变化和边缘信息损失。
method: 基于不同规模LLM注意力矩阵的高相似性，设计两种补偿机制辅助KV缓存压缩。
result: 在长上下文任务中，内存消耗大幅降低，性能损失微小。
conclusion: 小模型辅助补偿是提升KV缓存压缩的有效方法。
---

## Abstract
KV cache eviction has emerged as an effective solution to alleviate resource constraints faced by LLMs in long-context scenarios. However, existing token-level eviction methods often overlook two critical aspects: (1) their irreversible eviction strategy fails to adapt to dynamic attention patterns during decoding (the saliency shift problem), and (2) they treat both marginally important tokens and truly unimportant tokens uniformly, despite the collective significance of marginal tokens to model performance (the marginal information over-compression problem). To address these issues, we design two compensation mechanisms based on the high similarity of attention matrices between LLMs with different scales. We propose SmallKV, a small model assisted compensation method for KV cache compression. SmallKV can maintain attention matching between different-scale LLMs to: 1) assist the larger model in perceiving globally important information of attention; and 2) use the smaller model’s attention scores to approximate those of marginal tokens in the larger model. Extensive experiments on benchmarks including GSM8K, BBH, MT-Bench, and LongBench demonstrate the effectiveness of SmallKV. Moreover, efficiency evaluations show that SmallKV achieves 1.75 - 2.56 times higher throughput than baseline methods, highlighting its potential for efficient and performant LLM inference in resource constrained environments.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型在长上下文推理时面临巨大的 GPU 显存和计算压力，主要瓶颈在于自注意力机制的 KV 缓存（Key-Value Cache）存储。
- **现存问题**：现有的 KV 缓存淘汰方法（如基于注意力分数永久删除不重要的 token）存在两个被忽视的核心缺陷：
    1.  **显著信息偏移问题**：解码过程中 token 的重要性会动态变化，一次性永久删除的策略无法适应这种变化，导致后续需要的重要信息丢失。
    2.  **边缘信息过度压缩问题**：现有方法只区分“关键 token”和“不重要 token”，忽视了“边缘 token”（注意力分数中等但集体贡献显著）的重要性，对其采取了与完全不重要 token 相同的粗暴淘汰策略，损害模型性能。
- **整体含义**：论文旨在提出一种新的 KV 缓存压缩方法，利用小语言模型辅助大模型进行推理，通过补偿机制同时解决上述两个问题，从而在极低缓存预算下仍保持高性能。

### 2. 论文提出的方法论

- **核心思想**：**小模型辅助补偿**。论文观察到同一系列、不同规模的 LLM 之间具有高度相似的注意力模式。基于此，引入一个参数量较小的 SLM（Small Language Model）与大模型协同推理，利用小模型的完整 KV 缓存和注意力分数来指导大模型的缓存淘汰与补偿。
- **关键技术细节**：
    - **相似性匹配**：在预填充阶段，将小模型和大模型的注意力矩阵按头计算 Jaccard 相似度，为每个大模型的注意力头匹配一个最相似的小模型注意力头。
    - **显著信息偏移补偿**：在大模型解码时，不再仅依赖自身被压缩后的缓存来选择重要 token，而是参考小模型保留的**全局完整缓存**，由小模型的注意力分数来决定大模型中哪些 token 应当被保留为“关键 token”，从而避免错删后续变得重要的 token。
    - **边缘信息补偿**：提出**分层压缩策略**，将 token 分为三类：
        - **关键 token**：保留完整 KV 缓存。
        - **边缘 token**：保留 V 缓存，但**丢弃 K 缓存**，使用小模型对应注意力头的注意力分数来近似其在大模型中的注意力权重，从而减少 K 缓存占用。
        - **不重要 token**：完全淘汰。
        公式表达：混合注意力输出 `O* = A* · V`，其中 `A*` 对于关键 token 取大模型注意力分数，对于边缘 token 取小模型注意力分数，其余置 0。
- **系统实现**：KV 缓存在 GPU HBM 和 CPU 内存之间迁移，迁移与模型前向计算并行；关键 token 的计算使用 Flash Attention 加速，边缘 token 补偿计算仅为矩阵乘法，两者并行执行；可与投机解码结合进一步加速。

### 3. 实验设计

- **数据集 / 场景**：覆盖四种典型任务场景：
    - 数学推理：GSM8K
    - 语言理解：BBH
    - 多轮对话：MT-Bench
    - 长上下文：LongBench
- **对比方法**：
    - **H2O**：基于累积注意力分数的动态缓存淘汰。
    - **PyramidInfer**：基于层冗余差异的分层缓存预算分配。
    - **Full Cache**：不使用压缩的原始基线。
- **模型组合**：在 Qwen 和 LLaMA 系列上进行跨规模测试，包括：
    - Qwen2-0.5B 辅助 Qwen2-7B
    - Qwen2.5-0.5B 辅助 Qwen2.5-14B
    - Qwen2-7B 辅助 Qwen2-72B
    - LLaMA 3.2-1B 辅助 LLaMA 3.1-8B
- **效率测试设置**：在单块 A100 上，采用两种场景（2048 长度高并发和 16384 长度长上下文），评估吞吐量、首 token 延迟等。

### 4. 资源与算力

- **硬件**：所有实验在 **8 块 NVIDIA A100 (80GB) GPU** 上进行。
- **软件**：CUDA 12.0, PyTorch 2.4.0, Transformers 4.45.1。
- **训练**：本文方法为**无关训练**的推理加速技术，不涉及训练过程。文中未提及任何训练时长或微调所需的算力。
- **效率实验**：单独在 1 块 A100 GPU 上评估。

### 5. 实验数量与充分性

- **实验组数丰富**：
    - 在不同缓存预算下（100% 到 5%）对 4 种模型组合进行了 GSM8K、BBH、MT-Bench 的性能测试。
    - 在 3 个不同缓存预算下（30%、10%、5%）进行了 LongBench 的 5 大类子任务测试。
    - 与两个主流基线方法进行了全面的吞吐量及延迟对比。
    - 进行了消融实验，验证“显著信息偏移补偿”和“边缘信息补偿”各自的贡献。
    - 测试了辅助 SLM 的规模对性能的影响（0.5B 至 7B）。
    - 在附录中分析了方法的内存、计算开销，并对 SLM 压缩等优化进行了定量讨论。
- **充分性与公平性**：实验设计考虑周全，覆盖了多个主流基准、模型系列、任务类型和缓存压缩率，证实了方法的通用性。对比基线具有代表性，评估指标包括任务精度和系统吞吐量，较为客观公平。消融实验清晰展示了两个补偿机制各自的作用。

### 6. 论文的主要结论与发现

- SmallKV 在所有测试基准和模型上，几乎在所有缓存预算（尤其是低至 5%~10%）下，性能都**显著优于** H2O 和 PyramidInfer，且在多数情况下非常接近全量缓存的效果。
- 引入辅助小模型虽然增加了部分计算开销，但由于兼容 Flash Attention 等高效注意力实现，以及分层压缩减少了大模型 K 缓存加载，最终端到端吞吐量可达基线方法的 **1.75 到 2.56 倍**。
- 消融实验证明，“边缘信息补偿”对中等缓存预算下的性能提升至关重要，“显著信息偏移补偿”进一步提升了整体性能。
- 辅助小模型的规模越大，补偿效果越好，尤其在极低缓存预算下扩大 SLM 规模收益明显，但需权衡资源开销。

### 7. 优点

- **问题洞察深刻**：明确指出了“显著信息偏移”和“边缘信息过压缩”两个以往被忽略的关键问题，并用实验量化了它们的影响。
- **方法论创新新颖且合理**：利用同系列模型间的注意力相似性进行跨模型协作补偿，将 KV 缓存管理从“淘汰”提升为“分层压缩与补偿”，思路巧妙。
- **具备实践兼容性**：方法支持 Flash Attention，可与投机解码等主流技术无缝结合，给出的系统架构和开销分析（附录）非常务实。
- **实验充分全面**：在多个模型系列、多种任务和极端缓存预算下都进行了验证，有效展示了方法的鲁棒性和通用性。

### 8. 不足与局限

- **依赖同系列模型**：方法严重依赖 LLM 与 SLM 之间的注意力高相似性，这主要在**同系列模型**（如 Qwen2 家族）上成立。对于跨系列模型，相似性显著降低（论文附录中给出跨系列相似度仅 0.69 左右），限制了其通用性。
- **无理论证明**：虽然通过实验观察和公式推导说明了注意力相似性及补偿的合理性，但缺乏严格的数学理论证明来保证相似性的普遍存在和补偿的无损性。
- **额外资源开销**：独立部署时，辅助小模型本身会带来额外的显存和计算成本。论文虽提出了与投机解码共用、压缩 SLM 缓存等优化策略，但在未结合投机解码的场景下，额外开销不可完全忽视。
- **边缘 token 补偿逼近质量依赖小模型质量**：边缘 token 的注意力权重完全由小模型决定，若小模型在该特定位置注意力偏差较大，可能会导致误差传递。论文的实验结果虽好，但缺乏对补偿误差分布的直接分析。

（完）
