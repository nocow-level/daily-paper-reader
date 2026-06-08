---
title: "RocketKV: Accelerating Long-Context LLM Inference via Two-Stage KV Cache Compression"
title_zh: RocketKV：通过两阶段KV缓存压缩加速长上下文大语言模型推理
authors: "Payman Behnam, Yaosheng Fu, Ritchie Zhao, Po-An Tsai, Zhiding Yu, Alexey Tumanov"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=RyOpooIxDF"
tags: ["query:edge-llm"]
score: 8.0
evidence: 通过KV缓存压缩减少长上下文LLM推理的内存使用
tldr: 针对Transformer大语言模型在长上下文推理时KV缓存随输入长度线性增长、占用大量内存带宽与容量的问题，提出无需训练的RocketKV方法，分两阶段进行永久性粗粒度逐出和基于混合稀疏注意力的细粒度top-k近似，有效压缩KV缓存并加速推理。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 856, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 702, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1409, \"height\": 497, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 725, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 778, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1763, \"height\": 1952, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 846, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1715, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1762, \"height\": 850, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1760, \"height\": 868, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1674, \"height\": 1035, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1670, \"height\": 1044, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ryopooixdf/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1667, \"height\": 1047, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 890, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1365, \"height\": 1417, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1840, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1198, \"height\": 1794, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1695, \"height\": 1417, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1717, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1718, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1710, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1710, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1364, \"height\": 1418, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1840, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1717, \"height\": 1249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1718, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1718, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1718, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1364, \"height\": 1418, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1840, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1718, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1717, \"height\": 1249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1717, \"height\": 1249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ryopooixdf/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1718, \"height\": 1249, \"label\": \"Table\"}]"
motivation: 长上下文LLM推理时KV缓存大小剧增，带来内存带宽和容量压力。
method: 第一阶段粗粒度永久逐出输入序列中不重要的令牌KV，第二阶段采用混合稀疏注意力近似top-k注意力分数。
result: 在多种长上下文任务中显著减少内存占用同时加速推理，保持准确性。
conclusion: RocketKV为长上下文LLM的高效部署提供了一种简单的压缩方案。
---

## Abstract
Transformer-based Large Language Models rely critically on the KV cache to efficiently handle extended contexts during the decode phase. Yet, the size of the KV cache grows proportionally with the input length, burdening both memory bandwidth and capacity as decoding progresses. To address this challenge, we present RocketKV, a training-free KV cache compression strategy containing two consecutive stages. In the first stage, it performs coarse-grain permanent KV cache eviction on the input sequence tokens. In the second stage, it adopts a hybrid sparse attention method to conduct fine-grain top-k sparse attention, approximating the attention scores by leveraging both head and sequence dimensionality reductions. We show that RocketKV provides a compression ratio of up to 400×, end-to-end speedup of up to 3.7× as well as peak memory reduction of up to 32.6% in the decode phase on an NVIDIA A100 GPU compared to the full KV cache baseline, while achieving negligible accuracy loss on a variety of long-context tasks. We also propose a variant of RocketKV for multi-turn scenarios, which consistently outperforms other existing methods and achieves accuracy nearly on par with an oracle top-k attention scheme. The source code is available here: https://github.com/NVlabs/RocketKV.

---

## 论文详细总结（自动生成）

### 1. 论文核心问题与整体含义

- **背景与动机**：Transformer 架构的大语言模型（LLM）在解码阶段依赖 KV 缓存来避免重新计算，但随着上下文长度增长，KV 缓存大小线性膨胀，导致极高的内存带宽和容量压力。例如，Llama3.1-70B 在 batch size 32、序列长度 32K 时需约 320 GB 的 FP16 KV 缓存，超出高端 GPU 的能力。
- **关键观察**：已有研究发现，解码时仅需一小部分 KV token 即可保持精度，但现有方法（永久逐出或动态选择）在低 token 预算下精度显著下降，而“先知 top-k”注意力几乎无精度损失。分析显示，即使序列很长，所有解码步中唯一被 top-k 选中的索引数量也远小于序列长度，说明粗粒度永久逐出结合细粒度动态选择的潜力。
- **整体目标**：提出一种无需训练的 KV 缓存压缩方案 RocketKV，兼顾永久逐出（节省存储与带宽）和动态 top-k 选择（提高近似精度），在微小精度损失下实现高压缩比、显著加速和内存节省，并扩展到多轮对话场景。

### 2. 方法论

RocketKV 由两个连续阶段组成，且可以灵活集成不同技术。

- **第一阶段：粗粒度永久 KV 逐出**
  - 直接采用 **SnapKV**，利用输入上下文末尾“观察窗口”的聚合注意力分数，挑选最重要的 KV token 保留。
  - 针对分组查询注意力（GQA），按注意力组进行选择，而非按头，减少冗余存储。
  - 对池化核大小做了调整（设为 63），以适配粗粒度逐出的需求。

- **第二阶段：细粒度动态 KV token 选择 —— 混合稀疏注意力（HSA）**
  - **步骤 1**：将键张量沿序列维分组为连续页（pages），存储每页的逐元素最大值 $K_{\text{max}}$ 和最小值 $K_{\text{min}}$ 作为辅助数据，按头维对齐布局。
  - **步骤 2**：对于每个查询向量 $q$，沿头维找出 $k_1$ 个绝对值最大的索引；根据 $q$ 的符号选择 $K_{\text{max}}$ 或 $K_{\text{min}}$，计算近似注意力分数 $s_1 = \text{score}(q_{i_1}, P)$（其中 $P$ 为对应页的极值张量），再沿序列维选出 $k_2$ 个最高分数的索引。
  - **步骤 3**：根据这些索引获取原始的键和值张量，执行稀疏注意力。
  - 该方法同时在头和序列两个维度进行降维近似，比单维度方法（如 Quest、SparQ）在低 token 预算下估算更准。

