---
title: "QuantSpec: Self-Speculative Decoding with Hierarchical Quantized KV Cache"
title_zh: QuantSpec：基于分层量化KV缓存的自投机解码框架
authors: "Rishabh Tiwari, Haocheng Xi, Aditya Tomar, Coleman Richard Charles Hooper, Sehoon Kim, Maxwell Horton, Mahyar Najibi, Michael W. Mahoney, Kurt Keutzer, Amir Gholami"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=7SHbJENgHX"
tags: ["query:edge-llm"]
score: 10.0
evidence: 直接针对边缘设备上的大模型推理，采用量化KV缓存和自投机解码。
tldr: 边缘设备上部署大语言模型进行长上下文推理时，KV缓存成为主要的内存和延迟瓶颈。本文提出QuantSpec自投机解码框架，通过让草稿模型与目标模型共享架构并对KV缓存进行分层量化，不仅大幅压缩了缓存内存占用，还提高了投机解码的接受率。实验表明QuantSpec能在边缘硬件上实现显著的推理加速，为资源受限环境下的高效大模型服务提供了切实可行的方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1778, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1752, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1589, \"height\": 484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 856, \"height\": 368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1787, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1080, \"height\": 923, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1064, \"height\": 890, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-7shbjenghx/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1064, \"height\": 714, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1782, \"height\": 883, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 765, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 693, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1669, \"height\": 583, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1666, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 861, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1497, \"height\": 1260, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-7shbjenghx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1669, \"height\": 941, \"label\": \"Table\"}]"
motivation: 边缘设备上大模型的长上下文推理受限于KV缓存的内存和延迟问题。
method: 提出自投机解码框架，草稿模型与目标模型共享架构，对KV缓存进行分层量化。
result: 实现了更快的解码速度和更高的接受率，有效缓解了边缘端推理瓶颈。
conclusion: 为边缘设备上的高效大模型推理提供了一种实用的投机解码与量化联合方案。
---

## Abstract
Large Language Models (LLMs) are increasingly being deployed on edge devices for long-context settings, creating a growing need for fast and efficient long-context inference. In these scenarios, the Key-Value (KV) cache is the primary bottleneck in terms of both GPU memory and latency, as the full KV cache must be loaded for each decoding step. While speculative decoding is a widely accepted technique to accelerate autoregressive decoding, existing methods often struggle to achieve significant speedups due to inefficient KV cache optimization strategies and result in low acceptance rates. To address these challenges, we propose a novel self-speculative decoding framework, QuantSpec, where the draft model shares the architecture of the target model but employs a hierarchical 4-bit quantized KV cache and 4-bit quantized weights for acceleration. QuantSpec maintains high acceptance rates ($>$90\%) and reliably provides consistent end-to-end speedups upto $\sim2.5\times$, outperforming other self-speculative decoding methods that use sparse KV cache for long-context LLM inference. QuantSpec also reduces the memory requirements by $\sim 1.3\times$ compared to these alternatives.

---

## 论文详细总结（自动生成）

好的，我将基于提供的论文内容，生成一份符合要求的结构化、深入、客观的中文总结。

### **1. 论文核心问题与整体含义**

*   **研究背景与动机**：大型语言模型（LLM）越来越多地被部署到终端设备上进行长上下文推理（如文档摘要、长对话等）。在这种场景下，KV缓存（Key-Value Cache）成为性能的主要瓶颈，因为每一步解码都需要从内存中加载庞大的KV缓存，这严重消耗了GPU内存并导致高延迟。
*   **现有方法局限**：传统的投机解码方法利用一个小型“草案模型”来快速生成候选词元，再由“目标模型”来验证。但在长上下文中，草稿模型常因缺乏长文本理解能力导致接受率低，且需维护两份KV缓存，内存占用大。现有的一些自投机解码（使用稀疏KV缓存）虽然减少了内存加载，但可能导致预测不匹配，接受率下降，且加速效果不稳定。
*   **核心问题**：如何在长上下文推理中，设计一种既能通过投机解码实现加速，又能高效管理KV缓存、提升内存效率和保持高接受率的方法。
*   **整体含义**：论文提出**QuantSpec框架**，一种新型的自投机解码方法。它通过让“草稿模型”与“目标模型”共享架构，并对KV缓存实施分层量化，来同时解决内存占用、解码速度和接受率的问题，从而在终端设备上实现高效且可靠的LLM推理。

