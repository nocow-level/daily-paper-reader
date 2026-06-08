---
title: "CommVQ: Commutative Vector Quantization for KV Cache Compression"
title_zh: CommVQ：面向KV缓存压缩的可交换矢量量化
authors: "Junyan Li, Yang Zhang, Muhammad Yusuf Hassan, Talha Chafekar, Tianle Cai, Zhile Ren, Pengsheng Guo, Foroozan Karimzadeh, Colorado Reed, Chong Wang, Chuang Gan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=sbbyCB39HN"
tags: ["query:edge-llm"]
score: 9.0
evidence: 通过矢量量化压缩KV缓存以减少长上下文LLM推理的内存使用
tldr: 针对大语言模型长上下文推理中KV缓存造成的内存瓶颈，提出可交换矢量量化方法CommVQ，通过轻量级编码器和码本压缩缓存，并设计码本与RoPE可交换以高效集成到自注意力中，显著降低内存占用，同时保持模型性能，为在资源受限设备上运行长上下文Transformer模型提供了有效路径。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-sbbycb39hn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 769, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sbbycb39hn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1733, \"height\": 782, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sbbycb39hn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 970, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-sbbycb39hn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 700, \"height\": 516, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1708, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1707, \"height\": 444, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 705, \"height\": 439, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 829, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 629, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 857, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 651, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 352, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 411, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 587, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-sbbycb39hn/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 673, \"height\": 296, \"label\": \"Table\"}]"
motivation: 长上下文推理时，GPU上KV缓存成为内存瓶颈，限制大模型部署。
method: 提出可交换矢量量化，使用加法量化和与RoPE可交换的码本压缩KV缓存。
result: 显著减少内存使用，且解码可通过简单矩阵乘法实现，保持准确度。
conclusion: CommVQ有效缓解了长上下文推理的内存压力，推动了大模型在有限内存设备上的应用。
---

## Abstract
Large Language Models (LLMs) are increasingly used in applications requiring long context lengths, but the key-value (KV) cache often becomes a memory bottleneck on GPUs as context grows. To address this, we propose Commutative Vector Quantization (CommVQ) to significantly reduce memory usage for long-context LLM inference. We first introduce additive quantization with a lightweight encoder and codebook to compress the KV cache, which can be decoded via simple matrix multiplication. To further reduce computational costs during decoding, we design the codebook to be commutative with Rotary Position Embedding (RoPE) and train it using an Expectation-Maximization (EM) algorithm. This enables efficient integration of decoding into the self-attention mechanism. Our approach achieves high accuracy with additive quantization and low overhead via the RoPE-commutative codebook. Experiments on long-context benchmarks and GSM8K show that our method reduces FP16 KV cache size by 87.5% with 2-bit quantization, while outperforming state-of-the-art KV cache quantization methods. Notably, it enables 1-bit KV cache quantization with minimal accuracy loss, allowing a LLaMA-3.1 8B model to run with a 128K context length on a single RTX 4090 GPU. The source code is available at: https://github.com/UMass-Embodied-AGI/CommVQ.

---

## 论文详细总结（自动生成）

好的，以下是基于论文内容的结构化总结。

### 1. 论文的核心问题与整体含义

- **核心问题**：大语言模型在处理越来越长的上下文时，其推理过程中必需的键值（KV）缓存会随着上下文长度线性增长，成为GPU显存的主要瓶颈。这严重限制了长上下文模型在单卡或资源受限设备上的部署与推理。
- **整体含义**：本文提出了一种名为“可交换矢量量化”的新方法，旨在对KV缓存进行极高压缩比（如1-bit/2-bit）的量化，在显著降低显存占用的同时，尽可能保持模型的长文本处理能力和复杂推理性能，从而让大模型在消费级GPU上运行超长上下文成为可能。

### 2. 论文提出的方法论

- **核心思想**：抛弃传统的逐标量（per-scalar）量化方式，改为以整个令牌的键/值向量为单位，利用**加法量化**进行压缩，并创新性地设计了一个与**旋转位置嵌入（RoPE）矩阵可交换的码本**，以实现计算高效的解码过程。

- **关键技术细节**：
    - **加法量化**：
        - 使用一个轻量级编码器（Encoder）将每个键/值向量（d维）映射为一个长度为 Nc 的二进制序列。
        - 存储时仅保留这些二进制序列，从而实现高压缩比。压缩率为 \( 1 - N_c / 16d \)，平均比特宽度为 \( N_c / d \)。
        - 解码时通过简单的矩阵乘法：`解码向量 = 二进制序列 * 码本(codebook)` 来恢复原始向量。
    - **与RoPE可交换的码本设计**：
        - **动机**：常规的解码后计算自注意力（decode-then-self-attention）的计算复杂度是原始注意力的 Nc 倍，开销巨大。
        - **原理**：利用RoPE矩阵是块对角旋转矩阵的性质，在 2x2 子空间内设计满足特定形式的码本。由于RoPE旋转矩阵与该形式的码本满足乘法交换律，可以将自注意力计算中的“查询向量与解码后键向量的点积”顺序重排。
        - **效果**：重排后，计算量最大的部分（查询向量与码本的乘积）对于所有令牌变为共享和可复用的，从而将解码的计算复杂度从原始的 \( O(2dN_cN + dN) \) 大幅降低。
    - **码本训练**：
        - 使用期望最大化（EM）算法在标定数据集上学得可交换码本。E步将每个键向量分配给最近的聚类中心，M步通过闭合解更新码本。
        - 为稳定训练，采用了软聚类中心分配和温度退火技巧。
        - 为在更低位宽下保持精度，引入了组共享（group sharing）和残差量化（iterative refinement across R codebooks）策略。

