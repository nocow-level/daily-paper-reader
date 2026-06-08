---
title: "Ladder-Residual: Parallelism-Aware Architecture for Accelerating Large Model Inference with Communication Overlapping"
title_zh: 梯形残差：通过通信重叠加速大模型推理的并行感知架构
authors: "Muru Zhang, Mayank Mishra, Zhongzhu Zhou, William Brandon, Jue WANG, Yoon Kim, Jonathan Ragan-Kelley, Shuaiwen Leon Song, Ben Athiwaratkun, Tri Dao"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=bJnSplWSCL"
tags: ["query:edge-llm"]
score: 4.0
evidence: 通过重叠通信加速多GPU大模型推理
tldr: 针对模型并行中通信成为瓶颈的问题，提出Ladder Residual结构，通过在残差网络中重叠计算和通信来隐藏通信延迟，加速多GPU上的大模型推理。该方法适用于所有基于残差的模型，提供了简单的并行加速方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-bjnsplwscl/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 816, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bjnsplwscl/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1723, \"height\": 1309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bjnsplwscl/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bjnsplwscl/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 829, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bjnsplwscl/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 832, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bjnsplwscl/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 864, \"height\": 422, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-bjnsplwscl/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 624, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bjnsplwscl/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 835, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bjnsplwscl/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1472, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bjnsplwscl/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1372, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bjnsplwscl/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1476, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bjnsplwscl/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1523, \"height\": 200, \"label\": \"Table\"}]"
motivation: 模型并行中设备间通信成为主要瓶颈，限制多GPU扩展的收益。
method: 提出梯形残差结构，通过架构修改实现计算与通信的重叠，隐藏通信延迟。
result: 在多GPU推理中有效隐藏通信开销，提升扩展效率。
conclusion: Ladder Residual为多GPU大模型推理提供了简单有效的通信优化方法。
---

## Abstract
Large language model inference is both memory-intensive and time-consuming, often requiring distributed algorithms to efficiently scale. Various model parallelism strategies are used in multi-gpu training and inference to partition computation across multiple devices, reducing memory load and computation time. However, using model parallelism necessitates communication of information between GPUs, which has been a major bottleneck and limits the gains obtained by scaling up the number of devices. We introduce Ladder Residual, a simple architectural modification applicable to all residual-based models that enables straightforward overlapping that effectively hides the latency of communication. **Our insight is that in addition to systems optimization, one can also redesign the model architecture to decouple communication from computation.** While Ladder Residual can allow communication-computation decoupling in conventional parallelism patterns, we focus on Tensor Parallelism in this paper, which is particularly bottlenecked by its heavy communication. For a Transformer model with 70B parameters, applying Ladder Residual to all its layers can achieve 29% end-to-end wall clock speed up at inference time with TP sharding over 8 devices. We refer the resulting Transformer model as the Ladder Transformer. We train a 1B and 3B Ladder Transformer from scratch and observe comparable performance to a standard dense transformer baseline. We also show that it is possible to convert parts of the Llama-3.1 8B model to our Ladder Residual architecture with minimal accuracy degradation by only retraining for 3B tokens.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：在大模型推理中，广泛采用的张量并行（Tensor Parallelism）会将模型权重和激活值划分到多个 GPU 上协同计算，但设备间必须进行 AllReduce 通信来同步部分和。这种通信是阻塞式的，成为推理加速的主要瓶颈，即便使用 NVLink 等高速互联，70B 模型在 8 卡 TP 下通信延迟仍占端到端延迟的 38% 左右。
- **整体含义**：本文提出**Ladder Residual**，一种对残差架构模型的简单修改，通过重新设计计算流将通信与计算解耦，使 AllReduce 可以与后续层的计算重叠，从而隐藏通信延迟。核心思想是：**模型架构本身也可以被重新设计来“解耦”通信与计算**，而不仅仅依赖低层的系统优化。

### 2. 论文提出的方法论
- **核心思想**：标准 Transformer 的残差流为 \(x_{i+1}=h_{i+1}(x_i)+x_i\)，需要等待 \(x_i\) 的通信完成才能执行 \(h_{i+1}\)。Ladder Residual 改为 \(x_{i+1}=h_{i+1}(x_{i-1})+x_i\)，即在计算第 \(i+1\) 个模块时使用“陈旧”的上一轮残差输入 \(x_{i-1}\)，从而使得第 \(i\) 个模块输出的 AllReduce 可以与第 \(i+1\) 个模块的计算并行执行。
- **关键技术细节**：
  - 实现伪代码（Algorithm 1）：每一层启动 `AsyncAllReduce` 获得句柄，在下一层等待前一层 MLP 的通信句柄，同时启动当前层的注意力计算和后续的异步 AllReduce，形成流水线重叠。
  - 该设计可应用于任何基于残差的模型，但本文聚焦于 Transformer 并命名为 **Ladder Transformer**。
  - 实验中将 Ladder Residual 与现有方案对比：**标准 Transformer** 以及 **Parallel Attention/MLP**（融合 QKV 和门控上投影，并行执行注意力和 MLP 以减半通信量）。

