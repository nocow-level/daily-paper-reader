---
title: "StatsMerging: Statistics-Guided Model Merging via Task-Specific Teacher Distillation"
title_zh: StatsMerging：通过任务特定教师蒸馏进行统计引导的模型合并
authors: "Ranjith Merugu, Bryan Bo Cao, Shubham Jain"
date: 2025-04-06
pdf: "https://openreview.net/pdf?id=4PZMjjElQz"
tags: ["query:edge-llm"]
score: 6.0
evidence: 使用教师蒸馏进行模型合并以减少内存，与知识迁移和部署相关
tldr: StatsMerging为解决多任务模型存储占用过多GPU内存的瓶颈，提出基于统计引导的模型合并方法，通过特定任务的教师蒸馏引导合并过程。该方法在无需额外标注样本的情况下，有效压缩模型体积，为多任务部署场景下的内存优化提供了新途径。
source: NeurIPS-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-4pzmjjelqz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1295, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4pzmjjelqz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1453, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4pzmjjelqz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1436, \"height\": 175, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-4pzmjjelqz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1324, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4pzmjjelqz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1321, \"height\": 646, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4pzmjjelqz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1466, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4pzmjjelqz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 556, \"height\": 430, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4pzmjjelqz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 698, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4pzmjjelqz/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 763, \"height\": 256, \"label\": \"Table\"}]"
motivation: 多个任务特定大模型导致GPU内存不足，现有合并方法启发式简单且效果有限。
method: 利用任务特定教师模型蒸馏信号，结合权重分布统计指导模型合并。
result: 在保持多任务能力的同时降低了存储需求。
conclusion: StatsMerging通过蒸馏引导的合并，在有限内存下有效容纳多个模型。
---

## Abstract
As large models are increasingly deployed across various tasks, the limited GPU memory available for storing task-specific models presents a growing bottleneck. Model merging has emerged as a promising solution to accommodate multiple large models within constrained memory budgets. While traditional multi-task learning methods attempt to merge shared layers, they require labor-intensive annotated labels and incur significant computational overhead. Recent merging techniques aim to address this issue by combining models at inference time; however, these approaches often rely on simplistic heuristics, ignore weight distribution characteristics, assume architectural identity, or require access to test samples to infer merging coefficients, thereby limiting their generalization capability and scalability. We present **StatsMerging**, a novel lightweight learning-based model merging method guided by weight distribution statistics without training ground truth labels or test samples. StatsMerging offers three key advantages: (1) It uniquely leverages **singular values** from singular value decomposition (SVD) to capture task-specific weight distributions, serving as a proxy for task importance to guide task coefficient learning; (2) It employs a lightweight learner **StatsMergeLearner** to model the weight distributions of task-specific pre-trained models, improving generalization and enhancing adaptation to unseen samples; (3) It introduces **Task-Specific Teacher Distillation**, a merging training paradigm that avoids costly ground-truth labels by task-specific teacher distillation. Notably, we present two types of knowledge distillation, (a) distilling knowledge from task-specific models to train StatsMerge Learner; and (b) for the first time, distilling knowledge from models with different architectures prior to merging, following a distill-then-merge paradigm. Extensive experiments across eight tasks demonstrate the effectiveness of StatsMerging. Our results show that StatsMerging outperforms state-of-the-art techniques in terms of overall accuracy, generalization to unseen tasks, and robustness to image quality variations.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究背景
- **问题**：大量任务特定的大模型部署导致 GPU 内存不足，存储和执行多个专用模型成为瓶颈。模型合并（model merging）作为一种后处理方案，能够在有限内存下融合多个模型，但现有方法存在局限。
- **现有方法不足**：传统多任务学习需要昂贵的标注数据和高计算开销；近期模型合并方法大多使用简单启发式（如权重平均），忽略权重分布特性，假设架构一致，或依赖测试样本推断合并系数，泛化性和可扩展性受限。
- **本文动机**：提出 **StatsMerging**，一种基于权重分布统计指导的轻量级模型合并方法，无需真实标签或测试样本，以提升合并模型的准确性、泛化能力和鲁棒性。

## 2. 方法论
### 2.1 核心思想
- 利用**权重分布统计特征**（均值、方差、模、SVD 奇异值）捕捉任务特定信息，指导合并系数的学习。
- 设计轻量级 MLP **StatsMergeLearner**，输入统计特征，输出任务级或层级合并系数 λ。
- 提出**任务特定教师蒸馏**训练范式，利用已训练好的任务模型作为教师生成伪标签，避免人工标注。

### 2.2 关键技术与流程
#### 权重统计提取
- 对每个任务模型 θ_k，计算统计特征：
  - 均值 μ、方差 σ²、模 m。
  - 对权重矩阵进行 **奇异值分解（SVD）**，取秩 r 的奇异值 σ′_r。
- 组合得到统计向量：
  - 任务级：S_k = [μ, σ², m, σ′_r]
  - 层级：S_lk = stats(θ_lk)

#### 合并系数预测（StatsMergeLearner）
- 使用两隐层 MLP，输入统计特征 S，输出合并系数 λ。
- 任务级：λ_k = SML(S_k)
- 层级：λ_lk = SML(S_lk)
- 合并后模型权重：θ_merged = Σ_k λ_k θ_k（任务级）或对每层加权求和。

