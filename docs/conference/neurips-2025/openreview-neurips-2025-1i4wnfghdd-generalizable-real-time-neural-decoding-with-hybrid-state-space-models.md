---
title: "Generalizable, real-time neural decoding with hybrid state-space models"
title_zh: 基于混合状态空间模型的泛化实时神经解码
authors: "Avery Hee-Woon Ryoo, Nanda H Krishna, Ximeng Mao, Mehdi Azabou, Eva L Dyer, Matthew G Perich, Guillaume Lajoie"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=1i4wNFgHDd"
tags: ["query:edge-llm"]
score: 4.0
evidence: 混合SSM用于低资源实时神经解码，一种边缘推理场景
tldr: 提出POSSM混合架构，结合交叉注意力与递归模块，在低资源实时神经解码任务中实现高效推理，但对LLM端侧部署直接借鉴意义有限。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-1i4wnfghdd/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 620, \"height\": 219, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1i4wnfghdd/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1458, \"height\": 811, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1i4wnfghdd/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1433, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1i4wnfghdd/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1446, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1i4wnfghdd/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1451, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-1i4wnfghdd/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1421, \"height\": 453, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1455, \"height\": 786, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 543, \"height\": 512, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 467, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1278, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1453, \"height\": 640, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 605, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1042, \"height\": 207, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1379, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1063, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1131, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-1i4wnfghdd/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1288, \"height\": 211, \"label\": \"Table\"}]"
motivation: 现有实时神经解码方法难以兼顾速度和泛化能力。
method: 采用交叉注意力模块结合状态空间模型设计混合架构。
result: 在神经解码基准上实现高精度和低延迟。
conclusion: 该架构为实时应用提供了新选择，对边缘设备推理有一定参考价值。
---

## Abstract
Real-time decoding of neural activity is central to neuroscience and neurotechnology applications, from closed-loop experiments to brain-computer interfaces, where models are subject to strict latency constraints. Traditional methods, including simple recurrent neural networks, are fast and lightweight but often struggle to generalize to unseen data. In contrast, recent Transformer-based approaches leverage large-scale pretraining for strong generalization performance, but typically have much larger computational requirements and are not always suitable for low-resource or real-time settings. To address these shortcomings, we present POSSM, a novel hybrid architecture that combines individual spike tokenization via a cross-attention module with a recurrent state-space model (SSM) backbone to enable (1) fast and causal online prediction on neural activity and (2) efficient generalization to new sessions, individuals, and tasks through multi-dataset pretraining. We evaluate POSSM's decoding performance and inference speed on intracortical decoding of monkey motor tasks, and show that it extends to clinical applications, namely handwriting and speech decoding in human subjects. Notably, we demonstrate that pretraining on monkey motor-cortical recordings improves decoding performance on the human handwriting task, highlighting the exciting potential for cross-species transfer. In all of these tasks, we find that POSSM achieves decoding accuracy comparable to state-of-the-art Transformers, at a fraction of the inference cost (up to 9x faster on GPU). These results suggest that hybrid SSMs are a promising approach to bridging the gap between accuracy, inference speed, and generalization when training neural decoders for real-time, closed-loop applications.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：实时神经解码（将神经活动映射为行为变量）在闭环实验和脑机接口中要求高精度、低延迟和强泛化能力。传统RNN速度快但难以泛化到新被试/任务，基于Transformer的模型泛化好但计算复杂度高，不适于资源受限的在线场景。
- **研究动机**：需要一种能同时满足**准确预测、因果且低延迟推理、跨被试/跨任务灵活泛化**的神经解码器。
- **整体含义**：论文提出**POSSM**，一种结合尖峰令牌化和递归状态空间模型的混合架构，旨在以极低的推理成本实现与SOTA Transformer相当的精度，并展示跨物种迁移潜能，推动通用实时神经解码。

### 2. 方法论
- **核心思想**：将**POYO式尖峰令牌化**（灵活输入）与**递归SSM骨干**（恒定时间推理）相结合，兼顾泛化与效率。
- **关键技术细节**：
  - **尖峰令牌化**：每个神经尖峰表示为单元嵌入（UnitEmb）和旋转位置嵌入（RoPE）时间戳，形成一个可变长度令牌序列，不依赖固定时间分箱。
  - **输入交叉注意力**：利用可学习查询向量，将每个50 ms时间块内的变长尖峰令牌序列压缩为一个固定维度的潜在向量z(t)。
  - **递归骨干**：z(t)送入SSM（如S4D、Mamba）或GRU，更新隐藏状态h(t) = f_SSM(z(t), h(t-1))，整合局部与全局时序信息。
  - **输出交叉注意力与头**：取最近k个隐藏状态，通过交叉注意力模块查询行为预测，支持多时间点预测、对齐延迟和非对齐输出。
