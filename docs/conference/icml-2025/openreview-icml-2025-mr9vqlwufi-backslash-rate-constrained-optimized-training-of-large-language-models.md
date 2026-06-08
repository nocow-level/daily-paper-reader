---
title: "BackSlash: Rate Constrained Optimized Training of Large Language Models"
title_zh: BackSlash：大语言模型的率约束优化训练
authors: "Jun Wu, Jiangtao Wen, Yuxing Han"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=MR9VQLWUFI"
tags: ["query:edge-llm"]
score: 7.0
evidence: 通过率失真优化的训练时压缩
tldr: "着眼于训练阶段压缩大语言模型以减少参数冗余，提出基于率失真优化的训练时压缩方法BackSlash，能灵活权衡精度与复杂度。实验表明，可在不损失准确率的情况下减少60%-90%的内存占用，优于训练后压缩，为边缘部署提供更紧凑的模型。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1740, \"height\": 686, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 813, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1647, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 807, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-mr9vqlwufi/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 811, \"height\": 417, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-mr9vqlwufi/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mr9vqlwufi/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 858, \"height\": 705, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mr9vqlwufi/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1780, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mr9vqlwufi/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mr9vqlwufi/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1717, \"height\": 444, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mr9vqlwufi/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1809, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-mr9vqlwufi/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1736, \"height\": 299, \"label\": \"Table\"}]"
motivation: 大模型训练后压缩已成研究热点，但训练中压缩仍未被充分探索。
method: 提出率约束训练（BackSlash），一种基于率失真优化的训练时压缩方法。
result: "内存使用减少60%-90%且无精度损失，压缩增益优于训练后压缩。"
conclusion: 训练时压缩是生成轻量LLM的有效途径，有利于后续边缘部署。
---

## Abstract
The rapid advancement of large-language models (LLMs) has driven extensive research into parameter compression after training has been completed, yet compression during the training phase remains largely unexplored. In this work, we introduce Rate-Constrained Training (BackSlash), a novel training-time compression approach based on rate-distortion optimization (RDO). BackSlash enables a flexible trade-off between model accuracy and complexity, significantly reducing parameter redundancy while preserving performance. Experiments in various architectures and tasks demonstrate that BackSlash can reduce memory usage by 60\% - 90\% without accuracy loss and provides significant compression gain compared to compression after training. Moreover, BackSlash proves to be highly versatile: it enhances generalization with small Lagrange multipliers, improves model robustness to pruning (maintaining accuracy even at 80\% pruning rates), and enables network simplification for accelerated inference on edge devices.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型参数量急剧增长，如GPT-4已达1.8T参数，导致计算、存储和部署成本剧增。当前模型压缩（剪枝、量化、低秩分解等）多在训练完成后进行，训练过程中的压缩很少被探索。
- **核心问题**：能否在模型训练阶段就整合压缩目标，同时优化模型性能与参数冗余度，从而训练出天生轻量的高性能模型？
- **整体含义**：论文提出一种基于率失真优化的训练框架BackSlash，将模型参数量度纳入损失函数，训练出既准确又紧凑的模型，大幅减少显存和存储占用，且为边缘设备部署提供更高效的推理能力。

## 2. 论文提出的方法论

- **核心思想**：将参数分布建模为广义高斯分布（GGD），用率失真优化（RDO）联合优化推理损失（失真）与参数编码代价（码率），实现训练时压缩。
- **关键技术细节**：
    - **广义高斯模型**：发现LLM参数分布（训练后）形状参数常小于2，具有更尖的峰和更长的尾，适合用GGD建模。
    - **离散广义高斯码率（DGGR）**：基于GGD推导出量化形式的码率度量：\( R(\theta) = \frac{1}{N_p}\sum_{i=1}^{N_p} |\theta_i|^{\nu} \)，其中形状参数\(\nu\)动态估计。
    - **损失函数**：\( J = D + \lambda \cdot R \)，\(D\)是任务损失，\(R\)是DGGR，\(\lambda\)控制压缩与性能的权衡。
    - **动态形状参数估计**：每批训练前通过公式\(\rho(\nu)=\Gamma(1/\nu)\Gamma(3/\nu)/\Gamma^2(2/\nu)=E[\theta^2]/E^2[|\theta|]\)求解\(\nu\)。
    - **软梯度裁剪**：因\(\nu<1\)时梯度爆炸，添加小常数\(\epsilon\)使度量变为\( (|\theta|+\epsilon)^\nu \)。
    - **熵编码**：训练后采用Exp-Golomb编码（k=0），对参数量化、频率排序建表，再用索引编码，达到接近熵极限的压缩率。