#### 任务特定教师蒸馏训练
- 将每个预训练模型 θ_k 视为其任务数据的教师，生成**伪标签** ŷ_i,k。
- 构建聚合数据集 {x_i, ŷ_i,k}，用交叉熵损失训练 StatsMergeLearner：
  - L_CE = -Σ_c ŷ_c log(ˆy_c)
- 训练细节：500 epochs，Adam 优化器，学习率 1e-3，StepLR 衰减。

#### 异构架构合并
- 首次提出**蒸馏后合并**范式：将不同架构（如 ViT 和 ResNet）的教师模型通过知识蒸馏迁移到统一目标架构，随后应用 StatsMerging。
- 蒸馏损失结合交叉熵和 KL 散度：L = α L_CE(y, ŷ) + (1-α) T² L_KL(σ(z/T), σ(s/T))，其中 T 为温度，α 为权重。

## 3. 实验设计
### 3.1 数据集与任务
- 8 个图像分类数据集：SUN397、Stanford Cars、RESISC45、EuroSAT、SVHN、GTSRB、MNIST、DTD。
- 预训练骨干：**ViT-B/32 CLIP**（主要）和 **ResNet50**（异构实验）。
- 每个数据集独立微调得到任务模型。

### 3.2 对比基准与方法
- 传统多任务学习（Traditional MTL）、单独训练（Individual）、权重平均、Task Arithmetic、Fisher Merging、RegMean、Ties-Merging、AdaMerging 及 AdaMerging++。
- 评估指标：**各任务测试集的平均准确率（Avg Acc %）**。

### 3.3 实验场景
- **多任务合并**：8 个任务，任务级（TW）和层级（LW）合并。
- **泛化能力**：从 6 个 seen 任务合并，测试 2 个 unseen 任务（两组交叉验证）。
- **异构架构合并**：ResNet50 与 ViT-B/32 之间的蒸馏后合并。
- **消融研究**：统计特征（均值、方差、模、奇异值）的贡献；损失函数（GT 标签 vs. 教师蒸馏伪标签）；系数分布可视化。

## 4. 资源与算力
- 训练StatsMergeLearner合并4个ViT仅需约 **3小时**，体现轻量性。
- 实验使用 **NVIDIA RTX A6000 GPU**（在检查清单中提及），但未详细列出具体 GPU 数量或总耗时。
- 整体方法可运行于普通 GPU 环境，无需大规模集群。

## 5. 实验充分性与客观性
- **实验覆盖全面**：包含 8 个不同视觉任务，任务级和层级两种粒度，同构和异构架构，以及泛化测试。
- **对比方法丰富**：与 7 种代表性模型合并/多任务方法进行了横向比较，采用统一的公开数据集和评估协议，公平客观。
- **消融分析充分**：验证了统计特征各部分（特别是奇异值）的贡献，对比了伪标签与真实标签的训练效果，并分析了系数的分布规律，增强了方法的可解释性。
- **潜在偏差**：所有实验基于图像分类，且主要使用 CLIP ViT 预训练权重，向其他任务或领域的泛化性仍需验证。

## 6. 主要结论与发现
- StatsMerging 在 8 任务合并中达到 **84.5%** 平均准确率，显著优于 SOTA 方法 AdaMerging++ 的 **81.1%**，提升 **3.4%**。
- 层级合并优于任务级，更精细地分配系数能保留更多任务特定知识。
- 泛化到未见任务的性能同样领先（+0.8% 到 +2.2%）。
- 异构架构合并成功将 ResNet 和 ViT 融合，平均准确率达 **81.3%**，比 Task Arithmetic 高 7.6%。
- **SVD 奇异值** 是关键统计特征，能有效捕捉任务重要性。
- 使用任务特定教师蒸馏训练的 StatsMergeLearner 可以接近使用真实标签的性能，摆脱了对人工标注的依赖。

## 7. 优点
- **无标签/无测试样本需求**：仅利用权重统计和教师蒸馏，完全避免标注成本和测试时调参。
- **首次支持异构架构合并**：扩展了模型合并的应用范围。
- **轻量高效**：StatsMergeLearner 结构简单，训练耗时短，易于实际部署。
- **可解释性较好**：通过系数热力图展示了不同任务和层级的合并规律，支撑了层级设计的合理性。

## 8. 不足与局限
- **任务范围限制**：当前仅在图像分类上验证，未涉及目标检测、分割、生成等其他视觉任务或 NLP 领域。
- **统计计算成本**：对每一层权重进行 SVD 会增加计算开销，在超大模型（如 LLM）上可能成为瓶颈。
- **教师质量依赖**：伪标签质量取决于各任务教师模型的性能，若个别任务模型精度低，可能引入噪声，影响最终合并效果。
- **训练数据需求**：虽然无需人工标注，但仍需访问各任务的原始训练样本，无法完全脱离数据。
- **合并系数可解释性有限**：MLP 为黑箱，统计特征与系数之间的具体映射关系未深入分析，可能影响 Trustworthy 方面的考量。

（完）
