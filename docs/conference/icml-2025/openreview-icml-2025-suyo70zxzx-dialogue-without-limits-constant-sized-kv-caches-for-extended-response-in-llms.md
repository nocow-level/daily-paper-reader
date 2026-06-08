---
title: "Dialogue Without Limits: Constant-Sized KV Caches for Extended Response in LLMs"
title_zh: 无限制对话：用于LLM扩展响应的恒定大小KV缓存
authors: "Ravi Ghadia, Avinash Kumar, Gaurav Jain, Prashant J. Nair, Poulami Das"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=SuYO70ZxZX"
tags: ["query:edge-llm"]
score: 8.0
evidence: 恒定大小KV缓存的LLM高效推理
tldr: 针对自回归Transformer中KV缓存线性增长导致的内存和带宽瓶颈，MorphKV提出一种推理时技术，通过自适应令牌排序和相关性感知选择，维持恒定大小缓存而不牺牲精度。它消除了早期令牌偏差，平衡了长程依赖与局部一致性。实验表明该方法能有效支持LLM的扩展响应生成，为资源受限设备上的长文本推理提供了新思路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 842, \"height\": 273, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1746, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1578, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 845, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 841, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 844, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1759, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-suyo70zxzx/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1741, \"height\": 714, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 642, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 842, \"height\": 665, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1764, \"height\": 619, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 854, \"height\": 133, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1680, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 875, \"height\": 587, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 857, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1420, \"height\": 793, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1061, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-suyo70zxzx/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 832, \"height\": 179, \"label\": \"Table\"}]"
motivation: LLM中KV缓存随上下文线性增长导致内存消耗过高，影响长文本生成。
method: 提出MorphKV，通过相关性感知选择自适应排序令牌，维持恒定大小KV缓存。
result: MorphKV在保持精度的同时实现恒定内存占用。
conclusion: MorphKV是一种无需训练的免损推理技术，有效解决长上下文内存瓶颈。
---

## Abstract
Autoregressive Transformers rely on Key-Value (KV) caching to accelerate inference. However, the linear growth of the KV cache with context length leads to excessive memory consumption and bandwidth constraints. Existing methods drop distant tokens or compress states in a lossy manner, sacrificing accuracy by discarding vital context or introducing bias.

We propose ${MorphKV}$, an inference-time technique that maintains a constant-sized KV cache while preserving accuracy. MorphKV balances long-range dependencies and local coherence during text generation. It eliminates early-token bias while retaining high-fidelity context by adaptively ranking tokens through correlation-aware selection. Unlike heuristic retention or lossy compression, MorphKV iteratively refines the KV cache via lightweight updates guided by attention patterns of recent tokens. This approach captures inter-token correlation with greater accuracy, which is crucial for tasks like content creation and code generation. Our studies on long-response tasks show 52.9\% memory savings and 18.2\% higher accuracy on average compared to state-of-the-art prior works, enabling efficient deployment.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的结构化深入总结。

### 1. 论文的核心问题与整体含义

本论文聚焦于大语言模型在**长响应生成任务**中的推理效率瓶颈：**键值（KV）缓存的内存占用随着生成序列长度线性增长，极易超出高端GPU的显存容量**。

-   **研究背景**：自回归Transformer依赖KV缓存来避免重复计算，从而加速解码。但在长对话、文章撰写、代码生成等需要生成数千乃至上万token的场景中，KV缓存成为内存和带宽的主要制约因素。
-   **现有方法局限**：
    -   **恒定大小缓存方法**（如Scissorhands， StreamingLLM）通过丢弃远距离token来限制缓存大小，但精度损失严重。
    -   **高精度压缩方法**（如当前最佳SnapKV）虽然在长上下文理解任务中表现良好，但它在解码阶段**保留所有生成的token**，导致KV缓存大小仍随响应长度增长，无法解决长响应任务的根本问题。
    -   其他方法（如H2O）存在**早期token偏见**，即倾向于保留历史中被频繁访问的token，而忽略了未来生成所需的关键上下文。