- **泛化策略**：
  - **单元辨识（UI）**：冻结预训练权重，仅训练新单元/会话嵌入（<1%参数）。
  - **完整微调（FT）**：先UI后逐渐解冻全模型，适应新个体/任务/物种。

### 3. 实验设计
- **数据集**：
  - **NHP到达任务**：包含4个猴运动皮层数据集（中心向外、随机目标、迷宫任务等），共148个会话，6.7亿尖峰，26032个神经单元。
  - **人手写**：1名受试者想象手写字符，9个会话的阈值交叉尖峰，分类字符或线条。
  - **人语音**：1名受试者尝试说话，24个会话的多单元活动，解码音素序列。
- **Benchmark与对比方法**：
  - NHP：MLP、S4D、Mamba、GRU、POYO（单/多会话版）、NDT-2。
  - 手写：PCA-KNN、S4D、Mamba、GRU、POYO。
  - 语音：GRU、S4D、Mamba，并测试单向/双向模型。
- **评估协议**：因果评估（逐时间块流式输入），验证长序列泛化；手写和语音采用分类准确率、音素错误率；在GPU和CPU上衡量推理延迟。

### 4. 资源与算力
- **训练**：
  - 单会话模型：单张NVIDIA RTX8000 GPU，训练时间<30分钟。
  - 多数据集预训练（o-POSSM）：4张NVIDIA H100 GPU，总时长约36小时。
  - 人手写和语音任务：分别在RTX8000和A100（80 GB）上训练。
- **推理评测**：在RTX8000 GPU和AMD EPYC 7502 CPU上测量延迟，单会话POSSM约2.44 ms/chunk，o-POSSM约5.65 ms/chunk（CPU环境），GPU上最快可达毫秒级。

### 5. 实验数量与充分性
- **主要实验组**：
  - 2种时间块大小（50 ms、20 ms）的NHP解码。
  - 3种骨干（S4D、GRU、Mamba）在单会话和预训练条件下的对比。
  - 两种泛化策略（UI与FT）在不同泛化难度上对比。
  - 跨任务/跨物种迁移（猴→手写、语音）。
- **消融与分析**：
  - 尖峰时间信息的影响、特征混合器MLP的使用、递归编码器替代交叉注意力、输出滞后预测、LoRA微调、样本与训练效率等。
- **是否充分**：实验覆盖多个任务、数据集和模型变体，采用统计检验（配对t-检验）报告标准差，对比公平（统一因果评估、相同数据划分），实验设计与消融较为完整。

### 6. 主要结论与发现
- POSSM在NHP到达、人手写、人语音解码三个任务上均达到与SOTA Transformer相当的精度，且推理速度快达9倍（GPU上）。
- 多数据集预训练（o-POSSM）显著提升单会话性能，在新被试/任务上通过完整微调可进一步优化。
- 首次展示**跨物种迁移**：仅用猴运动皮层数据预训练的POSSM在人类手写任务上微调后，精度大幅超越从零训练的模型（提升2%～5%）。
- 语音解码的长时间上下文任务中，POSSM有效克服了Transformer的二次复杂度瓶颈，性能优于GRU基线。
- 架构保留尖峰时刻信息能持续提升解码表现。

### 7. 优点
- **架构创新**：首次将POYO式灵活令牌化与递归SSM结合，实现固定计算成本的流式推理。
- **效率与精度平衡**：低参数量、毫秒级延迟，在GPU/CPU上均适合实时部署。
- **泛化能力突出**：通过单元辨识和完整微调，能够泛化到新被试、新任务乃至跨物种。
- **实验扎实**：覆盖多任务、多对比方法、消融实验，提供统计显著性，代码将开源。
- **实用性强**：可直接应用于闭环BCI，为临床神经假体提供高效方案。

### 8. 不足与局限
- **解码模式单一**：目前仅处理尖峰数据，虽可扩展但尚未验证其他模态（如LFP、EEG、钙信号）。
- **区域局限**：实验集中于运动皮层，对感觉、认知等皮质区域的解码能力未充分评估。
- **离线评估**：所有实验均为离线模拟，未在实际在线闭环环境中测试鲁棒性。
- **预训练策略**：当前仅依赖监督行为信号，未探索自监督预训练或多模态融合。
- **长序列语音解码**：仍借用了传统CTC损失和滑动窗口，未对超长上下文进行端到端优化。
- **跨物种泛化的推广性**：仅展示猴到人的一种场景，对其他物种或神经差异更大的物种可能需额外适应。

（完）
