---
title: "CodeGEMM: A Codebook-Centric Approach to Efficient GEMM in Quantized LLMs"
title_zh: CodeGEMM：量化大语言模型中面向码本的高效GEMM方法
authors: "Gunho Park, Jeongin Bae, Byeongwook Kim, Baeseong park, Jiwon Ryu, Hoseung Kim, Se Jung Kwon, Dongsoo Lee"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=OH7U836jKk"
tags: ["query:edge-llm"]
score: 10.0
evidence: 基于码本的量化内核消除反量化开销，实现低比特LLM推理
tldr: 该论文针对低比特量级LLM推理中反量化操作带来的延迟和缓存压力，提出CodeGEMM内核。通过预计算码本中心与激活向量的内积，避免了在线权重重建，直接从码索引收集部分和。该方法大幅减少片内占用和内存访问，支持在极低位宽下实现高效边缘推理。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-oh7u836jkk/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1448, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-oh7u836jkk/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1428, \"height\": 310, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-oh7u836jkk/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1444, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-oh7u836jkk/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1453, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-oh7u836jkk/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1455, \"height\": 460, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 822, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1428, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1431, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1430, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1239, \"height\": 515, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1025, \"height\": 550, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 789, \"height\": 618, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1442, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-oh7u836jkk/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1417, \"height\": 1251, \"label\": \"Table\"}]"
motivation: 低比特量化LLM推理中，传统反量化方式导致高延迟和缓存压力。
method: 设计码本中心的GEMM内核，用预计算内积薄记本替代在线反量化。
result: 消除逐元素查找，显著降低延迟和内存占用，实现高效2比特推理。
conclusion: CodeGEMM通过架构创新提升量化LLM推理效率，对边缘部署尤为关键。
---

## Abstract
Weight-only quantization is widely used to mitigate the memory-bound nature of LLM inference. Codebook-based methods extend this trend by achieving strong accuracy in the extremely low-bit regime (e.g., 2-bit). However, current kernels rely on dequantization, which repeatedly fetches centroids and reconstructs weights, incurring substantial latency and cache pressure. We present CodeGEMM, a codebook-centric GEMM kernel that replaces dequantization with precomputed inner products between centroids and activations stored in a lightweight Psumbook. At inference, code indices directly gather these partial sums, eliminating per-element lookups and reducing the on-chip footprint. The kernel supports the systematic exploration of latency–memory–accuracy trade-offs under a unified implementation.
On Llama-3 models, CodeGEMM delivers 1.83x (8B) and 8.93x (70B) speedups in the 2-bit configuration compared to state-of-the-art codebook-based quantization at comparable accuracy and further improves computing efficiency and memory subsystem utilization.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容撰写的结构化中文总结。

### 1. 论文的核心问题与整体含义

- **研究背景与动机**：为降低大语言模型（LLM）的显存占用和带宽需求，基于码本（Codebook）的权重量化技术在极低位宽（如2比特）下表现出极高的精度优势。然而，现有的推理内核存在显著效率瓶颈。
- **核心问题**：当前基于码本量化的内核普遍采用“在线反量化”方式，即根据压缩后的码字（Code）实时从码本查找中心向量并重建权重。此过程会重复地将整个码本加载到高速缓存，导致严重的延迟和缓存压力，抵消了量化带来的内存收益。
- **论文目标**：提出一种名为 CodeGEMM 的码本中心化矩阵乘法（GEMM）内核，从根本上消除反量化开销和冗余计算，从而在极低位宽下实现真正的推理加速和能效提升。

### 2. 论文提出的方法论

- **核心思想：部分和薄记本**
    - **颠覆传统流程**：CodeGEMM 将“加载码本 → 查表反量化 → 计算”的传统流程，转变为“预计算 → 存储 → 直接检索累加”。
    - **Psumbook 机制**：在计算开始前，预先计算激活输入与码本中所有中心向量之间的内积，生成一系列部分和，并将其存储于一个轻量级的“部分和薄记本”中。
    - **推理计算过程**：
        1.  **输入重塑**：将激活输入分块，使其维度与码本中的向量维度对齐。
        2.  **构建 Psumbook**：将每个输入块与对应码本的所有中心向量进行内积运算，结果存入可编程缓存（如GPU共享内存）的`Psumbook`中。
        3.  **检索与累加**：计算输出时，直接用压缩后的权重的码字作为索引，从`Psumbook`中检索预计算好的部分和，然后累加得到最终结果，完全避免在线权重重建。
- **关键技术优势**：
    - **降低计算复杂度**：将 GEMM 操作的计算量从 `O(MNK)` 降低至约 `O(MNK * m/v)`，其中 `m` 是码本数，`v` 是向量长度。
    - **降低空间复杂度**：缓存所需存储空间从完整的码本（ `O(m * 2^b * v)` ）缩减为 Psumbook（ `O(m * 2^b * tw/v)` ），`tw` 为张量核的宽度，显著减小了对稀缺片上缓存的占用。
- **统一化超参支持**：该内核设计支持广泛的码本量化超参数（如码本数量`m`、向量长度`v`、分组大小`g`），允许开发者在同一个实现下系统性地探索延迟、内存和精度之间的权衡。