-   **核心问题与含义**：论文旨在提出一种**在推理时维持恒定大小KV缓存，同时不牺牲生成精度**的技术，实现“无限制对话”，打破内存对LLM生成长度的制约。

### 2. 论文提出的方法论

论文提出了**MorphKV**，一种推理时、免训练的KV缓存动态管理技术。其核心思想是：**利用最近token的注意力模式，自适应地识别并保留与当前上下文最相关的远距离token，从而用固定大小的缓存捕获长程依赖和局部连贯性**。

-   **核心思想与关键机制**：
    -   **上下文分区**：将上下文分为两部分：
        -   **近期上下文（R）**：最近生成的R个token，用于保持局部连贯性。
        -   **远距离上下文（D）**：早期的token，用于捕捉长程依赖。
    -   **缓存结构**：MorphKV维护一个大小为 **C + R** 的恒定KV缓存，其中C是从远距离上下文D中选择保留的token数量。
    -   **相关性感知选择**：核心洞见在于，近期token在生成时已经“关注”过远距离token。因此，通过分析近期token的注意力模式，可以推断出哪些远距离token对未来的生成仍然至关重要。MorphKV正是通过这种**迭代更新的相关性感知选择**，来消除早期token偏见，精准保留高保真度的上下文。

-   **算法流程与公式解释**：
    1.  **构建辅助评分向量 `F_i`**：对于当前步 `i`，定义一个包含最近`R`个token的窗口 `W_i`。MorphKV检查这些近期token的注意力权重，为每个远距离token `k`计算一个相关性分数 `F_i[k]`。
        -   计算公式: `F_i[k] = f(AW_i-1[k]， AW_i-2[k]， ...， AW_i-R[k])`
        -   其中 `AW_r[k]` 是近期token `r` 对远距离token `k` 的注意力权重。
        -   **融合函数 `f(·)`**：论文提出了两种选择：
            -   `Sum Fusion`：对窗口内所有近期token的注意力权重求和。该方法倾向于保留被多个近期token持续关注的远距离token。
            -   `Max Fusion`：取窗口内所有近期token的注意力权重的最大值。该方法倾向于保留至少被一个近期token强烈关注的远距离token。
    2.  **动态Token选择与缓存更新**：算法根据评分向量 `F_i`，选出得分最高的`C`个远距离token，并将其KV对与固定的`R`个近期token的KV对合并，构成新的恒定大小KV缓存 `G_{i+1}`。
        -   更新规则: `G_{i+1} = { Top_C(F_i) } ∪ { R recent tokens }`
    3.  **多头注意力处理**：MorphKV兼容多头注意力（MHA）和分组查询注意力（GQA）。对于GQA，它会先聚合同一组内多个查询头的注意力分数，再计算融合分数，从而进一步降低内存开销。

### 3. 实验设计

-   **数据集与场景**：
    -   **长响应生成任务**：
        -   LongWriter：包含邮件、博客、论文、小说等开放式长文本生成，要求100到12000字的响应。
        -   LongGenBench：包含结构化长文本生成，如日记条目、菜单规划、摩天大楼设计、城市规划等。
    -   **长上下文理解任务**：
        -   LongBench：一个双语、多任务的基准，涵盖16K-128K token的上下文，如代码库导航、多文档问答等。
-   **对比方法**：
    -   `SnapKV`：当前最先进的KV缓存压缩方法（基线）。
    -   `H2O`：在解码阶段进行KV缓存剪枝的方法（更相关的基线）。
    -   `Full-Attention`：保留所有token的KV缓存（精度上界）。
-   **评测模型**：在Llama-3.1 8B、Mistral-7B、Qwen2.5 7B、Phi-4 14B四个不同架构和尺寸的最新模型上进行评估，以验证方法的鲁棒性和泛化性。

### 4. 资源与算力

-   **硬件环境**：实验运行在NVIDIA Grace Hopper超级芯片节点上，配置为**单个H100 GPU（96GB HBM3）** 和Grace CPU（116GB LPDDR5），通过NVLink互联。
-   **软件实现**：基于HuggingFace Transformers库实现，并集成了FlashAttention-2以进行硬件感知优化。
-   **训练时长**：MorphKV是一种**推理时**技术，无需任何训练，因此没有提及训练时长。

