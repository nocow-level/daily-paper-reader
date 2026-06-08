---
title: Efficient Low Rank Attention for Long-Context Inference in Large Language Models
title_zh: 面向大语言模型长上下文推理的高效低秩注意力
authors: "Li Tenghui, Guoxu Zhou, Xuyang ZHAO, Yuning Qiu, Qibin Zhao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Mc0eJHZhW5"
tags: ["query:edge-llm"]
score: 10.0
evidence: 低秩注意力降低资源受限设备上长上下文LLM的KV缓存内存
tldr: 提出低秩查询与键注意力框架LRQK，通过分解查询和键矩阵为紧凑的低秩因子，在解码阶段以线性复杂度计算近似注意力，并选择关键令牌，大幅降低KV缓存内存消耗，使LLM能在资源受限设备上处理长上下文。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-mc0ejhzhw5/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1133, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mc0ejhzhw5/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 871, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mc0ejhzhw5/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1050, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mc0ejhzhw5/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1050, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mc0ejhzhw5/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 882, \"height\": 339, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1391, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 642, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1225, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 654, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1511, \"height\": 513, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1218, \"height\": 463, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1096, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1209, \"height\": 495, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1028, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1109, \"height\": 529, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1395, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-mc0ejhzhw5/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1425, \"height\": 416, \"label\": \"Table\"}]"
motivation: 长上下文LLM的KV缓存占用巨大GPU内存，限制其在资源受限设备上的应用。
method: 提出两阶段LRQK框架，联合分解查询与键矩阵，并选择top-k令牌进行高效注意力计算。
result: 显著降低内存占用，在多个基准上实现与全注意力相当的性能，同时推理速度提升。
conclusion: 低秩注意力是实现长上下文LLM在内存受限硬件上高效推理的关键技术。
---

