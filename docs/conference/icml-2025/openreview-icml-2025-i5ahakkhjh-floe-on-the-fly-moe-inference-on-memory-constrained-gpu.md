---
title: "FloE: On-the-Fly MoE Inference on Memory-constrained GPU"
title_zh: FloE：内存受限GPU上的即时MoE推理
authors: "Yuxin Zhou, zheng li, Jun Zhang, Jue WANG, Yiping Wang, Zhongle Xie, Ke Chen, Lidan Shou"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=i5aHAkkhJH"
tags: ["query:edge-llm"]
score: 9.0
evidence: 内存受限GPU上的即时MoE推理
tldr: 针对内存受限GPU上的MoE模型推理，FloE利用专家内部参数矩阵的冗余进行压缩，减少PCIe数据移动开销。结合稀疏预测技术，实现了低延迟的即时推理。实验验证了其在保持模型质量的同时显著提升效率。该方法为MoE模型在边缘设备的部署提供了可行方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1756, \"height\": 609, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 887, \"height\": 639, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 816, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 712, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1676, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 783, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 833, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 830, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 812, \"height\": 818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1755, \"height\": 754, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-i5ahakkhjh/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1075, \"height\": 836, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1697, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1588, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1441, \"height\": 546, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1423, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 978, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1318, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 937, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-i5ahakkhjh/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1210, \"height\": 582, \"label\": \"Table\"}]"
motivation: MoE模型在内存受限设备上的推理面临专家加载时的PCIe带宽瓶颈。
method: 提出FloE，通过对专家内部参数矩阵进行压缩，减少数据移动量。
result: 实验表明FloE有效降低了推理延迟。
conclusion: FloE是一种适用于内存受限GPU的即时MoE推理系统。
---

## Abstract
With the widespread adoption of Mixture-of-Experts (MoE) models, there is a growing demand for efficient inference on memory-constrained devices.
While offloading expert parameters to CPU memory and loading activated experts on demand has emerged as a potential solution, the large size of activated experts overburdens the limited PCIe bandwidth, hindering the effectiveness in latency-sensitive scenarios.
To mitigate this, we propose FloE, an on-the-fly MoE inference system on memory-constrained GPUs.
FloE  is built on the insight that there exists substantial untapped redundancy within sparsely activated experts.
It employs various compression techniques on the expert's internal parameter matrices to reduce the data movement load, combined with low-cost sparse prediction, achieving perceptible inference acceleration in wall-clock time on resource-constrained devices.
Empirically, FloE  achieves a 9.3$\times$ compression of parameters per expert in Mixtral-8$\times$7B; enables deployment on a GPU with only 11GB VRAM, reducing the memory footprint by up to 8.5$\times$; and delivers a 48.7$\times$ inference speedup compared to DeepSpeed-MII on a single GeForce RTX 3090—all with only a 4.4\% $\sim$ 7.6\% average performance degradation.

---

## 论文详细总结（自动生成）

# FloE：内存受限GPU上的即时MoE推理 论文详细总结

## 1. 核心问题与整体含义
*   **研究动机**：Mixture-of-Experts (MoE) 模型通过少量专家激活降低推理计算量，但庞大的非激活专家参数占据大量 GPU 显存（如 Mixtral-8×7B 需约 94GB VRAM）。在消费级或内存受限的 GPU 上部署时，内存不足成为核心瓶颈。
*   **现有方案的局限**：将专家参数卸载到 CPU 内存并按需加载到 GPU 是自然解法，但这使瓶颈从**内存带宽**转移到了**PCIe 传输带宽**。PCIe 上传送几百 MB 的 FP16 专家权重动辄需数十毫秒，远超计算时间，无法隐藏加载延迟，难以实现用户无感知的**即时推理**。
*   **核心问题**：**如何在内存受限 GPU 上，将专家加载的 I/O 开销隐藏在模型计算中，并在最小化生成性能损失的前提下，实现 MoE 模型的即时推理？**

## 2. 方法论：核心思想、关键技术细节
FloE 的核心思想是挖掘 **MoE 专家内部未被充分利用的冗余**，通过混合压缩与稀疏预测，大幅减少需要经由 PCIe 传输的数据量，并实现加载和计算的流水线隐藏。

