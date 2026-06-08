---
title: "DynaPipe: Dynamic Layer Redistribution for Efficient Serving of LLMs with Pipeline Parallelism"
title_zh: DynaPipe：面向LLM高效服务的动态层级重分配流水线并行
authors: "HongXin Xu, Tianyu Guo, Xianwei Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=D6w7wIN360"
tags: ["query:edge-llm"]
score: 4.0
evidence: 动态层级重分配消除LLM服务中的流水线气泡以加速推理
tldr: DynaPipe 针对LLM推理服务中流水线并行因尾部阶段后处理导致的计算不均问题，提出动态层级重分配方法，通过实时调整各阶段层分配减少停顿，提升整体推理吞吐量。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 流水线并行中尾部阶段后处理造成计算不均与气泡，降低推理效率。
method: 提出 DynaPipe，根据计算负载差异动态重分配各阶段层数以平衡流水线。
result: 缓解了气泡问题，提升了 LLM 推理服务的吞吐量。
conclusion: 动态负载均衡是优化 LLM 服务流水线并行效率的有效手段。
---

## Abstract
To accelerate large language model (LLM) inference, pipeline parallelism partitions model layers into sequential stages, each assigned to a different device for concurrent execution. However, this method often suffers from pipeline bubbles caused by imbalanced computation in the tail stage. While upstream stages focus solely on layer-forward operations, the final stage must also handle post-processing tasks like sampling, introducing significant latency. This uneven workload leads to pipeline misalignment, forcing upstream stages to idle and degrading overall performance. Existing frameworks typically distribute layers evenly across stages without accounting for computational load differences. To address this, we propose DynaPipe, a dynamic layer redistribution scheme that adaptively balances computation by predicting execution latency in real time. Moreover, we introduce an asynchronous key-value (KV) cache migration coordinator to enable
non-blocking layer redistribution during inference. Experiments on representative LLMs demonstrate that DynaPipe reduces average end-to-end request latency by 8% to 49% across diverse workloads, outperforming state-of-the-art pipeline parallelism systems.

---

## 论文详细总结（自动生成）

# DynaPipe：面向LLM高效服务的动态层级重分配流水线并行

## 1. 论文的核心问题与整体含义
- **核心问题**：在大语言模型（LLM）推理的流水线并行（Pipeline Parallelism, PP）中，模型层被划分为多个顺序阶段并分配到不同设备并发执行。然而，传统的平均分层策略忽略了各阶段实际计算负载的差异：**尾部阶段除了层前向计算，还需额外完成 token 采样等后处理任务**，导致该阶段成为瓶颈，产生流水线气泡（pipeline bubble），使上游阶段空闲等待，严重降低硬件利用率和端到端推理延迟。
- **整体含义**：论文旨在解决这一被长期忽视的**采样引发阶段间负载不均衡**问题，通过动态调整流水线中各阶段分配的层数来平衡计算，从而减少流水线停顿，提升 LLM 推理服务的整体效率与服务级别目标（SLO）达成率。

## 2. 论文提出的方法论
- **核心思想**：**在运行时根据实时的负载特征动态重分配层数**，将尾部阶段的部分层迁移到上游阶段，以抵消采样带来的额外计算开销，使流水线各阶段计算时间对齐。
- **系统架构**：DynaPipe 包含三个核心组件：
  - **执行时间预测器**：构建两个独立的轻量预测模型，分别估算单个 Transformer 层的前向计算时间（基于 batch 内 token 数 `n` 和序列长度 `L`）和采样耗时（基于解码请求数 `N_decode`）。前向时间模型为 `T_layer = Σ(ϕ1·n_i + ϕ2·n_i·L_i + ε)`，采样时间模型为 `T_sample = α·N_decode + β`。参数通过离线 profiling 拟合。
  - **气泡感知调度器**：根据预测器提供的延迟估计，计算尾部阶段与上游阶段的执行时间差异，并决定从尾部阶段移除 `k` 层并均匀重分配至 `m` 个上游阶段（`m = min(k, num_stages - 1)`）。优化目标是最小化不平衡度量 `Δ = T_sample - k·T_layer - (k/m)·T_layer`，使 `Δ ≈ 0`。为防止频繁重分配带来的抖动，引入**滑动窗口阈值机制**，仅当候选配置在窗口内一致出现时才执行调整。
  - **迁移协调器**：当调度器触发重分配时，**预加载的额外层权重**已就位，同时利用流水线并行的通信与计算重叠能力，**异步传输被迁移层的 KV 缓存**。源阶段完成计算后立即发送缓存；目标阶段在处理到新分配的层之前异步接收缓存，从而避免长时间停顿，实现无阻塞的动态层重分配。

