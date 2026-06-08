---
title: "Gradual Binary Search and Dimension Expansion : A general method for activation quantization in LLMs"
title_zh: 渐进式二分搜索与维度扩展：LLM激活量化通用方法
authors: "Lucas Maisonnave, Cyril Moineau, Olivier BICHLER, Fabrice Rastello"
date: 2025-05-08
pdf: "https://openreview.net/pdf?id=3Wrv6Zay74"
tags: ["query:edge-llm"]
score: 9.0
evidence: 利用哈达玛矩阵进行激活量化以消除异常值，实现LLM在边缘设备上的高效部署
tldr: 针对LLM部署于边缘设备时参数量大、激活值存在异常值的问题，本文提出基于哈达玛矩阵的通用激活量化方法，通过逐步二进制搜索和维度扩展有效抑制异常值，实现更低位宽量化，在保持模型精度的同时大幅减少内存和推理时间，推动LLM边缘部署。
source: NeurIPS-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-3wrv6zay74/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1421, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3wrv6zay74/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 629, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3wrv6zay74/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1150, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3wrv6zay74/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1417, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3wrv6zay74/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1391, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-3wrv6zay74/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 511, \"height\": 393, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-3wrv6zay74/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1455, \"height\": 853, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3wrv6zay74/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1464, \"height\": 818, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3wrv6zay74/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1467, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3wrv6zay74/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1467, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3wrv6zay74/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1420, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-3wrv6zay74/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1431, \"height\": 540, \"label\": \"Table\"}]"
motivation: LLM 规模庞大，异常激活值阻碍低比特量化，边缘部署困难。
method: 利用哈达玛矩阵替代随机旋转矩阵，提出逐步二进制搜索与维度扩展策略抑制异常值。
result: 在 LLM 上实现高效激活量化，保持精度的同时降低内存占用与推理延迟。
conclusion: 该方法显著降低了 LLM 边缘部署的门槛，推动了量化技术的边界。
---

## Abstract
Large language models (LLMs) have become pivotal in artificial intelligence, demonstrating strong capabilities in reasoning, understanding, and generating data. However, their deployment on edge devices is hindered by their substantial size, often reaching several billion parameters. Quantization is a widely used method to reduce memory usage and inference time, however LLMs present unique challenges due to the prevalence of outliers in their activations. In this work, we leverage the theoretical advantages of Hadamard matrices over random rotation matrices to push the boundaries of quantization in LLMs. We demonstrate that Hadamard matrices are more effective in reducing outliers, which are a significant obstacle in achieving low-bit quantization. Our method based on a gradual binary search enables 3-bit quantization for weights, activations, and key-value (KV) caches, resulting in a 40% increase in accuracy on common benchmarks compared to SoTA methods. We extend the use of rotation matrices to support non-power-of-2 embedding dimensions, similar to the Qwen architecture, by employing the Paley's algorithm. Our experimental results on multiple models family like Mistral, LLaMA, and Qwen demonstrate the effectiveness of our approach, outperforming existing methods and enabling practical 3-bit quantization.

---

## 论文详细总结（自动生成）

# 论文深度分析总结：《渐进式二分搜索与维度扩展：LLM激活量化通用方法》

## 1. 论文的核心问题与整体含义

- **研究背景**：大型语言模型（LLM）在推理、理解和生成方面能力强大，但参数规模动辄数十亿，极大限制了其在边缘设备上的部署。
- **核心挑战**：量化是减少内存占用和推理时间的主流方法，但LLM的激活值中广泛存在**异常值（outliers）**，导致传统对称均匀量化在低位宽（如4-bit及以下）时性能急剧下降。
- **核心问题**：如何更有效地抑制激活张量中的异常值，从而将LLM的权重、激活和KV Cache安全地量化至3-bit，同时保持模型性能。
- **整体含义**：本文从理论和实践双维度提出了一套通用量化方案，显著突破了现有方法在极低位宽下的精度瓶颈，为LLM在资源受限设备上的部署提供了可行路径。

## 2. 论文提出的方法论

### 核心思想
- 利用**哈达玛矩阵（Hadamard matrix）替代随机旋转矩阵**对激活值进行线性变换，从理论上证明其能更有效地“摊平”异常值（将异常值能量均匀扩散到多个维度）。
- 引入**渐进式二分搜索（Gradual Binary Search, GBS）** 自动寻找每个投影层的最优裁剪比（clipping ratio），以最小化困惑度（perplexity）作为目标。
- 提出**维度扩展（Dimension Expansion）** 策略，使旋转矩阵可适配非2的幂次嵌入维度（如Qwen架构），并利用Paley算法生成所需维度的哈达玛矩阵。

### 关键技术细节
- **哈达玛矩阵的异常值抑制理论**：
  - 定理3.1 证明：对于含有异常值 $x=(c,\epsilon,...,\epsilon)^T$，哈达玛矩阵 $H$ 使最大值缩小 $c/\sqrt{n}$，而随机正交矩阵 $Q$ 仅能缩至 $c\sqrt{2\log n / n}$，前者在高维下更优。
  - 定理3.2 证明哈达玛矩阵在正交矩阵族中达到最优异常值抑制界（$1/\sqrt{n}$）。