## Abstract
As the length of input text increases, the key-value (KV) cache in LLMs imposes prohibitive GPU memory costs and limits long-context inference on resource constrained devices.
  Existing approaches, such as KV quantization and pruning, reduce memory usage but suffer from numerical precision loss or suboptimal retention of key-value pairs.
  In this work, Low Rank Query and Key attention (LRQK) is introduced, a two-stage framework that jointly decomposes full-precision query and key matrices into compact rank-\(r\) factors during the prefill stage, and then employs these low-dimensional projections to compute proxy attention scores in \(\mathcal{O}(lr)\) time at each decode step.
  By selecting only the top-\(k\) tokens and a small fixed set of recent tokens, LRQK employs a mixed GPU-CPU cache with a hit-and-miss mechanism where only missing full-precision KV pairs are transferred, thereby preserving exact attention outputs while reducing CPU-GPU data movement.
  Extensive experiments on the RULER and LongBench benchmarks with LLaMA-3-8B and Qwen2.5-7B demonstrate that LRQK matches or surpasses leading sparse-attention methods in long context settings, while delivering significant memory savings with minimal accuracy loss. Our code is available at \url{https://github.com/tenghuilee/LRQK}.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLM）在长上下文推理中，键值（KV）缓存的显存占用随序列长度线性增长，严重制约了在资源受限设备上的部署。
- **现有方法的局限**：
  - **量化（Quantization）**：降低数值精度，可能损失语义保真度。
  - **剪枝（Pruning）**：可能丢弃当前不重要但后续推理关键的信息。
  - **卸载（Offloading）**：频繁的PCIe数据传输引入高延迟，影响实时性。
- **关键观察**：
  1. 解码器式Transformer中，键矩阵具有显著的低秩特性；查询-键交互矩阵可被低秩近似。
  2. 注意力激活具有稀疏性——只有少量令牌获得显著权重，且最近令牌往往具有高注意力分值。
- **整体含义**：论文提出混合注意力机制 **LRQK**，在解码时利用低秩代理精确计算近似注意力、只选择少量关键令牌进行真实注意力计算，同时采用GPU-CPU混合缓存及命中/缺失机制，实现**内存大幅节省**并**保持精确注意力输出**，以支撑长上下文高效推理。

### 2. 论文提出的方法论

**总体思路**：两阶段框架，分别处理预填充（prefill）与解码（decode）。

- **预填充阶段**：
  - 对全精度查询矩阵 \(Q\) 和键矩阵 \(K\) 进行**联合低秩分解**：
    \[
    QK^\top \approx A_Q A_K^\top,\quad Q \approx A_Q B_Q,\quad K \approx A_K B_K
    \]
  - 通过约束优化问题求解，导出交替更新的闭式解（如 \(A_Q, A_K\) 使用矩阵逆更新，因秩 \(r\) 很小，\(O(r^3)\) 开销可接受）。
  - 采用“块坐标下降”（BCD）算法迭代求解各因子。

- **解码阶段**：
  - 输入令牌 \(x_t\) 得到 \(q_t, k_t, v_t\)。
  - 将 \(q_t, k_t\) 近似为低维向量 \(\hat{q}_t \in \mathbb{R}^{1\times r}, \hat{k}_t \in \mathbb{R}^{1\times r}\)，通过求解保持内积与过去关键令牌一致性的优化问题（加入正则化项）。
  - 利用低秩键矩阵 \(A_{K,\Omega,t-1}\) 计算**代理注意力分数** \(\hat{q}_t A_{K,\Omega,t-1}^\top\)，选出 top-\(k\) 活跃令牌索引 \(\Omega_k\)。
  - 结合固定数量的**最近令牌（lite tokens）**，构成 GPU 缓存索引集 \(\Omega\)。
  - 采用**命中/缺失（hit/miss）机制**：若所需令牌已在 GPU 缓存中则直接使用；缺失部分从 CPU 加载，避免冗余传输。
  - 最后在选出的全精度键、值对（\(K_\Omega, V_\Omega\)）上进行精确注意力计算。同时异步将新生成的 \(k_t, v_t\) 存入 CPU。

- **缓存结构**：GPU 缓存 = [活跃令牌( top-k ) | 最近令牌( lite )]。
- **在线更新**：解码时对 \(B_Q, B_K\) 使用一步梯度下降微调，学习率由闭式最优解给出。

### 3. 实验设计

- **数据集与 Benchmark**：
  - 长上下文基准：**RULER**（序列长度 128K 及 4K/8K/16K 子集），**LongBench**。
  - 文本生成与总结等任务上也使用了 Wikitext-2 等进行效率评估。
- **对比方法**：
  - 动态稀疏注意力基线：**Loki**、**InfiniGen**、**Quest**、**ShadowKV**。
  - 部分实验还对比了全 GPU、全 CPU 方案及与 KV 量化方法 **KVQuant** 的组合效果。
- **主干模型**：
  - LLaMA-3-8B-1M、Qwen2.5-7B-Instruct，以及 LLaMA-3.1-8B、Mistral-7B、Phi-3-mini、Qwen2.5-14B/32B 等。
- **关键超参数**：秩 \(r \in \{8,16,24,32,48\}\)，top-k \(\in \{128,256,512,1024,2048\}\)，lite 令牌数 \(\in \{4,8,16,32,64\}\)。
- **性能指标**：准确率（各个子任务）、吞吐量（tokens/s）、未命中率、GPU 内存占用、功率消耗等。

### 4. 资源与算力

- **硬件平台**：
  - NVIDIA A100 GPU（80GB 和 40GB 显存版本）。
  - NVIDIA A6000（48GB）用于部分模型。
  - NVIDIA GeForce RTX 3090（24GB）用于吞吐量对比实验。
  - CPU 为 AMD EPYC 7742 64核处理器。
- **推理配置**：batch size = 1；模型精度为 bfloat16 推理，部分矩阵逆运算临时转 float32。
- 论文**未明确提及训练时长或总 GPU 小时数**（因为不涉及训练，仅为推理评估），但对不同上下文长度（4K-128K）和多种方法进行了详细的吞吐量测试，并提供了完整的实验环境说明。

### 5. 实验数量与充分性

- **实验类型非常丰富**：
  - 在 RULER（多个长度）、LongBench 上与 4 种主流方法对比。
  - 替换多种模型（LLaMA 系列、Qwen2.5、Mistral、Phi-3）验证泛化性。
  - 消融实验：单独分析秩 \(r\)、top-\(k\) 数量、lite 令牌数的影响。
  - 初始化策略（随机、top-r、topcol）对比。
  - 缓存命中率统计（多组合网格搜索）。
  - 吞吐量与功耗分析（对比全 GPU、全 CPU、ShadowKV、LRQK 变体）。
  - 与 KV 量化方法（KVQuant）的结合实验。
- **充分性**：实验设计覆盖了多模型、多上下文长度、多基线、消融研究、效率分析及混合方案，规模较大，结论可靠。
- **公平性**：对比方法均采用公开代码与推荐配置，统一评估框架（OpenCompass），具有较好的公平性。LRQK 本身为推理时的准确加速方法，不存在训练偏差。

### 6. 论文的主要结论与发现

- LRQK 在长上下文任务（128K RULER）上达到或超越先进稀疏注意力方法（如 ShadowKV），且内存消耗大幅减少。
- 在 LongBench 的检索类任务（如 PRetr）上表现突出。
- 低秩近似 \(r=32\) 与 top-\(k=2048\) 在很多场景下是最佳权衡。
- 通过命中/缺失缓存机制，平均可将 CPU-GPU 数据传输量降低约 **60%**（平均未命中率约 40%）。
- 吞吐量：GPU-only 在超长上下文会 OOM；CPU offload 解码极慢；LRQK 在 64K 上下文下仍可保持较稳定及可观的解码速度。
- 方法具有较强的鲁棒性，对初始化策略不敏感，可结合量化方案（如 KVQuant）无显著性能崩塌。

### 7. 优点（方法或实验亮点）

- **精度无损**：代理注意力仅用于选令牌，最终注意力仍在精选的全精度键值对上计算，保证数学精确性。
- **内存高效**：混合缓存与选择机制使 GPU 缓存大小固定，不随序列长度线性增长。
- **低通信开销**：命中/缺失机制避免全量 KV 的 CPU-GPU 传输，仅加载必要的缺失令牌。
- **理论与实现结合紧密**：从低秩观察到优化问题建模，再到闭式解和在线更新，推导严谨。
- **实验扎实全面**：覆盖多模型、多长度、多基线，且有消融、效率、混合方案等分析。
- **超参数调优指导明确**：给出默认配置和选择策略，实用性强。

### 8. 不足与局限

- **推理延迟仍受 CPU 索引限制**：论文指出 CPU 端索引操作成为主要瓶颈，而非 PCIe 带宽。
- **超参数需任务调整**：最优的秩 \(r\) 和 top-\(k\) 依赖于具体模型和任务，需要小范围经验验证。
- **GPU 利用率不够充分**：在吞吐量对比中可见 LRQK 的 GPU 功耗低于其他方法，说明计算资源未被完全利用，存在性能优化空间。
- **部分任务性能偏低**：在 MK2、NQA 等任务上稍逊于最佳基线，对特定长序列检索任务仍有改进空间。
- **仅评估推理阶段**：未涉及训练阶段的低秩加速，方法限定于推理场景。

（完）
