---
title: Accelerating Linear Recurrent Neural Networks for the Edge with Unstructured Sparsity
title_zh: 利用非结构化稀疏加速面向边缘的线性循环神经网络
authors: "Alessandro Pierro, Steven Abreu, Jonathan Timcheck, Philipp Stratmann, Andreas Wild, Sumit Bam Shrestha"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=UNrfYfbLZ3"
tags: ["query:edge-llm"]
score: 9.0
evidence: 利用非结构化稀疏加速边缘设备上的线性RNN推理
tldr: 针对线性循环神经网络在边缘设备上实现高效流式推理的需求，研究非结构化稀疏对推理效率的影响，通过缩放研究发现高度稀疏的线性RNN在各种推理计算预算下均能实现更好的效率-性能平衡，展示了其作为边缘部署候选方案的潜力。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 754, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1609, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1761, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1714, \"height\": 648, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 837, \"height\": 669, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 848, \"height\": 714, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 853, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1748, \"height\": 953, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 846, \"height\": 652, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1658, \"height\": 674, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-unrfyfblz3/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1405, \"height\": 766, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-unrfyfblz3/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1604, \"height\": 558, \"label\": \"Table\"}]"
motivation: 线性RNN具有恒定的内存和每令牌时间优势，但边缘部署需要硬件感知优化以降低延迟和能耗。
method: 系统调查不同稀疏度下线性RNN的性能和效率Pareto前沿，评估非结构化稀疏在边缘硬件上的加速效果。
result: 稀疏线性RNN在大多数推理计算预算下始终优于稠密模型，实现更好的效率-性能权衡。
conclusion: 非结构化稀疏是一种有前景的边缘端线性RNN优化技术。
---

## Abstract
Linear recurrent neural networks enable powerful long-range sequence modeling with constant memory usage and time-per-token during inference. These architectures hold promise for streaming applications at the edge, but deployment in resource-constrained environments requires hardware-aware optimizations to minimize latency and energy consumption. 
Unstructured sparsity offers a compelling solution, enabling substantial reductions in compute and memory requirements--when accelerated by compatible hardware platforms. 
In this paper, we conduct a scaling study to investigate the Pareto front of performance and efficiency across inference compute budgets.
We find that highly sparse linear RNNs *consistently* achieve better efficiency-performance trade-offs than dense baselines, with $2\times$ less compute and $36$\% less memory at iso-accuracy.
Our models achieve state-of-the-art results on a real-time streaming task for audio denoising.
By quantizing our sparse models to fixed-point arithmetic and deploying them on the Intel Loihi 2 neuromorphic chip for real-time processing, we translate model compression into tangible gains of $42\times$ lower latency and $149\times$ lower energy consumption compared to a dense model on an edge GPU.
Our findings showcase the transformative potential of unstructured sparsity, paving the way for highly efficient recurrent neural networks in real-world, resource-constrained environments.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

*   **研究动机与背景**：线性循环神经网络（RNN）在流式序列建模中显示出巨大潜力，因其在推理时具有恒定的内存占用和每时间步的恒定计算时间，非常适合资源受限的边缘设备。
*   **核心问题**：尽管具有理论优势，但在真实边缘环境中部署线性 RNN 仍需硬件感知的优化，以最大限度地降低延迟和能耗。非结构化稀疏是一种极具吸引力的模型压缩方案，但其收益能否在实际硬件上兑现，尤其是与特定硬件架构结合时，仍有待探索。
*   **整体含义**：本文旨在系统性地研究非结构化稀疏（权重与激活稀疏）对线性 RNN 效率与性能权衡的影响，并通过在神经形态芯片上的实际部署，将理论上的计算/内存节省转化为可测量的延迟与能耗增益，证明该方法在资源受限环境中的变革性潜力。

### 2. 论文提出的方法论

*   **核心思想**：将非结构化的权重剪枝与激活稀疏化相结合，大幅削减线性 RNN 的有效计算量（MACs），然后通过量化技术将其部署在专为非结构化稀疏和事件驱动计算设计的神经形态硬件（Intel Loihi 2）上，从而实现极致的推理加速。
*   **关键技术细节**：
    *   **基础架构**：采用对角化 S5 模型，其核心是线性状态空间模型，后接门控线性单元进行非线性通道混合。
    *   **权重剪枝**：采用迭代幅度剪枝，在训练过程中按照三次多项式调度逐步增加稀疏度至目标水平（例如 90%），并结合 Erdős-Rényi-Kernel（ERK）策略为不同层动态分配稀疏度。
    *   **激活稀疏化**：将模型中的 GELU 激活函数替换为 ReLU，并在残差连接和 S5 隐藏层后插入额外的 ReLU 激活函数，以诱导出高度稀疏的激活值，从而减少矩阵向量乘法的有效运算量。
    *   **量化与定点部署**：采用量化感知训练（QAT），使用静态量化方案将权重（W8，递归矩阵为 W16）和激活值（A16）转换为定点整数，以适应 Loihi 2 的低精度算术单元。
    *   **硬件映射**：将 S5 模型的操作（如复数矩阵乘法分解、逐元素操作融合等）映射到 Loihi 2 的可编程神经元和突触层上，以充分利用其计算-内存紧耦合和异步事件驱动的架构特性。

### 3. 实验设计

*   **数据集与场景**：
    *   **主任务**：Intel N-DNS Challenge 2023 的流式音频降噪任务，包含6万条训练/验证样本和1.2万条测试样本。
    *   **辅助任务**：Google Speech Commands V2-35 的关键词识别任务。
