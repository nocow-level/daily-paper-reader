---
title: Attention-Level Speculation
title_zh: 注意力级别推测
authors: "Jack Cai, Ammar Vora, Randolph Zhang, Mark O'Connor, Mark C. Jeffrey"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=4OszSYdsgO"
tags: ["query:edge-llm"]
score: 4.0
evidence: 用于降低LLM推理延迟的推测并行
tldr: 针对大语言模型长上下文推理延迟问题，提出注意力级别推测并行方法，通过在不同设备上提前执行后续操作来重叠计算，将128K上下文注意力延迟最多降低5倍，端到端解码延迟提升1.65倍，且无质量损失。该方法为推测执行建立了基础，并简化了实现。对于提升GPU上大模型推理效率有一定借鉴意义。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1769, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1526, \"height\": 294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 867, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 837, \"height\": 1079, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 601, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1591, \"height\": 223, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1697, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 838, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1426, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1420, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1733, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1746, \"height\": 752, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4oszsydsgo/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1722, \"height\": 904, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1602, \"height\": 561, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 774, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1600, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 904, \"height\": 767, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 905, \"height\": 938, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 750, \"height\": 800, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 743, \"height\": 719, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 924, \"height\": 1011, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 900, \"height\": 954, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 750, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4oszsydsgo/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 742, \"height\": 555, \"label\": \"Table\"}]"
motivation: 大模型长上下文推理时传统并行扩展面临收益递减，注意力延迟成为瓶颈。
method: 提出注意力级别推测并行（ALSpec），预测自注意力输出以提前执行后续操作，重叠注意力和非注意力计算。
result: 在128K上下文上注意力延迟最高降低5倍，端到端解码延迟提升1.65倍，无质量损失。
conclusion: 方法为推测执行奠定基础，简化实现，有效降低长上下文推理延迟。
---

## Abstract
As Large Language Models (LLMs) grow in size and context length, efficient inference strategies are essential to maintain low-latency token generation. Unfortunately, conventional tensor and data parallelism face diminishing returns when scaling across multiple devices. We propose a novel form—attention-level speculative parallelism (ALSpec)—that predicts self-attention outputs to execute subsequent operations early on separate devices. Our approach overlaps attention and non-attention computations, reducing the attention latency overhead at 128K context length by up to 5x and improving end-to-end decode latency by up to 1.65x, all without sacrificing quality. We establish the fundamental pillars for speculative execution and provide an execution paradigm that simplifies implementation. We show that existing attention-approximation methods perform well on simple information retrieval tasks, but they fail in advanced reasoning and math. Combined with speculative execution, we can approximate up to 90% of self-attention without harming model correctness. Demonstrated on Tenstorrent's NPU devices, we scale up LLM inference beyond current techniques, paving the way for faster inference in transformer models.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **长上下文推理瓶颈**：随着大语言模型（LLM）上下文长度和模型规模的增长，自注意力（self‑attention）的计算开销随序列长度线性增长，逐渐成为解码延迟的主导因素，而非自注意力运算（如前馈网络）耗时保持不变。
- **传统并行策略的局限**：张量并行（tensor parallelism）在扩展到多设备时因通信（如all‑gather）开销增加而导致边际收益递减；数据并行、流水线并行虽然提升吞吐量，但无法降低单次推测的解码延迟。
- **静态注意力近似的不足**：一些近似方法（如注意力池、滑动窗口注意力）虽可减少计算，但在高级推理、数学等任务上会显著损害模型精度，且固定层级的近似策略缺乏灵活性。
- **核心思想**：提出**注意力级别推测并行（ALSpec）**，通过动态预测自注意力输出，将后续非注意力操作提前在独立设备上执行，实现注意力和非注意力计算的并行重叠，从而**在保证输出质量的前提下显著降低长上下文下的推理延迟**。

### 2. 论文提出的方法论：核心思想、关键技术细节

#### 2.1 推测并行框架
- **预测器**：使用一种简化版注意力池（attention sink），仅关注KV缓存中的前若干token和最近 S 个token。S 取值较小（如128、256、512），远小于完整上下文长度。
- **推测‑验证流程**（对应原论文Algorithm 1）：
  1. 对每一层，先以近似注意力计算推测输出 \(\tilde A_i\)，并在另一设备/线程启动非注意力操作的执行（如前馈网络）。
  2. 同时，在原设备上运行完整自注意力，得到精确输出 \(A_i\)。
  3. 在验证阶段，若 \(\| \tilde A_i - A_i \|_2 < \lambda \cdot \| A_i \|_2\)（\(\lambda\) 为超参数），则接受推测结果；否则丢弃已启动的后续计算，使用完整注意力的输出重新执行。
- **误差界**：利用Lipschitz连续性，给出最终输出偏差的上界，并推导出一个高概率误差边界（与层数 \({\sqrt{N}}\) 相关），为阈值 \(\lambda\) 的选择提供理论支撑。

#### 2.2 实现优化
- **推测闪存解码内核（Speculative Flash Decode）**：在闪存解码的基础上，通过改变KV块读取顺序，优先计算首尾块的部分注意力结果作为推测值，同时完成全注意力的计算并一步内融合验证步骤，几乎无额外开销。
- **SGDC与优先级门控**：提出“静态图、动态并发”（Static Graph, Dynamic Concurrency）执行范式，保持主机代码的静态操作图，底层通过优先级向量控制设备间激活结果的流转。当推测成功时，发送方设备跳过后续运算；若失败，接收方设备承担剩余计算，从而实现设备间的动态负载均衡。

### 3. 实验设计：数据集/场景、基准、对比方法

