---
title: "70% Size, 100% Accuracy: Lossless LLM Compression for Efficient GPU Inference via Dynamic-Length Float (DFloat11)"
title_zh: "70%大小，100%精度：基于动态长度浮点的LLM无损压缩实现高效GPU推理"
authors: "Tianyi Zhang, Mohsen Hariri, Shaochen Zhong, Vipin Chaudhary, Yang Sui, Xia Hu, Anshumali Shrivastava"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=xdNAVP7TGy"
tags: ["query:edge-llm"]
score: 10.0
evidence: "无损压缩框架，将LLM和DM体积减少30%，且输出比特一致"
tldr: "提出DFloat11无损压缩框架，利用BFloat16权重的低熵特性，通过熵编码动态分配编码长度，将LLM模型体积减少30%且输出完全一致，显著降低了存储和内存需求，有利于在资源受限硬件上高效部署。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1436, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1424, \"height\": 654, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1447, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1434, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1430, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1431, \"height\": 696, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1422, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1443, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1439, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1433, \"height\": 860, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1442, \"height\": 828, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1133, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xdnavp7tgy/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1453, \"height\": 626, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-xdnavp7tgy/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1443, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xdnavp7tgy/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1433, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xdnavp7tgy/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1296, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xdnavp7tgy/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1387, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xdnavp7tgy/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1155, \"height\": 219, \"label\": \"Table\"}]"
motivation: LLM规模增长使得在资源受限硬件上部署困难。
method: 利用LLM权重BFloat16表示的低熵特性，采用熵编码实现近似信息最优的无损压缩。
result: "模型体积减少30%，且输出与原始模型比特一致。"
conclusion: DFloat11提供了一种无损压缩方案，平衡了模型大小与精度，适用于边缘硬件推理。
---

## Abstract
Large-scale AI models, such as Large Language Models (LLMs) and Diffusion Models (DMs), have grown rapidly in size, creating significant challenges for efficient deployment on resource-constrained hardware. In this paper, we introduce Dynamic-Length Float (DFloat11), a lossless compression framework that reduces LLM and DM size by 30\% while preserving outputs that are bit-for-bit identical to the original model. DFloat11 is motivated by the low entropy in the BFloat16 weight representation of LLMs, which reveals significant inefficiency in the existing storage format. By applying entropy coding, DFloat11 assigns dynamic-length encodings to weights based on frequency, achieving near information-optimal compression without any loss of precision. To facilitate efficient inference with dynamic-length encodings, we develop a custom GPU kernel for fast online decompression. Our design incorporates the following: (i) compact, hierarchical lookup tables (LUTs) that fit within GPU SRAM for efficient decoding, (ii) a two-phase GPU kernel for coordinating thread read/write positions using lightweight auxiliary variables, and (iii) transformer-block-level decompression to minimize latency. Experiments on Llama 3.3, Qwen 3, Mistral 3, FLUX.1, and others validate our hypothesis that DFloat11 achieves around 30\% model size reduction while preserving bit-for-bit identical outputs. Compared to a potential alternative of offloading parts of an uncompressed model to the CPU to meet memory constraints, DFloat11 achieves 2.3--46.2$\times$ higher throughput in token generation. With a fixed GPU memory budget, DFloat11 enables 5.7--14.9$\times$ longer generation lengths than uncompressed models. Notably, our method enables lossless inference of Llama 3.1 405B, an 810GB model, on a single node equipped with 8$\times$80GB GPUs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **核心问题**：大型语言模型(LLM)与扩散模型(DM)规模急剧膨胀，部署在资源受限的硬件上（如单节点GPU）面临巨大内存压力。量化等有损压缩虽能减少体积，但引入精度损失、行为偏移和合规风险。
- **整体含义**：本文提出一种**无损压缩框架 DFloat11**，可在完全不改变模型输出的前提下，将BFloat16模型的体积压缩至约70%（约11比特/权重），并通过定制GPU内核实现高效在线解压推理。相比CPU卸载方案，在同等内存预算下吞吐量大幅提升，支持更长生成长度，甚至使Llama 3.1 405B能在单节点8×80GB GPU上运行。

### 2. 方法论

- **核心思想**：观察到LLM中BFloat16权重的指数位（8bit）信息熵极低（约2.6bit），存在大量冗余。利用熵编码（Huffman编码）对指数位进行可变长度编码，而符号位与尾数位保持原样，实现近信息理论极限的无损压缩。
- **关键技术细节**：
  - **动态长度浮点（DFloat11）格式**：对指数做Huffman编码后打包成紧凑字节流`EncodedExponent`，符号与尾数保持固定长度存储于`PackedSignMantissa`。平均每权重降至约11bit。
  - **高效GPU解压**：
    - **分层查找表(LUT)**：将完整Huffman树拆解为一组高度为8的子表（每个256条目），利用未用指数值（240–255）作为表间指针。所有LUT驻留GPU SRAM，实现常数时间查表解码。
    - **两阶段内核**：每个线程处理一段连续字节的解码。第一阶段仅计数解码出的元素个数；通过Blelloch前缀和计算出每个线程的输出起始位置；第二阶段重解码并将结果写入SRAM缓冲区，最后批量写回HBM。使用轻量级`Gaps`数组记录线程起始位偏移，`BlockOutputPos`数组记录块级输出起始索引，避免线程级位置存储开销。
    - **Transformer块级批解压**：将同一Transformer块内所有权重矩阵的解压合并为一个批次，以减少延迟并提高GPU利用率。
  - **算法流程伪代码**（Algorithm 1）详细描述了并行解压的步骤。

