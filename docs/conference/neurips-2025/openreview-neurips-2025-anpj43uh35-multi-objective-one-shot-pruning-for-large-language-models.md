---
title: Multi-Objective One-Shot Pruning for Large Language Models
title_zh: 面向大语言模型的多目标一次性剪枝
authors: "Weiyu Chen, Hansi Yang, Yunhao GOU, Han Shi, En-Liang Hu, Zhenguo Li, James Kwok"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=aNpj43Uh35"
tags: ["query:edge-llm"]
score: 10.0
evidence: 一次性剪枝用于资源受限环境下的LLM部署
tldr: 提出多目标一次性剪枝方法MOSP，将LLM剪枝建模为多目标优化问题，无需重训练即可生成帕累托最优压缩模型，支持用户根据偏好选择不同能力权衡的模型，有效解决资源受限环境下的部署挑战。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1436, \"height\": 756, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 707, \"height\": 699, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 684, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 686, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1425, \"height\": 1016, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1427, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 718, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1141, \"height\": 818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1136, \"height\": 813, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1141, \"height\": 821, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1136, \"height\": 816, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1142, \"height\": 817, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1137, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-anpj43uh35/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1142, \"height\": 818, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-anpj43uh35/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 833, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-anpj43uh35/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 557, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-anpj43uh35/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 667, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-anpj43uh35/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1333, \"height\": 568, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-anpj43uh35/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1162, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-anpj43uh35/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 943, \"height\": 436, \"label\": \"Table\"}]"
motivation: 大语言模型计算资源需求大，限制其在资源受限环境中的部署。
method: 将LLM剪枝形式化为多目标优化问题，生成不同能力权衡的帕累托最优剪枝模型。
result: 实验表明，MOSP能高效生成满足多种偏好的剪枝模型，实现不同目标间的平衡。
conclusion: 该方法为LLM在资源受限设备上的灵活部署提供了有效的压缩解决方案。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable capabilities across various tasks but require substantial computational resources, limiting their deployment in resource-constrained environments. While one-shot pruning methods can reduce model size without expensive retraining, they typically optimize for single objectives, ignoring LLMs' multi-faceted applications. We introduce Multi-Objective One-Shot Pruning (MOSP), which formulates LLM pruning as a multi-objective optimization problem. MOSP efficiently generates a Pareto set of pruned models representing different capability trade-offs, allowing users to select solutions aligned with their preferences. The proposed approach identifies share core support while enabling specialized support. Experiments across various LLMs and sparsity levels demonstrate MOSP's superior performance in navigating multi-objective trade-offs compared to baseline methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）在文本理解、数学推理、代码生成等多类任务上表现出色，但其巨大的参数量对算力和内存的需求使得资源受限环境下的部署成为难题。
- **现有方法局限**：当前主流的一次性剪枝方法（如SparseGPT、Wanda、ALPS）通常仅针对单一目标（单一校准数据集）进行压缩，产生一个固定的稀疏模型，忽视了用户对不同任务能力的多样化偏好。
- **核心问题**：如何在**不进行昂贵重训练**的前提下，**一次性**生成一组能够灵活权衡**多个目标性能**（如通用文本、数学、代码）的剪枝模型，使用户可根据自己的偏好选择最适合的压缩模型。

### 2. 论文提出的方法论

论文提出 **MOSP（Multi-Objective One-Shot Pruning）**，将LLM剪枝形式化为多目标优化问题，生成一组帕累托最优的剪枝模型。MOSP包含三个阶段，其核心思想是通过**分离共享知识（核心支撑集）与任务特定知识**，实现高效生成不同偏好下的子模型。

#### 阶段1：双ADMM识别核心支撑（Dual ADMM for Core Support Identification）
- 将多个标定任务的激活矩阵拼接为 \(\tilde{\mathbf{X}}\)，构建一个**双层优化问题**：
  - **外层**：优化核心支撑 \(W_c\)（稀疏度为总预算的 \(\alpha\) 比例），要求其支撑集是内层支撑 \(W\) 的子集。
  - **内层**：优化全局支撑 \(W\)（总稀疏度 \(k\)）。
- 采用**交替方向乘子法（ADMM）**同时求解内外层问题，更新 \(W\), \(D\), \(V\) 以及 \(W_c\), \(D_c\), \(V_c\)。
- 关键步骤：
  - \(W\) 和 \(W_c\) 的更新均通过 \((\mathbf{H}+\rho\mathbf{I})^{-1}\) 计算（利用特征分解预计算）。
  - 核心支撑投影 \(D_c\) 限制在 \(W\) 的支撑内选取最显著的 \(\alpha k\) 个权重。
- 论文提供了该双ADMM算法的收敛性证明，保证序列收敛。

#### 阶段2：任务特定ADMM（Task-Specific ADMM）
- 对每个任务 \(i\)，固定核心支撑 \(S_c\)，求解约束问题：
  \[
  \min_{\mathbf{W}_i} \|\mathbf{X}^{(i)}\hat{\mathbf{W}} - \mathbf{X}\mathbf{W}_i\|^2_F + \gamma\|\hat{\mathbf{W}} - \mathbf{W}_i\|^2_F \quad \text{s.t.} \|\mathbf{W}_i\|_0 \le k,\; \mathrm{Supp}(\mathbf{W}_c) \subset \mathrm{Supp}(\mathbf{W}_i)
  \]
  其中初始化使用阶段1得到的 \(W\)。