### 3. 实验设计

- **模型与训练数据**：主要实验基于 **LLaMA-3.1-8B-Instruct**模型，使用 **FineWeb-Edu** 数据集的一个子集来学习编码器和码本。还在LLaMA-2-7B和Mistral-7B上进行了泛化性测试。
- **评估基准**：
    - **长上下文基准**：**LongBench**（8个子任务，最大长度128K）和 **InfiniteBench**（包含检索、问答等多种任务，最大长度128K）。
    - **复杂推理基准**：**GSM8K**（数学推理）。
    - **检索压力测试**：**Needle-in-a-Haystack**测试。
    - **效率分析**：评估了延迟和实际显存占用。
- **对比方法**：将CommVQ与三种最先进的KV缓存量化方法进行对比，分别是 **KIVI**（非对称量化）、**KVQuant**（非均匀量化）和 **VQLLM**（残差矢量量化），比较指标包括平均量化比特位宽（Avg. bit）和各项任务得分。

### 4. 资源与算力

- **未明确说明**：论文正文中**未提及**具体的训练耗时、所使用的GPU型号数量等详细算力信息。
- **提及的设备**：实验的显存占用测试明确提到了在 **H100-80GB** GPU 和 **RTX 4090** 消费级GPU上进行，其中一项重要成果是在单张RTX 4090上实现了LLaMA-3.1 8B模型在128K上下文长度下的推理。

### 5. 实验数量与充分性

- **实验数量**：实验设计较为全面，涵盖约**7个主要方面**，包括：
    1.  **主流长上下文基准测试**：在LongBench和InfiniteBench两个高难度榜单上进行系统性评估。
    2.  **复杂推理任务测试**：GSM8K数据集评估量化对推理能力的影响。
    3.  **压力与可视化测试**：Needle-in-a-Haystack测试直观展示不同方法在极长文本下的检索保真度。
    4.  **模型消融实验**：在不同模型（LLaMA-2, Mistral）上验证方法的泛化性。
    5.  **领域偏移鲁棒性分析**：在数学、代码等不同领域的数据上测试，验证对训练集领域偏移的鲁棒性。
    6.  **效率与显存分析**：包含延迟对比的理论分析和实际显存占用的Triton实现测试。
    7.  **内部配置消融**：在附录中对码本的组大小、残差次数等关键超参数进行了消融研究。
- **充分性与公平性**：实验对比**充分且客观**。对比基准选择全面，覆盖了当时最新的各类量化方法；所有对比都在相同的模型和设定下复现；既评估了任务精度，也评估了实际压缩率和显存占用，结论说服力强。

### 6. 论文的主要结论与发现

- **高精度高压缩**：CommVQ在**2-bit**量化时就能实现**近无损性能**，在LongBench上平均得分（47.98）几乎与FP16基线（48.05）持平，同时优于所有同类量化方法。
- **极限压缩突破**：成功实现了**1-bit**极低比特量化，性能显著优于其他基线。例如，在GSM8K上，CommVQ-1的准确率（66.57%）远超KIVI-1（2.20%）和VQLLM-1（1.67%）。
- **显著效率提升**：经可交换码本优化后，解码计算延迟相比朴素实现最高有9.6倍加速。实际显存占用大幅下降，使得原本需要高端GPU的场景（128K上下文）可在单张消费级RTX 4090上运行。
- **强鲁棒性**：方法对预训练领域外的数据（如数学、代码）表现鲁棒，且能成功泛化到其他模型架构。

### 7. 优点

- **创新的量化视角**：将KV缓存压缩从标量级提升到向量级，结合加法量化和RoPE的数学性质，是一个新颖且有效的思路。
- **理论与工程的结合**：不仅提出了高压缩比的量化方案，还深入设计可交换码本以解决计算开销问题，并提供了Triton实现，展现了从理论到实际部署的完整流程。
- **极致的压缩性能**：成功证明了1-bit KV缓存量化的可行性，且性能远非其他方法能比，将压缩比推向了新的极限。
- **扎实的实验验证**：实验设计全面，囊括了准确率、效率、鲁棒性和泛化性等多个维度，结论非常可靠。

### 8. 不足与局限

- **离线训练需求**：该方法依赖于一个标定数据集来训练编码器和码本，虽然对领域偏移鲁棒，但仍存在一定的“离线开销”和潜在的极端领域不适配风险。
- **额外计算和存储开销**：尽管已大幅优化，仍引入了额外的码本存储和编解码计算。码本虽小，但在极小模型或极短文本场景下占比较为突出。
- **只评估了8B模型**：主要实验集中在7B-8B规模的模型上，该方法在更大规模模型（如70B）上的效果和效率仍有待验证。
- **编码器开销未细述**：论文重点优化了解码端，但对提示处理阶段的编码开销未做详细分析，这可能影响首令牌延迟。

（完）
