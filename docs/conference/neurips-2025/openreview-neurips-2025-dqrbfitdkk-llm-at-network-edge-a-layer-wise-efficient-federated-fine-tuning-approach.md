---
title: "LLM at Network Edge: A Layer-wise Efficient Federated Fine-tuning Approach"
title_zh: 网络边缘的LLM：一种分层高效联邦微调方法
authors: "Jinglong Shen, Nan Cheng, Wenchao Xu, Haozhao Wang, Yifan Guo, Jiajie Xu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=DqRbfiTdKK"
tags: ["query:edge-llm"]
score: 4.0
evidence: 提升联邦学习微调效率，保持模型性能并最小化客户端计算开销
tldr: 提出LEFF方法，在联邦学习设置下对LLM进行层间高效微调，通过根据客户端计算能力选择层和重要性驱动采样来减少开销，缓解异构环境中的掉队效应。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1455, \"height\": 810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 592, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 593, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 470, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 468, \"height\": 268, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 570, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 472, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dqrbfitdkk/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 988, \"height\": 649, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-dqrbfitdkk/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1451, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dqrbfitdkk/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 516, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dqrbfitdkk/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 586, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dqrbfitdkk/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 885, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dqrbfitdkk/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1048, \"height\": 1004, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dqrbfitdkk/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 879, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dqrbfitdkk/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1451, \"height\": 265, \"label\": \"Table\"}]"
motivation: 联邦学习中微调LLM带来巨大计算负担，尤其边缘设备异构。
method: LEFF根据客户端算力选择微调层，并采用重要性驱动的层采样机制。
result: 理论分析表明收敛速率为O(1/√)，实验验证了效率提升。
conclusion: LEFF在保证模型性能的同时显著降低边缘联邦微调的计算开销。
---

## Abstract
Fine-tuning large language models (LLMs) poses significant computational burdens, especially in federated learning (FL) settings. We introduce Layer-wise Efficient Federated Fine-tuning (LEFF), a novel method designed to enhance the efficiency of FL fine-tuning while preserving model performance and minimizing client-side computational overhead. LEFF strategically selects layers for fine-tuning based on client computational capacity, thereby mitigating the straggler effect prevalent in heterogeneous environments. Furthermore, LEFF incorporates an importance-driven layer sampling mechanism, prioritizing layers with greater influence on model performance. Theoretical analysis demonstrates that LEFF achieves a convergence rate of $\mathcal{O}(1/\sqrt{T})$. Extensive experiments on diverse datasets demonstrate that LEFF attains superior computational efficiency and model performance compared to existing federated fine-tuning methods, particularly under heterogeneous conditions.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究背景
- **问题定义**：在联邦学习（FL）场景下微调大语言模型（LLMs）时，边缘设备（如手机、PC）计算能力有限，导致严重的计算瓶颈与“掉队者”效应。
- **研究动机**：现有参数高效微调（PEFT）方法（如LoRA、BitFit）虽能降低客户端开销，但在非独立同分布（non‑IID）数据条件下性能退化明显；而全参数微调计算成本过高，无法直接应用于资源受限的客户端。
- **整体含义**：论文提出一种“层级别的高效联邦微调”方法（LEFF），旨在同时兼顾模型性能（应对数据异构）与客户端计算效率（应对设备异构），在边缘场景中实现实用的联邦LLM微调。

### 2. 方法论（LEFF）
LEFF 按通信轮次进行四步操作：

- **层选择与重要性采样**：
  - 每个客户端根据自身算力确定可微调的层数 $L_i$。
  - 服务器为每个客户端采样一层 **连续层块**（block）。采样概率由层重要性得分决定：基于一阶泰勒展开计算各参数重要性 $I^{(1)}_m(\Theta) = (g_m \theta_m)^2$，汇总得层重要性 $I_{\Theta_l} = \sum_{m \in \Theta_l} (g_m\theta_m)^2$，再经 Softmax 归一化得到采样分布 $p_i$。
- **未选层的模型压缩**：
  - 服务器对客户端未微调的层 $L_i^-$ 进行知识蒸馏压缩。使用公共代理数据集 $D_{\text{proxy}}$，以隐藏状态均方误差（MSE）和注意力矩阵 KL 散度的加权和作为蒸馏损失：
  \[
  E_{\text{distill}} = (1-\alpha) \text{MSE}(H_t, H_s) + \alpha\, \text{KL}(A_t, A_s)
  \]
  - 压缩后的学生模型 $\check{\Theta}_g^{L_i^-}$ 与选中的原始微调层拼成客户端专属模型。
- **局部训练**：
  - 客户端仅微调选中的层 $\Theta_g^{L_i}$，压缩层冻结。使用 AdamW 优化器，学习率 $1\times 10^{-5}$，每轮本地训练 1 个 epoch。
- **层级聚合**：
  - 客户端上传微调后的层参数，服务器按层加权平均：
  \[
  \Theta_g = \left\{ \sum_{i \in S_l} \frac{D_i}{\sum_{j\in S_l} D_j} \Theta_l^i \;\middle|\; l = 1,\dots,L \right\}
  \]
- **理论保证**：在标准 FL 假设（L‑smooth、梯度方差有界、数据异质性有界）及 LEFF 特有的模型近似误差有界假设下，证明了方法收敛速率为 $\mathcal{O}(1/\sqrt{T})$，但存在由近似误差 $\bar{\Delta}^2$、异质性 $\zeta^2$、随机梯度方差 $\sigma^2/K$ 共同决定的误差底。

