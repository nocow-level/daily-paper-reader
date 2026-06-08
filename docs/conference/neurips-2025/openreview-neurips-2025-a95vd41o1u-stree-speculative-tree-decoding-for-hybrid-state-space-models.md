---
title: "STree: Speculative Tree Decoding for Hybrid State Space Models"
title_zh: STree：面向混合状态空间模型的推测树解码
authors: "Yangchao Wu, Zongyue Qin, Alex Wong, Stefano Soatto"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=a95Vd41o1u"
tags: ["query:edge-llm"]
score: 7.0
evidence: 推测树解码加速状态空间模型推理，一种神经网络加速技术
tldr: 针对混合状态空间模型，提出首个可扩展的推测树解码算法，通过硬件并行性实现多步令牌生成，在保持模型质量的同时显著提升推理效率。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-a95vd41o1u/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1105, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-a95vd41o1u/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1446, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-a95vd41o1u/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 727, \"height\": 401, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-a95vd41o1u/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 528, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-a95vd41o1u/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1402, \"height\": 399, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-a95vd41o1u/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1393, \"height\": 353, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1241, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 727, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1281, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1150, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 889, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1339, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1065, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1194, \"height\": 503, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-a95vd41o1u/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1398, \"height\": 159, \"label\": \"Table\"}]"
motivation: 现有推测解码方法未在SSM上利用树验证，效率提升受限。
method: 设计面向SSM的可扩展树解码算法，利用紧凑状态进行高效树计算。
result: 与基准相比，解码速度提升，且保持生成质量。
conclusion: 推测解码可有效加速状态空间模型的推理。
---

## Abstract
Speculative decoding is a technique to leverage hardware concurrency in order to enable multiple steps of token generation in a single forward pass, thus improving the efficiency of large-scale autoregressive (AR) Transformer models. State-space models (SSMs) are already more efficient than AR Transformers, since their state summarizes all past data with no need to cache or re-process tokens in the sliding window context. However, their state can also comprise thousands of tokens; so, speculative decoding has recently been extended to SSMs. Existing approaches, however, do not leverage the tree-based verification methods, since current SSMs lack the means to compute a token tree efficiently. We propose the first scalable algorithm to perform tree-based speculative decoding in state-space models (SSMs) and hybrid architectures of SSMs and Transformer layers. We exploit the structure of accumulated state transition matrices to facilitate tree-based speculative decoding with minimal overhead relative to current SSM implementations. Along with the algorithm, we describe a hardware-aware implementation that improves naive application of AR Transformer tree-based speculative decoding methods to SSMs. Furthermore, we outperform vanilla speculative decoding with SSMs even with a baseline drafting model and tree structure on three different benchmarks, opening up opportunities for further speed up with SSM and hybrid model inference. Code can be find at: https://github.com/wyc1997/stree.

---

## 论文详细总结（自动生成）

# STree：面向混合状态空间模型的推测树解码 论文总结

## 1. 论文的核心问题与整体含义
- **研究背景**：大规模语言模型的自回归推理受限于逐token串行生成，推测解码通过一个“草稿模型”多条猜测和一个“验证模型”并行检查来加速推理。该技术在Transformer上已成熟，而状态空间模型（SSM）本身因无需缓存历史token而更高效，但现有SSM推测解码方法**尚未利用树形验证**来提高接受长度。
- **核心问题**：SSM的状态更新是严格因果的，缺乏直接计算任意token树结构的高效机制。将前缀树展开为多条序列会引入大量重复计算和状态存储开销，限制了树形推测解码在SSM中的应用。
- **整体含义**：本文旨在为SSM和SSM-Transformer混合架构设计首个可扩展的树形推测解码算法，填补这一空白，从而在保持生成质量一致的前提下进一步加速SSM模型的推理。

## 2. 论文提出的方法论
- **核心思想**：将树结构打包为单个序列，并通过一个**树掩码**（tree mask, \(L\)）描述token间的父子关系。利用SSM状态转移矩阵 \(A\) 的**对角结构**，将序列长度的乘积转化为指数‑对数求和，从而定义“树累积”状态转移量 \(A_{tree} = L \cdot A_{\log}\)，一次性计算树中所有路径的隐藏状态。
- **关键技术细节**：
  - 根据通用SSM形式 \(x_{t+1}=A(u_t)x_t + B(u_t)u_t,\; y_t=C(u_t)x_t\)，将递归展开，得到输出序列的矩阵形式：  
    \(y = M_x x_0 + M_u u\)，  
    其中 \(M_x\) 和 \(M_u\) 利用树掩码 \(L\) 和累积的 \(\exp(A_{tree})\) 计算。
  - 该方法可视为 Mamba2 矩阵变换形式的**推广**：当 \(L\) 为下三角因果掩码时，退化为标准因果扫描；任意 \(L\) 即可描述树结构。
