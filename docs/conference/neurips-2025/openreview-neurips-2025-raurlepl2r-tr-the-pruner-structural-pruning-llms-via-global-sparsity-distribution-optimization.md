---
title: "Týr-the-Pruner: Structural Pruning LLMs via Global Sparsity Distribution Optimization"
title_zh: Týr-the-Pruner：通过全局稀疏分布优化实现LLM结构化剪枝
authors: "Guanchen Li, Yixing Xu, Zeping Li, Ji Liu, Xuanwu Yin, Dong Li, Emad Barsoum"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=rAuRLePL2R"
tags: ["query:edge-llm"]
score: 9.0
evidence: 端到端全局结构化剪枝实现硬件无关的LLM推理效率
tldr: 该论文针对结构化剪枝局部优化忽视全局依赖的问题，提出端到端搜索式全局结构化剪枝框架Týr-the-Pruner。通过构建超级网络并全局优化稀疏度分布，实现了性能保持的高效压缩模型。该方法硬件无关，可广泛应用于LLM的推理加速与边缘部署。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-raurlepl2r/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1464, \"height\": 678, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-raurlepl2r/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 846, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-raurlepl2r/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 689, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-raurlepl2r/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1457, \"height\": 841, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-raurlepl2r/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1451, \"height\": 928, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-raurlepl2r/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1446, \"height\": 445, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1442, \"height\": 1237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 482, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 752, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 668, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 684, \"height\": 175, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1444, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1447, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 730, \"height\": 158, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 957, \"height\": 805, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1447, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 867, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 691, \"height\": 1079, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 692, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 692, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 695, \"height\": 1076, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 693, \"height\": 1076, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 694, \"height\": 1076, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 695, \"height\": 1074, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-raurlepl2r/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 696, \"height\": 1074, \"label\": \"Table\"}]"
motivation: 现有结构化剪枝方法常忽略结构间依赖，无法实现端到端优化。
method: 构建超级网络，通过重复局部剪枝并进行全局搜索优化稀疏分布。
result: 获得的高效压缩模型在推理效率上显著提升，且性能保持。
conclusion: 全局搜索式剪枝框架实现了更优的模型压缩，为LLM边缘部署铺平道路。
---

## Abstract
Structural pruning enhances hardware-agnostic inference efficiency for large language models (LLMs) yet often fails to maintain comparable performance. Local pruning performs efficient layer-by-layer compression but ignores global topology. Although global pruning aims to identify an optimal sparse model, intuitive methods typically adopt a two-stage paradigm that first evaluates substructure saliency and then applies global pruning, which ignores inter-structure dependencies and fails to achieve end-to-end optimization. To address these limitations, we propose Týr-the-Pruner, an efficient end-to-end search-based global structural pruning framework. This framework constructs a supernet by repeatedly applying local pruning across a range of sparsity ratios to each layer in an LLM, with the core goal of determining the optimal sparsity distribution under a target overall sparsity ratio. Concretely, we introduce an effective local pruning and an expectation error accumulation approach to improve supernet construction. Furthermore, we employ an iterative prune-and-search strategy with coarse-to-fine sparsity granularity to ensure efficient search convergence. Experimental results show that Týr-the-Pruner achieves state-of-the-art structural pruning, retaining 97% of the dense model's performance while removing a challenging 50% of Llama-3.1-70B's parameters.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：大型语言模型（LLM）的部署受计算与存储资源限制，结构化剪枝是实现硬件无关推理加速的关键手段。然而，目前的局部剪枝方法（逐层独立压缩）忽略了模型全局拓扑结构，而多数全局剪枝方法采用“先评估子结构重要性、再全局排序”的两阶段范式，未能建模结构间依赖，无法实现端到端优化。
- **核心问题**：如何在对 LLM 进行结构化剪枝时，既能高效地实现全局稀疏分配，又能通过端到端的方式保持模型性能，避免局部最优与全局偏差。
- **整体含义**：论文提出 **Týr‑the‑Pruner** 框架，将剪枝视为一个全局超网搜索问题，通过构建包含不同稀疏子结构的超网络，并利用进化搜索找到满足整体稀疏目标的最优逐层分布，在激进剪枝下仍能保持极高性能。