- **算法伪代码**：见原文Algorithm 1，每次迭代包括估算\(\nu\)、构建RD损失、反向传播并更新参数等步骤。注意L1、L2正则化可看作DGGR在\(\nu=1\)和\(\nu=2\)时的特例。

## 3. 实验设计

- **数据集/场景**：
    - 分类任务：IMDB情感分析、Enron-Spam垃圾邮件检测、20 Newsgroups主题分类。
    - 生成任务：SQuAD问答、WMT-19翻译、DeepSeek下一 token 预测。
- **模型**：BERT（110M）、GPT-2（774M）、Llama-3（1B）、Gemma-2（2B）、DeepSeek（7B）等。
- **对比方法**：
    - 正常训练后使用固定长度编码、Exp-Golomb编码、Huffman编码的压缩基线。
    - BackSlash训练后同样用三种编码对比。
    - 消融实验对比固定形状的Lp正则化（L0.5、L1、L2）与BackSlash的DGGR。
    - 量化/剪枝鲁棒性测试。

## 4. 资源与算力

- 论文未提供具体GPU型号、数量及训练时长。仅提及对BERT、GPT、Llama、Gemma等模型进行了训练，未说明计算资源消耗。因此无法从文中获取确切算力信息。

## 5. 实验数量与充分性

- **实验组数**：
    - 分布拟合图：4个模型的GGD vs 高斯分布验证。
    - 不同λ下的训练曲线、形状参数变化、平均码长、准确率图（约4-5组）。
    - 四种模型架构参数压缩对比表（BERT、GPT、Llama、Gemma）。
    - 五种下游任务压缩对比表（Sentiment、Spam、Topic、Q-A、Translation）。
    - 量化鲁棒性（不同step）和剪枝鲁棒性（不同剪枝率）实验。
    - 消融实验：DGGR与L0.5、L1、L2的压缩与精度对比。
- **充分性评价**：实验覆盖了多种模型规模（110M-2B），多种任务类型（分类、生成），多种编码方式，以及量化/剪枝部署场景。消融实验对比了固定形状正则化，证明了自适应形状的必要性。总体实验设计较全面、客观、公平。

## 6. 论文的主要结论与发现

- BackSlash可在不损失精度（甚至有轻微提升）的情况下，将模型压缩60%-90%（如Gemma压缩90%，BERT压缩76%）。
- 训练时压缩明显优于训练后压缩：正常训练后用熵编码只能节省27%-45%，BackSlash结合熵编码可节省74%-90%。
- 模型对量化鲁棒性与正常训练相当，但对剪枝鲁棒性极强：正常训练模型剪枝50%即掉点，BackSlash模型可在80%剪枝率下保持准确率。
- 自适应形状参数比固定L1/L2正则化更能平衡压缩率与精度。
- 使用固定Exp-Golomb码表即可高效编码，无需每模型定制Huffman表。

## 7. 优点

- **创新性**：首次将率失真优化融入LLM训练过程本身，而不是训练后压缩。
- **理论基础扎实**：从参数分布建模出发，推导DGGR度量，与L1/L2自然关联。
- **实验全面**：跨模型、跨任务、跨压缩场景，验证了通用性和部署优势。
- **工程友好**：Exp-Golomb编码结构简单，硬件实现容易，适配边缘设备。
- **附加收益**：增强剪枝鲁棒性，为后续模型硬压缩提供更大空间。

## 8. 不足与局限

- **λ超参选择**：Lagrange乘子需试错确定，尽管文中提到初步经验，但缺乏系统指导。
- **算力开销未披露**：未说明训练BackSlash相比普通训练额外时间/硬件成本。
- **实验规模有限**：最大模型仅到2B（Gemma-2），未在更大LLM（如7B、13B、70B）上报告结果，更大模型上结论待验证。
- **生成任务评估单一**：用“下一token准确率”衡量生成质量可能不全面，缺乏如困惑度、BLEU等指标。
- **压缩率有上限**：依赖于GG分布假设和熵编码，极低码率下模型性能可能坍塌。
- **硬件实现未展开**：虽提边缘推理加速，但未提供具体推理时延或功耗对比。

（完）
