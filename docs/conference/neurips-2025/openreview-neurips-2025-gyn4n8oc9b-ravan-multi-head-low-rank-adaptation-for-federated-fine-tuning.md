---
title: "Ravan: Multi-Head Low-Rank Adaptation for Federated Fine-Tuning"
title_zh: Ravan：面向联邦微调的多头低秩适配
authors: "Arian Raje, Baris Askin, Divyansh Jhunjhunwala, Gauri Joshi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=gyn4n8oC9B"
tags: ["query:edge-llm"]
score: 7.0
evidence: 在边缘设备计算和通信受限条件下实现LLM的参数高效联邦微调
tldr: Ravan 解决联邦学习中边缘设备上LLM微调时的计算与数据异构问题，提出自适应多头低秩适配方法，通过重参数化权重更新在参数效率与模型表达力之间取得平衡，提升边缘端微调的精度，为隐私保护下的个性化部署提供支持。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1423, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1427, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1340, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1323, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1144, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1241, \"height\": 1923, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 618, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 623, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 621, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 621, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 622, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 623, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 621, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gyn4n8oc9b/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 621, \"height\": 412, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 593, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1454, \"height\": 537, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1452, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1448, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 671, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1387, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1449, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1448, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1446, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1446, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1446, \"height\": 348, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1187, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 793, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1377, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1376, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1379, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-gyn4n8oc9b/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1381, \"height\": 299, \"label\": \"Table\"}]"
motivation: 边缘数据未能被LLM有效利用，联邦微调面临精度下降与异构性挑战。
method: 提出 Ravan，一种自适应多头 LoRA 方法，重参数化权重更新以平衡效率与表达力。
result: 在异构联邦场景下，Ravan 提升了微调精度，超过现有 LoRA 变体。
conclusion: 为在边缘设备上高效、准确地微调 LLM 提供了新方案，推动隐私敏感的端侧智能。
---

## Abstract
Large Language Models (LLMs) have yet to effectively leverage the vast amounts of edge-device data, and Federated Learning (FL) offers a promising paradigm to collaboratively fine-tune LLMs without transferring private edge data to the cloud. To operate within the computational and communication constraints of edge devices, recent literature on federated fine-tuning of LLMs proposes the use of low-rank adaptation (LoRA) and similar parameter-efficient methods. However, LoRA-based methods suffer from accuracy degradation in FL settings, primarily because of data and computational heterogeneity across clients. We propose Ravan, an adaptive multi-head LoRA method that balances parameter efficiency and model expressivity by reparameterizing the weight updates as the sum of multiple LoRA heads, $s_i\textbf{B}_i\textbf{H}_i\textbf{A}_i$, in which only the $\textbf{H}_i$ parameters and their lightweight scaling factors $s_i$ are trained. These trainable scaling factors let the optimization focus on the most useful heads, recovering a higher-rank approximation of the full update without increasing the number of communicated parameters since clients upload $s_i\textbf{H}_i$ directly. Experiments on vision and language benchmarks show that Ravan improves test accuracy by 2–8\% over prior parameter-efficient baselines, making it a robust and scalable solution for federated fine-tuning of LLMs.

---

## 论文详细总结（自动生成）

好的，下面是对这篇论文的结构化总结。

### 1. 论文的核心问题与研究动机

*   **核心问题**：如何在边缘设备计算与通信资源受限、且数据分布高度异构的联邦学习（FL）场景下，对大型语言模型进行高效且高精度的微调。
*   **研究动机**：
    *   **边缘数据价值**：云端LLM未能有效利用海量的边缘设备私有数据。
    *   **隐私与效率需求**：联邦学习允许不共享原始数据而协作训练，但面临边缘设备的计算和通信瓶颈。
    *   **现有方法局限**：主流的参数高效微调（PEFT）方法 LoRA 虽然能降低开销，但在联邦场景下会因客户端数据异构性导致**精度显著下降**，因为它将模型更新限制在了低秩子空间内，无法捕捉异构数据带来的多样化、更高秩的更新。
    *   **异构性挑战**：联邦环境不仅存在数据异构，还存在客户端算力异构，现有方法难以同时优雅地处理这两类异构性问题。

