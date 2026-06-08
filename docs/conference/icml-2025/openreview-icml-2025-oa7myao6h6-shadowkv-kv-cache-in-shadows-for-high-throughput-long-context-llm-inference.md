---
title: "ShadowKV: KV Cache in Shadows for High-Throughput Long-Context LLM Inference"
title_zh: ShadowKV：隐藏在阴影中的KV缓存实现高吞吐长上下文LLM推理
authors: "Hanshi Sun, Li-Wen Chang, Wenlei Bao, Size Zheng, Ningxin Zheng, Xin Liu, Harry Dong, Yuejie Chi, Beidi Chen"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=oa7MYAO6h6"
tags: ["query:edge-llm"]
score: 8.0
evidence: 低秩键缓存和CPU卸载以减少GPU内存的长上下文LLM推理
tldr: 针对长上下文LLM服务中KV缓存导致GPU内存高和吞吐低的问题，提出ShadowKV系统，在GPU上存储低秩键缓存并将值缓存卸载至CPU，结合动态稀疏注意，在保持生成质量的同时大幅降低GPU内存占用，提升吞吐量，适用于内存受限的边缘推理场景。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 781, \"height\": 671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1763, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1785, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1757, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 510, \"height\": 275, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 420, \"height\": 337, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1766, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 857, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 760, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oa7myao6h6/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1627, \"height\": 2216, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1774, \"height\": 831, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 867, \"height\": 181, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 867, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 863, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 866, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 866, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1466, \"height\": 584, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1464, \"height\": 581, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1457, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1456, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1460, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1465, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1477, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1277, \"height\": 136, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oa7myao6h6/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1443, \"height\": 445, \"label\": \"Table\"}]"
motivation: 长上下文LLM的KV缓存内存占用大，传统动态稀疏注意无法充分降低GPU内存或引入较大延迟。
method: Striped-低秩键缓存存储于GPU，值缓存和准确定KV缓存卸载至CPU，结合稀疏注意。
result: 实现了高吞吐长上下文推理，降低了GPU内存占用。
conclusion: ShadowKV为长上下文LLM的高效内存感知部署提供了有效的系统方案。
---

## Abstract
With the widespread deployment of long-context large language models (LLMs), there has been a growing demand for efficient support of high-throughput inference. However, as the key-value (KV) cache expands with the sequence length, the increasing memory footprint and the need to access it for decoding both result in low throughput when serving long-context LLMs. While various dynamic sparse attention methods have been proposed to accelerate inference while maintaining generation quality, they either fail to sufficiently reduce GPU memory usage or introduce significant decoding latency by offloading the KV cache to the CPU. We present ShadowKV, a high-throughput long-context LLM inference system that stores the low-rank key cache and offloads the value cache to reduce the memory footprint for larger batch sizes and longer sequences. To minimize decoding latency, ShadowKV employs an accurate KV selection strategy that reconstructs minimal sparse KV pairs on-the-fly. By evaluating ShadowKV on benchmarks like RULER, LongBench, and models such as Llama-3.1-8B and GLM-4-9B-1M, we demonstrate that it achieves up to 6$\times$ larger batch sizes and 3.04$\times$ higher throughput on an A100 GPU without sacrificing accuracy, even surpassing the performance achievable with infinite batch size under the assumption of infinite GPU memory.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：随着长上下文大语言模型（LLM）的广泛部署，键值对（KV）缓存的内存占用随着序列长度急剧增长，成为限制高吞吐推理的主要瓶颈。传统方法要么因丢弃KV对导致精度损失，要么因将KV缓存卸载到CPU而引入严重的解码延迟。
- **整体含义**：提出 **ShadowKV** 系统，旨在**最小化GPU显存占用**的同时**保持高吞吐和精度**，通过利用KV缓存的低秩特性与精准的稀疏注意力机制，实现大规模长上下文推理的加速。

### 2. 方法论：核心思想与关键技术
- **核心洞察**：
  - **低秩键缓存与离线值缓存**：发现应用旋转位置编码（RoPE）之前的键缓存在同一序列内具有极高相似度的低秩子空间，而跨序列则不共享。值缓存不具备低秩特性，因此可卸载至CPU。
  - **高精度KV选择**：应用RoPE后的键缓存在相邻token间具备高余弦相似度。少数异常块（仅0.3%）难以近似，但需专门保留。
