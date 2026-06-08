---
title: "msf-CNN: Patch-based Multi-Stage Fusion with Convolutional Neural Networks for TinyML"
title_zh: msf-CNN：面向TinyML的基于块的CNN多阶段融合
authors: "Zhaolan Huang, Emmanuel Baccelli"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=fgW3IZzxmE"
tags: ["query:edge-llm"]
score: 9.0
evidence: 通过块融合优化MCU上CNN的数据流，实现高效端侧推理
tldr: 针对MCU上CNN推理面临的内存与延迟约束，msf-CNN通过有向无环图表示融合解空间，高效搜索最优的块融合配置。实验表明，相比先前工作，msf-CNN能发现更广泛的解集，显著提升极低资源设备上的推理效率。该方法为TinyML场景下的CNN部署提供了关键优化手段。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-fgw3izzxme/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1432, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fgw3izzxme/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 680, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fgw3izzxme/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 345, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-fgw3izzxme/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1394, \"height\": 661, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-fgw3izzxme/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1373, \"height\": 637, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fgw3izzxme/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1411, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fgw3izzxme/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 659, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fgw3izzxme/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 706, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fgw3izzxme/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 881, \"height\": 146, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-fgw3izzxme/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1181, \"height\": 746, \"label\": \"Table\"}]"
motivation: MCU的极小内存（如128kB RAM）和实时约束要求CNN架构极致高效。
method: 将融合解空间建模为有向无环图，通过图遍历搜索最优块融合配置。
result: 找到了比先前工作更广的融合解，提升了CNN在MCU上的推理性能。
conclusion: msf-CNN显著推进了CNN在微控制器上的能效，为TinyML部署提供了实用工具。
---

## Abstract
AI spans from large language models to tiny models running on microcontrollers (MCUs). Extremely memory-efficient model architectures are decisive to fit within an MCU's tiny memory budget e.g., 128kB of RAM. However, inference latency must remain small to fit real-time constraints. An approach to tackle this is *patch-based fusion*, which aims to optimize data flows across neural network layers. In this paper, we introduce *msf-CNN*, a novel technique that efficiently finds optimal fusion settings for convolutional neural networks (CNNs) by walking through the fusion solution space represented as a directed acyclic graph. Compared to previous work on CNN fusion for MCUs, msf-CNN identifies a wider set of solutions. We published an implementation of msf-CNN running on various microcontrollers (ARM Cortex-M, RISC-V, ESP32).  We show that msf-CNN can achieve inference using 50% less RAM compared to the prior art (MCUNetV2 and StreamNet). We thus demonstrate how msf-CNN offers additional flexibility for system designers.

---

## 论文详细总结（自动生成）

### 研究动机与核心问题
随着人工智能物联网的兴起，将深度神经网络部署到资源极度受限的微控制器上已成为关键需求。然而，深度神经网络对计算和内存（RAM）的巨大需求与微控制器通常仅有几十到几百KB RAM的硬件条件之间存在尖锐矛盾。例如，一个量化的ResNet-34模型中的单个卷积层就可能消耗超过400KB的RAM，远超许多物联网设备的内存预算。现有的解决方案如MCUNetV2和StreamNet虽然通过基于块的层融合技术来降低内存占用，但仍存在中间特征图重计算开销高、输入尺寸受限、硬件平台绑定性强等问题。本文的核心问题是如何在微控制器上，通过一种更优的多阶段块融合策略，在满足严格推理延迟或内存约束的前提下，最大限度地降低卷积神经网络推理的峰值RAM使用量。

### 方法论：核心思想与关键技术
msf-CNN提出了一种自动寻找卷积神经网络最优块融合配置的通用技术，其核心思想是将融合方案的搜索空间建模为一个**有向无环图（DAG）**，并通过图论算法高效求解。

