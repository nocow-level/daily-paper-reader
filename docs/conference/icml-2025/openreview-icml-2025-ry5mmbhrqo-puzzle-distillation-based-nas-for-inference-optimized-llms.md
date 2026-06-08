---
title: "Puzzle: Distillation-Based NAS for Inference-Optimized LLMs"
title_zh: Puzzle：基于蒸馏的神经架构搜索用于推理优化的大语言模型
authors: "Akhiad Bercovich, Tomer Ronen, Talor Abramovich, Nir Ailon, Nave Assaf, Mohammed Dabbah, Ido Galil, Amnon Geifman, Yonatan Geifman, Izhak Golan, Netanel Haber, Ehud Dov Karpas, Roi Koren, Itay Levy, Pavlo Molchanov, Shahar Mor, Zach Moshe, Najeeb Nabwani, Omri Puny, Ran Rubin, Itamar Schen, Ido Shahaf, Oren Tropp, Omer Ullman Argov, Ran Zilberstein, Ran El-Yaniv"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=RY5MMBHRqo"
tags: ["query:edge-llm"]
score: 9.0
evidence: 使用块级局部知识蒸馏进行架构搜索，创建推理优化的大模型
tldr: 为解决大语言模型推理成本高、部署困难的问题，提出Puzzle框架，结合大规模神经架构搜索和块级局部知识蒸馏，生成硬件感知的推理优化模型如Nemotron-51B。该模型在保持高质量的同时显著加速推理，为LLM的高效部署提供了系统性解决方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1328, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 842, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 845, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 304, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 692, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 835, \"height\": 622, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ry5mmbhrqo/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 865, \"height\": 454, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 871, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 882, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 157, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 708, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 783, \"height\": 116, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1782, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 883, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 860, \"height\": 152, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 859, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 866, \"height\": 131, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 855, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 858, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 859, \"height\": 153, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 860, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 869, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 863, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 862, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ry5mmbhrqo/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1782, \"height\": 481, \"label\": \"Table\"}]"
motivation: LLMs推理成本高，参数增加与实用部署之间存在差距。
method: 采用大规模神经架构搜索，利用块级局部知识蒸馏进行并行探索，结合混合整数规划优化约束。
result: 打造出如Nemotron-51B等推理优化模型，加速推理且保持质量。
conclusion: Puzzle框架为高效部署LLM提供了自动化设计方案，推动平衡推理成本和性能。
---

## Abstract
Large language models (LLMs) offer remarkable capabilities, yet their high inference costs restrict wider adoption.
While increasing parameter counts improves accuracy, it also broadens the gap between state-of-the-art capabilities and practical deployability. We present **Puzzle**, a hardware-aware framework that accelerates the inference of LLMs while preserving their capabilities.
Using neural architecture search (NAS) at a large-scale, Puzzle optimizes models with tens of billions of parameters.
Our approach utilizes blockwise local knowledge distillation (BLD) for parallel architecture exploration and employs mixed-integer programming for precise constraint optimization.

We showcase our framework’s impact via Llama-3.1-Nemotron-51B-Instruct (Nemotron-51B) and Llama-3.3-Nemotron-49B, two publicly available models derived from Llama-70B-Instruct. Both models achieve a 2.17x inference throughput speedup, fitting on a single NVIDIA H100 GPU while retaining 98.4% of the original model's benchmark accuracies. 
These are the most accurate models supporting single H100 GPU inference with large batch sizes, despite training on 45B tokens at most, far fewer than the 15T used to train Llama-70B.
Lastly, we show that lightweight alignment on these derived models allows them to surpass the parent model in specific capabilities.
Our work establishes that powerful LLM models can be optimized for efficient deployment with only negligible loss in quality, underscoring that inference performance, not parameter count alone, should guide model selection.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

大语言模型（LLM）虽能力强大，但推理计算成本极高，严重制约了其从顶尖研究到实际商业部署的转化。增加参数量虽然提升精度，却进一步拉大了前沿能力与可行部署之间的鸿沟。传统 Transformer 架构为训练稳定性和扩展便利性而设计，采用同构重复层，忽视了各层的计算开销与其对整体性能贡献之间的平衡，因此不适合推理优化。论文的核心问题是：**如何将训练好的 LLM 从“利于训练”的结构，自动转化为面向特定硬件（如单张 H100 GPU）、满足严格推理约束（吞吐、延迟、内存）且几乎不损失模型能力的高效推理结构？**

整体含义在于提出一种可扩展的自动化框架，以极低成本（相对从头训练）实现“一父多子”的模型定制，从而推动大模型在个人化、商业化场景中的普及，并引导行业以推理性能而非单纯参数规模作为模型选型的标准。