### 5. 实验数量与充分性

论文进行了多组全面、系统的实验，评估较为充分、客观和公平。

-   **主要对比实验**：
    -   在**2个长响应**和**1个长上下文**基准上，对**4个模型**，对比**3种方法**的性能和内存使用，覆盖了约 （2+1） × 4 × 3 = 36种主要配置。
-   **深度分析实验**：
    -   **性能随响应长度变化**：分析生成长度从400增至1600 token时，不同方法的性能衰减情况。
    -   **超参数敏感性研究**：详细分析了融合函数（`sum` vs `max`）、窗口大小（`R`）、KV缓存预算（`C`）等关键设计参数的影响。
    -   **压缩率鲁棒性测试**：在1%到7%的极端缓存预算下，对比MorphKV与SnapKV的性能差距。
-   **消融与补充实验**：
    -   **粗粒度驱逐策略**：研究了降低KV驱逐频率对性能和吞吐量的影响，探讨了延迟与精度的权衡。
    -   **与正交方法结合**：初步探索了与层级KV缓存保留策略（对浅层保留所有token）结合的效果，证明MorphKV的兼容性。
    -   **输出质量退化分析**：通过测量N-gram重复率，解释了MorphKV为何能超越全注意力，因为它能动态驱逐噪声token，减少文本退化。

### 6. 论文的主要结论与发现

-   **高精度下的恒定内存**：MorphKV在维持恒定大小KV缓存的同时，在长响应任务上的平均精度比SnapKV和H2O分别高出**18.2%** 和**9.4%**，同时KV缓存内存平均节省了**52.9%和88.1%**。
-   **对长度的鲁棒性**：随着响应长度增加，MorphKV的性能衰退（约10%）显著低于SnapKV和H2O（15-18%），表现出更强的鲁棒性。
-   **超越全注意力的能力**：在某些长上下文任务中，MorphKV甚至超越了全注意力模型的表现，因为它有效过滤了无关token的噪声，减少了输出退化（如重复）。
-   **内存效率显著**：兼容GQA架构使MorphKV的内存效率比基于MHA的方法高出**4倍**，带来了极高的系统吞吐量（Table 4显示吞吐量是SnapKV的4.68倍）。

### 7. 优点

-   **问题新颖性强**：首次明确指出并系统性地解决了“长响应”任务中KV缓存尺寸不断增长这一被忽视的问题，与传统的“长上下文”任务优化形成清晰界限。
-   **方法优雅且高效**：
    -   **免训练**：作为即插即用的推理时方法，无需任何额外训练或微调。
    -   **动态自适应**：基于近期token的注意力模式进行动态选择，比基于历史累积重要性的方法更准确和灵活。
    -   **底层架构兼容**：对MHA和GQA均有效，且能利用GQA的特性获得更高内存效率。
-   **实验评估极其详尽严格**：在多个模型、多个基准（长响应与长上下文）、多个维度（性能、内存、吞吐量、长度鲁棒性）上进行了充分对比，并深入分析了各项超参数的影响，说服力强。
-   **开源可复现**：论文提供了开源代码仓库，增强了结果的透明度和可复现性。

### 8. 不足与局限

-   **推理延迟开销**：MorphKV每步都需计算部分注意力并更新缓存，带来了**额外50%的推理延迟**（Table 4），这是其恒定内存优势的代价，虽然可通过粗粒度驱逐来权衡。
-   **与其他优化技术的集成未深入**：论文仅初步探索了与层级KV保留的结合，但承认将其与跨注意力头、跨层优化等方法更深度地集成是未来工作，尚未给出综合性最优方案。
-   **任务类型局限**：评估虽覆盖长响应和长上下文，但主要在结构化生成和摘要类任务上，未涉及需要严格多轮交互和推理的复杂对话场景。
-   **超参数依赖**：虽然鲁棒性较好，但最佳窗口大小（`R`）和缓存预算（`C`）等参数仍需根据具体任务和模型进行调整，没有给出完全自动化的自适应机制。

（完）