- **模型与硬件**：
  - 主要模型：Llama 3.1 8B（32层），部分实验使用Llama 3.1 70B。
  - 推理硬件：Tenstorrent N150芯片（8个）用于实际部署和延迟测量；NVIDIA A100/H100 GPU用于精度评测和部分延迟仿真。
- **基准任务**（覆盖问答、信息检索、推理、数学、长上下文）：
  - IFEval、GPQA、SWDE、GSM8K、MATH、MGSM、HotpotQA、RepoBench、MMLU PRO多科目（带链式思维）等。
- **评估指标**：
  - 模型精度：相对基线模型的得分或准确率。
  - 推测命中率（speculation hit rate）：近似注意力被接受的比例。
  - 延迟：每层/端到端解码延迟，吞吐量（tokens/s/user）。
- **对比方法**：
  - 纯注意力池（baseline approximation）；
  - 固定层级的注意力池（静态选择某些层使用近似）；
  - 基线无近似模型（full attention）；
  - 全张量并行（tensor parallelism，1/2/4/8设备）作为加速参照。
  - 数据并行、流水线并行等传统策略的理论对比。

### 4. 资源与算力
- **推理硬件**：
  - Tenstorrent N150 芯片（8个），使用TT‑Metalium内核库，BF16激活、8位KV缓存和混合精度权重。
  - NVIDIA A100（用于部分精度测评）和H100（4×/8×张量并行延迟测量，SGLang/FlashInfer后端）用于对比分析和性能预估。
- **训练/微调**：本方法无需重新训练或修改模型权重，仅为推理时的动态执行优化，因而**未消耗额外训练算力**。
- **延迟测量**：基于设备内核执行时间（忽略主机调度开销），通过逐层延迟折算端到端指标；ALSpec在H100上的投影性能基于实测的4×TP延迟和65%推测命中率进行估算。

### 5. 实验数量与充分性
- **实验组数**：
  - 在不同\(\lambda\)（0.05, 0.10, 0.15, 0.20, 0.25）下评估了Llama 3.1 8B在约13个基准上的精度和推测命中率；
  - 相同设置扩展至Llama 3.1 70B的部分任务（4个基准）；
  - 在N150芯片上进行了1K~128K上下文长度、多种推测命中率（50%–87.5%）和设备数（2/4/8）的系统延迟/吞吐量扫描；
  - 增加了H100上的性能投影对比（4×TP vs. 8×TP vs. ALSpec预估）；
  - 非数值实验：通过“干草堆中的针”定性任务展示静态近似失效案例。
- **充分性与客观性**：
  - 评估覆盖了多种类型任务，验证了动态推测在不同难度场景下的保真度；
  - 对比了静态近似、张量并行等基线，展示了ALSpec在延迟和精度权衡上的优势；
  - 延迟分析基于实测内核时长，并考虑了通信开销和推测失败的回退代价，较为客观；
  - 实际部署限于Tenstorrent硬件，GPU结果部分为仿真或投影，缺乏直接的GPU实现验证；但本研究核心在于方法验证，硬件迁移性在理论层面可行。

### 6. 论文的主要结论与发现
- 在128K上下文下，ALSpec可将注意力延迟开销降低多达5倍，端到端解码延迟最多提升1.65倍（与同等数量设备下的全张量并行相比）。
- 使用简单的注意力池作为预测器，动态验证（\(\lambda=0.05\)–0.10）可在不同任务上达到18%–90%的推测命中率，同时保持与全注意力基线一致的输出精度。
- 静态近似（固定层或全注意力池）在处理需要全局信息的推理任务时会出现严重失误，而ALSpec通过运行时验证有效避免此类错误。
- 将推测并行与张量并行结合，可超越全张量并行的扩展极限，在8设备上继续获得加速，证明该范式是对传统并行策略的有力补充。

### 7. 优点：方法或实验设计上的亮点
- **动态性**：将推测执行引入transformer的层内计算，打破了静态近似方法的局限，在保证精度的同时最大化重叠执行。
- **低开销实现**：推测闪存解码内核和SGDC机制几乎不增加额外计算负担；发送方设备可完全跳过后续运算，资源利用率高。
- **理论支撑**：从Lipschitz连续性推导误差界，给出高概率误差范围（\(\propto \sqrt{N}\lambda\)），为阈值选择提供理论依据，而非纯经验调参。
- **跨任务一致性**：现有近似方法在数学/推理类任务上精度严重下降，而ALSpec在所有测试类别上均能保持与基线相当的表现。
- **通用性展望**：论文指出该方法可扩展至循环层、连续思考等新架构，并且可与其他并行技术及token级推测解码结合。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **硬件平台单一**：实际部署和系统性能测量仅在Tenstorrent NPU上完成，缺少在主流GPU（如A100/H100）上经过优化的CUDA实现和端到端延迟数据。
- **推测预测器简单**：仅使用注意力池，可能在长尾或极高精度的场景下命中率不足；更复杂的近似方法是否能进一步提升性能未做探索。
- **静态开销**：优先级的同步（all‑gather）和残差流对齐等操作可能在特定硬件或极低延迟场景下成为额外瓶颈，文中虽提及但未详细量化。
- **\(\lambda\) 的选择**：错误阈值的设定目前依赖于任务和经验，缺乏完全自适应的机制，可能影响实际部署的泛化性。
- **无训练/微调策略**：若允许轻量级微调以提升推测命中率（如增强模型对近似预判的校准），可能获得更大加速，但该方法未涉及。
- **实验公平性**：与张量并行的对比基于相同数量的设备，但未考虑在同等功耗或成本约束下的优化动态优先级调度开销是否会影响收益。

（完）