*   **基准评估指标**：
    *   **性能指标**：尺度不变信噪比（SI-SNR）。
    *   **效率指标**：有效乘加运算次数（MACs）和内存占用（MB）。
    *   **硬件指标**：在 Intel Loihi 2 和 NVIDIA Jetson Orin Nano 上测量单令牌延迟（μs）、吞吐量（tokens/s）、每样本能量消耗（mJ）和每令牌能量消耗（μJ）。
*   **对比方法**：
    *   **模型变体**：对比了一系列不同宽度（参数规模）的稠密模型和稀疏模型。
    *   **硬件平台**：将稀疏、量化的模型部署在 Loihi 2 上，与在边缘 GPU（Jetson Orin Nano）上运行的性能相近但尺寸更小的稠密模型进行能效和延迟对比。
    *   **量化方法**：对比了量化感知训练（QAT）与训练后量化（PTQ）对模型性能的影响。
    *   **其他基线**：与 N-DNS 挑战赛的前冠军模型 Spiking-FullSubNet-XL 进行效率和性能对比。

### 4. 资源与算力

*   **文中未明确说明**：论文未提及训练模型所用的具体 GPU 型号、数量或总训练时长。文中仅提及使用 JAX 框架进行训练，并在 NVIDIA Jetson Orin Nano 上进行推理性能比对。

### 5. 实验数量与充分性

*   **实验数量**：实验数量较丰富，主要包含以下几组：
    1.  **效率-性能帕累托前沿**：训练了包含多个宽度缩放因子的稠密模型族和稀疏模型族（总计约 8 个不同配置），绘制其在 MACs 和内存占用下的 SI-SNR 曲线。
    2.  **激活稀疏性分析**：分析了不同模型深度下的激活稀疏度，并比较了有无权重剪枝对激活稀疏度的影响。
    3.  **量化消融实验**：对比了从浮点（FP32）到静态量化再到定点（FXP）模拟和 Loihi 2 芯片部署的逐阶段性能损失，并对比了 QAT 与 PTQ。
    4.  **硬件加速验证**：在 Loihi 2 和 Jetson Orin Nano 上设置了多种执行模式（如令牌级处理、连续序列处理、批处理）进行详尽的延迟、吞吐量和能耗对比。
    5.  **批处理影响分析**：分析了不同批大小对 Loihi 2 和 Jetson Orin Nano 能效和延迟的影响。
    6.  **辅助任务验证**：在关键词识别任务上重复了效率-性能帕累托前沿实验。
*   **充分性与公平性**：实验设计较为充分、客观且公平。帕累托前沿分析为结论提供了有力支撑；硬件对比时，选择了性能相近但架构不同的模型，并考虑了多种实际运行模式，使得能效对比结论更具说服力。

### 6. 论文的主要结论与发现

*   **稀疏模型效率更优**：在给定的推理计算预算下，具有高度权重和激活稀疏性的线性 RNN 在效率-性能权衡上始终优于稠密基线模型。
*   **显著的压缩效果**：与实现相同精度的稠密模型（dense-3）相比，稀疏模型（sparse-8）实现了 2 倍的计算量减少和 36% 的内存占用降低。
*   **状态最好的任务性能**：稀疏 S5 模型在音频降噪任务上达到了最先进的性能，并且在同等精度下，比前冠军模型（Spiking-FullSubNet-XL）的计算量减少 3.2 倍，内存降低 5.37 倍。
*   **真实的硬件加速收益**：通过量化和神经形态部署，理论上的压缩优势转化为巨大的实际收益。在实时令牌级处理中，与边缘 GPU 上的稠密模型相比，Loihi 2 上的稀疏模型实现了 42 倍的延迟降低和 149 倍的能耗降低。
*   **量化的重要性**：量化感知训练对于维持模型在定点算术中的性能至关重要，训练后量化的性能退化非常严重。

### 7. 优点

*   **方法系统性**：涵盖了从模型算法（剪枝、激活函数替换）、软件工具链（量化感知训练）到专用硬件（神经形态芯片）的完整压缩与加速研究流程。
*   **硬件验证扎实**：不局限于理论计算（MACs），而是在真实硬件上对延迟和能耗进行端到端测量，并考虑了多种实际执行模式（单令牌、流式、批处理），使实验结果更具工程指导意义。
*   **对比公平且深入**：在与 GPU 的对比中，选择了性能相当但更小的稠密模型作为基线，使得能效提升的结论更加可靠；帕累托前沿分析直观地展示了稀疏模型在宽泛计算预算下的优越性。

### 8. 不足与局限

*   **未明确算力开销**：论文未报告模型训练和剪枝过程所需的算力资源（如 GPU 时数）和能耗，未能给出整个“训练-压缩-部署”生命周期的完整效率图景。
*   **定点模拟与实际芯片存在差距**：从定点模型（JAX模拟）到 Loihi 2 上实际运行存在性能降级，论文指出了可能的溢出处理方式差异，但未完全解决这一问题。
*   **Loihi 2 批处理方式的局限性**：Loihi 2 通过模型复制来实现批处理，导致资源占用随批量线性增加，这限制其在大批量高吞吐场景下的可扩展性。
*   **任务和模型尺度有限**：主要验证集中在较小规模的音频降噪模型上，其结论能否扩展到更大规模的模型（如大语言模型）和更复杂的任务仍有待验证。

（完）