- **问题建模**：论文定义了一对对偶优化问题。**P1**是在计算开销（以乘加操作MACs为指标）不超过给定上限的约束下，最小化峰值RAM使用量；**P2**则是在峰值RAM不超过给定上限的约束下，最小化计算开销。整个卷积神经网络被视为一个有向无环图 \( G = (V, E) \)。节点 \( V \) 代表输入/输出特征图张量，边 \( E \) 则代表单个网络层（如卷积层）或一个由多层组成的融合块。每条边被编码了该操作（或融合块）所需的RAM使用量和MAC计算量。
- **搜索与剪枝**：寻找满足约束的最优融合配置被转化为在有向无环图中寻找最优路径（如最小-最大路径或最短路径）及其变体问题。为应对无约束条件下指数级爆炸的搜索空间，msf-CNN设计了剪枝策略。例如，对于问题P1，算法迭代地从图中移除具有当前最大RAM使用量的边，并在新的子图上求解MAC最短路径，直至找到满足计算约束的解，将复杂度从 \(O(2^{V-2})\) 降至 \(O(V^3)\)。所有最优路径搜索均使用经典Dijkstra算法。该搜索过程在部署前的PC上离线完成。
- **缓存与计算模型**：msf-CNN选用了**H-Cache（水平缓存）** 方案，即在融合块内仅在水平方向缓存部分重叠区域，以在缓存大小和重计算量之间取得平衡。论文给出了融合块内每层缓存大小 \(Buf_i = t_i \times k_i \times cin_i\) 和总体乘加操作数 \(C_{layer} = N_{tile} \times O_{tile} \times k^2 \times c_{out}\) 的计算公式，并以此作为图边权重编码的基础。
- **额外内存优化**：除了融合卷积层，msf-CNN还引入了**迭代式计算**来进一步压缩全局池化层和全连接层的RAM使用量。对于全局池化，它逐元素接收输入并迭代更新结果，而非一次性加载整个特征图。对于全连接层，它将权重矩阵按列切分，每次仅处理一个输入元素并累加部分和。

### 实验设计
- **使用模型与数据集**：实验选取了三个具有代表性的轻量级卷积神经网络模型：MobileNetV2（宽度系数0.35，输入尺寸144x144x3）、MCUNetV2-VVW-5fps（输入尺寸80x80x3）和MCUNetV2-320KB-ImageNet（输入尺寸176x176x3）。这些模型已在AIoT领域被广泛用作骨干网络。为验证精度无损，额外在ImageNet和Visual Wake Words数据集上进行了Top-1准确率测试。
- **硬件平台**：为展示硬件通用性，实验覆盖了基于ARM Cortex-M、Espressif Xtensa和RISC-V三种主流32位微控制器架构的六款开发板，具体型号见下表。

| 开发板型号 | 微控制器芯片 | CPU 核心与频率 | RAM (KB) |
| :--- | :--- | :--- | :--- |
| Nucleo-f767zi | STM32F767ZI | Cortex-M7 @ 216 MHz | 512 |
| Stm32f746g-disco | STM32F746NG | Cortex-M7 @ 216 MHz | 320 |
| Nucleo-f412zg | STM32F412ZG | Cortex-M4 @ 100 MHz | 256 |
| esp32s3-devkit | ESP32-S3-WROOM-1N8 | Xtensa @ 240 MHz | 512 |
| esp32c3-devkit | ESP32c3-1-MINI-M4N4 | RISC-V @ 160 MHz | 384 |
| hifive1b | SiFive FE310-G002 | RISC-V @ 320 MHz | 16 |

- **对比方法**：主要对比了两个最先进的同类工作——**MCUNetV2**和**StreamNet（StreamNet-2D）**。基准线为**未融合的原始模型**。
- **评估指标**：核心评估指标为**峰值RAM使用量（kB）** 和**推理延迟（ms）**，并通过不同约束下的帕累托曲线展示两者的权衡关系。

