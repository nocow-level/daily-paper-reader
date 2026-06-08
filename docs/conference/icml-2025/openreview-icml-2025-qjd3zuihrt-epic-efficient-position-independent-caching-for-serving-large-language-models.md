---
title: "EPIC: Efficient Position-Independent Caching for Serving Large Language Models"
title_zh: EPIC：高效的位置无关缓存用于大语言模型服务
authors: "Junhao Hu, Wenrui Huang, Weidong Wang, Haoyi Wang, tiancheng hu, zhang qin, Hao Feng, Xusheng Chen, Yizhou Shan, Tao Xie"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=qjd3ZUiHRT"
tags: ["query:edge-llm"]
score: 7.0
evidence: 位置无关缓存跨请求重用KV向量，提升LLM服务效率
tldr: 针对现有LLM上下文缓存要求前后缀完全匹配、限制重用场景的问题，提出位置无关缓存(PIC)，允许模块化重用KV向量而与位置无关，从而在少样本学习和RAG等场景下有效降低内存开销、提升服务效率。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 854, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 845, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1748, \"height\": 756, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 853, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 853, \"height\": 1397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 840, \"height\": 127, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 853, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 589, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qjd3zuihrt/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 863, \"height\": 1351, \"label\": \"Figure\"}]"
motivation: 现有上下文缓存仅支持前缀完全匹配，无法在文档前缀变化时复用不可变内容。
method: 提出位置无关缓存技术，使KV向量能被模块化重用而不受序列位置影响。
result: 在多种场景下显著提高LLM服务吞吐量并减少内存占用。
conclusion: EPIC通过位置无关缓存扩展了LLM缓存重用的适用范围。
---

## Abstract
Large Language Models (LLMs) show great capabilities in a wide range of applications, but serving them efficiently becomes increasingly challenging as requests (prompts) become more complex. Context caching improves serving performance by reusing Key-Value (KV) vectors, the intermediate representations of tokens that are repeated across requests. However, existing context caching requires exact prefix matches across requests, limiting reuse cases in settings such as few-shot learning and retrieval-augmented generation, where immutable content (e.g., documents) remains unchanged across requests but is preceded by varying prefixes. Position-Independent
Caching (PIC) addresses this issue by enabling modular reuse of the KV vectors regardless of prefixes. We formalize PIC and advance prior work by introducing EPIC, a serving system incorporating our new LegoLink algorithm, which mitigates the inappropriate “attention sink” effect at every document beginning, to maintain accuracy with minimal computation. Experiments show that EPIC achieves up to 8× improvements in Time-To-First-Token (TTFT) and 7× throughput gains over existing systems, with negligible or no accuracy loss.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）在问答、聊天等应用中被广泛使用，但复杂请求（如多文档问答、少样本学习、检索增强生成）使得提示词变得很长，且包含大量可复用的不可变文本片段。
- **现有局限**：传统上下文缓存（prefix-based caching）要求请求之间具有完全相同的前缀，才可复用 Key-Value（KV）向量。当同一批文档在不同请求中前面附带不同的前缀（如不同的用户指令或系统消息）时，前缀缓存失效，复用机会大幅减少。
- **整体含义**：论文形式化提出了**位置无关缓存（Position-Independent Caching, PIC）**，允许在任意前缀下模块化地复用不可变 token 的 KV 向量。针对 PIC 在偏离标准注意力机制时带来的准确度损失，提出了 **EPIC 服务系统**及**LegoLink 算法**，以极小的计算代价缓解准确度下降，从而显著提升首 token 生成时间（TTFT）和吞吐量。

## 2. 论文提出的方法论

- **两步框架（编译-链接）**
  - **编译（Compile）**：用户将各不可变内容块单独提交给 LLM，以零起始位置 ID 做一次 prefill，生成对应的 KV 向量并存储，返回缓存 ID。此步类似编译位置无关代码。
  - **链接（Link）**：用户发送包含可变 token 与缓存 ID 的请求，系统检索并拼接缓存 KV 向量，再选择性重算一部分 KV 向量以恢复准确度，之后进入解码阶段。
