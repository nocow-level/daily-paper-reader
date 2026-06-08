---
title: "KVLink: Accelerating Large Language Models via Efficient KV Cache Reuse"
title_zh: KVLink：通过高效KV缓存复用加速大语言模型
authors: "Jingbo Yang, Bairu Hou, Wei Wei, Yujia Bao, Shiyu Chang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=oDcAGSXZZP"
tags: ["query:edge-llm"]
score: 6.0
evidence: 通过复用KV缓存减少LLM冗余计算，利于边缘部署效率
tldr: KVLink针对LLM应用中输入上下文重叠导致的重复编码问题，提出独立预计算文档KV缓存并按需拼接复用的方法。通过缓解独立缓存带来的性能下降，该方法显著减少了推理计算量，为多查询场景下的高效LLM部署提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-odcagsxzzp/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 727, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-odcagsxzzp/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1453, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-odcagsxzzp/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 735, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-odcagsxzzp/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1435, \"height\": 684, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-odcagsxzzp/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1441, \"height\": 1073, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-odcagsxzzp/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1256, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-odcagsxzzp/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1321, \"height\": 648, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-odcagsxzzp/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1460, \"height\": 1113, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-odcagsxzzp/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1458, \"height\": 779, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-odcagsxzzp/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1391, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-odcagsxzzp/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1445, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-odcagsxzzp/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1452, \"height\": 154, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-odcagsxzzp/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1241, \"height\": 321, \"label\": \"Table\"}]"
motivation: LLM在多个查询共享重叠上下文时仍需重复编码整个上下文，导致计算冗余。
method: 独立预计算每个文档的KV缓存，推理时拼接并复用，配合性能损失缓解技术。
result: 减少冗余计算，提升推理效率。
conclusion: KVLink通过缓存复用大幅降低需重复计算的上下文开销，是一种通用LLM推理加速方案。
---

## Abstract
We describe KVLink, an approach for efficient key-value (KV) cache reuse in large language models (LLMs). In many LLM applications, different inputs can share overlapping context, such as the same retrieved document appearing in multiple queries. However, the LLMs still need to encode the entire context for each query, leading to redundant computation. In this paper, we investigate a new strategy to eliminate such inefficiency, where the KV cache of each document is precomputed independently. During inference, the KV caches of retrieved documents are concatenated, allowing the model to reuse cached representations instead of recomputing them. To mitigate the performance degradation when using KV caches computed independently for each document, KVLink introduces two key techniques: adjusting positional embeddings of the KV cache at inference to match the global position after concatenation, and using trainable special tokens to restore self-attention across independently encoded documents. Experiments across 7 datasets demonstrate that KVLink improves question answering accuracy by an average of 4% over state-of-the-art methods. Furthermore, by leveraging precomputed KV caches, our approach reduces time-to-first-token by up to 96% compared to standard LLM inference, making it a scalable and efficient solution for context reuse. Additionally, KVLink can be combined with KV cache compression to further save cache loading and storage overhead while outperforming the baselines.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：在大语言模型（LLM）应用中（如检索增强生成RAG），不同查询往往共享相同的上下文文本（例如同一篇检索文档），但传统推理流程仍需为每个查询从头编码整个拼接后的上下文，造成大量冗余计算和预填充延迟。
- **整体含义**：论文提出 **KVLink**，通过**独立预计算每篇文档的 KV 缓存、在推理时按需拼接复用**的策略，从根本上消除重复编码。同时针对独立编码导致的性能下降，引入位置重编码与可训练链接 token 两项关键技术，实现既高效又高质量的缓存复用。

### 2. 方法论
- **核心思想**：预先将知识库中每篇文档以“无上下文”方式单独通入 LLM，记录其去除位置旋转编码后的纯净 KV 状态。推理时，根据查询检索到的文档，直接加载并拼接这些预计算缓存，仅需少量额外计算即可生成回答。
- **关键技术 1：KV 缓存位置重编码**
  - 独立编码文档时，每个 token 的位次索引仅限于文档内部，拼接后整体位次信息缺失。
  - 解决方案：存储 KV 缓存时**预先移除 RoPE 旋转矩阵**，即仅保留 `W_k x_i` 和 `W_v x_i`；推理拼接后，再为每个 token 根据其全局位置**重新应用对应的 RoPE 旋转**。
  - 这一操作几乎不引入额外延迟，并解决了位次编码不匹配导致的注意力计算错误。
- **关键技术 2：跨文档重连的链接 token（Link Tokens）**
  - 独立编码使后续文档无法关注前序文档，丢失跨文档依赖。
  - 解决方案：在每个文档末尾附加一组**可训练的链接 token**（数量 \(K\)，如 1 或 5）。训练时使用定制注意力掩码：
    - 文档内部的原始 token 仅保留局部因果注意力。
    - 每个链接 token 可以关注**自身文档、所有前序文档及其链接 token**。
  - 推理时，文档 KV 缓存为预计算固定内容；链接 token 的 KV 状态则在加载缓存后**实时计算并拼接**，从而以极低开销重建跨文档注意力通路。
- **与 KV 缓存压缩结合**：为缓解缓存存储开销，KVLink 可与两类压缩方法集成：
  - **LLMLingua**：通过重要性删除压缩 token。
  - **改进的 ANLLM（Anchor-based LLM）**：将文档分块，每块压缩为多个可训练的 anchor token，并设计对应注意力掩码使模型仅依赖 anchor token 进行后续预测。KVLink 在该压缩缓存上依然有效。