- **多轮变体 RocketKV-MT**
  - 在多轮对话中，为避免永久逐出导致后续轮次丢失关键 token，第一阶段不逐出任何 token，所有 KV 缓存跨轮保留；但解码阶段仍仅在第一阶段筛选出的子集上执行 HSA 动态选择。从而保留全历史，同时维持每轮加速。

- **自适应压缩分解机制**
  - 定义总压缩比 $c = S / t$（序列长度 / token 预算）。
  - 通过公式 $r = \min(0.2 + 0.06 \cdot \log_2(c), 0.8)$ 将总压缩比分解为第一阶段 $c^r$ 和第二阶段 $c^{(1-r)}$，以平衡两阶段的压缩强度。
  - 第二阶段 HSA 再均匀拆分为序列维和头维的压缩比。

### 3. 实验设计

- **模型**：
  - Llama3.1-8B-Ins (GQA, max 128K)。
  - Mistral-7B-Ins-v0.2 (GQA, max 32K)。
  - LongChat-7B-v1.5 (MHA, max 32K)。
  
- **下游任务与基准**：
  - LongBench（双语多任务长上下文理解）。
  - Needle-in-a-Haystack (NIAH，检索性测试)。
  - RULER（不同序列长度，16K/32K/64K/96K 等）。
  - SCBench（多轮场景分析）。

- **对比方法**：
  - Full-KV（基准）。
  - Exact-TopK（先知 top-k 注意力）。
  - DuoAttention（检索头+流式头混合）。
  - SnapKV（仅第一阶段）。
  - Quest（页面近似）。
  - SparQ（头维低秩近似）。
  - 以及 RocketKV 和 RocketKV-MT。

- **评估指标**：在不同 token 预算（256 ~ 4096 或更高）下比较平均准确率，并评估速度提升和峰值内存节省。

### 4. 资源与算力

- 效率实验运行在 **NVIDIA A100** 和 **H100** GPU 上，使用 FP16 精度，batch size 为 1。
- 基于 **gpt-fast** 框架进行端到端测量，未使用定制 CUDA 核或高级框架如 FlashInfer，仅用于展示加速潜力。论文未报告具体的训练时长或额外算力消耗（方法无需训练）。

### 5. 实验充分性分析

- 实验覆盖 **3 种不同架构的模型**（带 GQA 和 MHA），**4 类主流长上下文基准**，在不同 token 预算、不同序列长度下进行系统比较。
- 包含消融实验（HSA 与 Quest/SparQ 单独对比、静态与自适应分解因子对比），验证各模块贡献。
- 多轮设置单独评估（SCBench），展示 RocketKV-MT 的必要性。
- 从速度和内存角度测量了实际系统增益。
- 总体实验组数达数百组（多种 token 预算 × 多种序列长度 × 多基准 × 多模型），实验设计公平，对比方法均按统一 token 预算实现，且考虑了辅助数据存储与流量。

### 6. 主要结论与发现

- RocketKV 在 **token 预算 256** 下即可在 LongBench 上保持接近 Full-KV 的精度，且在 NIAH 上达到 100% 准确率（压缩比超 400×）。
- 随着预算降低，RocketKV 始终明显优于 SnapKV、Quest、SparQ 等单一阶段或单维度方法。
- 在 A100 上实现最高 **3.7 倍端到端加速**，**峰值内存节省 32.6%**；在 H100 上的加速略有下降但仍显著（因 H100 内存带宽更高）。
- RocketKV-MT 在多轮 SCBench 中消除了永久逐出带来的精度下降，接近先知 top-k。
- 自适应分解策略优于固定分拆比。

### 7. 优点

- **无需训练**，可直接部署于现有模型。
- **两阶段协同**：粗粒度 SnapsKV 减少后续 HSA 的搜索空间，HSA 双维度近似提升低预算下的 top-k 估算精度。
- **兼容性好**：适配 FlashAttention、张量并行、以及分离式推理系统。
- **关注实际系统影响**：将估算过程的内存流量计入 token 预算，使得比较更公平。
- **多轮场景优化**：通过保留全历史避免信息丢失。

### 8. 不足与局限

- HSA 需要存储额外的 $K_{\text{max}}$、$K_{\text{min}}$ 辅助张量，增加了一定的额外存储开销（尽管整体仍远小于全缓存）。
- 如文中提到，python 实现尚未极致优化，如果利用定制 CUDA 核可能带来进一步加速；但文中未实现。
- 对于超出模型有效上下文长度的序列（如 RULER 中极长序列），稀疏注意力方法仍存在精度下降，RocketKV 也不例外。
- 自适应分解公式基于启发式，虽有效但缺乏严格理论依据，可能在某些极端场景下次优。
- 实验中 batch size 固定为 1，对于高吞吐服务场景的批量效果未评估。
- 依赖 SnapKV 的观察窗口，若提示结构特殊可能影响第一阶段的选择质量。

（完）