### **2. 方法论**

论文提出了一个名为QuantSpec的自投机解码框架，其核心思想是：让草稿模型与目标模型共享同一套模型架构和KV缓存物理存储，通过精度切换（4-bit vs 8-bit）来实现角色转换，从而避免额外的内存开销和量化/反量化损失。

*   **核心思想：分层量化KV缓存（Hierarchical Quantized KV Cache）**
    *   利用INT8 KV缓存（目标模型使用）可以无损地分解为一个“高位INT4”和一个“低位INT4”的特性。这样，在物理上只需要存储两份INT4数据。
    *   **草稿模型生成阶段**：只加载“高位INT4”KV缓存并进行反量化，用于快速生成候选词元。这极大减少了内存带宽压力，实现加速。
    *   **目标模型验证阶段**：同时加载“高位”和“低位”INT4 KV缓存，将它们重组为高精度的INT8表示，再执行验证，确保了与全精度基线相近的生成质量。
*   **公式化表示**：一个INT8的KV缓存值 \(C_{\text{INT8}}\) 可以被其高位 \(C_{\text{INT4}}^U\) 和低位 \(C_{\text{INT4}}^L\) 表示为：  
    \[
    C_{\text{FP32}} = C_{\text{INT8}} \cdot S_{\text{INT8}} + Z_{\text{INT8}} = (2^4 C_{\text{INT4}}^U + C_{\text{INT4}}^L) \cdot S_{\text{INT8}} + Z_{\text{INT8}}
    \]  
    其中 \(S\) 是缩放因子， \(Z\) 是零点。
*   **关键技术细节**
    1.  **双精度缓存区（Double Full-Precision Buffer）**：为配合投机解码的回滚机制，设计了一个大小为 \(2G\)（\(G\)是量化组大小）的全精度缓存区。
        *   **作用**：保留近期生成（最多 \(2G\) 个）词元的全精度KV缓存，仅对较远历史的KV对进行量化。
        *   **工作流程**：新生成的词元先存入全精度缓存区，当缓存区满时，待目标模型验证后，仅将“前一半”（\(G\) 个）已经验证过的词元进行量化并移入INT4 KV缓存，然后“后一半”作为新的全精度缓存继续使用。这避免了频繁的量化/反量化操作，也保证了最近上下文的精度，从而提升接受率。
    2.  **权重量化**：除了KV缓存，论文也对草稿模型的权重进行4-bit量化（目标模型仍为FP16），以适应短上下文场景下权重加载为主要瓶颈的情况。
*   **算法流程（文字描述）**
    1.  **预填充阶段**：用目标模型处理输入，生成FP16 KV缓存。对大部分KV缓存（除最后 \(G\) 个）执行分层量化，得到高位和低位INT4缓存。
    2.  **解码阶段**：
        *   **草案生成**：加载INT4量化权重和“高位INT4”KV缓存，快速生成 γ 个候选词元。
        *   **目标验证**：加载FP16权重、重组后的INT8 KV缓存以及全精度缓冲区中的近期缓存，对候选词元逐一验证。
        *   **接受与回滚**：根据验证结果接受/拒绝词元。若发生拒绝，灵活丢弃全精度缓存区中对应的词元，无需对量化部分进行操作。
        *   **缓存更新**：当全精度缓存区满，将已验证的旧部分量化，并移动剩余部分。

### **3. 实验设计**

*   **数据集与场景**：
    *   **语言建模**：PG-19 (长文本书籍数据)
    *   **长上下文摘要**：∞BENCH Sum (虚构书籍摘要), Multi-LexSum (法律文书多文档摘要)
    *   所有实验均在长上下文（4k到128k）环境下进行。
*   **基准方法与对比对象**：
    *   **基础基线**：不使用投机解码的**自回归生成（Autoregressive）**。
    *   **自投机解码基线**：使用稀疏KV缓存加速草稿模型的两种方法：**StreamingLLM** 和 **SnapKV**。为保证公平，稀疏方法的草稿KV预算设置为与4-bit量化KV缓存的等效大小。
