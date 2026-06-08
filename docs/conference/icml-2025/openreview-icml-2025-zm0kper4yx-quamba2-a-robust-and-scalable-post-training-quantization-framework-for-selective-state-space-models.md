---
title: "Quamba2: A Robust and Scalable Post-training Quantization Framework for Selective State Space Models"
title_zh: Quamba2：一种面向选择性状态空间模型的鲁棒可扩展后训练量化框架
authors: "Hung-Yueh Chiang, Chi-Chih Chang, Natalia Frumkin, Kai-Chiang Wu, Mohamed S. Abdelfattah, Diana Marculescu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Zm0Kper4yx"
tags: ["query:edge-llm"]
score: 9.0
evidence: 针对资源受限设备的状态空间模型量化框架
tldr: 针对状态空间模型在云服务和资源受限设备上的部署挑战，提出Quamba2量化框架，通过鲁棒的后训练方案适应不同位宽配置（如W4A8/W4A16），在保持性能的同时减少模型尺寸并利用硬件加速。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1621, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1436, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 716, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1777, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 720, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1736, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1774, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 684, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 696, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zm0kper4yx/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1763, \"height\": 603, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 842, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 841, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 723, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 681, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 811, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 755, \"height\": 421, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 586, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 779, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1732, \"height\": 1539, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 529, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zm0kper4yx/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 850, \"height\": 290, \"label\": \"Table\"}]"
motivation: 大规模SSM部署面临挑战，量化是有效手段，但对量化误差敏感。
method: 提出后训练量化框架，兼顾不同位宽需求，降低误差影响。
result: 实现多种位宽下的高效推理，适用于云和个人设备。
conclusion: Quamba2为SSM的高效部署提供了灵活鲁棒的量化解决方案。
---

## Abstract
State Space Models (SSMs) are gaining attention as an efficient alternative to Transformers due to their constant memory complexity and comparable performance. Yet, deploying large-scale SSMs on cloud-based services or resource-constrained devices faces challenges. To address this, quantizing SSMs using low bit-width data types is proposed to reduce model size and leverage hardware acceleration. Given that SSMs are sensitive to quantization errors, recent advancements focus on quantizing a specific model or bit-width to improve their efficiency while maintaining performance. However, different bit-width configurations, such as W4A8 for cloud service throughput and W4A16 for improving question-answering on personal devices, are necessary for specific scenarios.
To this end, we present Quamba2, compatible with \textbf{W8A8}, \textbf{W4A8}, and \textbf{W4A16} for both \textbf{Mamba} and \textbf{Mamba2}, addressing the rising demand for SSM deployment across various platforms. We propose an offline approach to quantize inputs of a linear recurrence in 8-bit by sorting and clustering for $x$, combined with a per-state-group quantization for $B$ and $C$. To ensure compute-invariance in the SSM output, we offline rearrange weights according to the clustering sequence. The experiments show Quamba2-8B outperforms several state-of-the-art SSMs quantization methods and delivers 1.3$\times$ and 3$\times$ speedup in the pre-filling and generation stages and 4$\times$ memory reduction with only a $1.6$% accuracy drop on average. The code and quantized models will be released at:

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景与动机**：状态空间模型（SSMs），尤其是 Mamba1 和 Mamba2，以恒定的内存复杂度和与 Transformer 可比的效果，成为序列建模的高效替代方案。然而，大规模 SSMs 在云服务和资源受限的边缘设备上的部署面临巨大挑战。
- **现存问题**：模型量化（如 W8A8、W4A8）是降低存储和计算需求的关键手段，但 SSMs 的线性递归部分对量化产生的误差极为敏感。现有的 SSM 量化工作（如 MambaQuant、Quamba）要么仅支持单一模型或位宽（如仅 W8A8），要么在更低比特（如 W4A8）下性能下降严重，无法满足多样化部署场景（例如 W4A8 提升云端吞吐，W4A16 加速单人短提示生成）的需求。
- **整体含义**：本文提出 **Quamba2**，一个鲁棒且可扩展的后训练量化框架，旨在为 Mamba1 和 Mamba2 提供 **W8A8、W4A8、W4A16** 多种位宽支持，同时覆盖从嵌入层到输出头的全链路（head‑to‑toe）量化，从而适配云端和边缘多种平台。

## 2. 方法论