### 资源与算力
论文的核心算法（最优融合配置搜索）是**离线执行**的，其计算复杂度为 \(O(V^3)\)，对于微控制器上运行的深度神经网络而言，作者指出该过程可在数秒内完成。这说明搜索本身所需的计算资源极少，在普通PC上即可胜任。论文并未提及使用特定的大型GPU资源来进行此项搜索。

### 实验数量与充分性
实验设计相当全面与充分：
1.  **多模型、多硬件**：在3个模型、6款不同架构和RAM容量的MCU板上验证了RAM和延迟数据。
2.  **多维度约束分析**：系统性地探索了问题P1和P2在不同约束下的结果。P1实验将计算开销上限（Fmax）从1.1设置到无穷大；P2实验将RAM上限从16kB设置到256kB，每组都提供了分析解和实测值。
3.  **全面的对比**：与vaniila、MCUNetV2和StreamNet进行了详细的横向对比，涵盖了极端低RAM、不同RAM预算和不同计算预算等多种场景。
4.  **公平性考量**：为与高度依赖ARM CMSIS-NN库的StreamNet进行公平比较，msf-CNN额外实现了CMSIS后端并给出了对应的性能数据。
5.  **一致性验证**：对比了表1中的理论分析结果与图4/表6中的实际板卡测量结果，验证了优化器的正确性。同时，补充了精度无损的验证实验，确保优化不影响模型输出。

### 主要结论与发现
1.  **显著降低内存占用**：在不考虑计算约束的极限情况下，msf-CNN能将峰值RAM使用量相比传统CNN降低超过90%，比MCUNetV2和StreamNet进一步减少约50%-87%，甚至能让MobileNetV2模型运行在仅有16kB RAM的SiFive开发板上。
2.  **提供灵活的内存-计算权衡**：msf-CNN通过双优化器（P1/P2），能够精确地在用户设定的内存或延迟约束内，找到一系列处于帕累托前沿的融合配置，为系统设计师提供了前所未有的灵活性。
3.  **硬件通用性强**：msf-CNN生成的代码不依赖特定硬件指令集，成功部署在ARM、RISC-V和ESP32等多种微控制器架构上，并可选地集成了CMSIS-NN库以在ARM平台上实现更优性能。
4.  **解的质量更优**：与MCUNetV2仅融合模型头部的启发式策略相比，msf-CNN通过全局搜索能发现更优的多阶段融合方案，即在相同内存下延迟更低，或在相同延迟下内存更小。

### 优点
- **创新的问题建模方法**：将融合优化问题巧妙地转化为有向无环图的最短路径问题，并设计了高效的剪枝算法，使得在多项式时间内找到最优解成为可能，理论清晰。
- **极佳的平台通用性**：实现与特定硬件和指令集解耦，显著优于前序工作中的硬件绑定问题，具有很高的实用价值。
- **精细的优化手段**：对全局池化和全连接层的迭代计算优化是对融合策略的有效补充，进一步挤压了内存占用。
- **实验全面扎实**：在多种模型、多款MCU上，与当前最优方法进行了多维度、公平的对比，结果有力支撑了核心论断。

### 不足与局限
1.  **搜索空间受限**：当前的优化器仅探索融合块的位置和深度，而融合块每次迭代输出的元素数量固定为1。作者承认该参数对计算和内存有显著影响，但并未纳入搜索空间。缓存策略也仅限于H-Cache一种。
2.  **模型结构局限**：目前仅支持卷积神经网络架构。作者已在附录中探讨向RNN/LSTM/GRU和Transformer架构的扩展，但尚未完整实现，特别是对Transformer的优化空间有限。
3.  **计算开销估算与实测偏差**：优化器基于乘加操作数估算计算开销，但实际延迟还包含访存（如从闪存读取权重）等I/O开销。这导致实际测得的延迟开销比（F值）高于设定值，尤其在极端融合配置下更为明显。
4.  **未涵盖的优化层面**：本文的量化分析证明了融合的解空间有效，但并未涉及模型精度、或能量消耗的详细影响。能量消耗仅初步评估为与延迟线性相关。

（完）