- 使用固定 \(\rho\) 的ADMM，预计算Cholesky分解加速迭代（最多10次迭代）。

#### 阶段3：精炼（Refinement）
- 利用预条件共轭梯度（PCG）进一步优化每个任务模型在对应支撑集上的权重值。

#### 推理阶段（Inference）
- 给定用户偏好向量 \(\boldsymbol{\lambda}\)，通过一个映射 \(\boldsymbol{\lambda} \to \boldsymbol{\lambda}'\)（带温度参数 \(p\)）来调整任务特定修正项的影响：
  \[
  \mathbf{W}_{\boldsymbol{\lambda}} = P_{k, S_c}\left( \mathbf{W} + \sum_{i=1}^m \lambda'_i (\mathbf{W}_i - \mathbf{W}) \right)
  \]
  最后投影保证稀疏度和核心支撑的完整性，实现即时的模型定制。

- **半结构化稀疏扩展**：通过修改投影步为 \(N:M\) 形式（块内保留 \(N\) 个最大元素），并调整核心支撑识别策略，MOSP同样能处理2:4等半结构化稀疏。

### 3. 实验设计

- **数据集/场景**：
  - **通用文本**：C4（WikiText校准，测试集困惑度）。
  - **数学推理**：GSM8K。
  - **代码生成**：Code（Python代码指令数据集）。
- **评估指标**：各任务测试集上的困惑度（PPL），以及多目标优化中的**超体积（Hypervolume）**。
- **被剪枝模型**：Llama-2（7B, 13B）、Llama-3（8B）、OPT（1.3B, 2.7B, 30B）。
- **稀疏度设置**：50%、60%、70%、80% 非结构化稀疏，以及2:4半结构化稀疏。
- **对比基线**：
  - 幅度剪枝（MP）、Wanda、SparseGPT、ALPS。
  - 基线方法使用激活拼接策略（Extension 1）作为公平比较。
  - 简单多目标扩展（独立剪枝再合并）因效果极差仅作讨论。

### 4. 资源与算力

- **硬件配置**：实验使用8 NVIDIA A6000 GPU的服务器（单次实验仅用一块GPU）。
- **运行时间**：以Llama-2-7B 70%稀疏度为例，ALPS耗时1.09h，MOSP耗时1.36h，GPU内存开销从18.7GB增至20.3GB，开销很小。
- 文中未报告所有实验的精确总GPU时，但指出复现全部实验约需100小时。

### 5. 实验数量与充分性

- **实验组数**：涵盖两大主要场景（二目标、三目标）、多种模型家族、4种稀疏度 + 一个半结构化设置，且包含消融实验。
- **消融研究**：
  - 核心共享参数 \(\alpha\) 的影响（0, 0.5, 1.0）。
  - 偏好转换映射的作用（有无变换）。
- **公平性**：
  - 所有方法使用相同的校准数据（128片段，最多2048 token）。
  - 基线方法统一使用激活拼接策略。
  - 超体积对比使用与SparseGPT性能挂钩的参考点，确保对比的公平。
- **定量指标**：超体积（HV）对比反映多样性与性能的平衡，MOSP在绝大多数设置下显著优于ALPS、SparseGPT等。
- 实验覆盖较为全面，验证了方法的普适性和有效性。

### 6. 论文的主要结论与发现

- MOSP成功将LLM一次性剪枝框架化为多目标优化问题，能生成反映不同任务能力权衡的帕累托前沿。
- 通过分离核心支撑和任务特定支撑，MOSP既保持了共享知识，又允许定制化，且计算/存储开销适中。
- 在二目标和三目标场景下，MOSP生成的多样化模型库在超体积指标上一致超越所有单模型基线，展现出更好的“性能-多样性”平衡。
- 消融实验表明，适中的核心支撑比例（\(\alpha=0.5\)）和应用偏好映射能有效提升中间偏好模型的性能。

### 7. 优点

- **新颖性**：首次将LLM剪枝建模为多目标优化，并提出实际可行的单次压缩方案。
- **高效性**：一次运行生成多个偏好模型，推理时仅需简单加权和投影，无需单独重训练或存储大量独立模型。
- **理论保证**：双ADMM算法提供了收敛性证明，增强了方法的可靠性。
- **扩展性**：方法自然兼容非结构化和半结构化稀疏。
- **开源细节充分**：提供了详细的超参数、计算成本和推导过程。

### 8. 不足与局限

- **实验广度局限**：仅在几个主流模型系列上测试，未涵盖更多新兴LLM架构或更大模型。
- **目标数量有限**：目前最多展示了四个目标（附录补充），但现实应用可能涉及更多维度，大规模目标下的效率未验证。
- **无误差条与统计显著性**：受资源限制未报告多次运行的均值和方差，结论的统计稳定性有待加强。
- **下游任务评估欠缺**：评估指标主要是困惑度，未在更复杂的下游任务（如准确率、BLEU等）上验证，可能无法完全反映真实可用性。
- **固定参数敏感性**：参数 \(p\) 和 \(\alpha\) 固定为0.5，未进行调优说明，可能并非所有场景最优。
- **延迟推理问题**：当用户偏好切换时，需要重新组合加权模型并投影，虽然快速，但在频繁切换下可能引入少许延迟。

（完）