### 2.1 核心观察
基于 SSM 计算的两个关键特性：
- **通道顺序保持**（channel order preserving）：SSD 计算为逐通道操作，输出通道的顺序与输入一致。
- **激活持久性**（activation persistence）：SSM 输入 \(x\) 的通道幅值分布以及输入依赖参数 \(B, C\) 的激活状态（活跃通道/状态组）在时间步和不同样本间保持稳定。

### 2.2 关键技术细节

#### a) Sort‑and‑Cluster（排序聚类量化，针对 \(x\)）
- 利用通道持久性，先通过校准集获取每个通道的最大值，再对 Head 进行排序，使相似特征的 Head 聚集。
- 对排序后的 Head 进行聚类（例如分为 \(m=4\) 组），然后在每个 Head 组内对通道再次聚类（例如分为 \(n=4\) 组）。
- 为每个 Head‑通道组合计算一个独立的量化步长（共 \(m \times n\) 个缩放因子），从而在 8‑bit 精度下更好地捕捉 \(x\) 的分布，减小量化误差。

#### b) Per‑State‑Group 量化（针对 \(B\) 和 \(C\)）
- 观察发现 \(B\) 和 \(C\) 矩阵中仅有部分状态组（state group）被持续激活，且其值域范围在各组间差异悬殊。
- 采用按状态组分配量化缩放因子的方式，对值域较小的组使用更精细的步长，显著提升 \(B, C\) 的量化精度。

#### c) Cluster‑Aware Weight Reordering（离线权重重排）
- 为保证计算一致性，根据排序和聚类的索引，离线重新排列输入投影、因果卷积、归一化、输出投影等权重的行列顺序，使得在线激活的排序与权重排序匹配，不增加额外在线开销。

#### d) 离线 Hadamard 矩阵融合
- 将 Hadamard 变换融合到投影层的权重矩阵中（\(W_{in}H^{\top}\)，\(H W_{out} H^{\top}\)），配合在线 Hadamard 量化消除异常值，同时保证块输出不变（compute‑invariance）。

#### e) 高效 4‑bit/8‑bit 内核与全链路量化
- 针对投影层、因果卷积、SSD 扫描等实现定制 CUDA 内核，支持 W8A8/W4A8/W4A16 权重与激活。
- 对嵌入层和输出 Head 同样进行 4‑bit/8‑bit 量化，达成 head‑to‑toe 量化，最大化内存节省。

### 2.3 算法流程概述
1. 校准阶段：使用少量数据收集激活统计量，确定排序索引与聚类结果，计算各组的静态缩放因子。
2. 权重重排与 Hadamard 融合：离线修改模型权重，使其按照排序聚类后的激活通道序存储。
3. 推理阶段：激活 \(x\) 按预先排序聚类顺序生成并分组量化；\(B, C\) 按状态组分别量化；线性递归和 SSD 计算中加载对应 8‑bit 状态，实现低比特运算。

## 3. 实验设计

- **评测数据集**：
  - 零样本下游任务：LAMBADA、HellaSwag、PIQA、ARC‑easy、ARC‑challenge、WinoGrande（采用 Mamba 论文的评测协议，HellaSwag 和 ARC‑challenge 按长度归一化）。
  - 大规模多任务数据集：MMLU（5‑shot），用于检验泛化性和鲁棒性。
  - 生成任务：Natural Questions 和 SQuAD v2。
- **Baselines**：主要对比 MambaQuant（W8A8、W4A8）和 Quamba（W8A8）两个专门针对 SSM 的后训练量化方法。
- **测试环境**：云端显卡 Nvidia A5000（24GB）和边缘设备 Nvidia Orin Nano 8G，测量 TPOT（每 token 生成时间）、TTFT（首 token 时间）和内存占用。

## 4. 资源与算力

- 论文属于后训练量化（PTQ），**校准过程仅需随机抽取 Pile 数据集中的 512 个句子**，无需大量训练计算。
- 量化后的模型部署与延迟测试在 **A5000** 和 **Orin Nano 8G** 上进行，但未提及校准或搜索过程占用的 GPU 小时数或具体训练时长。
- 用于混合精度搜索的进化算法相对轻量（种群 40、5 代），但同样没有给出确切的算力消耗指标。
- 总体而言，**论文没有报告具体的训练/校准算力总数**，但 PTQ 方法本身决定了其对算力需求极低。