### 2. 论文提出的方法论

Puzzle 框架采用**解耦合的神经架构搜索（NAS）** 策略，包含三个阶段：

**第一步：构建“拼图块”库（块级局部蒸馏，BLD）**
- 搜索空间定义：对父模型的每一 Transformer 层，注意力子块提供多种 GQA（不同 KV 头数）、线性层或无操作（no‑op）选项；FFN 子块提供不同中间维度（从完整尺寸到 10%）、线性层或无操作选项。整个 80 层模型搜索空间可达约 \(54^{80} \approx 10^{138}\) 种架构。
- 块级局部蒸馏（BLD）：将每个可能的子块变体独立且并行地训练，使其输出模仿对应父块输出，损失函数为归一化 MSE：\(L = \frac{\mathrm{MSE}(o_p, o_c)}{\mathrm{MSE}(o_p, 0)}\)。
- 解耦 BLD：为了降低训练成本，将乘法型搜索空间转化为加法型。训练注意力子块变体时冻结 FFN 子块（保持为父块），训练 FFN 子块变体时冻结注意力子块，随后再组合成完整块。这一设计使所需训练的变体数从 \(m \times n \times l\) 降至 \((m+n) \times l\)。
- 子块初始化：通过通道贡献度排序初始化 FFN 缩减版本，通过均值池化初始化减少 KV 头数的注意力等。
- 使用仅 1B tokens 的 Distillation Mix 数据集进行蒸馏训练，即可初步恢复大部分性能。

**第二步：组装最优架构（混合整数规划，MIP）**
- 对库中每个块变体进行“替换一个块”（replace‑1‑block）评分，衡量其替换单一父块后对模型质量的影响（推荐使用 KL 散度作为评分指标，同时支持 LM 损失或下游任务准确率）。
- 将架构选择建模为分组背包问题的 MIP：以最大化全局质量评分（所有层所选块评分之和）为目标，满足参数内存 + KV‑cache 内存约束、吞吐量下限、批次时延上限，每层恰好选一个块变体。硬件资源需求均通过在目标硬件（如 H100）上实测各块变体在不同序列长度和批量下的延迟得到。
- 通过 python‑mip 求解器在几十秒内获得高质量解，并可通过多样性约束生成多个候选架构。

**第三步：全局知识蒸馏（GKD）后训练**
- 由于 BLD 未考虑块间兼容性，对组装后的子模型进行端到端的全局知识蒸馏（GKD），损失函数定义为：
  \[
  L_{\mathrm{GKD}} = \underbrace{\sum_{l=1}^{L} \left(1 - \frac{h_l^c \cdot h_l^p}{\|h_l^c\|\|h_l^p\|}\right)}_{\text{余弦相似度损失}} + \underbrace{\sum_{i=1}^{N} p_i \log \frac{p_i}{q_i}}_{\text{KL 散度损失}}
  \]
- 实验发现引入语言建模损失会损害下游任务，故仅使用上述两项损失。

### 3. 实验设计

**数据集与场景**
- 蒸馏训练数据：Distillation Mix（224B tokens，混合 FineWeb、Dolma、Buzz‑V1.2）；部分消融实验使用 Project Gutenberg（纯文学）。
- 评估基准：MMLU、MT‑Bench、Winogrande、ARC Challenge、HellaSwag、GSM8K、TruthfulQA、XLSum、HumanEval、Arena Hard、RULER（长上下文）等。
- 部署场景：以 FP8 量化在 NVIDIA H100 SXM GPU 上运行，测试不同输入/输出长度（如 128/128、2048/2048 等）。还测试了 RTX 4090 消费级 GPU。

**主要对比方法**
- 父模型 Llama‑3.1‑70B‑Instruct 和 Llama‑3.3‑70B‑Instruct。
- 同量级或不同量级的公开模型：Llama‑3.1‑8B‑Instruct、Llama‑3.2‑3B‑Instruct、Mixtral 8x22B 等。
- 消融与基线：贪心算法、随机架构（来自库或完全随机）、仅使用 no‑op 的受限搜索空间、数据无关的“最大化参数数量”策略、Wanda 结构化稀疏、低秩近似 + 蒸馏。

### 4. 资源与算力

**训练资源**
- BLD 阶段：对 80 层模型，解耦 BLD 需训练约 \((6+9)\times 80 \approx 1200\) 个子块（每个子块使用 1B tokens 训练），利用流水线并行在多 GPU 上并行训练，但未给出具体 GPU 数量或总 GPU 小时数。
- GKD 阶段：子模型（如 Nemotron‑51B）在至多 45B tokens 上进行全局蒸馏（实际可以少至 3.7B tokens 恢复 98.8% 的 MMLU+MT‑Bench 性能），同样未披露具体 GPU 类型与数量，但暗示相比从头训练（15T tokens）成本极低。
- 推理测试：主要使用单个 NVIDIA H100 SXM GPU（FP8），TensorRT‑LLM 推理引擎，自动选择最佳张量并行和批次大小。部分实验使用 RTX 4090。

