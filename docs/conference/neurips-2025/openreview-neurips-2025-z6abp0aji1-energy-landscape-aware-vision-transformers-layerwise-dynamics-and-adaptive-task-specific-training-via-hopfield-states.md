---
title: "Energy Landscape-Aware Vision Transformers: Layerwise Dynamics and Adaptive Task-Specific Training via Hopfield States"
title_zh: 能量景观感知的视觉Transformer：通过Hopfield状态的逐层动态与自适应任务特定训练
authors: "Runze Xia, Richard Jiang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Z6aBp0AJI1"
tags: ["query:edge-llm"]
score: 6.0
evidence: ViT层动态分析可能带来计算节省，与端侧加速相关
tldr: 该工作从能量记忆系统视角分析ViT层动态，提出层不稳定性指数，发现某些层会早期收敛到吸引状态。这一发现揭示了利用层次功能特化进行提前退出的可能性，为视觉Transformer的推理加速提供了理论依据，有望指导面向端侧的轻量化设计。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-z6abp0aji1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1416, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-z6abp0aji1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1432, \"height\": 494, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-z6abp0aji1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1459, \"height\": 687, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-z6abp0aji1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1457, \"height\": 495, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-z6abp0aji1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1371, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-z6abp0aji1/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1445, \"height\": 439, \"label\": \"Table\"}]"
motivation: 深度ViT的均匀层结构带来显著计算开销，需要挖掘层次动态以提高效率。
method: 通过连接自注意力与Hopfield网络，构建层不稳定性指数量化层状态的亚稳定性。
result: 分析表明某些层会收敛到吸引子态，显示出功能特化和早期稳定特性。
conclusion: 该分析为设计层次敏感的高效ViT架构提供了新见解，有望降低推理成本。
---

## Abstract
Recent advances in Vision Transformers (ViTs) have shown remarkable performance across vision tasks, yet their deep, uniform layer structure introduces significant computational overhead. In this work, we explore the emergent dynamics of ViT layers through the lens of energy-based memory systems, drawing a connection between self-attention and modern Hopfield networks. We introduce a novel metric—Layer Instability Index (LII)—derived from the operational softmax mode and its variability, to quantify the metastability of each Transformer layer over time. Our analysis reveals that certain layers exhibit consistent convergence to attractor-like states, suggesting functional specialisation and early stabilisation. Leveraging this insight, we propose an adaptive training framework that dynamically freezes or skips stable layers based on their energy landscape behavior. Our method reduces training costs while maintaining or improving accuracy. Extensive experiments on ViT-S/B/L on CUB-200-2011, CIFAR-10/100, Food-101, Stanford Dogs, and Beans demonstrate the generality and efficiency of our approach. This work provides new theoretical and practical perspectives for energy-aware optimisation of deep Transformer models.

---

## 论文详细总结（自动生成）

# 论文总结：《Energy Landscape-Aware Vision Transformers: Layerwise Dynamics and Adaptive Task-Specific Training via Hopfield States》

## 1. 论文的核心问题与整体含义
- **研究背景**：Vision Transformers (ViTs) 在各类视觉任务中表现优异，但其深层且均匀的层结构造成显著的计算开销。现有优化策略多聚焦于标记稀疏化、深度自适应或参数高效微调（PEFT），但普遍忽视不同层内部收敛行为的差异，缺乏理论依据来判定哪些层可被安全冻结或跳过。
- **核心问题**：如何利用 ViT 层内部动态的差异，在微调过程中自适应地冻结稳定层，以降低训练开销并保持或提升精度？
- **整体含义**：论文将自注意力机制重新解读为现代 Hopfield 网络的能量最小化过程，提出基于能量景观的逐层动力学分析方法，并据此设计自适应训练框架，从理论和实践两个层面推动能量感知的 Transformer 优化。

## 2. 方法论
- **核心思想**：将 Transformer 自注意力视为 Hopfield 能量最小化过程，通过量化层输出分布的稳定性来识别已收敛的“吸引子”层，并在微调中将其冻结，仅更新剩余的不稳定层。
- **关键技术细节**：
  - **能量景观建模**：借鉴 Ramsauer 等人工作，定义每层的 Hopfield 能量函数 \(E = -\text{lse}(\beta, X^T \xi) + \frac{1}{2}\xi^T \xi + C\)。
  - **运行模式**：定义每层的操作模式 \(\bar{k}_\ell\) 为累积 90% 注意力质量所需的最小 token 数量的中位数（表示注意力集中程度）。
  - **层不稳定性指数**：使用滑动窗口内 \(\bar{k}_\ell\) 的中位数绝对偏差（MAD）作为层不稳定性指数，低 LII 表示层稳定。
  - **理论桥接**：证明 LII 作为能量间隙的上界，低 LII 层对应 Fisher 平坦区，可安全冻结；LII 还与注意力分布的 Wasserstein 距离相关。
  - **自适应训练流程**：
    1. **预热阶段**：所有层可训练，利用滑动窗口（默认长度 20）在线计算每层的 LII。
    2. **冻结决策**：预热结束后（如 T = 3W），一次性将 LII 低于阈值 τ 的层冻结（`requires_grad = False`）。
    3. **巩固阶段**：仅训练剩余未冻结层。
  - **特点**：无额外可学习参数，LII 直接由注意力得分计算，决策只需一次，节省计算和内存。