### 3. 实验设计

- **模型与平台**：实验主要在 **Llama-3.1-8B** 和 **Llama-3.1-70B** 模型上进行，推理硬件平台为 **NVIDIA A100 80GB GPU**。
- **评估基准与任务**：
    - **精度基准**：使用 `lm-eval-harness` 基准套件，评估任务包括 **MMLU（5-shot）**，以及 **WinoGrande、HellaSwag、ARC-Easy、ARC-Challenge** 四个零样本任务的平均准确率。
    - **延迟与吞吐**：报告了单个Transformer解码器层所有线性层的内核级延迟总和（微秒）。端到端吞吐量（每秒生成令牌数）使用 HuggingFace 库进行测量。
    - **资源利用率**：通过 `nvidia-smi` 遥测数据评估了能效（GFLOPS/W）和内存子系统利用率。
- **对比方法**：
    - **浮点基线**：cuBLAS (FP16)。
    - **均匀/非均匀量化方法**：LUT-GEMM（用于FlexRound, 2-bit）, QuIP# (e8p), QTIP (r2)。
    - **码本量化方法**：AQLM的两个主要配置（1x16, 2x8）及其结合PV-Tuning的版本。

### 4. 资源与算力

- 论文明确指出，所有延迟和吞吐量测量均在 **NVIDIA A100 80GB GPU** 上执行。
- 对于模型量化的具体训练/校准时长、使用的GPU数量等算力细节，**文中未作说明**。

### 5. 实验数量与充分性

- **实验组数**：该工作进行了较为全面的实验。
    - 进行了多组 **延迟 vs. 内存** 和 **精度 vs. 内存** 的超参数消融研究（图4），考察了`m`, `v`, `g`等配置的影响。
    - 提供了详尽的 **精度对比表**（表4, 5），包含多种方法和配置。
    - 进行了 **内核延迟、能效、内存利用率** 的对比（表2, 3）。
    - 展示了 **吞吐量 vs. 精度** 的权衡图（图5），并对比了8B和70B模型。
    - 附录中提供了 **Psumbook构建与检索周期分解**、**分块大小敏感性**、**不同batch size和矩阵规模的全面延迟数据**（表6-10）。
- **充分性与客观性**：实验设计充分，覆盖了从内核微基准到端到端应用级性能、从算法精度到硬件利用率的多维度评估。对比对象涵盖了当时主流的均匀量化和码本量化方案，结论较为客观公正。特别是对标量化和吞吐量-精度的联合分析，有力支撑了论文的核心主张。

### 6. 论文的主要结论与发现

- **显著的加速效果**：在2-bit配置下，与最先进的码本量化方法AQLM相比，CodeGEMM 在 Llama-3-8B 上实现了 **1.83倍** 的端到端加速，在 Llama-3-70B 上实现了惊人的 **8.93倍** 加速，同时保持了可比的精度。
- **效率与利用率提升**：CodeGEMM 大幅提升了计算效率（GFLOPS/W）和内存系统利用率（表3），表明其更有效地利用了硬件资源。
- **优越的超参数权衡空间**：通过统一的内核支持，系统性地揭示了不同超参数（`m`, `v`, `g`）下延迟、内存和精度的权衡。发现更小向量长度`v`（如`m1v4`）的配置在吞吐量和精度上通常优于类似位宽的`m2v8`配置。
- **良好的可扩展性**：在从8B扩展到70B模型时，CodeGEMM 的性能优势更加明显，验证了该方法在更大规模模型上的有效性。

### 7. 优点

- **方法论创新**：提出的 `Psumbook` 概念巧妙地通过预计算-检索模式取代了传统的反量化计算模式，从根本上解决了码本量化推理的两大痛点（缓存压力和冗余计算），这是一个核心亮点。
- **算法-硬件协同设计**：内核设计充分考虑了GPU的缓存大小与计算特性，通过降低空间和计算复杂度，实现对片上存储的有效利用，是算法与硬件协同优化的典范。
- **全面的实验评估与可复现性**：实验不仅覆盖了精度和速度，还深入到硬件层面的利用率。提供的丰富的附录实验和开源的代码，极大地增强了工作的可信度和实用价值。
- **统一灵活的框架**：支持多种码本配置的超参数，为实际部署中寻找最优压缩方案提供了很大的灵活性。

### 8. 不足与局限

- **对超大型码本的支持受限**：由于`Psumbook`需驻留在有限的片上共享内存中，内核不支持像`b=16`这样拥有`2^{16}`个条目的超大型码本，文中通过固定`b=8`并使用细粒度分组归一化来弥补，这是一种折中方案。
- **大批量推理性能不足**：作为基于CUDA核心的量化GEMM内核，当批量大小变大时（例如`M > 32`），其性能会低于基于Tensor Core的`cuBLAS`。这属于当前GPU架构的限制，而非算法特有缺陷，但限制了其在某些高吞吐服务场景的应用。
- **量化方法本身的依赖**：CodeGEMM 构建于AQLM等累加码本量化的框架之上，其最终的模型精度上限仍受制于底层量化算法本身。文中也通过结合PV-Tuning等校准技术来进一步提升，体现了这一点。

（完）