## 5. 实验数量与充分性

- **模型与位宽组合丰富**：涵盖 Mamba1‑1.4B/2.8B 和 Mamba2‑2.7B/8B，每种模型均测试 W8A8、W4A8、W4A16 三种配置，共计约 20 组主要结果。
- **多任务对比**：在六项零样本任务上取五轮平均，与两个 baseline 进行系统对比；还专门在 MMLU 上评估泛化能力，并对比了纯 W4A8、纯 W4A16 以及手工和自动搜索的混合精度 W4A{X}。
- **消融实验完备**：
  - W4A8 设置下逐步添加 Hadamard、Per‑Group、GPTQ、Per‑State‑Group、Sort‑and‑Cluster，清晰展示各模块贡献。
  - W4A16 设置下对比 Per‑Group 与 GPTQ，验证 Hadamard 的关键作用。
  - 嵌入层和输出 Head 量化的单独消融。
- **系统性能分析**：大量批次大小下的延迟、内存占用、Roofline 模型分析，验证不同位宽在不同并发规模下的优势。
- **生成任务补充**：额外报告 NQ 和 SQuAD v2 分数，证明 8‑bit 缓存状态的有效性。
- 实验设计全面、对比公平，充分验证了方法的有效性和鲁棒性。

## 6. 主要结论与发现

- Quamba2 在两个 Backbone 上均实现了 W8A8、W4A8、W4A16 的头部到头部量化，且精度损失极小（如 Mamba2‑8B 平均准确率仅降 1.6%）。
- **Sort‑and‑Cluster** 和 **Per‑State‑Group 量化** 是弥补 SSM 量化精度损失的关键，大幅优于传统的组量化或 GPTQ。
- 框架提供了显著的**实际加速和内存缩减**：在 A5000 上 W4A8 模型预填充加速 1.39×、生成加速 3.05×，内存减少 4×；并成功将 Mamba2‑8B 部署在仅 8GB 内存的 Orin Nano 上（约 13 tokens/s）。
- 纯 W4A8 在大型推理任务（MMLU）上存在泛化能力下降，而通过进化搜索自动混合 W4A8/W4A16 可恢复 2.9% 准确率，且只增加少量预填充延迟。
- 8‑bit 量化缓存 SSM 状态是可行且高效的，在批次增大时能显著降低内存与状态更新延迟。

## 7. 优点

- **广泛的适配性**：同时支持 Mamba1/Mamba2 和 W8A8/W4A8/W4A16，满足从云端到边缘的多样化部署需求。
- **创新的量化策略**：基于 SSM 特有的通道和状态持久性，设计 sort‑and‑cluster 和 per‑state‑group 量化，针对性解决 SSM 的量化敏感问题。
- **真正的端到端加速**：提供高效的 CUDA 内核，并实现 head‑to‑toe 量化，不仅指标漂亮，还在真实硬件上获得可观的吞吐提升和内存缩减。
- **可部署性验证**：在边缘设备（Orin Nano 8G）上完成 8B 模型的部署与生成测试，证明了其实用价值。
- **系统的实验与消融**：从多个维度验证了各模块的必要性，并深入分析了不同批次大小下的性能表现及泛化能力，实验扎实且具有说服力。

## 8. 不足与局限

- **泛化性局限**：W4A8 纯配置在 MMLU 上的表现显示，低位宽对多步推理等复杂任务的泛化仍有损害，混合精度虽能缓解但增加了设计复杂度。
- **依赖校准数据分布**：排序聚类和缩放因子依赖校准集，对于分布外数据可能出现精度波动，文中未深入分析。
- **未与更广泛的 LLM 量化方案对比**：主要对比了 MambaQuant 和 Quamba，缺乏与通用 LLM 量化方法（如 AWQ、SmoothQuant 在 SSM 上的适配版）的系统比较，但该点也受限于 SSM 的特殊结构。
- **模型规模有限**：实验最大为 8B 参数，对于更大规模（如数十 B）的 Mamba 模型，框架的扩展性和性能有待验证。
- **延迟开销**：W4A8/W4A16 的反量化过程仍引入额外的预填充延迟（如 TTFT 慢于 FP16），在推理时序严格的应用中可能受限。
- **资源报告不完整**：未提供校准、搜索等步骤的精确算力/时间开销，不利于其他研究者完全复现资源成本。

（完）