- **系统设计（两阶段）**：
  - **预填充阶段**（Algorithm 1）：
    1. 对pre-RoPE键缓存执行**奇异值分解（SVD）**，仅保留低秩投影。
    2. 将post-RoPE键缓存分块，计算每个块的平均值作为**路标**。
    3. 检测余弦相似度最低的块作为**异常块**，其完整KV对保留在GPU。
    4. 其余值缓存**卸载至CPU**。
  - **解码阶段**（Algorithm 2）：
    1. **KV选择**：使用查询向量与路标计算近似注意力分数，选出Top-k个块索引。
    2. **低延迟重建**：通过CUDA多流并发，在CPU取回对应值缓存的同时，利用低秩矩阵在GPU上重建键缓存。
    3. **缓存策略**：利用解码过程的时序局部性，设置命中率高达60%的缓存机制，仅重建缺失的KV对。
- **理论等效带宽**：通过分层存储和重叠操作，ShadowKV在A100上理论等效带宽可达7.2 TB/s，远超原生显存带宽。

### 3. 实验设计
- **评测基准**：
  - **RULER**：多维度长上下文综合评测（包括大海捞针、多键检索、变量追踪等）。
  - **LongBench**：长文本问答与理解基准。
  - **Needle In A Haystack (NIAH)**：长上下文检索测试（最高1M token）。
- **模型与配置**：Llama-3.1-8B、Llama-3-8B-1M、GLM-4-9B-1M、Yi-9B-200K、Phi-3-Mini-128K等。默认分块大小为8，秩为160，稀疏预算为1.56%。
- **对比基线**：Quest、Loki、InfiniGen等动态稀疏注意力方法，以及SnapKV等KV驱逐方法。

### 4. 资源与算力
- **硬件平台**：实验主要在 **NVIDIA A100 GPU** 上进行。
- **时间开销**：作者特别展示了SVD、相似度计算等预填充阶段的额外开销占比极低（随序列增长降至约1%），解码延迟也因重叠操作被有效隐藏。

### 5. 实验数量与充分性
- **充足性验证**：设计了**多维度的消融实验**来证明系统鲁棒性：
  - **稀疏预算**：对比不同稀疏比例下的精度变化。
  - **秩的选择**：分析从低秩到满秩的误差趋势。
  - **分块大小**：测试不同粒度对精度和吞吐的影响。
  - **异常块影响**：验证异常保留机制对恢复精度的关键作用。
  - **精度敏感性**：验证FP8量化下的鲁棒性。
  - **多基准、多模型**：覆盖4个模型、3个主流长基准、最大1M序列长度，实验对比全面且客观公平。

### 6. 主要结论与发现
- **显著降显存**：ShadowKV可将KV缓存的GPU显存占用降低超过6倍，支持高达$6\times$的批次大小扩展。
- **高吞吐提升**：在保持推理精度的前提下，A100吞吐量提升高达 $3.04\times$，甚至超越了理论无限显存下全精度注意力的吞吐。
- **精度保持**：在1.56%的极小稀疏预算下，ShadowKV在RULER和LongBench上的得分极其接近甚至优于全注意力基线，且在多轮对话场景下无累积信息丢失。

### 7. 优点
- **创新的异构存储架构**：将高压缩率的低秩矩阵留存在高速GPU，配合CPU做高容量值缓存存储，兼顾了容量与速度。
- **极致的解码流水线**：通过路标近似匹配和重叠执行（值缓存取回与键缓存重建）显著降低了延迟开销。
- **高通用性与轻量化**：无需修改模型权重或进行针对性的重训练，流程完全自适应，且前置SVD成本随上下文长度增加而愈发可忽略。

### 8. 不足与局限
- **系统工程依赖**：高度依赖于精确的CUDA流重叠优化，对于物理存储（CPU与GPU）的带宽波动较为敏感。
- **异常块依赖性**：当存在大量具有独特语义的异常信息需要被保留时，固定大小的异常预算可能会成为精度短板。
- **长输出影响未充分论证**：虽然在附录中分析了新生成长文本的情况，但主实验主要聚焦于长上下文输入的解码阶段。

（完）