### 3. 实验设计
- **数据集与场景**：
  - **预训练（从头训练）**：1.2B 和 3.5B 参数模型，在 FineWeb‑edu 数据集上训练 100B tokens，使用 StarCoder 分词器。
  - **后训练适配**：将 Llama‑3.1‑8B‑Instruct 的部分层（上层 16 或 20 层）改造为 Ladder Residual，用 Infinity‑Instruct 数据集的 3B tokens 进行监督微调（SFT）两个 epoch。
  - **推理速度评测**：模拟不同模型规模（1B 至 405B）、不同 TP 世界大小（1/2/4/8，跨节点 16）、不同 batch size（1,4,16,64）、固定 1024 prompt + 512 生成 token，在 NVIDIA H100 GPU 上进行测评；同时测试 P2P 开启/关闭两种情况以模拟慢速互联。
- **对比方法**：
  - 标准 Transformer 和 Parallel Attention/MLP 架构。
  - 设置“无通信上界”作为理论最大加速比。
- **评测基准**：
  - 推理端：吞吐量（tokens/s）、预填充/解码延迟改善百分比。
  - 模型质量：ARC‑C、ARC‑E、HellaSwag、PIQA、SciQ、Winogrande、MMLU、TruthfulQA、GSM8K、HumanEval+、IFEval、AlpacaEval 以及 Wikitext 困惑度。

### 4. 资源与算力
- **训练用 GPU**：1.2B 模型使用 DDP 训练，3.5B 模型使用 HSDP（节点内 8×H100 GPU）。未明确给出具体的 GPU 卡数或训练时长，但批次大小为 4M tokens，训练 100B tokens，上下文长度 2048。
- **推理评测用 GPU**：所有推理基准均在 NVIDIA H100 GPU 上完成，最大配置为 8 卡单节点或 2 节点 16 卡（405B 模型）。
- **微调资源**：对 Llama‑3.1‑8B 的适配使用 3B tokens 的轻量 SFT，资源需求相对较小。

### 5. 实验数量与充分性
- **实验组数较多且覆盖全面**：
  - 推理速度加速比：在 1B/3B/8B/34B/70B/176B/405B 等 7 种模型规模、多种 TP 度数和 batch size 下，对比标准 Transformer、Parallel 和 Ladder Transformer（以及无通信上界），还分别测试 P2P 开启/关闭。
  - 模型质量实验：在 1.2B 和 3.5B 两个尺度上从零训练三种架构（标准、Parallel、Ladder），给出 6 项基准和困惑度。
  - 后训练适配实验：分别对上层 16 层和 20 层改造，给出零样本和重训后的 9 项指标结果。
  - 额外对比：验证了 30% 更大的 Ladder Transformer 与标准 Transformer 的性能与速度。
- **实验设计充分且公平**：消融了不同层数的适配影响，对比了现有并行优化方案，并从多维度（推理速度、模型质量）进行评估，具有较强的说服力。

### 6. 论文的主要结论与发现
- Ladder Residual 能够在 8 卡张量并行下，为 70B 模型带来 **29% 的端到端推理加速**（P2P 使能时），若禁用 P2P 加速比可达 59%。
- 在跨节点 TP（405B 模型）下，Ladder Residual 仍能提供超过 30% 的吞吐提升。
- 从零训练的 1.2B 和 3.5B Ladder Transformer 在基准评测和 Perplexity 上与标准 Transformer 性能相当。
- 将 Llama‑3.1‑8B‑Instruct 的上半部分层（16 层）改造为 Ladder Residual，仅用 3B tokens 轻量重训，即可恢复原始模型 95% 以上的性能，同时获得 21% 的推理加速。
- 与 Parallel Attention/MLP 方法相比，Ladder Residual 在预填充和解码延迟上均有更优表现。

### 7. 优点
- **极简的架构修改**：仅通过重新路由残差流，不涉及底层 kernel 编写，可在 PyTorch/JAX 等高层框架中轻松实现，便于跨硬件部署。
- **通用性强**：原则上适用于所有残差类模型，且与其他并行策略（如流水线并行、FSDP）兼容。
- **显著的实际加速效果**：在多种模型规模和通信条件下均有效，尤其在慢速互联或跨节点场景下收益更大。
- **保持模型质量**：从零训练或微调后的模型性能与标准架构相当，且微调成本极低（仅需 3B tokens），可行性高。

### 8. 不足与局限
- **实验覆盖局限**：主要基于 Transformer 架构（Llama 系列）验证，虽然声称适用于一般残差模型，但未展示在非 Transformer 模型上的结果。
- **后训练适配的深度受限**：将 Ladder Residual 应用到 Llama‑3.1‑8B 的全 32 层可能导致性能明显下降，目前仅适配上层 16~20 层；进一步扩展需要更多训练或蒸馏等技术，尚未探索。
- **训练规模有限**：从零训练的模型最大仅 3.5B，与当前主流 7B 甚至更大模型相比仍有距离；更大规模上的训练行为和对性能的影响未知。
- **可能收益递减**：当通信占比较低或计算能力极强时，重叠所能隐藏的延迟有限；随着模型尺寸增大，计算量的增长可能快于通信，加速比会有所下降（例如从 8B 到 70B 在 P2P 开启时的加速比从 46% 降至 29%）。

（完）
