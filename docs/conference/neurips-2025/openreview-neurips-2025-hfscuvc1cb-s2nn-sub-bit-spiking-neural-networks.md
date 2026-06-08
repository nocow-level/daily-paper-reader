---
title: "S$^2$NN: Sub-bit Spiking Neural Networks"
title_zh: S²NN：亚位脉冲神经网络
authors: "Wenjie Wei, Malu Zhang, Jieyuan Zhang, Ammar Belatreche, Shuai Wang, Yimeng Shan, Hanwen Liu, Honglin Cao, Guoqing Wang, Yang Yang, Haizhou Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=hFsCuVc1cB"
tags: ["query:edge-llm"]
score: 7.0
evidence: 用少于1比特表示权重，进一步挖掘SNN的压缩和加速潜力
tldr: 提出亚位脉冲神经网络，利用聚类模式和离群值感知量化将权重压缩至小于1比特，进一步挖掘脉冲神经网络的压缩和加速潜力，适用于资源有限的部署场景。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-hfscuvc1cb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-hfscuvc1cb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1397, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-hfscuvc1cb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1439, \"height\": 484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-hfscuvc1cb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1342, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-hfscuvc1cb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1362, \"height\": 764, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-hfscuvc1cb/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1420, \"height\": 385, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1456, \"height\": 1144, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 676, \"height\": 592, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 723, \"height\": 603, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 874, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 975, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1420, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1256, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1439, \"height\": 138, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1271, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1481, \"height\": 1520, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1007, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hfscuvc1cb/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1413, \"height\": 537, \"label\": \"Table\"}]"
motivation: 二进制SNN的存储和计算需求仍很大，需进一步压缩。
method: 基于训练好的二进制SNN核的聚类模式建立基线，设计离群值感知亚位权重量化方法。
result: 亚位表示实现了比二进制SNN更高的压缩率，同时保持精度。
conclusion: S²NN为SNN在资源受限设备上的高效部署提供了新的压缩范式。
---

## Abstract
Spiking Neural Networks (SNNs) offer an energy-efficient paradigm for machine intelligence, but their continued scaling poses challenges for resource-limited deployment. Despite recent advances in binary SNNs, the storage and computational demands remain substantial for large-scale networks. To further explore the compression and acceleration potential of SNNs, we propose Sub-bit Spiking Neural Networks (S$^2$NNs) that represent weights with less than one bit. Specifically, we first establish an S$^2$NN baseline by leveraging the clustering patterns of kernels in well-trained binary SNNs. This baseline is highly efficient but suffers from \textit{outlier-induced codeword selection bias} during training. To mitigate this issue, we propose an \textit{outlier-aware sub-bit weight quantization} (OS-Quant) method, which optimizes codeword selection by identifying and adaptively scaling outliers. Furthermore, we propose a \textit{membrane potential-based feature distillation} (MPFD) method, improving the performance of highly compressed S$^2$NN via more precise guidance from a teacher model. Extensive results on vision reveal that S$^2$NN outperforms existing quantized SNNs in both performance and efficiency, making it promising for edge computing applications.

---

## 论文详细总结（自动生成）

好的，请查收以下关于论文《S²NN: Sub-bit Spiking Neural Networks》的结构化总结。

### 1. 论文的核心问题与整体含义

- **核心问题**：脉冲神经网络（SNNs）凭借其事件驱动的特性，被认为是一种高能效的机器学习范式。然而，为了满足实际应用的性能需求，SNN模型规模正不断扩大，这导致其**存储和计算需求急剧增加**，给资源有限的边缘设备部署带来了巨大挑战。
- **当前局限**：尽管现有的二进制SNN（BSNN）通过将权重限制为1比特（-1和+1）来实现轻量化，但对于大规模网络而言，其**计算负担仍然沉重**。
- **整体含义**：本文旨在**进一步挖掘SNN的压缩和加速潜力**，提出“亚位脉冲神经网络”（S²NN），其核心思想是**用少于1比特来表示网络权重**，从而实现比BSNN更高的压缩率和更快的推理速度，为SNN在边缘计算场景下的高效部署提供了新的可能。

### 2. 论文提出的方法论

- **核心思想**：S²NN的核心思想源于一个关键观察：在训练有素的BSNN中，二值化卷积核在不同层内呈现出显著的**聚类模式**。即，对于一个$3 \times 3$的卷积核，所有可能的512（$2^9$）种组合中，只有少数一部分会被频繁使用。S²NN通过只存储和使用这一小部分核（紧凑码书）来编码权重，从而实现低于1比特的压缩。
- **关键技术细节**：
    1.  **S²NN基线模型（Baseline）**：
        -   **压缩与存储**：为每一层构建一个规模为$2^\eta$（$\eta < k_w \cdot k_h$，例如$\eta=4,5,6$）的紧凑码书（`Compact Codebook`）。对于第$\ell$层的一个32位浮点核 $\mathbf{w}^\ell_{f,c}$，在前向传播时，计算其与码书中每个码字（codeword）的平方$L_2$距离，选择距离最近的码字作为其二进制表示 $\mathbf{w}^\ell_{b,c}$。这样，原本需要$k_w \cdot k_h$比特存储的核，现在只需用1个$\eta$比特的索引来指代，从而实现了约$\eta/(k_w \cdot k_h)$倍的压缩率（例如，$3 \times 3$核在$\eta=4$时，每个参数仅需0.44比特）。
    2.  **离群值感知亚位权重量化（OS-Quant）**：
        -   **问题**：基线模型在计算浮点核与码字的距离时，容易受到**离群值（outlier）** 的影响。离群值会主导距离计算，导致选出的码字无法准确反映核中大多数元素的符号模式，从而产生“码字选择偏差”（quantization error）。
        -   **解决方法**：
            a. **IQR基线检测**：对每个32位核，计算其四分位距（IQR，Q3 - Q1），并根据`Tukey's fences`法则（`[Q1 - 1.5*IQR, Q3 + 1.5*IQR]`）判定该核内部的离群值。
            b. **空间感知放缩**：对于检测到的离群值，计算其与空间邻域内其他元素的平均绝对差 $\Omega_{i,j}$，然后将该离群值按$1/\Omega_{i,j}$的比例进行放缩。这消除了离群值对距离计算的主导，同时保留了原始核的空间特征。
            c. **最终量化**：用调整后的核 $\widehat{\mathbf{w}}^\ell_{f,c}$ 去选择码书中的码字，实现更优的权重映射（详见公式13）。
    3.  **基于膜电位的特征蒸馏（MPFD）**：
        -   **问题**：高度压缩的S²NN基线模型存在性能下降。
        -   **解决方法**：提出一种新的知识蒸馏框架，用性能更强的全精度教师模型来指导学生模型（S²NN）训练。
            -   **精度优化**：不同于传统的基于发放率的特征蒸馏（FRFD），MPFD直接计算教师和学生模型**膜电位**的归一化Gram矩阵之间的$L_2$距离（公式15 & 16）。这避免了梯度经过复杂的代理梯度函数，从而为反向传播提供了更精确的优化方向。
            -   **架构灵活性**：由于使用了内积形式的Gram矩阵，该蒸馏方法可以在维度不匹配的层对之间进行，支持跨架构知识迁移。