- **算法流程**：
  1. 用草稿模型从最后一个被接受的token出发，生成一棵token树（打包为单序列 \(S\)，对应树掩码 \(L\)）。
  2. 通过**激活回放**（activation replay）从缓存中重算正确的初始状态 \(x^*\)。
  3. 调用硬件感知的 **TREE SCAN** 核，输入 \(L\)、token序列和 \(x^*\)，一次前向得到整棵树的输出以及中间激活缓存。
  4. 根据验证模型的输出进行多步推测采样（或朴素采样），确定第一个被拒绝的位置，保留所有匹配路径上的token。
  5. 循环至生成结束。

## 3. 实验设计
- **使用模型**：
  - 纯SSM：Mamba2‑2.7B，以及为测量复杂度而随机初始化的7B/13B/23B模型。
  - 混合模型：MambaInLlama‑8B（50% Transformer层），及其变体（25%、0% Transformer）。草稿模型为由目标模型蒸馏的两层SSM或小规模SSM。
- **数据集/场景**：
  - MT‑Bench、HumanEval、GSM‑8K 三个基准，生成100或1024个token。
- **对比方法**：
  - 自回归解码（基准）。
  - 普通推测解码（Vanilla SD），采用融合选择性扫描（FSS）或分块扫描，草稿1条序列，长度4~5。
  - 基于展开树输入的基线（FSS on unrolled tree）。
  - STree（打包树输入 + 树扫描核），配合静态树或束搜索动态树。
- **消融实验维度**：
  - 温度（0 vs 1，以及连续变化温度）。
  - 采样算法（多步推测采样 vs 朴素top‑k采样）。
  - 静态树结构（不同宽度、深度和连接方式）。
  - Transformer层占比（50%、25%、0%）。
  - 草稿模型蒸馏步数（12k、48k、264k步）。
  - GPU型号（RTX 3090 和 H100）。

## 4. 资源与算力
- **GPU配置**：主要实验在 **NVIDIA RTX 3090 (24GB)** 上完成；附录补充了H100 GPU上的结果。
- **其他算力信息**：蒸馏草稿模型使用了与目标模型微调相同的数据；论文未报告训练所需的具体GPU·时或硬件数量，但提到推理速度与内存占用测量，蒸馏步数最高达264k步。

## 5. 实验数量与充分性
- **实验数量**：共包含约 **9个表格** 和 **多个图示**，覆盖端到端生成速度、前向延迟、内存占用、消融分析等多个维度，实验方案较丰富。
- **充分性与公平性**：
  - 对主要方法（自回归、Vanilla SD、STree）进行了多基准、多温度、多模型的系统性对比，且使用相同草稿模型和相同树结构以保证公平。
  - 消融实验从模型结构、采样方法、树拓扑、训练程度等角度验证了方法的鲁棒性和边界条件。
  - 存在少量不完整之处（如未提供某些实验的误差棒），但整体设计合理，能支撑核心论断。

## 6. 论文的主要结论与发现
- **STree能够高效实现SSM的树形推测解码**：相比将树展开为多条序列的基线，STree在较大树尺寸下延迟（从~60 ms降至~34 ms）和内存（最高节省近40%）均显著优化，且随着树尺寸增大优势扩大。
- **在混合模型上能实现端到端加速**：MambaInLlama‑8B上STree较自回归提速 **1.74×（温度0）和1.36×（温度1）**，并且始终优于普通推测解码（温度1时优势更明显）。
- **接受长度提升与运行开销可权衡**：通过简单线性/二次模型分析表明，对于8B混合模型，只需约 **1.1倍** 的接受长度提升即可补偿额外开销，而实验实现了约1.2‑1.4倍的接受长度提升，验证了有效性。
- **可扩展性良好**：随着模型尺寸增大（2.3B→23B），STree的相对开销从2.04倍降至1.26倍，暗示在大模型上潜力更大。

## 7. 优点
- **方法创新**：首次将树形验证引入SSM推测解码，填补了空白；提出的矩阵变换形式与现有Mamba2实现自然兼容，算法简洁。
- **硬件友好**：TREE SCAN核设计避免了中间状态实例化，利用共享内存和激活缓存，在短输入时仍然高效。
- **分析透彻**：通过线性/二次模型对运行时与接受长度的关系进行量化分析，为是否使用树解码提供了可操作的判断标准。
- **实验全面**：涵盖多模型、多基准、多温度及丰富的消融实验，并展示了向超大模型扩展的趋势。
- **开源可复现**：提供了代码仓库链接，便于后续研究。

## 8. 不足与局限
- **模型规模受限**：实际加速测量仅停留在8B级别，更大规模（如数十B）的实测结果缺失，未能完全证明在超大模型上的实用性。
- **草稿模型质量依赖**：当草稿模型蒸馏不充分时，STree速度甚至可能低于普通推测解码（见12k步结果），因此方法优势与草稿模型训练强相关。
- **树结构优化非自适应**：实验多采用固定静态树，动态最优树（如动态规划生成）可能带来进一步提升，但本文未深入探索。
- **短序列开销**：在极短输入长度或极小树尺寸下，STree因额外计算开销可能弱于普通推测解码，使用时需权衡。
- **未提供误差信**：部分实验未报告方差或置信区间，影响结果唯一性判断。
- **混合模型的通用性**：仅在特定的MambaInLlama系列上验证，其他SSM变体（如Griffin、Jamba）的泛化性尚待检验。

（完）
