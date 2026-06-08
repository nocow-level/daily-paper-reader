---
title: "NestQuant: nested lattice quantization for matrix products and LLMs"
title_zh: NestQuant：用于矩阵乘积和LLM的嵌套格量化
authors: "Semyon Savkin, Eitan Porat, Or Ordentlich, Yury Polyanskiy"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=4OWGON33HE"
tags: ["query:edge-llm"]
score: 10.0
evidence: 面向LLM高效部署的训练后量化
tldr: "为高效部署大型语言模型，NestQuant提出一种基于自相似嵌套格的训练后量化方案。该方法信息论最优地实现矩阵乘法的低精度量化，可即插即用于自注意力和MLP等模块。在Llama-3-8B上4位量化后，困惑度降低至6.6，优于现有方法55%以上。这为LLM在边缘设备上的低比特推理提供了高性能压缩工具。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-4owgon33he/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 736, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4owgon33he/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 786, \"height\": 298, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4owgon33he/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 831, \"height\": 493, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4owgon33he/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 854, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4owgon33he/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1660, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4owgon33he/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1189, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4owgon33he/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 917, \"height\": 745, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1723, \"height\": 529, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 867, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 848, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1720, \"height\": 873, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 774, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 560, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 895, \"height\": 171, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 708, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 932, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 788, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4owgon33he/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 759, \"height\": 175, \"label\": \"Table\"}]"
motivation: LLM的部署需要高效的训练后量化技术来降低内存和计算需求。
method: 基于自相似嵌套格，提出NestQuant量化方案，实现权重、激活和KV缓存的低精度量化。
result: "对Llama-3-8B的4位量化，困惑度降至6.6，比基线降低超55%。"
conclusion: NestQuant提供了一种信息论最优的低复杂度量化器，显著提升LLM压缩性能。
---

## Abstract
Post-training quantization (PTQ) has emerged as a critical technique for efficient deployment of large language models (LLMs). This work proposes NestQuant, a novel PTQ scheme for  weights and activations that is based on self-similar nested lattices. Recent works have mathematically shown such quantizers to be information-theoretically optimal for low-precision matrix multiplication. We implement a practical low-complexity version of NestQuant based on Gosset lattice, making it a drop-in quantizer for any matrix multiplication step (e.g., in self-attention, MLP etc).  For example, NestQuant quantizes weights, KV-cache, and activations of Llama-3-8B to 4 bits, achieving perplexity of 6.6 on wikitext2. This represents more than 55\% reduction in perplexity gap with respect to unquantized model (perplexity of 6.14) compared to state-of-the-art Meta's SpinQuant (perplexity 7.3), OstQuant (7.3) and QuaRot (8.2). Comparisons on bigger models (up to 70B) and on various LLM evaluation benchmarks confirm uniform superiority of NestQuant.

---

## 论文详细总结（自动生成）

## 1. 核心问题与背景

大型语言模型（LLM）的部署面临严峻的内存带宽、计算与通信瓶颈。训练后量化（PTQ）是降低模型存储与推理成本的关键手段，但目前对**激活值和KV缓存**的低比特量化（如4-bit）仍极具挑战。现有主流方案（如SmoothQuant、SpinQuant）多采用标量均匀量化，在高维空间存在“整形增益”损失，即大量码字浪费在概率极低的区域，导致量化误差较大。

论文提出 **NestQuant**，一种基于**自相似嵌套格**的PTQ方案，可在权重、激活和KV缓存上实现信息论上近乎最优的矩阵乘法低精度量化，从而在更低的困惑度代价下达到同等压缩率，为LLM在边缘设备的高效推理铺平道路。

## 2. 方法论

### 2.1 核心思想
- 将高维向量分块（如每块8维），对每个子向量使用**格量化**，避免标量量化的“立方整形”浪费。
- 利用**随机正交旋转**（如Hadamard矩阵）将权值/激活分布“高斯化”，抑制离群值。
- 采用**嵌套格（Voronoi码）** 实现低复杂度编解码，同时引入**多尺度缩放因子**（union of Voronoi codes）以降低过载误差。
- 提出 **QA‑LDLQ（量化感知的LDLQ）**，在校准过程中考虑激活值的量化噪声，修正权重量化目标。

### 2.2 关键技术细节
- **基格：Gosset格（\(E_8\)）**，维度 \(d=8\)，具有快速最近点查找算法，归一化二阶矩接近最优球格，且整系数可由 \(int8\) 乘加单元加速。
- **嵌套码书**：对给定整数 \(q\)，码书 \(C = \Lambda \cap q V_\Lambda\)，即格点中落在 \(q\) 倍Voronoi域内的部分。编码返回 \(q\) 元整数坐标（模 \(q\)），解码通过最小能量代表实现。
- **多尺度 \(\beta\) 组合**：使用 \(k\) 个不同缩放系数 \(\beta_1<\dots<\beta_k\)，对每个向量尝试所有 \(\beta\)，选择重构均方误差最小的一个，并将 \(\beta\) 索引与量化坐标一起存储。通过动态规划从候选集自动挑选最优 \(\beta\) 集合。
- **整体流程（算法3）**：
  1. 对输入行向量计算 \(\ell_2\) 范数 \(s\)，并归一化。
  2. 每 8 个元素尝试所有 \(\beta_p\)，编码并解码，选择失真最小的 (\(\text{enc}, \beta\))。
  3. 量化后的点积可通过直接组合解码值及 \(\beta\) 加速（算法4）。