### 2. 方法论：rava 方法

rava 的核心思想是**重参数化模型权重更新为多个增广式 LoRA 头的加权和**，以此来提升更新近似的“有效秩”，并同时解决数据异构和计算异构的问题。

*   **模型更新形式**：对于模型权重 \( W \)，其前向传播变为：
    \[
    W + \sum_{i=1}^{h} s_i B_i H_i A_i
    \]
    其中，\( B_i \) 和 \( A_i \) 是随机初始化后冻结的基矩阵，**仅有核心矩阵 \( H_i \) 和轻量缩放因子 \( s_i \) 是训练参数**。

*   **关键设计细节**：
    1.  **提升有效秩**：
        *   如使用 \( h \) 个结构为 \( B_i H_i A_i \) 的头，在同等可训练参数量 \( N \) 下，更新矩阵的总秩次理论上限为 \( \sqrt{Nh} \)，远高于标准 LoRA 的 \( \Theta(1) \)。
        *   通过初始化为相互正交或近似正交的 \( B_i \) 和 \( A_i \)，确保各头学习到的子空间相互独立，最大化整体近似矩阵的秩和表达能力，从而更好地拟合联邦场景中更高秩的全局更新。
    2.  **确保精确聚合**：由于客户端只上传可训练的 \( s_i H_i \) 乘积，服务器可直接对其求平均，数学上等同于聚合所有权重更新，完美解决了标准 LoRA 中分别平均 `B` 和 `A` 所带来的不精确性问题。
    3.  **应对计算异构**：算力较弱的客户端可以根据自身资源，通过头选择策略，仅选择一部分最重要的头进行微调，而冻结其余头。这避免了算力不足的设备掉队，同时不影响服务器端的精确聚合。

*   **算法流程**：
    1.  **初始化**：冻结所有 \( B_i, A_i \) (及原模型权重)，为每个头分别采用“随机正态”或“格拉姆-施密特”正交初始化，\( H_i \) 初始化为零，\( s_i \) 初始化为 1。
    2.  **客户端选择与广播**：服务端选择参与客户端，广播所有 \( H_i \)。
    3.  **本地训练**：每个客户端根据其算力预算，使用评分函数（如随机、基于权重范数或梯度范数）选择前 \( K_c \) 个最重要的头，仅对选中的 \( H_i \) 和 \( s_i \) 进行多轮本地训练。
    4.  **上传与聚合**：客户端将训练好的 \( s_i H_i \) 乘积上传至服务器，服务器对每个头 \( i \) 独立地、精确地聚合所有训练了该头的客户端上传的 \( s_i H_i \)，得到新一轮的全局 \( H_i \)。

### 3. 实验设计

*   **数据集与场景**：
    *   **视觉任务**：在 CIFAR-100 和 SVHN 数据集上微调 ViT-B/16 模型。
    *   **语言任务**：在 20 Newsgroups 和 MRQA 数据集上微调 T5-Base 模型；在 GLUE 基准上微调 LLaMA3.2-1B 模型。
    *   **数据异构模拟**：通过狄利克雷分布（\( \alpha=0.3 \)）划分数据集，构建 Non-I.I.D. 的联邦场景。
    *   **计算异构模拟**：从钟形、均匀、右偏三种分布中采样客户端的可训练参数预算。

*   **对比方法（Baselines）**：将 Ravan 与 FedIT, FedEx-LoRA, FFA-LoRA, Fed-SB, HetLoRA, FlexLoRA 等 SOTA 联邦 PEFT 方法进行了全面比较。

*   **评估指标**：图像分类准确率（%）和问答任务的 F1 分数（%）。

### 4. 资源与算力