### 3. 实验设计

- **数据集与基准测试**：
  - 精度评估：MMLU、TruthfulQA（准确率），WikiText、C4（词级困惑度）。
  - 推理效率：测量延迟（秒/Token）与吞吐量（Token/秒），在不同批大小、不同GPU（A5000、A100、RTX 8000）下对比。
  - 图像生成：Stable Diffusion 3.5 Large在相同种子与提示词下生成图像，验证像素级一致性。
- **对比方法**：
  - 原始BF16模型（可能需CPU卸载以满足显存限制）。
  - NVIDIA nvCOMP ANS解压（对比解压吞吐与延迟）。
  - CPU到GPU的矩阵传输带宽（作为参照）。
- **消融实验**：分析DF11解压与原始BF16在推理各阶段（嵌入、Transformer块、LM头）的延迟贡献，研究解压开销与批大小的关系。

### 4. 资源与算力

- **硬件配置**（文中Table 4提供详细信息）：
  - A5000 (24GB), A100 (40GB), Quadro RTX 8000 (48GB)。
  - CPU: AMD EPYC 7513/7742，内存 504GB–1.48TB。
- **压缩与解压**：压缩为一次性预处理，文中报告了各模型每Transformer块的压缩时间（如Llama 3.1 8B为191秒），可并行化。推理实验在单GPU或多GPU（如4×A100）下运行。
- **训练相关**：本文不涉及模型训练，无需训练算力。

### 5. 实验数量与充分性

- **模型覆盖**：压缩了Llama 3.1/3.3, Qwen 3, Mistral Nemo/Small, Phi 4, DeepSeek R1 Distill, FLUX.1, Stable Diffusion 3.5等十几种模型，覆盖LLM和DM。
- **指标丰富**：包含模型体积压缩比、精度/困惑度一致性、推理吞吐/延迟比较（不同批大小）、解压内核自身吞吐/延迟、生成上下文长度极限、扩散模型图像一致性。
- **对比充分**：与CPU卸载方案对比，在多种GPU和模型组合下展示优势；与nvCOMP ANS解压对比，显示解压速度优势。
- **消融**：展示了不同批大小下的延迟拆解，证明了解压开销可被摊销。
- **公正性**：推理对比时DF11模型完全驻留GPU，而BF16需部分卸载至CPU，该setup体现实际部署约束，比较合理。
- 总体实验设计较为全面，覆盖了无损性的验证、效率提升的定量分析以及底层内核的性能剖析。

### 6. 主要结论与发现

- DFloat11将BFloat16模型体积压缩约30%，平均权重降至~11bits，且输出与原始模型**比特级完全一致**。
- 在GPU内存不足需CPU卸载的场景下，DF11可提供2.3–46.2倍的吞吐量提升，并显著降低每Token延迟。
- 同等GPU内存预算下，DF11可支持5.7–14.9倍的更长上下文生成（因节省的显存可容纳更长的KV缓存）。
- 压缩和解压开销可控：压缩一次性预处理；解压延迟在较大批处理时几乎可忽略。
- 成功实现Llama 3.1 405B（810GB）在单节点8×80GB A100上运行，硬件需求减半。

### 7. 优点

- **真无损**：解压后权重与原始BFloat16完全一致，消除量化可能带来的精度和行为不确定性。
- **内存效率突出**：显著降低显存占用，使超大模型可在受限硬件上运行，或支持更长上下文。
- **推理性能优于CPU卸载**：吞吐量大幅领先，且随批大小增加优势扩大。
- **定制GPU内核高效**：利用分层LUT、两阶段并行、块级批处理等技术，解压速度远超通用压缩库（nvCOMP）。
- **方法普适**：已验证多种LLM和扩散模型，且对模型结构无侵入性。

### 8. 不足与局限

- **格式限制**：仅针对BFloat16设计，未考虑FP32、FP16、FP8等其他格式，需调整策略。
- **延迟开销在小批处理下存在**：虽然大batch时摊销，但单样本或小batch推理中增加的固定延迟可能影响对延迟敏感的任务。
- **硬件平台单一**：仅在NVIDIA GPU上验证，未评估CPU、TPU或FPGA等平台，需定制化优化。
- **压缩比为30%左右**：未追求更高压缩比，若需进一步降低体积仍需结合其他方法（如量化）。
- **压缩预处理时间较长**：大模型单块几十到几百秒，但可并行且只需一次。

（完）