### 2.1 专家混合压缩
FloE 发现不同投影矩阵对压缩方式的敏感性不同，采用差异化压缩策略：
*   **上下文稀疏化（Contextual Sparsification）应用于 gate 和 down 投影**：
    *   **观察**：专家内部激活值（up 投影输出）的大量元素幅度集中趋近于零，移除对应的 gate 和 down 投影的通道（列/行）对效果影响最小。
    *   **方法**：对 up 投影的输出激活 $a_{up}$ 进行幅度裁剪，生成二值掩码，仅保留绝对值大于阈值 $t$ 的通道。后续前向计算仅需加载和计算被保留的 gate 列和 down 行，压缩比可达 10% 甚至更低。
    *   **理论支撑**：定理证明对 down 投影输入进行稀疏化带来的误差上界 $L_{down}$ 最小，up 投影输出稀疏化的误差 $L_{up}$ 次之，均远优于对 gate 投影 SiLU 输出的稀疏化。
*   **超低位宽量化（Ultra-low-bit Quantization）应用于 up 投影**：
    *   **观察**：up 投影（感知作“键”）对量化极不敏感，即使压缩到 INT2 或 INT1，其导致的性能下降也远小于 gate 和 down 投影（感知作“值”）。
    *   **方法**：仅对需完整参与稀疏掩码计算的 up 投影使用 INT2 量化，用 HQQ 方法压缩。

### 2.2 专家稀疏性预测
压缩虽减小了单次传输量，但若等待下一层路由和 up 投影计算完成再加载数据，则仍然串行。为隐藏传输延迟，FloE 利用连续层间隐藏状态的**高度相似性**，设计了两个轻量级预测器：
*   **层间专家预测器（Inter-expert Predictor）**：基于当前层输入隐藏状态，通过一个学习得到的小型 MLP（参数量随层深从 32K 动态增至 2M）预测下一层将被激活的专家索引。
*   **层内稀疏性预测器（Intra-expert Predictor）**：直接将当前层隐藏状态与下一层的 up 投影矩阵相乘，近似计算下一层 up 投影的输出激活，从而提前获得上下文稀疏掩码。该预测器参数复用，无额外学习开销。
*   **工作机制**：在处理第 $i$ 层时，两个预测器基于当前隐藏状态异步预取下一层所需的、经过稀疏化（仅保留掩码对应通道）和量化后的压缩专家权重，实现传输与计算的流水线重叠。

### 2.3 系统协同优化
*   **高效稀疏 GEMV 内核**：基于 Triton 开发专门内核，利用转置矩阵和列主序存储，仅按掩码加载 gate 和 down 权重列，在 GPU 上实现计算加速。
*   **紧凑异步传输**：在 DRAM 中紧凑排列 gate 的列和 down 对应行，形成连续大块，并利用 SIMD（AVX-512）和多线程异步传输技术，使 PCIe 带宽利用率从原生 PyTorch 的不到 10% 提升至 88%。

## 3. 实验设计
*   **主体模型与数据**：以 **Mixtral-8×7B** 为主要测试模型，延迟测试使用 **ShareGPT** 对话提示，质量测试使用 **WikiText-2**（困惑度）及 **EleutherAI LM Harness** 的 7 个下游任务（BoolQ, SciQ, ARC, MMLU 等）。
*   **对比基线**：
    *   **DeepSpeed-MII**：ZeRO-Infinity 卸载方案的工业级实现。
    *   **Mixtral-Offloading**：集成预测、缓存与均匀量化卸载的社区方案。
    *   **Fiddler**：采用 CPU-GPU 协同计算的先进卸载系统。
    *   **Mixtral-GPU**：使用 HQQ INT2 量化使整个模型常驻 GPU，作为即时推理场景的**理论速度上限**。
    *   稀疏化/量化专用方法：CATS、CHESS、HQQ 量化。
*   **评估场景与指标**：在 **GeForce RTX 3090 (24GB VRAM)** 上，限制不同 VRAM 用量（12-24GB），测试不同输入/输出长度下的**端到端生成速度（TPS，每秒 token 数）**，并同步跟踪模型性能下降。