### 2. 方法论
- **超网构建**：对 LLM 的每一层，在不同的稀疏比例（如 12.5% 间隔）下重复执行局部剪枝，生成多个不同稀疏程度的子结构，组合形成超网。
- **有效局部剪枝**：
  - 利用 **泰勒展开** 同时考虑一阶梯度与二阶 Hessian 信息，识别冗余注意力头或 FFN 神经元。
  - 被剪通道的选择公式：  
    \( p = \arg \min_{W_{p,:}} \left( G_{p,:} W_{p,:}^\top + \frac{\|W_{p,:}\|^2}{2 [H^{-1}]_{p,p}} \right) \)
  - 剩余权重的补偿更新：\( \delta W_{\sim p,:} = - H_{\sim p,\sim p}^{-1} G_{\sim p,:} \)，并通过 Sherman‑Morrison‑Woodbury 公式在 \(O(d_{in}^2)\) 复杂度下高效更新 Hessian 逆。
  - 渐进式剪枝，逐步移除一个注意力头或 16 个 FFN 神经元，保证精度。
- **期望误差累积**：超网中同一层可能存在多个稀疏子结构，为避免误差传播路径模糊，采用加权平均输出作为下一层的输入：
  \[
  \bar{X}_{\ell+1} = \sum_{e=1}^{E} \frac{1 - S_e}{\sum_{e'}(1 - S_{e'})} X_{\ell+1,e}
  \]
  权重由各子结构稀疏度决定，使浅层剪枝的误差能被深层子结构合理感知。
- **进化搜索与迭代 refine**：
  - 以 **蒸馏启发式度量** 作为目标：最小化各层激活差异与 logits KL 散度的加权和，引导搜索使子网络行为对齐密集模型。
  - 采用 **进化搜索**：通过层间稀疏度随机偏移（变异）生成候选分布，经多层验证（2K→16K→128K tokens）筛选最优后代。
  - **迭代式剪枝‑搜索**：初始以较大稀疏间隔（12.5%）构建超网并搜索出粗粒度分布；之后每次将间隔减半，在上一轮最优解附近构建更精细的超网，继续搜索，直至达到设定粒度（如 1.5625%）。这一策略将搜索空间从 \(10^{145}\) 级别降低到每轮约 \(10^{76}\)，实现快速收敛。
- **算法流程**：`local_pruning` 执行局部剪枝；`prune_to_supernet` 构建超网并累积误差；`evolutionary_search` 在超网上搜索；`Týr-the-Pruner` 迭代协调上述过程。

### 3. 实验设计
- **数据集与场景**：
  - 校准数据：来自 FineWeb‑Edu 的约 4M tokens（约 1k 条、长度上限 4k 的样本）。
  - 评估：语言理解困惑度（WikiText2 测试集），下游任务 0‑shot 准确率（ARC‑C, ARC‑E, BoolQ, HellaSwag, OpenBookQA, RTE, WinoGrande）及 5‑shot MMLU。
- **模型与剪枝目标**：Llama‑2（7B, 13B, 70B）、Llama‑3.x（3‑8B, 70B）、Mistral（7B‑v0.3, Nemo）。剪枝对象为注意力头和 FFN 中间神经元，非均匀层间稀疏度。
- **对比方法**：ShortGPT, LaCO+, SliceGPT, Wanda‑SP, LLM‑Pruner, ZipLM, OSSCAR, FLAP 等众多 SOTA 结构化剪枝方法。
- **消融实验**：
  - 局部剪枝设计（有无 Hessian/梯度、是否渐进、不同校准数据）。
  - 误差累积策略（无累积、随机累积、均匀累积 vs 期望累积）。
  - 搜索方向（单任务困惑度 vs 相似性度量）。
  - Týr‑the‑Pruner 迭代次数 vs 单纯细粒度搜索。