### 3. 实验设计

- **数据集与场景**：
    - **图像分类**：CIFAR-10、CIFAR-100、ImageNet-1K、DVS-CIFAR10（神经形态数据集）。
    - **目标检测**：COCO 2017。
    - **语义分割**：ADE20K。
- **基准模型与对比方法**：
    - **架构**：测试了多种架构，包括MS-ResNet、VGGSNN、Spike-driven Transformer v3 (SDT3)等，验证了方法的扩展性。
    - **对比方法**：与当前先进的SNN量化/压缩方法进行对比，如BitSNN、Q-SNN、Q-Spikformer、BESTformer等。在目标检测和分割任务上，也与多种BNN方法（如BiDet、ReActNet等）进行了对比。

### 4. 资源与算力

- **文中未明确提及**完成所有实验具体使用的GPU型号、数量及总训练时长。

### 5. 实验数量与充分性

- **实验数量**：实验设计较为充分，涵盖了超过**6组主要实验**，包括：
    - 在**4种不同数据集**上的图像分类实验。
    - 在**3种不同压缩率（$\eta=4,5,6$）** 下进行了评估。
    - 在**3种下游任务**（分类、检测、分割）上进行了验证。
    - **消融实验**：验证了OS-Quant和MPFD两个核心模块各自的有效性，以及对MPFD中不同蒸馏方案（LGKD, FRFD, MPFD）的对比。
    - **硬件验证**：在FPGA上对比了S²NN与BSNN的片上/片外数据传输量和延迟。
- **充分性与客观性**：实验覆盖了静态图像、神经形态数据、目标检测和语义分割，并对比了多个领域内的SOTA方法，实验设置全面且客观。消融研究清晰证明了各模块的独立贡献，FPGA验证为效率提升提供了硬件层面的证据，增强了结论的说服力。

### 6. 论文的主要结论与发现

- **高压缩高效率**：S²NN能在权重比特位宽低于1比特（如0.44-0.67比特）的条件下，实现模型大小和操作数（OPs）的大幅降低（$1.4\times$至$6.8\times$），充分挖掘了SNN的压缩与加速潜力。
- **性能SOTA**：在多个任务和数据集上，S²NN在保持极低资源开销的同时，取得了优于或持平现有量化SNN方法的最佳性能。例如，在ImageNet-1K上，其性能优于此前的BSNN工作$3.5\%\sim4.6\%$；在ADE20K分割任务上，其性能超越了全精度SNN基线。
- **方法有效性**：所提出的**OS-Quant**方法有效解决了离群值导致的码字选择偏差问题，而**MPFD**通过更精准的膜电位知识迁移，显著提升了压缩模型的性能。

### 7. 优点

- **创新性强**：开创性地将“亚比特”压缩概念引入SNN领域，实现了低于1比特的极致模型压缩，为SNN的高效部署开辟了新方向。
- **问题洞察深刻**：准确识别并定义了“离群值引发的码字选择偏差”这一关键问题，并为此设计了精巧的OS-Quant方法，从源头优化了量化过程。
- **方法论扎实**：OS-Quant结合了鲁棒的IQR统计与保留空间特征的放缩策略；MPFD则直接作用于膜电位，提供了比传统方法更精确的蒸馏梯度，二者兼具理论合理性与实践效果。
- **实验全面详尽**：评估任务从分类扩展到检测和分割，数据集涵盖静态与动态视觉，并在FPGA上进行了硬件验证，多维度证明了方法的有效性与实用性。

### 8. 不足与局限

- **算力成本未明确**：论文未提供实验所需的算力详情（GPU型号/数量/时间），难以评估方法在大规模任务上的训练开销。
- **性能差距依然存在**：尽管在压缩效率上取得了巨大进步，但在极具挑战性的任务（如ImageNet-1K）上，S²NN与全精度SNN模型之间仍存在不可忽视的绝对精度差距（约10%）。
- **应用场景偏向**：论文主要集中在视觉任务上验证，其在其他模态（如自然语言处理、语音）或更复杂的序列建模任务上的适用性有待进一步探索。
- **依赖教师模型**：MPFD方法的性能增益依赖于一个预训练良好的全精度教师网络，这在实际应用中增加了一道工序。

（完）