*   **硬件**：所有实验均在配备 **单张 NVIDIA V100 32GB GPU** 和 256GB RAM 的SLURM集群上运行。
*   **训练时长**：
    *   ViT-B-16 视觉任务：每次实验约 1 GPU小时。
    *   T5-Base 在 20 Newsgroups上：约 2 GPU小时。
    *   T5-Base 在 MRQA 上：约 3 GPU小时。
    *   LLaMA3.2-1B 在 GLUE 上：每个子任务约 2 GPU小时。

### 5. 实验数量与充分性

*   **实验矩阵丰富**：实验覆盖了多个维度，包括 2 种视觉数据集、2 种语言数据集、一个大规模 GLUE 语言基准、20/50 客户端数量、I.I.D./Non-I.I.D. 两种数据分布、高低两种参数预算，以及多样的计算异构分布。
*   **消融研究全面**：对方法的关键组件进行了详细的消融实验，包括：
    *   **初始化方法**：比较了随机正态、格拉姆-施密特、常数、共享子空间四种初始化。
    *   **缩放因子**：验证了可训练的 \( s_i \) 相对于固定为 1 的优势。
    *   **头数量**：分析了头数 \( h \) 对性能的影响，并揭示了其理论上的最优边界。
    *   **计算异构选择策略**：对比了随机、权重、梯度三种头选择的评分函数。
*   **公平性与客观性**：实验设定严格，所有方法在相同硬件、批量大小、优化器设置下进行比较，并通过超参数网格搜索为每个基线选择最佳配置。结果均报告了 3 次随机种子的平均值，确保了客观性和可复现性。

### 6. 主要结论与发现

*   **性能显著提升**：在数据异构的联邦场景下，Ravan 的准确率一致性地且大幅度地超越现有 PEFT 基线。例如，在 CIFAR-100（50 Non-I.I.D. 客户端，低预算）上，比 FedIT 高出 **5.6%**，比 FedEx-LoRA 高出 **7.2%**。
*   **应对计算异构鲁棒**：在所有模拟的计算异构分布（尤其是极端右偏分布）中，Ravan 的性能下降远低于 HetLoRA 和 FlexLoRA 等基线，显示出极强的鲁棒性。
*   **正交初始化有效**：通过格拉姆-施密特方法初始化 \( B_i, A_i \) 使其子空间正交，能最大化有效秩，在视觉任务上带来显著的性能增益。
*   **缩放因子作用关键**：可训练的缩放因子 \( s_i \) 允许模型自适应的聚焦于最有用的 LoRA 头，对提升精度有稳定贡献。
*   **有效秩的理论验证**：实验证实，增加头数 \( h \) 带来的性能提升，仅在其理论有效秩 \( \sqrt{Nh} \) 不超过原始权重维度 \( d \) 时成立，符合理论预期。

### 7. 优点

*   **创新性的多参数化策略**：通过冻结基矩阵、仅训练核心小矩阵和缩放因子的方式，在不增加通信开销的前提下，显著提升了 LoRA 更新的有效秩和表达能力，是一种聪明的权衡策略。
*   **统一解决双重异构**：方法内在的设计同时优雅地解决了联邦学习中的数据异构（通过高秩表达）和计算异构（通过头选择与冻结）问题，而无需两个独立的处理模块。
*   **理论与实验紧密结合**：对有效秩的理论推导清晰直接，并通过实验验证了其边界条件，增强了方法的解释性。
*   **兼容性强**：精确聚合的特性使其能直接集成到标准的联邦平均（FedAvg）框架中，无需复杂的聚合算法改变。

### 8. 不足与局限

*   **跨层灵活性不足**：论文指出，当前框架要求模型**每一层**都选择相同数量的头进行微调，这降低了在面对计算异构时的灵活性。
*   **隐私保障待验证**：方法尚未在差分隐私（DP）等更强的隐私保护要求下进行测试和验证，其在该场景的性能仍是未知数。
*   **初始化方案存在改进空间**：当前的 \( B_i, A_i \) 初始化是数据无关的。论文作者承认，未来设计数据感知的初始化方案可能进一步提升性能。

（完）
