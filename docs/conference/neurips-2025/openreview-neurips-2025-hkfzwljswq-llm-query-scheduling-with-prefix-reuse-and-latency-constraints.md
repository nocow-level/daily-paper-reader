---
title: LLM Query Scheduling with Prefix Reuse and Latency Constraints
title_zh: 具有前缀重用和延迟约束的大语言模型查询调度
authors: "Gregory Dexter, Shao Tang, Ata Fatahibaarzi, Qingquan Song, Tejas Dharamsi, Aman Gupta"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=HKfZwLjSwQ"
tags: ["query:edge-llm"]
score: 8.0
evidence: 带前缀重用的查询调度用于延迟约束下的高效LLM推理
tldr: 针对LLM在线推理的延迟约束问题，提出基于前缀重用的查询调度理论框架，揭示了现有FCFS和LPM策略的局限，并设计了更优的调度算法以同时满足TTFT和TPOT需求。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-hkfzwljswq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1123, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-hkfzwljswq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 662, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-hkfzwljswq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1440, \"height\": 1126, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-hkfzwljswq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 813, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hkfzwljswq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 811, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-hkfzwljswq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 217, \"label\": \"Table\"}]"
motivation: LLM在线服务需在严格延迟约束下优化推理性能。
method: 建立RadixAttention前缀重用下的查询调度理论框架，设计新的调度策略。
result: 理论分析和实验证明新调度算法显著优于现有策略。
conclusion: 该框架为延迟敏感型LLM部署提供了调度优化基础。
---

## Abstract
The efficient deployment of large language models (LLMs) in online settings requires optimizing inference performance under stringent latency constraints, particularly the time-to-first-token (TTFT) and time-per-output-token (TPOT). This paper focuses on the query scheduling problem for LLM inference with prefix reuse, a technique that leverages shared prefixes across queries to reduce computational overhead. Our work reveals previously unknown limitations of the existing first-come-first-serve (FCFS) and longest-prefix-match (LPM) scheduling strategies with respect to satisfying latency constraints. We present a formal theoretical framework for LLM query scheduling under RadixAttention, a prefix reuse mechanism that stores and reuses intermediate representations in a radix tree structure. Our analysis establishes the NP-hardness of the scheduling problem with prefix reuse under TTFT constraints and proposes a novel scheduling algorithm, $k$-LPM, which generalizes existing methods by balancing prefix reuse and fairness in query processing. Theoretical guarantees demonstrate that $k$-LPM achieves improved TTFT performance under realistic traffic patterns captured by a data generative model. Empirical evaluations in a realistic serving setting validates our findings, showing significant reductions in P99 TTFT compared to baseline methods.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机
- **背景**：大语言模型（LLM）在线推理需在严格延迟约束（如首Token时间 TTFT 和每输出Token时间 TPOT）下优化吞吐，即“有效吞吐”（goodput）。
- **问题**：基于前缀重用（RadixAttention）的LLM推理中，查询调度策略对性能有重大影响，但现有先到先服务（FCFS）和最长前缀匹配（LPM）调度算法在满足延迟约束方面存在未知局限，尤其在高负载场景下可能导致TTFT尖峰。
- **目标**：形式化该调度问题，揭示其复杂性，并设计一个能稳健平衡前缀重用与等待时间的调度算法。

### 2. 方法论核心
- **计算模型**：定义查询流 \( Q \) 和LLM实例计算模型（Definition 2），该模型捕获了前缀复用带来的计算缩减以及查询的到达时间约束，聚焦于预填充主导（prefill-dominant）场景。
- **复杂性分析**：证明在 RadixAttention 和TTFT约束下，判定查询流是否存在可行调度是 **NP-Hard** 问题（Theorem 1），这与无前缀重用或所有查询同时到达的情况形成对比。
- **核心算法：\( k \)-LPM**
    - **思想**：通过超参数 \( k \) 泛化 FCFS 和 LPM。其流程为：先执行 \( k-1 \) 次贪心选择，处理当前队列中与上一查询前缀共享最多的查询；然后处理队列中等待时间最长的查询。当 \( k=1 \) 时退化为 FCFS，当 \( k \to \infty \) 时退化为 LPM。
    - **理论保证**：针对一个反映真实流量模式的数据生成模型（Definition 4，具有树形前缀结构和随机到达的查询流），证明 \( k \)-LPM 在最大TTFT上能同时优于 FCFS 和 LPM（Theorem 2, Corollary 3）。
    - **近似算法**：此外，在附录A中提供了一个近似算法，能在多项式时间内返回一个满足 \( (1-p) \) 分位数TTFT约束的调度，或证明其不可行。

