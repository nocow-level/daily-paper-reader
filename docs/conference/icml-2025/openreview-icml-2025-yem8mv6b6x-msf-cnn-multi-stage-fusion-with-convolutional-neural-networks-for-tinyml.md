---
title: "msf-CNN: Multi-Stage Fusion with  Convolutional Neural Networks for TinyML"
title_zh: msf-CNN：面向TinyML的多阶段卷积神经网络融合
authors: "Zhaolan Huang, Emmanel Baccelli"
date: 2025-01-14
pdf: "https://openreview.net/pdf?id=YEm8MV6b6X"
tags: ["query:edge-llm"]
score: 10.0
evidence: 针对微控制器（MCU）极小内存预算设计高效的CNN融合，用于设备端推理。
tldr: 在TinyML应用中，微控制器（MCU）仅有极小的内存（如128kB RAM），对神经网络模型部署构成极大挑战。本文提出msf-CNN多阶段融合方法，将卷积网络层间的数据流优化问题建模为有向无环图上的搜索，通过高效遍历解空间找出最优融合设置。相较于现有技术，msf-CNN找到了更丰富的可行融合方案，在保持精度的同时显著降低了推理延迟和内存占用，为资源极端受限设备上的CNN推理提供了通用优化框架。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-yem8mv6b6x/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 743, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yem8mv6b6x/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 853, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yem8mv6b6x/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-yem8mv6b6x/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 850, \"height\": 416, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-yem8mv6b6x/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1329, \"height\": 632, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yem8mv6b6x/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1541, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yem8mv6b6x/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yem8mv6b6x/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 894, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-yem8mv6b6x/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1226, \"height\": 808, \"label\": \"Table\"}]"
motivation: 微型微控制器（MCU）内存极小（如128kB RAM），需要极度高效的神经网络架构。
method: 提出msf-CNN技术，通过遍历有向无环图表示的融合空间，找到最优的多阶段融合设置。
result: 与已有CNN融合方法相比，识别出更广泛的可行方案，降低了推理延迟。
conclusion: 为资源极端受限设备上的CNN推理提供了一种通用且高效的优化方法。
---

## Abstract
AI spans from large language models to tiny models running on microcontrollers (MCUs). Extremely memory-efficient model architectures are decisive to fit within an MCU's tiny memory budget e.g., 128kB of RAM. However, inference latency must remain small to fit real-time constraints. An approach to tackle this is *fusion*, which aims to optimize data flows across neural network layers. In this paper, we introduce *msf-CNN*, a novel technique that efficiently finds optimal fusion settings for convolutional neural networks (CNNs) by walking through the fusion solution space represented as a directed acyclic graph. Compared to previous work on CNN fusion for MCUs, msf-CNN identifies a wider set of solutions. We published an implementation of msf-CNN running on various microcontrollers (ARM Cortex-M, RISC-V, ESP32). We show for instance that msf-CNN achieves inference using 50\% less RAM compared to the prior art (MCUNetV2 and StreamNet). msf-CNN thus offers additional flexibility for system designers.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在微型微控制器（MCU，如128 kB RAM）上部署卷积神经网络（CNN）时，极度受限的内存资源（RAM）与CNN的高内存占用之间存在巨大鸿沟，同时推理延迟必须满足实时性要求。已有的层融合技术虽然能减少内存使用，但仍存在中间特征图重计算开销高、输入尺寸受限、以及实现与硬件/模型强绑定等问题。
- **整体含义**：论文旨在提供一个更通用、更高效的融合优化方法——msf-CNN，通过系统化地探索多阶段融合解空间，在满足用户定义的计算或内存约束下，显著降低峰值RAM使用，并适配多种MCU架构与CNN模型，为TinyML系统设计者提供新的灵活权衡空间。

## 2. 论文提出的方法论

- **核心思想**：
  - 将CNN推理过程中的层融合问题建模为两个对偶优化问题：**P1** – 在计算开销上限 \(F_{\text{max}}\) 下最小化峰值RAM；**P2** – 在峰值RAM上限 \(P_{\text{max}}\) 下最小化计算开销。
  - 将融合后的CNN表示为**有向无环图（DAG）**，节点为张量，边为单层算子或多层融合块，边的权重编码了对应的RAM使用量与MAC操作数。
  - 通过图上的最短路径/最小最大路径算法结合剪枝策略高效求解，将搜索复杂度从 \(O(2^{V-2})\) 降至 \(O(V^2)\)。
  - 实现中进一步采用了**迭代式全局池化**与**迭代式全连接层**，在不增加计算量的前提下进一步压缩内存。
- **关键技术细节**：
  - **缓存方案**：选用H-Cache（水平方向缓存，垂直方向重计算），缓存大小 \(Buf_i = t_i \times k_i \times cin_i\)。
  - **图构建**：对于n层连续卷积，所有可能的融合块均作为“跳跃边”加入图中。
  - **编码**：边的RAM使用量 \(P_{e_i} = I + O + Buf\)；计算开销为各边MAC之和；总峰值RAM取路径上各边最大值；计算开销因子 \(F = C_S / C_{vanilla}\)。
  - **P1求解**：迭代构造子图 \(G_i\)（每次删除最大RAM边），在子图中求最短路径（最小MAC）作为候选解，从中筛选满足 \(F_{\text{max}}\) 且RAM最小的解。
  - **P2求解**：直接删除RAM超过 \(P_{\text{max}}\) 的边，再求最短路径。
  - **迭代算子**：全局池化逐元素迭代更新；全连接将输入向量拆分为单个元素，依次乘加权重列，减少输入缓冲需求。