**数据获取成本**
- 仅需父模型权重而非原始训练数据，适用于“开放权重、闭源数据”场景。

### 5. 实验数量与充分性

论文进行了**系统且充分的实验**，涵盖多维度验证：
- 两种父模型（Llama‑3.1‑70B、Llama‑3.3‑70B）及对应的多个子模型（Nemotron‑51B、Nemotron‑49B 及其基础与对齐版本，8B 子模型等）。
- 十余项标准基准 + 人类盲测 + 长上下文 RULER 测试。
- 广泛的消融实验（近 10 组）：
  - 解耦 BLD vs 耦合 BLD
  - 数据集组成与规模对 BLD 的影响
  - 不同评分指标（KL 散度、LM 损失、下游任务）
  - 受限搜索空间（仅 no‑op）
  - MIP vs 贪心算法 vs 随机基线 vs 参数最大化
  - GKD 损失组合（有无 LM 损失）
  - 训练 token 预算（3.7B 到 45B）
  - 与结构化稀疏、低秩方法的对比
- 所有对比均在相同吞吐约束下进行，具备客观性和公平性。
- 实验总体设计严谨，覆盖了方法核心组件、对比基线和实际部署场景，提供了充足证据支持结论。

### 6. 论文的主要结论与发现

- **极高效的知识继承**：即便只使用父模型权重和少量数据（1B tokens BLD），Puzzle 也能构建出高质量块库，最终子模型仅需 45B tokens 的 GKD（父模型训练数据量的 0.3%）即可保留 98.4% 的基准性能。
- **硬件感知的非对称架构**：MIP 自动发现最优架构呈现出非对称结构——早期和后期层大幅降低注意力或 FFN 计算，中间层保持完整，且 FFN 从未被完全跳过，表明其在维护模型能力中更为关键。
- **突破效率前沿**：Nemotron‑51B 在单张 H100 上实现 2.17 倍吞吐提升，成为当时在单 H100 上支持大批次推理的最准确模型；8B 子模型在 RTX 4090 上也突破其效率前沿。
- **长上下文与对齐能力可扩展**：通过短时高上下文训练，子模型可保持甚至超越父模型在 16K～128K 上的性能；经过 RLHF 对齐后，部分基准可超过父模型。
- **评分指标选择至关重要**：KL 散度优于 LM 损失和简单参数最大化；针对特定任务自定义评分可进一步提升目标性能。
- **全局优化优于层间逐次贪心**：MIP 能够做出反直觉的局部决策以换取全局最优，而贪心算法导致显著精度下降。

### 7. 优点

- **自动化与低人力成本**：用户只需指定硬件约束，框架自动完成搜索和训练，无需人工设计非对称架构。
- **卓越的训练效率**：仅需父模型权重和少量 token，即可快速产生多个适配不同硬件的子模型，极大降低部署门槛。
- **硬件与真实场景深度融合**：直接测量真实硬件上的延迟和内存占用，支持 FP8 等实际量化方案，并通过定制推理引擎（TensorRT‑LLM）实现即插即用。
- **搜索空间巨大且可扩展**：解耦 BLD 使得探索大规模操作变体成为可能，未来可轻松纳入窗注意力、状态空间模型等新算子。
- **全面的评估与消融**：多基准、人类评估、长上下文测试及丰富的消融实验，验证了方法有效性和设计的合理性。

### 8. 不足与局限

- **对父模型的高度依赖**：子模型能力天花板由父模型决定，无法获得超越父模型训练数据分布的全新知识（尽管对齐可小幅超父）。
- **长上下文需额外训练**：若 BLD 未包含足够长上下文，子模型在超长序列上性能会明显下降，需要针对性的长窗口后训练。
- **实验资源透明度有限**：论文未明确给出 BLD 和 GKD 阶段使用的 GPU 数量、总 GPU 小时数，难以精确估算总体计算开销。
- **搜索空间仍有局限**：当前要求每个子块输入/输出维度与父块相同，尚未探索嵌入维度的动态变化；所有变体均基于 Transformer 组件，未包含混合架构（如 Mamba）。
- **评分指标通用性的边界**：KL 散度在大部分情况下有效，但对于高度专业的任务，仍需定制评分，可能增加部署复杂度。
- **潜在的偏差风险**：蒸馏数据集和评测基准的领域覆盖度可能影响子模型在某些小众或低资源场景下的表现。

（完）