## 4. 资源与算力
*   **测试硬件**：主要端到端性能评估在单张 **NVIDIA GeForce RTX 3090**（24GB 显存）上进行，配套 64 核 CPU 和 256GB 内存，通过 PCIe 4.0 互联。
*   **稀疏性分析**：单专家 GEMV 内核的延迟加速在额外三款 GPU（H100, A100, A6000）上进行了对比验证。
*   **计算开销**：论文明确指出预测器极为轻量（最大 2M 参数），且采用参数复用的无学习预测器，未提及大规模训练所需的算力与时间，整体方法属推理系统优化，无昂贵重训练需求。

## 5. 实验数量与充分性
实验设计较为全面，包括：
*   **多维度效率评估**：包含 9 组不同输入/输出长度的端到端延迟对比、5 档 VRAM 限制（12GB 至 24GB）下的吞吐测试、4 款不同算力 GPU 上的单专家加速比、以及不同传输块大小和带宽利用率对比。
*   **多维度质量评估**：覆盖 7 个下游任务准确率、WikiText-2 困惑度，并专门在不同稀疏率和不同量化位宽下进行了敏感性分析，验证了方案对性能损失的极致控制。
*   **消融与兼容性**：细致对比了对 gate/up/down 三个投影分别施加稀疏化的效果，以及稀疏化叠加不同位宽量化的兼容性。
实验对比基线丰富，指标（速率与质量）平衡，消融透彻，具备较强的**客观性与公平性**。

## 6. 主要结论与发现
*   **极致推理加速**：FloE 在单张 RTX 3090 上实现端到端速度达到全量 GPU 驻留模型（Mixtral-GPU）的 91%，比 DeepSpeed-MII 快 **48.7 倍**，比 Mixtral-Offloading 和 Fiddler 分别快 2.6 倍和 3.14 倍。
*   **存储压缩**：每专家参数压缩 **9.3 倍**，使得 Mixtral-8×7B 可在仅 **11GB VRAM** 的 GPU 上部署，显存占用缩减 8.5 倍。
*   **质量保持**：实现上述加速与内存节省的代价极低，下游任务平均性能（准确率）仅下降 **4.4% ~ 7.6%**，优于同等压缩水平的其他方法（如 HQQ INT2, CHESS-90%）。

## 7. 优点
*   **问题洞察深刻**：敏锐捕捉并量化了 MoE 专家内部投影矩阵间对压缩敏感性的显著差异，据此设计非对称混合压缩，最大化压缩收益的同时最小化精度损失。
*   **轻量流水线设计**：利用层间相似性设计的极轻量、部分无参数的预测器，巧妙地将加载操作隐藏于计算之下，避免了笨重的数据预取模型。
*   **系统级全栈优化**：从算法（稀疏化、量化预测）到底层内核（稀疏 GEMV）再到数据传输（紧凑布局、SIMD 异步）的全链路协同优化，使理论优势完全转化为实际时钟速度提升。
*   **理论实证结合**：不仅给出了激活分布实验观察，还对不同稀疏化策略的误差上界给出了非平凡理论证明，增强了方法的可信度。

## 8. 不足与局限
*   **主要验证模型单一**：核心实验与理论分析均围绕 Mixtral-8×7B 展开，尽管附录中部分验证了 Phi-3.5-MoE、DeepSeek-V2 等，但端到端系统性能的泛化性仍有待更广泛验证。
*   **预测器离线依赖**：上下文稀疏阈值需要离线统计激活分布确定，可能对数据分布偏移敏感；层间预测器也需收集小量数据训练。
*   **应用场景限定**：系统明确聚焦于消费级 GPU 上的**低延迟单 batch 交互式推理**（on-the-fly），其设计在追求高吞吐量的离线批量服务场景中优势可能减弱。
*   **极端稀疏下的退化**：虽然 90% 稀疏率下性能控制良好，但 MMLU 等知识密集型任务上相较原模型仍有可见下降（69.5% → 60.1%），对精度极其敏感的场合需要权衡。

（完）
