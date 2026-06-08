---
title: "SKIM: Any-bit Quantization Pushing The Limits of Post-Training Quantization"
title_zh: SKIM：突破后训练量化极限的任意比特量化
authors: "Runsheng Bai, Bo Liu, qiang liu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=JpoDVFYx2w"
tags: ["query:edge-llm"]
score: 9.0
evidence: 用于LLM推理的混合精度后训练量化
tldr: 针对LLM部署中量化方法在低精度下性能下降和仅提供有限位宽方案的问题，提出SKIM方法，基于缩放K均值聚类和混合精度，实现任意比特的高效后训练量化。实验表明，本方法在低精度下仍保持高性能，为LLM在边缘设备上的量化部署提供了灵活且鲁棒的解决方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-jpodvfyx2w/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 829, \"height\": 622, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jpodvfyx2w/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1728, \"height\": 770, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jpodvfyx2w/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 627, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jpodvfyx2w/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 823, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jpodvfyx2w/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 829, \"height\": 631, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jpodvfyx2w/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1036, \"height\": 758, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 466, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 870, \"height\": 890, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1788, \"height\": 841, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1433, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1775, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1775, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1772, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1777, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1080, \"height\": 572, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 762, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jpodvfyx2w/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 763, \"height\": 273, \"label\": \"Table\"}]"
motivation: 现有LLM量化方法在低精度下性能下降且通常仅支持少数特定比特位宽。
method: 提出SKIM，基于缩放K均值聚类和混合精度的后训练量化方法。
result: 实现任意比特量化，在低精度下性能仍保持良好。
conclusion: SKIM为LLM量化提供了灵活的高性能方案，推动量化在边缘部署中的应用。
---

## Abstract
Large Language Models (LLMs) exhibit impressive performance across various tasks, but deploying them for inference poses challenges. Their high resource demands often necessitate complex, costly multi-GPU pipelines, or the use of smaller, less capable models. While quantization offers a promising solution utilizing lower precision for model storage, existing methods frequently experience significant performance drops at lower precision levels. Additionally, they typically provide only a limited set of solutions at specific bit levels, many of which are extensively manually tuned. To address these challenges, we propose a new method called \textbf{SKIM}: Scaled K-means clustering wIth Mixed precision. Our approach introduces two novel techniques: 1. A \textit{greedy algorithm} to solve approximately optimal bit allocation across weight channels, and 2. A \textit{trainable scaling vector} for non-differentiable K-means clustering. These techniques substantially improve the model performance and can be adapted to any given bit. Notably, in terms of perplexity, our method narrows the gap between quantized LLaMA models and their full precision counterparts by around \textbf{14\%} on average.

---

## 论文详细总结（自动生成）

# SKIM 论文详细总结

## 1．核心问题与研究意义
**研究背景**：大语言模型（LLMs）在各种任务中表现优异，但其庞大的计算与内存需求严重制约了实际部署。量化技术通过降低数值精度来压缩模型，但现有方法面临两大痛点：  
- 在**低比特宽度**（如 3‑bit、2‑bit）下，模型性能出现**剧烈下降**。  
- 大多数方法仅提供**少数固定的比特方案**，且需要大量**手工调参**，灵活性差。  

**论文目标**：提出 SKIM 方法，实现**任意比特**的后训练量化，并在低比特下大幅度缩小与全精度模型的性能差距，从而为 LLM 的高效部署提供更灵活、更鲁棒的解决方案。

---

## 2．方法论：核心思想与关键技术

### 2.1 优化目标的统一与选择
文章首先将层间重建误差（`L-full` / `L-diag`）和基于灵敏度的二阶误差（`S-full` / `S-diag`）统一为类似结构，揭示其核心差异仅在于是否包含了输出梯度信息 `g_{y_i}`。基于理论分析与实验（消融实验），确立了目标选择原则：  
- 需要完整误差矩阵的场景（如混合精度分配、缩放向量训练）：采用 **`L-full`** 形式。  
- 涉及逐元素加权和（如加权 K‑means 聚类）：采用 **`S-diag`** 形式。  
这一统一视角为后续方法中的多目标协同优化奠定了基础。

### 2.2 通道间自适应混合精度（Mixed Precision）
**动机**：不同权重通道的数值分布差异巨大，量化误差呈现长尾分布，且误差随比特增加的变化难以预测（图 3、图 4）。为所有通道分配相同比特会造成资源浪费。  
**方法**：将问题建模为受总比特约束的误差最小化问题（背包问题变体），并设计**贪心算法** 近似求解最优比特分配：  
- 预录制每个通道在不同比特下的量化误差矩阵 `E`。  
- 从最小比特开始，每次选择误差**减少量最大**的通道增加 1 比特，直到满足总比特预算。  
- 复杂度低（`O(n log n)`），支持**任意比特**（包括非整数值）。

### 2.3 可训练缩放向量（Trainable Scaling Vector）
**动机**：缩放向量能平滑不同通道的分布，与混合精度互补。但传统经验值（如 SmoothQuant）在此失效，且 **K‑means 聚类不可微**，无法直接通过反向传播优化缩放因子。  
**方法**：提出**迭代优化策略**：  
- 交替执行“**分组优化**”（用当前缩放因子对权重进行 K‑means 聚类，得到标签）与“**缩放优化**”（固定标签，以 `L-full` 损失为目标，通过梯度下降训练缩放向量 α）。  
- 实际应用中仅需 1 次迭代即可获得显著收益，同时有效避免过拟合。