- **算法流程**：解析模型 → 构建带权DAG → 根据约束（P1或P2）执行图搜索 → 生成融合配置 → 通过microTVM重写计算图并编译部署。

## 3. 实验设计

- **使用模型（数据集/场景）**：
  - MobileNetV2 (width multiplier 0.35, 输入144×144×3)
  - MCUNetV2-VVW-5fps (输入80×80×3, 视觉唤醒词)
  - MCUNetV2-320KB-ImageNet (输入176×176×3)
- **对比基准与方法**：
  - 未融合的原始模型（Vanilla）
  - 已有的MCU融合方法：MCUNetV2、StreamNet-2D
- **硬件平台**：
  - ARM Cortex-M7/M4 (STM32F767ZI, STM32F746NG, STM32F412ZG)
  - Xtensa (ESP32-S3)
  - RISC-V (ESP32-C3, SiFive FE310-G002)
- **评估指标**：峰值RAM占用（kB）、推理延迟（ms），以及在给定 \(F_{\text{max}}\) 或 \(P_{\text{max}}\) 下的实际表现。

## 4. 资源与算力

- 论文未提及任何训练过程或GPU使用，所有工作均为**推理阶段**的编译优化与在物理MCU板上的测量。因此，本文未涉及神经网络训练所需的算力资源。

## 5. 实验数量与充分性

- **实验组数**：
  - 分析性实验（表1）：3个模型 × 多组 \(F_{\text{max}}\)（1.1–∞）及 \(P_{\text{max}}\)（16–256 kB），探索理论解空间。
  - 实测实验（表3、4）：3个模型在6种MCU上的最小RAM峰值与对应的延迟。
  - 约束实测实验（表5）：在特定MCU (Nucleo-f767zi) 上，对3个模型测试了 \(F_{\text{max}}\) 从1.1到∞ 和 \(P_{\text{max}}\) 从16 kB到256 kB的多个条件，给出实际RAM与延迟。
  - 总计覆盖了**3个模型、6种MCU硬件、多个约束级别**，对比了2种主流方法。
- **充分性与公平性**：
  - 实验在**相同MCU硬件和软件栈**上复现对比方法，保证了公平性。
  - 实验系统性地展示了不同约束下的权衡，支撑了论文主张。
  - **明显不足**：所有实验**未评估融合对模型精度（准确率）的影响**，只聚焦于资源效率；同时未与更多种类的融合缓存策略或模型架构进行对比。

## 6. 论文的主要结论与发现

- msf-CNN能在保证用户指定约束的前提下，找到比已有方法**RAM使用降低50%以上**的融合配置（例如，MBV2-w0.35峰值RAM降至8.56 kB，而MCUNetV2为63 kB）。
- 通过多阶段融合与图优化手段，msf-CNN提供了**更广泛的解集**，实现了**延迟与内存之间更灵活的权衡**。
- 迭代式全局池化和全连接层可进一步压缩RAM而**无额外计算开销**。
- 方法具备**硬件普适性**，在ARM Cortex-M、RISC-V、Xtensa等多类MCU上均可部署。

## 7. 优点

- **方法论创新**：首次将CNN多阶段融合问题形式化为DAG上的约束最短路径问题，并用剪枝策略显著降低搜索复杂度。
- **系统实现完善**：基于microTVM和RIOT-ML，提供了开源实现，并适配多种MCU架构。
- **实际效果显著**：在最小RAM配置下，相较最先进方法内存减少65%~87%，且能够在仅16 kB RAM的SiFive板上运行MBV2-w0.35。
- **实用性强**：直接为用户提供对偶优化接口（给定延迟找最小内存，或给定内存找最快推理），贴合实际部署需求。

## 8. 不足与局限

- **精度缺失**：论文未报告任何融合后模型的**准确率/分类精度变化**，无法判断资源节省是否以牺牲任务性能为代价。
- **参数空间有限**：当前搜索仅优化融合块的位置与深度，**输出元素数固定为1**；未探索不同的缓存策略（仅H-Cache），可能遗漏更优配置。
- **架构支持面窄**：仅针对**CNN**，未涉及Transformer、RNN等现代网络结构。
- **计算建模与实测差距**：理论MAC比值 \(F\) 与实际延迟之比存在偏差（受Flash读取延迟等影响），约束设置不够精确。
- **实验规模与普适性**：
  - 仅测试了3个模型，均为MobileNet/MCUNet系列，缺乏更广泛CNN结构的验证。
  - 未与其他内存优化方法（如vMCU、MoDEL等非融合方法）进行综合对比。
  - 缺乏对实时性和功耗的详细分析。

（完）
