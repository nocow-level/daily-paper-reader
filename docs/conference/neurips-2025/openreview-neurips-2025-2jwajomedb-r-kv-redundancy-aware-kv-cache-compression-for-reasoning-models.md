---
title: "R-KV: Redundancy-aware KV Cache Compression for Reasoning Models"
title_zh: R-KV：面向推理模型的冗余感知KV缓存压缩
authors: "Zefan Cai, Wen Xiao, Hanshi Sun, Cheng Luo, Yikai Zhang, Ke Wan, Yucheng Li, Yeyang Zhou, Li-Wen Chang, Jiuxiang Gu, Zhen Dong, Anima Anandkumar, Abedelkadir Asi, Junjie Hu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=2jwAjomEDB"
tags: ["query:edge-llm"]
score: 9.0
evidence: 压缩KV缓存以减少LLM推理的内存占用
tldr: "该论文针对推理模型生成长输出导致KV缓存过大的问题，提出冗余感知的KV缓存压缩方法R-KV，可识别并移除冗余令牌。实验表明，仅用10%的缓存即可几乎保持全量缓存性能，大幅超越现有基线。该方法显著降低了内存需求，有助于在资源受限硬件上部署大模型推理。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1432, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1438, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 812, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1312, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 978, \"height\": 318, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 709, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-2jwajomedb/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 431, \"height\": 336, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-2jwajomedb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 577, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-2jwajomedb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-2jwajomedb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1449, \"height\": 1018, \"label\": \"Table\"}]"
motivation: 推理模型生成输出过长，导致KV缓存膨胀，现有压缩方法可能引起推理失败。
method: 提出R-KV方法，通过识别推理模型中的冗余令牌来压缩KV缓存。
result: "仅用10%的KV缓存即可保持接近100%的全量性能，显著优于现有方案。"
conclusion: R-KV有效解决了长序列推理的内存瓶颈，为资源受限设备上的高效推理提供了新途径。
---

## Abstract
Reasoning models have demonstrated impressive performance in self-reflection and chain-of-thought reasoning. However, they often produce excessively long outputs, leading to prohibitively large key-value (KV) caches during inference. While chain-of-thought inference significantly improves performance on complex reasoning tasks, it can also lead to reasoning failures when deployed with existing KV cache compression approaches. To address this, we propose Redundancy-aware KV Cache Compression for Reasoning models (R-KV), a novel method specifically targeting redundant tokens in reasoning models. Our method preserves nearly 100% of the full KV cache performance using only 10% of the KV cache, substantially outperforming existing KV cache baselines, which reach only 60% of the performance. Remarkably, R-KV even achieves 105% of full KV cache performance with 38% of the KV cache. This KV-cache reduction also leads to a 50% memory saving and a 2x speedup over standard chain-of-thought reasoning inference. Experimental results show that R-KV consistently outperforms existing KV cache compression baselines across two mathematical reasoning datasets.

---

## 论文详细总结（自动生成）

# 论文总结：R-KV——面向推理模型的冗余感知 KV 缓存压缩

## 1. 核心问题与背景
- **推理模型的部署瓶颈**：DeepSeek‑R1 等推理模型在复杂链式思考（CoT）生成中表现优异，但其输出长度极长（可达真实答案的 8 倍以上），导致 KV 缓存急剧膨胀，带来巨大的内存和计算压力。
- **现有 KV 缓存压缩的失效**：当前主流的 KV 缓存压缩方法（如 SnapKV）主要针对长输入提示词设计，且常用纯注意力重要性筛选。在推理模型中，反复出现的冗余内容（如自我反思、重复验证）会获取高注意力分数，导致这些无意义的重复 token 被保留，而关键推理片段却被误删，严重影响推理正确率。
- **论文动机**：因此，需要一种能识别并压缩推理模型中大量冗余 token 的方法，在有限的缓存预算内保留最重要且非重复的上下文，以维持推理性能。

## 2. 方法论：R‑KV 冗余感知 KV 缓存压缩
- **核心思想**：在解码阶段进行 KV 缓存压缩，联合考虑 token 的**重要性**（基于注意力权重）和**冗余度**（基于键向量的语义相似性），实现“去重留精”。
- **关键技术组件**：
  - **解码时压缩机制**（§3.1）：设定缓存预算 `B_budget` 和缓冲大小 `B_buffer`，每生成 `B_buffer` 个 token 后进行一次压缩。始终保留最后 α 个 token 作为观察窗口，其余候选 token 通过联合分数选择，保留 `B_budget - α` 个 token。
  - **重要性评分**（§3.2）：利用最后 α 个观察 token 对应的注意力权重。对多头注意力（MHA）直接计算 softmax 注意力矩阵；对分组查询注意力（GQA）则采用查询头组内 max‑pooling 后再 softmax。然后通过滑动窗口 max‑pooling 稳定化，得到每个 token 的重要性得分 `I_i^h`。
  - **冗余度估计**（§3.3）：对每一头的键向量进行 L2 归一化后计算余弦相似度矩阵，剔除对角线，并强制保留最近 β 个高相似度 token（将其相似度置零），再计算平均相似度并 softmax 得到冗余得分 `R_i^h`。
  - **联合选择策略**（§3.4）：最终 token 保留分数为 `Z_i^h = λ I_i^h - (1-λ) R_i^h`。其中 λ 控制重要性与冗余度的权衡（实验证明 λ=0.1 效果最佳）。按该分数从候选 token 中选取 Top‑k 保留。