### 2.4 整体算法流程
1. 用 `S-diag` 权重对每一行进行 K‑means 预录制，构建误差矩阵 `E`。  
2. 运行贪心算法获得各通道的比特分配 `b_i`。  
3. 按分配结果执行**带加权的 K‑means 聚类**（使用 `S-diag` 形式的目标权重）。  
4. 将聚类标签固定，通过迭代优化训练**缩放向量 α**，最小化 `L-full` 重建误差。  
5. 最终由标签、码本和缩放向量恢复量化权重。

---

## 3．实验设计

### 3.1 模型与数据集
- **模型**：LLaMA‑7B/13B/30B，LLaMA2‑7B，OPT‑2.7B/6.7B。  
- **评估数据集**：WikiText2（零样本）、C4（少样本困惑度）。  
- **校准数据**：C4 的 100/128 个样本。  
- **基准测试**：PIQA、ARC‑Challenge、ARC‑Easy、MMLU（测试知识保持与推理能力）。

### 3.2 对比方法与指标
- **主要基线**：SqueezeLLM（非均匀量化 SOTA）、OmniQuant（低比特灵活）、QuIP#（非微调版本）。  
- **附加对比**：DecoupleQ、ABQ‑LLM（见附录）。  
- **评价指标**：困惑度（PPL）、基准准确率、峰值内存占用。

### 3.3 量级设定
覆盖 **4‑bit、3‑bit、3.x‑bit、2.x‑bit** 等多个档位，其中混合精度使非整数比特成为可能。

---

## 4．资源与算力消耗
- **量化过程所需硬件**：  
  - 双 AMD EPYC 处理器（共 128 核 256 线程）+ RTX 3090 GPU。  
  - 量化 LLaMA‑7B **峰值内存不足 8 GB**，耗时约 **1 小时**（含预录制、聚类、缩放训练及打包）。  
  - 预录制误差矩阵一次即可，可复用于任意后续比特选择。  
- **推理阶段**：峰值内存随比特线性增加（图 6），3.2‑bit LLaMA‑7B 仅需约 3.13 GB，优于同等内存级别的 SqueezeLLM。

---

## 5．实验数量与充分性分析

**实验总量庞大且覆盖全面**：  
- 多模型、多数据集、多比特级的**主实验**（表 1、表 5、表 6）>20 组。  
- **基准准确率**评估（表 3）覆盖 4 项测试、2 种精度。  
- **消融实验**：  
  - 不同优化目标（`S-diag`、`L-diag`、`L-full`）的有效性对比（表 2）。  
  - 缩放向量与迭代优化的影响分析（图 5）。  
- **内存效率**分析（表 4、图 6）。  
- **附录**中与额外基线（DecoupleQ、ABQ‑LLM）的比较。

**公平性与客观性**：  
- 对未提供 2‑bit 支持的 SqueezeLLM，作者按其官方代码复现并统一评估，保证对比公平。  
- 比特水平对齐，并注明混合精度下的实际平均比特。  
- 同时使用了 LLM 社区的标准基准和公开模型。

---

## 6．主要结论与发现
- **性能突破**：在 3‑bit 量化下，SKIM 将 LLaMA‑7B 与全精度的困惑度差距**平均缩小 18.5%**；在多个模型上平均缩小 **≈14%**。  
- **任意比特能力**：SKIM 可自适应分配比特，3.2‑bit 模型甚至超越某些 3.25‑bit 模型，打破固定比特网格。  
- **组件验证**：混合精度与可训练缩放向量均贡献显著，且迭代一次即可收敛。  
- **泛化性**：在 LLaMA 系列与 OPT 系列上均稳定超越/匹配当前最佳方法。

---

## 7．方法优点与亮点
- **灵活性与扩展性**：首个实现“任意比特”的后训练权重量化方案，可按内存容量自适应。  
- **统一目标框架**：将两种主流量化目标纳入同一数学形式，指导后续模块的目标选择。  
- **工程高效**：贪心分配避免动态规划的高复杂度；K‑means 并行化与预录制使量化成本可控。  
- **理论与实验紧密结合**：目标选择的消融结果与理论排序完全吻合，增强说服力。  
- **充分的基准评估**：不仅看困惑度，还纳入知识密集型任务，验证了量化对下游能力的影响。

---

## 8．不足与局限性
- **应用范围局限**：仅针对**权重**量化，未涵盖激活值的低精度处理。  
- **最有效目标未用**：`S-full` 因内存需求过大而舍弃，可能损失提升空间。  
- **部分模型过拟合风险**：在 OPT 模型上，混合精度虽大幅降低重建误差，却导致 PPL 略升，需额外策略（如对整数比特关闭混合精度）缓解。  
- **迭代次数敏感**：缩放向量训练若迭代过多可能轻微过拟合，当前依靠经验固定为 1 次。  
- **极端低比特未验证**：实验最低至 2.25‑bit，未涉及 1‑bit 或二值化极限场景。  
- **硬件依赖**：实际推理加速仍需特定算子支持（论文关注存储压缩，未深入讨论自定义 Kernel 实现）。  
- **校准数据集偏差**：仅使用 C4 子集校准，对不同领域下游任务的泛化性仍需更广泛检验。

（完）