- **与其他压缩技术的兼容性**：在 50% 剪枝的 Llama‑3.1‑8B 上叠加量化（AWQ, SmoothQuant, FP8）和非结构化稀疏（SparseGPT, ALPS）。
- **效率分析**：端到端推理加速（TTFT、解码吞吐），以及超网的内存/存储开销。

### 4. 资源与算力
- **硬件**：实验采用 4 块 **AMD Instinct™ MI250 (64 GB)** 加速器；7‑13B 参数模型可在单块加速器上运行。
- **训练/校准**：无需反向传播训练，仅使用校准数据进行一次性剪枝与搜索；搜索分 4 次迭代，每次 50 代、每代 128 个候选，但整个过程在数小时级别完成（论文提及单代耗时约 190 秒）。
- **存储**：超网子结构存储于磁盘，仅加载一个完整模型至 HBM，7‑8B 模型约需 14‑16 GB HBM，磁盘占用约 40 GB。

### 5. 实验数量与充分性
- **实验覆盖**：
  - 跨 7 种模型、4 种稀疏度（12.5%、25%、37.5%、50%），每种组合均与 8 种以上基线对比，生成了约 200 组以上的主要结果。
  - 在 70B 级模型上单独报告 50% 剪枝结果。
  - 详实的消融实验（表 4‑6）覆盖了局部剪枝组件、误差累积、搜索方向、迭代策略。
  - 统计显著性分析：部分结果提供了随机种子下的标准差（n=5）。
- **公平性与客观性**：所有基线方法均使用相同的 FineWeb‑Edu 校准数据复现，并在统一评估协议下比较。对比方法包括近期高水平工作，且部分基线性能因校准数据质量而优于原始报告，仍被公平呈现。

### 6. 主要结论与发现
- Týr‑the‑Pruner 在跨任务、跨模型尺寸的结构化剪枝中均获得 **SOTA 结果**。例如，Llama‑3.1‑8B 剪枝 37.5% 时，困惑度比 FLAP 低 3.45，下游平均准确率高 10.26%；剪枝 50% 时，Llama‑3.1‑70B 仍能保持 **97% 的密集模型平均精度**。
- 非均匀稀疏分布是提升剪枝潜力的关键，Týr‑the‑Pruner 能自动发现与模型特性匹配的层间分配，无需人工先验。
- 局部剪枝中同时使用一阶梯度与二阶 Hessian 信息，以及期望误差累积策略，是构建高质量超网的基础。
- 迭代粗到细的搜索比单纯一次细粒度搜索更高效，且最终精度更高。
- 该方法与量化、非结构化稀疏兼容，可实现多级压缩。

### 7. 优点
- **端到端全局优化**：将剪枝形式化为超网搜索，克服了传统两阶段方法的局部与全局偏差。
- **技术贡献清晰有效**：泰勒二阶局部剪枝与期望误差累积，使超网中多子结构协同训练成为可能。
- **搜索效率高**：迭代 prune‑and‑search 和进化搜索设计，在有限 token 和数据下快速收敛。
- **强实证表现**：大量模型和任务上超越现有方法，尤其在激进剪枝下仍能维持高泛化能力。
- **实用性**：硬件无关，支持单 GPU 处理 13B 模型，内存/存储开销可控，可与后续压缩兼容。

### 8. 不足与局限
- **搜索时间成本**：虽然较全局细粒度搜索大幅减少，但进化搜索的迭代过程依然耗时，文中未给出明确端到端总时长；搜索代价对于更大模型仍是挑战。
- **校准数据依赖性**：方法依赖高质量校准样本（FineWeb‑Edu），在校准数据极为稀缺或分布转移场景下，性能可能下降。
- **结构剪枝范围**：当前仅针对注意力头和 FFN 神经元，未探索嵌入维度、层数等多维度联合压缩。
- **未涉及训练后的恢复 fine‑tuning 深入分析**：虽然给出了 LoRA 微调后的初步结果，但未系统讨论不同微调策略对最终性能的影响。

（完）