### 3. 实验设计与对比方法
- **模型与任务**：
  - 自然语言理解（NLU）：DeBERTaV3 Base 在 GLUE 基准（CoLA、SST‑2、MRPC、STS‑B、QQP、MNLI、QNLI、RTE）上评测。
  - 自然语言生成（NLG）：GPT‑2 Medium 在 E2E NLG Challenge 上评测（BLEU、NIST、METEOR、ROUGE、CIDEr）。
  - 更大规模验证：Llama‑3.1‑8B 在 MMLU（5‑shot）上评测。
- **对比方法**：
  - 全参数联邦平均 FedAvg。
  - 参数高效方法：FedBitFit（仅偏置）、FedLoRA、SLoRA。
  - 较新 SoTA：FLoRA、FlexLoRA（LLaMA‑3.1 实验）。
- **数据异质性模拟**：利用 Dirichlet 分布划分客户端数据，浓度参数 $\alpha \in \{0.05, 0.1, 0.5, 1.0, 5.0, 10.0, 50.0\}$。
- **客户端规模**：从 8 扩展到 40 客户端。
- **消融与附加实验**：
  - 压缩比 $r$ 的影响（0.2/0.5/0.8）。
  - 采样策略对比（重要性采样 vs. 轮询 vs. 随机）。
  - 代理数据集敏感性（WikiText‑103、WebNLG、OpenWebText）。
  - 统计稳定性（三次随机种子标准差）。
  - 算力开销分析（表5：可训练参数量与 GPU 峰值内存）。
  - 收敛曲线实证（图8）。

### 4. 资源与算力
- 论文明确指出：“All experiments were performed on a system with eight NVIDIA H100 GPUs.”
- 未提供单次实验的精确训练时长，但通过表 5 给出了详细的客户端 GPU 峰值内存（如 DeBERTaV3‑Base 下 LEFF 仅需 2.136 GB，而 FedAvg 需 3.841 GB），间接体现资源效率。

### 5. 实验数量与充分性
- **实验矩阵覆盖广**：至少包含 3 种模型架构、2 类任务（NLU/NLG）、多组 α 值、多客户端数量、3 种采样策略、多个压缩比、多种基线方法。
- **消融与鲁棒性验证**：代理数据集影响、结果标准差、收敛过程、参数量与内存分析，以及扩展至 LLaMA‑3.1‑8B 的 SoTA 对比。
- **公平性**：所有方法在同一硬件环境、相同微调 epoch、相同优化器与学习率下比较，非 IID 划分方法一致。
- 综合来看，实验设计充分、客观，支撑了论文的核心主张。

### 6. 主要结论与发现
- LEFF 在强异质性（$\alpha=0.05$）下 GLUE 平均分达 63.84，仅略低于全量微调的 65.88，大幅领先 FedLoRA（54.57）和 FedBitFit（53.41）。
- E2E NLG 任务上 LEFF（平均 2.2805）同样接近 FedAvg（2.2980），优于所有 PEFT 基线。
- 客户端计算资源消耗显著降低：在 GPT‑2 Large 上，LEFF 内存仅 3.24 GB，比 FedAvg 降低 79%，比 FedLoRA 降低 66%。
- LLaMA‑3.1‑8B 上，LEFF 峰值内存 29.88 GB（FedLoRA 需 46.87 GB），MMLU 5‑shot 得分 57.5，超过 FlexLoRA 和 FLoRA。
- 重要性采样策略优于轮询和随机采样；较高的压缩比（低压缩）性能更好；代理数据集选择对性能影响不大，方法具有一定鲁棒性。

### 7. 优点
- **双解耦设计**：通过层选择与重要性采样同时解决客户端算力异构和数据非 IID 两大难题。
- **高效的资源利用**：只加载和训练局部层，极大降低客户端 GPU 内存需求，使大模型边缘微调可行。
- **理论支撑**：给出了收敛速率 $\mathcal{O}(1/\sqrt{T})$ 及误差底分析，明确了效率与保真度的权衡。
- **实验全面**：涵盖多种模型规模、任务类型、异质性条件，且包含与最新 SoTA（FLoRA、FlexLoRA）的对比，实验可重复性高。
- **代理数据鲁棒**：蒸馏仅匹配中间表示，使方法对代理数据集域不敏感。

### 8. 不足与局限
- **服务器端额外开销**：每轮需计算层重要性（前向/反向传播）并执行知识蒸馏，增加了中心服务器计算负载。
- **通信成本可能较高**：若压缩比低（保留层多），向客户端分发定制模型可能增加下行通信量。
- **性能上界受限**：理论分析揭示模型近似误差 $\bar{\Delta}^2$ 会形成不可消除的误差底，限制了最终精度。
- **重要参数依赖**：重要性采样依赖一阶泰勒近似，在梯度稀疏或模型初始阶段可能不准确。
- **代理数据集实际可用性**：虽然实验表明敏感性低，但实际 FL 中获取合适的公共代理数据集有时不可行。
- **代码未公开**：论文未附代码链接，复现存在额外障碍。
- **长尾任务与更大规模客户端**：客户端数量增至 40 时某些困难任务（如 CoLA）性能显著下降；未测试 100+ 客户端的极限场景。

（完）