*   **评估指标**：
    *   **接受率（Acceptance Rate）**：目标模型接受草稿模型候选词元的比例。
    *   **吞吐量/加速比（Speedup）**：相对于自回归基线的端到端生成速度提升（Token/s）。
    *   **GPU峰值内存（Peak GPU Memory）**。

### **4. 资源与算力**

*   **硬件平台**：所有实验均在配备 **8块 NVIDIA RTX A6000 GPU** 的节点上进行。
*   **具体模型与规模**：
    *   Llama-2-7B-32K-Instruct
    *   LWM-Text-Chat-128k
    *   Mistral-7B-v0.3
    *   Llama-3.1-8B
    *   实验根据上下文长度使用了1或2张GPU。
*   **训练时长**：论文主要关注推理阶段的加速，不涉及模型训练。

### **5. 实验数量与充分性**

*   **实验矩阵**：实验覆盖了多种模型（4种）、多个数据集（3种）以及广泛的上下文长度（4k, 8k, 16k, 32k, 64k, 128k），形成了较全面的测试集。
*   **消融实验**：通过消融实验区分了“权重量化”和“KV缓存量化”在不同上下文长度下对加速的贡献，验证了分析的理论（短上下文权重量化收益大，长上下文KV缓存量化收益大）。
*   **超参数搜索**：针对投机长度（γ）进行了超参数搜索以选择各方法的最优值，这增加了对比的公平性。
*   **额外分析**：提供了Roofine模型分析、困惑度评估（验证INT8目标模型质量）、内核级延迟比较以及接受率随投机长度变化的对比，实验设计较为充分和客观。

### **6. 主要结论与发现**

1.  **高效且高接受率**：QuantSpec在保持高接受率（>90%）的同时，实现了高达约2.5倍的端到端加速，优于使用稀疏KV缓存的自投机解码方法。
2.  **内存节省**：相较于稀疏KV缓存方法，QuantSpec减少了约1.3倍的内存需求。
3.  **可靠性**：在摘要等对全部上下文信息都重要的任务中，稀疏方法接受率下降明显，而QuantSpec的量化方法能更好地保留信息，提供更稳定的加速。
4.  **瓶颈分析验证**：通过算术强度分析证实，长上下文下KV缓存加载是主要瓶颈（内存密集型），短上下文下模型权重加载是主要瓶颈。量化权重和KV缓存分别是针对这两个瓶颈的有效优化。

### **7. 优点**

*   **技术创新性**：提出的“分层量化KV缓存”设计精妙，利用INT8可分解为两个INT4的特性，在单一物理存储上实现了两种精度的灵活切换，完美适配了投机解码中“快而精”与“慢而准”的双重需求。
*   **工程实用性**：“双精度缓存区”设计有效解决了量化与投机解码回滚机制不兼容的问题，并提升了关键近期的上下文精度，这是提升接受率和系统效率的关键。
*   **理论与实验结合**：通过Roofine模型的算术强度分析，清晰地论证了不同上下文长度下的瓶颈所在，并以此指导定制化优化（短文本量化权重，长文本量化KV），实验消融也证实了这一观点。
*   **全面对比**：进行了详尽的实验，在不同模型、数据集、上下文长度下与强基线（稀疏KV）对比，充分证明了本方法的优越性和普适性。

### **8. 不足与局限**

*   **未与稀疏方法结合**：论文提到其方法可与稀疏KV方法结合以获取进一步加速，但未在本工作中实现和验证，留下了探索空间。
*   **生成质量评估有限**：评估主要依赖困惑度（Perplexity）和接受率，缺少对下游任务具体生成质量（如摘要的ROUGE分数）的直接对比。
*   **缺乏更多模型架构的验证**：虽然已覆盖Llama 2/3.1, Mistral, LWM等模型，但集中于7-8B参数规模，在更大模型或非Transformer架构上的效果有待考证。
*   **推理框架耦合度**：该方法需要定制CUDA内核来实现高效的分层量化和解码，这增加了与现有推理框架的集成成本，普适性受限于内核实现和优化程度。

（完）