- **LegoLink 算法核心思想**
  - 关键观察：每个文档块的开头几个 token 因位置从零开始而成为“注意力沉没（attention sink）”，异常吸引注意力，阻碍后续 token 关注相关内容。
  - 解决方案：在链接时，对除了第一块以外的每个文档块，重算其前 \(k\) 个 token（\(k \le 32\)）。这些 token 会因重新计算而“意识到”自己的非起始位置，削弱注意力沉没效应，使注意力能正确转移到相关信息。
  - 计算步骤：
    1. 选取所有块的前 \(k\) 个 token（总计 \(k'\) 个）连同用户查询 token，获取嵌入 \(E\)。
    2. 对每一层：计算这些 \(k'\) 个 token 的 \(Q, K, V\)。
    3. 将未选中的 \(N-k'\) 个 token 的缓存 KV 向量与刚计算的 \(K, V\) 拼接，得到 \(K_{exp}, V_{exp}\)。
    4. 计算带掩码的注意力 \(A = \text{softmax}(Q K_{exp}^T \cdot \text{MASK})\)。
    5. 输出 \(O = A V_{exp} W_O\)。
  - 复杂度：\(O(kN) \sim O(N)\)，\(k \ll N\)，且 \(k\) 随文档块数量增加而增加，而不随序列总长度 \(N\) 二次增长。
- **静态稀疏性**：LegoLink 预先固定要重算的 token（每块前 \(k\) 个），无需像 CacheBlend 那样在第一层全量计算后动态选择 token，大幅降低运行时代价。
- **极端变体 LegoLink‑0**：编译时在每个块前添加少量虚拟 token 吸收注意力沉没，并在存储 KV 前丢弃这些虚拟 token 的 KV 向量，实现链接阶段零重算成本，仍能保持较好准确度。

## 3. 实验设计

- **数据集**：
  - LongBench 中的 2WikiMQA、MuSiQue（多文档问答）、SAMSum（少样本指令跟随）、MultiNews（多文档摘要）
  - HotpotQA（多文档问答，用于细粒度分析）
  - Needle in a Haystack（长上下文检索测试）
  - 所有数据集各 200 个测试案例，可变 token 占比极低（95%–99% 为不可变 token）
- **评价指标**：
  - **TTFT**（首 token 生成时间）：衡量 prefill 阶段耗时
  - **F1 分数**（用于 2WikiMQA、MuSiQue、HotpotQA、Needle）
  - **Rouge‑L 分数**（用于 SAMSum、MultiNews）
- **对比方法**：
  - **Naive**（直接拼接缓存 KV，不重算）
  - **Fully Recompute (FR)**（全量重算，等同无缓存 prefill）
  - **CacheBlend‑r**（动态选择 \(r\%\) token 重算，以 CacheBlend‑15 为主要基线）
  - **LegoLink‑k**（重算每块前 \(k\) 个 token，如 \(k=2,4,8,16,32\)）
- **模型**：Mistral 7B Instruct、Llama 3.1 8B Instruct、Yi Coder 9B Chat
- **工作负载**：
  - **同步工作负载**：顺序处理测试用例，评估无并发时的准确度‑延迟权衡
  - **异步工作负载**：模拟多用户，用 2WikiMQA 构造不同到达率（泊松分布）和不同上下文缓存占比（CCR）场景，测量吞吐量和 TTFT

## 4. 资源与算力

- **硬件环境**：单台 NVIDIA A100 服务器，GPU 为 A100‑80GB ×1，CPU 为 128 核 Intel Xeon Platinum 8358P，1TB 内存。
- **软件**：Ubuntu 20.04，Linux 5.16.7，CUDA 12.6，vLLM 0.4.1。
- **训练**：本文为推理服务系统研究，**未进行模型训练**，不涉及训练算力报告。

## 5. 实验数量与充分性

- **实验组数**：
  - 6 个数据集 × 3 个模型 × 多种算法配置（FR、Naive、CacheBlend 多比例、LegoLink 多 k 值）→ 大量数据点（准确度‑延迟平面）。
  - 同步负载下的准确度与 TTFT 全面对比（图 6）。
  - 针对异步负载的 TTFT 与吞吐量对比（图 8）：多种请求率和 CCR 组合。
  - 长上下文压力测试：固定块大小、变化总长度，对比 FR、CacheBlend‑15、LegoLink‑16 的 TTFT 增长与 OOM 情况（图 9）。
  - 消融分析：引入 LegoLink‑0，展示零链接开销的可行性与注意力图变化（图 7）。
  - 额外分析：CacheBlend 的运行时开销分解（图 10）。
- **充分性评价**：实验覆盖多种任务类型、模型架构、算法变体，同时包含同步/异步、短/长上下文场景，维度较为全面。对比基线选择合理（当前最优 CacheBlend），且测试了不同超参数（\(k\) 和重算比例）。总体实验设计客观、公平，能够支撑论文的主要主张。

## 6. 主要结论与发现

- **准确度与效率的帕累托最优**：LegoLink 在准确度‑TTFT 平面上建立起新的帕累托前沿，多数情况下优于 CacheBlend。
- **极低重算即可保持准确度**：LegoLink‑2 可将准确度下降控制在 0%–7% 以内，TTFT 较 CacheBlend‑15 降低最高 3×；CacheBlend 在相似重算 token 数时准确度大幅下降。
- **异步场景显著增益**：LegoLink‑16 相比 CacheBlend‑15，TTFT 降低最多 8×，吞吐量提升最多 7×，且在高缓存占比下延迟更稳定。
- **支持更长上下文**：LegoLink‑16 的 TTFT 随长度呈近似线性增长，而 FR 和 CacheBlend 呈二次增长；CacheBlend 在约 35k token 处 OOM，LegoLink 可支持到约 50k token。
- **注意力沉没是主要障碍**：LegoLink‑0 通过提前消除起始 token 的注意力沉没，实现了零链接开销下的良好准确度，进一步验证了注意力沉没问题的重要性。

## 7. 优点

- **形式化框架**：明确将 PIC 抽象为编译‑链接两步，统一了现有工作，也为未来研究提供清晰方向。
- **算法简单有效**：LegoLink 仅重算每块的前 \(k\) 个 token，易于实现，却显著优于需要动态选择 token 的 CacheBlend。
- **静态稀疏降低开销**：相比 CacheBlend 的动态稀疏和第一层全量重算，静态选择 token 极大压缩了链接阶段的运行时开销。
- **系统实用性强**：基于 vLLM 实现，提供类 OpenAI 兼容 API，显式缓存管理，易于集成到现有 LLM 服务架构中。
- **零链接开销探索**：LegoLink‑0 展示了通过编译时消除注意力沉没，可实现链接阶段完全无开销的极端高效方案。

## 8. 不足与局限

- **模型与任务泛化性**：部分模型（Yi Coder 9B）在文档理解任务上本身表现差，导致所有算法准确度都较低，可能影响对 PIC 方法增益的评估；在 MultiNews 等任务上小模型普遍表现不佳。
- **冗长输出问题**：某些稀疏算法（包括 LegoLink 的部分变体）生成的回答虽然正确但过于冗长，导致 F1/Rouge‑L 等基于词重叠的自动评价指标偏低，未能完全反映真实质量。
- **异步负载构造简略**：PIC 缺乏公开真实 trace，模拟多用户场景时假定各用户反复发送同一查询，可能与真实使用模式存在偏差。
- **模型规模受限**：仅在 7B–9B 参数量的模型上评估，未在更大规模（>10B）模型或 MoE 模型上验证，对更昂贵推理环境下的优势尚待确认。
- **硬件环境单一**：所有实验均在单张 A100‑80G 上完成，未分析多 GPU 或分布式场景下的表现。
- **缓存存储层未深度优化**：作者自述 KV 存储实现较为基础，未针对大规模缓存管理做极致的性能调优。

（完）