### 2.3 QA‑LDLQ
考虑激活量化噪声 \(Z\) 独立零均值且协方差 \(J\)，权重量化目标修正为最小化 \(E[\|WX - U(X+Z)\|^2]\)，得到最优权值为 \(W H (H+J)^{-1}H\) 的形式。实际使用时，先估计 \(J\)，再在校正后的权值上执行LDLQ。

## 3. 实验设计

### 数据集与场景
- **合成数据**：独立高斯矩阵乘法，\(n=m=k=4096\)，对比信息论下界（Ordentlich & Polyanskiy，2024）。
- **语言模型**：Llama‑2（7B，13B，70B）和Llama‑3（1B，8B，70B），在WikiText2验证集上计算困惑度（PPL），并在ARC‑Easy/Challenge、HellaSwag、PIQA、WinoGrande等零样本基准上评测。

### 对比方法
SpinQuant、OstQuant、QuIP#、QuaRot、DuQuant、GPTQ、LLM‑QAT等，覆盖权重量化、权值+KV量化、全量化（W+KV+A）三种模式，主流均为4‑bit。

### 量化配置
默认参数 \(q=14\)、缩放系数数 \(k=4\)，实际平均比特率约3.99（压缩后）/4.06（未压缩），在部分实验中探索了3‑bit（\(q=7\)）等速率。

## 4. 资源与算力

文中**未明确列出所用GPU型号、数量及训练时长**。仅在致谢中提到感谢 Foundry.ai 和 Lambda Labs 提供算力，以及CUDA核的优化讨论。因此无法给出具体的计算资源开销。仅提供了推理阶段GEMV核的微观延迟对比（在A100上，8192×8192矩阵）。

## 5. 实验数量与充分性

实验覆盖较全面：
- **合成实验**：1组（对比信息论界与SpinQuant）。
- **LLM实验**：涵盖多个模型尺寸（1B→70B）、多种比特率（\(q\)变化）、多种量化范围（W、W+KV、W+KV+A），并在WikiText2和5个零样本评测上进行了系统比较（表格2，3等）。  
- **消融实验**：比较了有无LDLQ、不同旋转矩阵、不同 \(k\) 值、不同量化率下的PPL变化，还分析了多尺度 \(\beta\) 的效果。附带了硬件核延迟对比。
- **对比方法**：至少6种SOTA方案，且均采用公平比特率（包含 \(\beta\) 开销）进行对比。

总体实验数量充足，评价指标常用，且对比公平，消融研究清晰。

## 6. 主要结论与发现

- NestQuant在合成数据上逼近理论下界，显著优于标量均匀量化（SpinQuant）。
- 在Llama‑3‑8B上，**4‑bit全量化（W4A4KV4）** 达到 WikiText2 PPL 6.6，远优于SpinQuant（7.3）、OstQuant（7.3）、QuaRot（8.2），相对未量化模型的退化幅度减少超55%。
- 在多个模型尺寸和零样本评估上一致优于业界SOTA，甚至在某些配置下以全4‑bit超越了其他方法的4‑bit权重+4‑bit激活而KV保持16‑bit的效果。
- QA‑LDLQ对降低过放大幅值层的量化误差至关重要（否则出现∞困惑度）。

## 7. 优点

- **理论指导，实践高效**：将信息论上界、嵌套格理论及Voronoi码首次实际用于LLM激活与KV缓存量化。
- **即插即用**：作为矩阵乘法的drop‑in替代，支持无结构旋转+int8加速。
- **多尺度策略**：巧妙使用少量缩放系数联合格量化，平衡过载与粒度误差，且通过DP自动选参。
- **硬件友好**：提供CUDA实现细节，并给出简化版NestQuantM以进一步降低硬件复杂度。

## 8. 不足与局限

- **编码复杂度较高**：编码端需尝试多个 \(\beta\) 并进行多次格解码，代价大于简单均匀量化，可能影响在线服务的预填充延迟。
- **未结合微调**：为进一步压缩与避免“训练后”局限，作者未进行旋转矩阵优化或量化感知训练，这可能限制极限性能。
- **硬件实现细节有限**：虽然给出了CUDA核示例，但报告仅对比了矩阵向量乘的微基准，**未给出端到端推理延迟**或吞吐提升数据，实际加速效果尚不明确。
- **实验局限**：只在WikiText2及几个常识推理基准上评测，未覆盖对话、代码等更复杂任务，也未评估量化对长文本生成或思维链的影响。
- **依赖Hadamard变换**：当输入维度非2的幂次时，需要额外处理，文中虽有比较，但其对质量与效率的权衡没有完全量化。

（完）