## 3. 实验设计
- **数据集**：CUB-200-2011、Stanford Dogs、NABirds、Beans、CIFAR-10、CIFAR-100、Food-101、ImageNet-1k。
- **模型**：ViT-S/16、ViT-B/16、ViT-L/16（ImageNet-21k 预训练），以及 DeiT-B/16。
- **基线对比**：标准全量微调（Baseline）；在部分实验中与 ALaST（自适应层选择微调）对比。
- **评估指标**：Top-1 准确率、微调耗时、更新参数比例、推理延迟。
- **训练设置**：AdamW 优化器、余弦退火学习率调度、批大小 32；针对不同模型大小设置了不同学习率和权重衰减。

## 4. 资源与算力
- 论文明确指出：所有实验在单块 NVIDIA V100 GPU 上进行，分配 50 GB 内存。
- 未提供具体训练总时长，但给出了各数据集下各方法的微调耗时（分钟级别），例如 Full fine-tuning 在 Food-101 上为 297.9 分钟，ELA-ViT 为 283.0 分钟。
- ImageNet-1k 实验也提供了训练时间（小时级），如全量训练 43.45 小时，ELA-ViT-50% 为 38.81 小时。

## 5. 实验数量与充分性
- **实验规模**：覆盖 5+ 个图像分类基准（含 ImageNet-1k 大规模验证），3 种 ViT 变体（S/B/L），并额外测试了 DeiT 架构。
- **消融与分析**：包含不同冻结百分比（35%-75%）的帕累托分析、LII 在不同数据集上的 U 形曲线验证、与 ALaST 的对比消融。
- **公平性**：所有实验均基于相同预训练模型、统一微调协议，ELA-ViT 与 ALaST 均使用相同超参数设定（ALaST 沿用原论文设置），比较客观。
- **充分性**：实验覆盖了细粒度、通用、小样本等多种场景，并进行了训练时间和准确率的权衡分析，能够支撑其核心论点。统计稳定性通过 3 个随机种子取平均体现。

## 6. 主要结论与发现
- **层稳定性差异**：ViT 浅层（层 3-4）注意力往往快速收敛，深层（层 7-11）保持高不稳定性，呈现一致的 U 形剖面。
- **方法有效性**：LII 引导的层冻结可在减少微调时间（最高 12.2%）的同时提升或保持准确率（如 ViT-L 在 CUB-200 上提升 6.9%）。
- **效率优势**：相比需学习额外门控网络的 ALaST，ELA-ViT 的无参数 LII 机制在预热后立即释放计算收益，且无精度损失风险。
- **可扩展性**：在 ImageNet-1k 上，ELA-ViT-50% 训练时间减少 10.7%，推理延迟降低 16.7%，精度仅降 0.61%。
- **理论支撑**：LII 不仅与能量间隙有关，也控制注意力分布的 Wasserstein 距离，并与 Fisher 信息矩阵迹建立界，为冻结提供理论保证。

## 7. 优点
- **新颖的理论视角**：将 ViT 层动力学与现代 Hopfield 网络、能量景观及信息几何相联系，提供了有深度的机理解释。
- **轻量无参数决策**：LII 直接源自已有注意力得分，无额外可训练模块，计算开销极小（<1%）。
- **一次决策、即时收益**：与需要持续学习预算的 ALaST 不同，ELA-ViT 在预热后一次性冻结，后续训练无额外梯度计算，效率高。
- **良好的泛化与可组合性**：在多个数据集和模型大小上验证，且可与其他 PEFT 方法（如 Adapter、LoRA）正交叠加。

## 8. 不足与局限
- **稳定性代理的局限性**：使用注意力质量集中度（运行模式）作为表征稳定性的唯一代理，可能忽略其他潜在稳定性信号。
- **依赖历史统计**：需要预热阶段收集 LII 序列，在极低资源或极短微调场景下可能受限。
- **小模型上的潜在风险**：在 ViT-S 的小数据集（如 Beans、CIFAR-10）上出现过正则化，导致精度轻微下降（-1.6%~-2.1%），说明方法对不同容量的模型敏感度不同。
- **超参数敏感性未深入探讨**：尽管声称对滑动窗口长度鲁棒（10~40），但冻结阈值 τ 的选择策略（如中位数比例）可能影响结果，缺少详细消融。
- **仅聚焦图像分类**：尚未拓展到检测、分割等更复杂的视觉任务，以及 NLP 领域的 LLM，实用性有待进一步验证。

（完）