## 3. 实验设计
- **数据集与场景**：使用 **ShareGPT**（真实对话数据）和 **Azure-Conv**（生产服务对话数据，输入长度较高）两个数据集，模拟不同输入/输出长度比的工作负载。
- **Benchmark 与对比方法**：以平均端到端请求延迟（E2EL）和 SLO 达标率（综合 TTFT 和 TPOT 阈值）为指标，与三个先进推理框架比较：**vLLM**（流水线并行，PagedAttention）、**SGLang**（张量并行，结构化执行）以及 **gLLM**（流水线并行，自适应调度但未考虑采样开销）。
- **模型**：Qwen2.5-14B 和 Qwen2.5-32B，附录还包含 Qwen3-30B-A3B（MoE）和 Meta-Llama-3-8B-Instruct，用于验证方法在不同架构上的泛化性。

## 4. 资源与算力
- **硬件**：使用 **4 块 NVIDIA A100-PCIe-40GB** GPU，通过 PCIe 互联。多节点仿真时禁用共享内存、P2P 和 InfiniBand，强制走 TCP 栈模拟跨节点通信。
- **算力消耗**：论文聚焦推理服务优化，不涉及模型训练，因此未报告训练时长。实验部分给出了不同请求率下的运行结果，但未指明单次实验的总 GPU 时长。整体实验规模适中，主要开销来自多组推理基准测试。

## 5. 实验数量与充分性
- **实验组数**：至少包含 6 大类实验：
  1. **主性能对比**（4 种方法 × 2 数据集 × 2 模型 × 多种请求速率）；
  2. **不同输出/输入长度比实验**（合成数据，多种静态策略对比）；
  3. **窗口阈值消融**（分析阈值大小对延迟和重分配频次的影响）；
  4. **多节点环境实验**（14B 模型，与 gLLM 对比）；
  5. **预测器精度验证**（预测值与实测值对比，相对误差分析）；
  6. **额外模型性能**（MoE 与 Dense 架构）。
- **充分性与客观性**：实验覆盖多种模型尺寸、数据集、并发压力和并行策略，并与同期最先进的系统严格对比。消融实验明确展示了阈值机制的作用，并比较了静态重分配策略的短板，整体实验设计客观、公平，能充分支持核心结论。SLO 达标率也考虑了实际服务水平约束，增加说服力。

## 6. 论文的主要结论与发现
- DynaPipe 在多数据集、多模型和不同请求速率下，**平均端到端延迟降低 8%–41%**（ShareGPT 上最高 40%，Azure-Conv 上最高 34%），显著优于 vLLM、SGLang 和 gLLM。
- 在高吞吐量场景下，收益尤为突出，因为解码请求比例增加，采样开销突出，DynaPipe 能有效缓解尾部瓶颈。
- 动态层重分配成功使采样耗时与额外层的前向计算重叠，**大幅减少流水线气泡**，提升硬件利用率。
- SLO 达标率在高请求率下明显领先，可**支撑比 gLLM 高 19% 的请求率**仍维持 90% 达标水平。
- 预测器具有较高精度（层前向平均相对误差约 4.95%，采样误差约 0.31%），且预测开销可忽略。
- 方法在 MoE 和 Dense 模型上均有效，表明问题具有普遍性，DynaPipe 具备良好的通用性。

## 7. 优点
- **问题挖掘**：首次系统性地识别并量化了 LLM 推理流水线中**采样导致的气泡问题**，并用实际数据展示其严重性。
- **方案优雅**：通过实时层重分配和异步 KV 缓存迁移，实现了动态负载均衡，无需修改模型结构，与现有流水线系统兼容。
- **工程实现精巧**：预加载权重 + 通信计算重叠的迁移设计避免了调试中的长停顿；滑动窗口阈值的稳定性设计避免了配置震荡。
- **实验全面**：覆盖不同模型、数据集、并发量、O:I 比、网络环境，对比充分，消融严谨，提供了闭环验证。

## 8. 不足与局限
- **内存开销**：为支持动态重分配，需预加载额外的层权重，导致 GPU 内存使用增加（如 32B 模型约增加 7.5%），降低了内存利用效率。
- **通信开销**：KV 缓存迁移带来额外的跨 GPU 通信代价，尽管通过异步和重叠隐藏大部分延迟，但在小批量或低带宽环境中仍可能影响性能。
- **并行范式的局限**：当前仅针对**纯流水线并行**设计，未与张量并行、序列并行或专家并行等其他并行策略联合优化；文中未来工作方向也提及了这一点。
- **实验未完全消除随机性**：虽然结果趋势稳定，但论文未展示所有实验的多次运行误差条，可能缺少统计显著性的严格证明。
- **部署场景限制**：评估基于最多 4 卡单机或多节点 TCP 仿真，对于更大规模（如 8 卡以上）或更高速互联（如 NVLink）的场景虽可扩展，但未提供实测数据。

（完）