### 3. 实验设计
- **场景与数据**：模拟在线服务场景，使用一个真实的工业级推荐系统提示数据集（Team [2025]，2400个提示，结构为 `(指令)(用户画像)(历史交互)(问题)`），随机打乱后用于基准测试，其中前三个部分构成可共享的前缀。
- **基准与指标**：在 SGLang v0.4.1 推理框架上，使用其提供的服务基准测试工具。核心评估指标是不同请求率（泊松到达过程）下的 **P99 TTFT**，并观察P50、P90、P95等百分位指标。
- **对比方法**：将 \( k \)-LPM 算法在不同 \( k \) 值（\( k=1 \) 即 FCFS，\( k=2,3,4,1000 \)，以及 \( k=\infty \) 即 LPM）下的性能进行对比。
- **额外实验**：在单GPU上使用 Llama-3.2-1B 模型，构造合成数据（Definition 4），通过改变可重用前缀长度与总长度的比例，进一步验证算法在不同前缀复用程度下的表现。

### 4. 资源与算力
- **主实验资源**：使用 **8块A100 GPU**，通过张量并行（tensor parallelism）服务 **Llama-3.1-8B-Instruct** 模型。论文未提及整个实验的总运行时长，但指明了推理服务环境。
- **合成实验资源**：使用 **1块H100 GPU** 服务 Meta-Llama-3.2-1B-Instruct 模型。
- **代码与数据**：论文公开了算法细节和实验配置，但由于数据权限限制，未公开其所用的具体真实数据集。

### 5. 实验数量与充分性
- **实验组数**：
    1.  **主实验**：在一个真实数据集上，针对5种 \( k \) 值，测量了随请求率连续变化的P99 TTFT曲线。
    2.  **补充分析**：提供了该数据集上的P50、P90、P95、P99 TTFT的多维对比图表（Figure 3）。
    3.  **消融实验**：在合成数据上，针对3种代表性的 \( k \) 值（1, 4, ∞），测试了3种不同前缀长度比例下的TTFT表现（Table 1）。
- **充分性与公平性**：实验设计较为全面，覆盖了核心算法参数、关键性能指标和不同的数据特性。所有方法在相同的硬件、模型框架和数据流下进行对比，保证了公平性。不足在于缺乏多轮实验的统计误差信息。

### 6. 主要结论与发现
- \( k \)-LPM 算法在中到高负载下，其 **P99 TTFT 显著低于 FCFS 和 LPM**。
- 实验结果准确地验证了理论预测：FCFS 在低负载下表现更好，LPM 在高负载下更有优势，而 \( k \)-LPM 在更广泛的负载范围内表现鲁棒。
- 即使在实际部署中不完全满足理论的严格假设（如精确的树形结构、均匀重复），\( k \)-LPM 依然有效。选择适中的 \( k \) 值（如2或3）能有较好的性能平衡。

### 7. 优点
- **理论奠基**：首次为带前缀重用的LLM调度问题建立了严格的计算复杂性分析（NP-Hard），为后续研究提供了理论基础。
- **算法简洁实用**：提出的 \( k \)-LPM 算法是一个轻量级、易实现的插件，能够无损地集成到现有服务框架中，且兼容已有的FCFS和LPM策略。
- **理论与实际结合**：不仅在理论模型上证明了最优性，还在真实的工业级模型和数据上进行了验证，展示了从理论洞察到实践效果的转化能力。

### 8. 不足与局限
- **模型与假设简化**：计算模型假设批大小为1且仅考虑预填充阶段，虽进行了讨论，但可能忽略了连续批处理和解码阶段的复杂交互。数据生成模型也依赖于树形前缀结构等强假设。
- **实验覆盖范围**：真实数据集实验仅限于一个推荐系统的用例，模型的泛化性有待更多样化的场景（如代码生成、长文档摘要）验证。
- **可重复性与统计性**：因数据权限未公开数据集，且实验部分未提供误差条或多次运行结果的统计分析，使得结果的统计显著性难以精确评估。
- **超参数选择**：\( k \) 值的最优选择依赖于工作负载特性，论文未提供在线自适应选择 \( k \) 的策略，这在实际动态环境中是一个待解决的问题。

（完）