### 3. 实验设计
- **评估维度**：
  - 使用独立编码 KV 缓存的问答（QA）与文本摘要性能。
  - 推理效率（首 token 延迟 Time-to-First-Token, TTFT）。
  - 通用能力保持（数学推理、指令跟随等）。
  - 结合 KV 缓存压缩后的表现。
- **数据集**：
  - **QA 任务**：NaturalQuestions (NQ)、2WikiMQA、TriviaQA、HotpotQA、MuSiQue。
  - **摘要任务**：MultiNews、Samsum。
  - **通用能力测试**：IFEval、GSM8K、MMLU、ARC-C/E、PiQA、SciQ、Winogrande、HellaSwag。
- **对比方法**：
  - **PromptCache**：直接复用预计算 KV 缓存，并为其补齐全局位置编码（作者增强版）。
  - **CacheBlend**：拼接缓存后重计算约 18% 的 token 以缓解位次错配。
  - **BlockAttention**：微调模型以适配独立编码的缓存，但不含链接 token。
  - **TurboRAG**：在文档前后加入特殊标记，但标记只限局部注意力，与本方法对比补充。
  - **标准解码（Upperbound）**：完整拼接编码，作为性能上界。
- **模型规模**：基于 Llama-3.2-1B-Instruct、Llama-3.2-3B-Instruct、Llama-3.1-8B-Instruct 进行微调与测试。
- **微调数据混合**：混合了 TriviaQA、2WikiMQA 的检索增强 QA 数据、多轮对话数据（DaringAnteater）、摘要数据（XSum）、标准 SFT 数据（Tülu3）以及少量预训练数据（FineWeb），各部分按比例组合。

### 4. 资源与算力
- **训练资源**：使用 **8 块 H100 GPU**，全局批大小为 64，微调 **6000 步**。
- **评估**：推理效率测试在单个 GPU（如 A100 80GB）上进行，测量 TTFT 时包括从 CPU 加载缓存到 GPU 的开销，每个配置运行 100 次（含 10 次预热）。

### 5. 实验数量与充分性
- **实验量**：
  - 在 **7 个下游任务**上对比了 3 种基线及自身变体（0/1/5 个链接 token），覆盖 3 种模型规模，主表（Table 1）结果丰富。
  - 进行了**推理效率测试**（Figure 3），在不同上下文长度（1000–5000 tokens）下比较 TTFT。
  - **通用能力保持**实验（Table 2），覆盖 10 个基准。
  - **缓存压缩实验**（Table 3），对比两种压缩方法在 50%/75% 压缩率下的表现。
  - **消融实验**（Table 5）：测试不同数据混合（去除摘要、去除多轮对话、仅用 QA 数据）的影响。
  - 额外对比 TurboRAG（Table 6）。
- **充分性与公平性**：
  - 使用相同的微调数据和超参数对比 BlockAttention 等方法，保证了公平性。
  - 覆盖了从 1B 到 8B 的模型规模，实验设计全面，结果具有说服力。
  - 部分实验（如通用能力）仅与微调后模型比较，未单独列出训练前后变化，但整体仍能反映能力保持水平。

### 6. 主要结论与发现
- **性能提升**：KVLink 在所有 QA 数据集上均显著优于所有基线，平均准确率比最佳基线 BlockAttention 高出约 4%，并通过增加链接 token 数量可进一步提升。
- **效率飞跃**：利用预计算 KV 缓存，TTFT 相比标准解码降低 **最高 96%**（5000 token 上下文），且延迟增加极微。
- **能力保持**：KVLink 在数学推理、指令跟随、常识问答等通用任务上，与同等微调的标准模型表现相当，未出现严重能力退化。
- **压缩兼容**：KVLink 可无缝结合 KV 缓存压缩技术，在缓存存储和加载开销大幅降低的情况下，仍优于压缩后的基线方法。
- **链接 token 有效**：跨文档的链接 token 是性能提升的关键，仅依靠位置编码调整（KVLink 0）或 BlockAttention 均无法达到同等效果。

### 7. 优点
- **方法简洁高效**：通过解耦位次编码和引入极少量的链接 token，以极低成本解决了缓存复用的性能损失，实现“预计算一次，多次使用”。
- **即插即用潜力**：可与现有 KV 缓存压缩、逐出策略等方法结合，进一步降低存储与传输负担。
- **实验全面**：在多种模型规模、多类任务（QA、摘要、通用能力）上进行了详细评估，对比基线涵盖现有主流缓存复用方案，消融和压缩实验等增强了结论的稳健性。
- **通用性设计**：架构无关，仅需修改注意力掩码和添加少量 token，可适配各类 transformer 结构。

### 8. 不足与局限
- **存储开销依旧可观**：虽然 KVLink 本身加速推理，但预计算文档的完整 KV 缓存比原文本占用大数百倍（如 1k token 文档文本约 5KB，Llama3-8B 缓存约 131MB），存储和加载成本是大规模部署的挑战（论文在附录中讨论了分层存储等系统级方案）。
- **压缩后仍有性能下降**：结合 KV 缓存压缩后性能无法完全恢复至未压缩水平，更高压缩率时更为明显。
- **训练数据依赖**：性能受微调数据混合影响，文中初步消融显示移除多轮对话或摘要数据会导致某些任务指标变化，最佳数据配比仍待探索。
- **未报告统计显著性**：实验结果未提供置信区间或误差条，缺少对波动性的分析。
- **应用范围**：主要针对“文档级”上下文复用场景（如 RAG），若上下文块间依赖关系复杂且非模块化，链接 token 的有效性可能需要重新设计。

（完）