## 3. 实验设计
- **模型**：DeepSeek‑R1‑Distill‑Llama‑8B（简称 R1‑Llama‑8B）和 DeepSeek‑R1‑Distill‑Qwen‑14B（R1‑Qwen‑14B）。
- **数据集**：数学推理基准 MATH‑500 和 AIME 2024。
- **对比方法**：
  - **FullKV**：保留完整 KV 缓存，作为性能上限。
  - **SnapKV**：原本用于预填充阶段的注意力淘汰方法，本工作中被适配为同样周期进行解码时压缩，保持相同的预算和缓冲设置。
- **评估设置**：采用 pass@1 指标，每个问题生成 64 条回答，使用推荐的温度（0.6）和 top‑p（0.95）采样。最大生成长度设为 MATH‑500 为 16,384 tokens，AIME 2024 为 32,768 tokens。

## 4. 资源与算力
- 所有实验均在 **NVIDIA A100 80GB GPU** 上完成，未提及使用多卡训练（方法为训练自由，不涉及训练）。
- 论文未提供每项实验的具体 GPU 耗时或硬件数量，但提供了推理阶段的吞吐量和解码时间分析，可作为效率参考。

## 5. 实验数量与充分性
- **多预算对比**：针对两种模型在两个数据集上，设置了从 128 至 4096 等多个绝对缓存预算，对比 R‑KV、SnapKV 和 FullKV 的准确率，覆盖了极低预算到接近无损的范围。结果显示 R‑KV 几乎在全部预算下均显著优于 SnapKV。
- **消融实验**：对 λ 取值（0, 0.01, 0.1, 0.2, 0.4, 1）进行敏感性分析，说明仅靠冗余或仅靠注意力都会导致性能下降，λ=0.1 最优。
- **效率分析**：在不同生成长度（8K, 16K）下，对比了 R‑KV、SnapKV 和 FullKV 的内存节省比例、最大批量大小和端到端吞吐量，展示了实际部署收益。
- **定性案例**：提供可视化对比，展示 R‑KV 选择的 token 分布更均匀、覆盖更多有效信息，而 SnapKV 则集中在局部冗余段落。
- 实验覆盖了不同模型规模（8B, 14B）和不同难度推理任务，具有较好的充分性；对主要对比方法 SnapKV 的适配也保证了公平竞争。

## 6. 主要结论与发现
- **高效的压缩性能**：R‑KV 仅用 10%–34% 的原始 KV 缓存，即可达到与 FullKV 几乎相同的推理准确率（无损压缩）；在某些配置下甚至实现 105% 的 FullKV 性能（如 R1‑Llama‑8B 在 AIME24 上，16% 缓存）。
- **显著优于现有 baseline**：在相同预算下，R‑KV 较 SnapKV 准确率最高提升 40 个百分点，而 SnapKV 只能达到 FullKV 约 60% 的性能。
- **实际效率大幅提升**：在长序列场景下，R‑KV 可实现 90% 内存节省，最大批量扩大 9 倍以上，吞吐量提升高达 6.6 倍。
- **训练自由、即插即用**：方法完全依赖推理阶段的动态计算，无需额外训练或更改模型结构，适用于强化学习 rollout 和 LLM 服务。

## 7. 优点
- **创新性地引入冗余感知**：弥补了纯注意力淘汰在面对推理模型大量重复内容时的盲点，从“重要性+去冗余”双向优化缓存利用。
- **方法清晰、可复现**：对 MHA 和 GQA 的适配、重要性稳定化、相似度计算和 β 保留机制均有详细公式与实现，代码已开源。
- **实验评价严谨**：使用 pass@1 和多次采样，避免了贪婪解码带来的评估波动；效率分析既包含绝对预算又包含比例预算，贴近实际部署。
- **实际价值高**：在推理模型快速发展的背景下，该方法为缓解长序列推理的内存瓶颈提供了直接可用的方案。

## 8. 不足与局限
- **跨任务泛化未验证**：实验仅局限于数学推理（MATH‑500、AIME），未在更广泛的推理任务（如编程、科学推理）上测试，可能存在领域偏差。
- **与高级 attention 机制兼容性**：论文指出目前不兼容 paged attention 等推理优化，且在没有专用压缩接口的服务框架中，内存重分配可能带来额外开销。
- **超参数依赖性**：λ、β、T 等超参数的选择基于特定模型和数据集，迁移至新场景时可能需要额外调整。
- **未与更多基线比较**：主要比较对象为 SnapKV，缺乏与 H2O、StreamingLLM 等解码阶段缓存方法的直接对比（但论文将此归因于关注点不同）。

（完）