- **渐进式二分搜索（算法1）**：
  - 逐步量化模型：先量化第一个线性投影，固定其余为FP16，用二分搜索在该投影的裁剪比空间内寻找使困惑度最低的值；然后固定该投影的裁剪比，继续量化下一投影，依此类推。
  - 目标函数：直接最小化验证集上的交叉熵损失（困惑度），而非最小化量化误差。
- **维度扩展（Lemma 4.1）**：
  - 对于不支持直接生成哈达玛矩阵的维度（如1536），可通过在权重矩阵中填补零值扩展维度，使得新维度满足帕莱算法要求的“$p+1$ 且 $p$ 为素数，$p\equiv 3 (\mod 4)$”。
  - 扩展后的矩阵乘积可在离线阶段融合，推理时仅需在注意力块和MLP的输入/输出维度进行扩展，不引入额外计算开销（前提是扩展量不超过理论计算成本上限）。
- **与现有方法结合**：
  - 延续QuaRot的旋转架构：在注意力与MLP线性层前后插入哈达玛矩阵（如图1），并融合权重。
  - 支持per-token激活量化和GPTQ权重量化，KV cache采用非对称量化。

## 3. 实验设计

- **数据集**：训练/校准：WikiText2的10%训练集；评估：WikiText2测试集（PPL）及6个下游基准（PIQA、HellaSwag、ARC-Easy、ARC-Challenge、WinoGrande、Lambada），取其平均值作为AVG指标。
- **模型覆盖**：Mistral-7B (Instruct v0.3 / v0.1)、LLaMA2-7B、LLaMA3-8B、Qwen2.5-7B Instruct、Qwen2.5-1.5B Instruct。
- **对比方法**：以QuaRot为基线（本身已是SoTA），同时评估与SpinQuant、DFRot等其他旋转量化方法的结合效果。
- **比特宽度设置**：4-bit和3-bit两种设置（WAKV：权重、激活、KV cache全量化）。基础配置：激活per-token对称量化，权重GPTQ组量化，KV cache非对称量化组大小为128。

## 4. 资源与算力

- **硬件**：单张NVIDIA A100 GPU。
- **耗时**：对较大模型，使用4天完成量化及GBS搜索（校准集为WikiText2的10%）。
- 显存限制：维度扩展实验时因显存受限，LLaMA3-8B最多只扩充到2036维（见Figure 2说明）。

## 5. 实验数量与充分性

- **核心对比实验**（Table 1 & 2）：4-bit与3-bit下，6个模型×基线与GBS的对比，共24组主实验（包含PPL和6个基准分数）。
- **其他旋转方法验证**（Appendix E）：额外评估SpinQuant和DFRot在4-bit/3-bit下结合GBS的效果，覆盖4个模型，进一步证明GBS的泛化性。
- **消融与特性分析**：
  - Figure 4/5展示GBS在FP16起点与4-bit起点下的裁剪比收敛过程与稳定性差异。
  - Figure 2研究维度扩展数量对AVG的影响，并标注计算成本界限。
  - Figure 6展示PPL与AVG负相关关系，验证以PPL为优化目标的有效性。
- **充分性与公平性**：实验覆盖多种模型族、多个比特位宽、多个基线，且均在相同校准数据和硬件条件下完成，结果具有客观可比性。未报告误差条是因计算成本受限，但作者提供了详尽的配置细节以确保可复现。

## 6. 主要结论与发现

- 哈达玛矩阵在数学上被证明是正交矩阵族中**最优的异常值抑制工具**，其效果随嵌入维度增大而增强。
- 所提GBS方法在4-bit和3-bit WAKV量化下全面超越QuaRot：4-bit时平均提升3%~6%的基准准确率，3-bit时**提升幅度最高超40%**（如Mistral-7B Instruct从22.06%提升至61.32%）。
- 维度扩展成功使非2幂次维度的Qwen架构也能应用旋转量化，同时维度增加本身还能进一步提升量化性能（直至触及计算成本上限）。
- 以困惑度直接作为裁剪比优化的目标是可行且有效的，相比最小化量化误差，它更准确地导向高质量压缩配置。

## 7. 优点

- **理论贡献扎实**：给出哈达玛矩阵异常值抑制能力的严格证明，并明确其与维度的关系，为后续研究提供理论支撑。
- **方法实用且轻量**：GBS仅需后训练，无需任何微调；维度扩展简单易行，可直接嵌入现有旋转量化框架。
- **性能提升显著**：在极具挑战的3bit全量化场景下，达到前所未有的可用精度，验证了极低位宽部署的可能性。
- **良好的通用性**：同时对多种模型系列、多种旋转量化方法有效，展示了方法的广泛适应性。

## 8. 不足与局限

- **计算开销**：维度扩展虽在推理时可能无额外FLOPs，但前向过程仍需处理更大的矩阵，且扩展量受理论界限限制；过度扩展将抵消量化带来的效率收益。
- **搜索效率**：GBS需对每层反复计算困惑度，在大模型上耗时数天，限制了其在快速迭代场景下的应用。论文也指出可使用更少校准数据来加速，但未深入探索。
- **缺少误差分析**：实验未报告多次运行的标准差或置信区间，结果的统计显著性未经验证。
- **模型规模覆盖有限**：实验集中于7B~8B模型，未在更大规模（>13B）或更小（<1.5B）的模型上验证，推广至极大规模模型的有效性尚待确认。
- **对层间依赖的结构假设**：GBS假设逐层贪婪优化能逼近全局最优，但未分析层间裁剪比耦合可能造成的次优解风险。

（完）
