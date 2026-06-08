---
title: "LoTA-QAF: Lossless Ternary Adaptation for Quantization-Aware Fine-Tuning"
title_zh: LoTA-QAF：面向量化感知微调的无损三值适配
authors: "Junyu Chen, Junzhuo Li, Zhen Peng, Wenjie Wang, Yuxiang Ren, Long Shi, Xuming Hu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=9o7oH6DAHB"
tags: ["query:edge-llm"]
score: 10.0
evidence: 通过量化感知微调中的无损三值适配直接面向LLM端侧部署
tldr: 针对量化LLM微调时高低精度适配器不兼容、合并精度损失等挑战，LoTA-QAF提出一种无损三值适配方法，能够将适配器无损合并到低精度量化权重中。该技术充分释放了量化模型在边缘设备上的计算效率优势，同时维持了微调带来的精度提升，是实现LLM高效端侧部署的关键进展。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-9o7oh6dahb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1454, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-9o7oh6dahb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1458, \"height\": 589, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-9o7oh6dahb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1442, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-9o7oh6dahb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1450, \"height\": 902, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-9o7oh6dahb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1364, \"height\": 1907, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-9o7oh6dahb/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1178, \"height\": 469, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-9o7oh6dahb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1365, \"height\": 2306, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-9o7oh6dahb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1438, \"height\": 517, \"label\": \"Table\"}]"
motivation: 量化LLM微调时存在数据类型不匹配、适配器合并精度损失等问题。
method: 设计无损三值适配机制，使适配器能与低精度权重进行无损合并。
result: 实现了适配器的无损嵌入，保障了量化模型的推理效率与微调精度。
conclusion: LoTA-QAF为边缘LLM部署提供了精确且高效的量化微调方案。
---

## Abstract
Quantization and fine-tuning are crucial for deploying large language models (LLMs) on resource-constrained edge devices. However, fine-tuning quantized models presents significant challenges, primarily stemming from: First, the mismatch in data types between the low-precision quantized weights (e.g., 4-bit) and the high-precision adaptation weights (e.g., 16-bit). This mismatch limits the computational efficiency advantage offered by quantized weights during inference. Second, potential accuracy degradation when merging these high-precision adaptation weights into the low-precision quantized weights, as the adaptation weights often necessitate approximation or truncation. Third, as far as we know, no existing methods support the lossless merging of adaptation while adjusting all quantized weights. To address these challenges, we introduce lossless ternary adaptation for quantization-aware fine-tuning (LoTA-QAF). This is a novel fine-tuning method specifically designed for quantized LLMs, enabling the lossless merging of ternary adaptation weights into quantized weights and the adjustment of all quantized weights. LoTA-QAF operates through a combination of: i) A custom-designed ternary adaptation (TA) that aligns ternary weights with the quantization grid and uses these ternary weights to adjust quantized weights. ii) A TA-based mechanism that enables the lossless merging of adaptation weights. iii) Ternary signed gradient descent (t-SignSGD) for updating the TA weights. We apply LoTA-QAF to Llama-3.1/3.3 and Qwen-2.5 model families and validate its effectiveness on several downstream tasks. On the MMLU benchmark, our method effectively recovers performance for quantized models, surpassing 16-bit LoRA by up to 5.14\%. For task-specific fine-tuning, 16-bit LoRA achieves superior results, but LoTA-QAF still outperforms other methods. Code is available in github.com/KingdalfGoodman/LoTA-QAF.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）在资源受限的边缘设备上部署时，量化压缩与任务特定的微调是关键需求，但现有方法在两者结合时面临多个根本性挑战。
- **核心问题**：
  - **推理效率损失**：低精度量化权重（如 4‑bit）与高精度适配器（如 16‑bit LoRA）之间存在数据类型不兼容，导致推理时无法充分发挥量化带来的计算效率优势。
  - **精度退化**：将高精度适配器权重合并回低精度量化权重时，不可避免的近似或截断会重新引入量化误差，损害微调精度。
  - **现有方案局限性**：已有无损合并方法（如 QA‑LoRA）只能调整量化零点因子，无法直接修改量化权重本身，限制了适配器的表达能力和微调上限。
- **整体含义**：论文旨在提出一种能够在保持严格低比特推理效率的前提下，直接调整所有量化权重、且合并过程完全无损的量化感知微调方法，从而突破现有融合策略的瓶颈。

### 2. 方法论

#### 2.1 总体框架：LoTA‑QAF （Lossless Ternary Adaptation for Quantization-Aware Fine-Tuning）
提出一种专为量化大语言模型设计的无损三值适配方法，通过三项核心技术实现“适配器无损并入量化权重”目标。

#### 2.2 核心组件与技术细节
- **三值适配器（Ternary Adaptation, TA）**：
  - 可训练适配器矩阵 \(A_T \in \{-1,0,1\}^{D_{\text{in}}\times r}\) 和 \(B_T \in \{-1,0,1\}^{r\times D_{\text{out}}}\)，其乘积 \(\Delta W = A_T B_T\) 的元素为 \([-r, r]\) 内的整数。
  - 通过阈值 \(\omega \in (0, r)\) 将 \(\Delta W\) 映射为三值矩阵 \(\hat{W} \in \{-1,0,1\}^{D_{\text{in}}\times D_{\text{out}}}\)，用于直接调节整数量化权重 \(W_{\text{int}}\)。
  - 引入偏移矩阵 \(\tilde{W}\) 和偏移因子 \(\mu\)，将未被 \(\hat{W}\) 利用的剩余信息吸收到零点因子 \(z\) 中，保证合并后量化网格的对齐。
- **无损合并机制**：
  \[
  W'_{\text{int}} = W_{\text{int}} + \hat{W}, \quad z' = z + s\cdot\mu
  \]
  合并后权重仍处于量化栅格内，不需要截断或重量化，从而避免适配器级别的精度损失，并保留仅使用低比特整型权重的推理效率。
- **三值符号梯度下降（t‑SignSGD）**：
  - 受到 SignSGD 在离散优化中应用的启发，专门针对 \(\{-1,0,1\}\) 的受限参数空间设计。
  - 更新规则：
    \[
    A_{T,t+1} = \text{clip}\big(A_{T,t} - \text{sign}(g_t) \cdot \mathbb{I}_{|g_t| > \max(\tau, \sigma_t)}, -1, 1\big)
    \]
  - 采用固定最小梯度阈值 \(\tau\) 和动态百分位数阈值 \(\sigma_t\)（从 top‑5% 衰减至 0.01%），仅更新梯度幅度足够显著的参数。
  - 无显式学习率，通过阈值选择实现自适应、由粗到细的搜索，促进收敛。

### 3. 实验设计

- **模型与量化方式**：
  - Llama 3.1 8B、Qwen 2.5 14B、Qwen 2.5 32B、Llama 3.3 70B。
  - 使用 GPTQ 非对称量化，组大小 64（8B, 14B）或 128（32B, 70B），在 C4 数据集上校准。
- **任务场景**：
  - **性能恢复**：在 Alpaca 指令数据集上微调后，评估 5‑shot MMLU 准确率。
  - **任务特定微调**：分别在 GSM8K（数学推理）、SQL 生成和 ViGGO（对话数据到文本）上微调，使用各自测试集进行 0‑shot 评估。
- **对比方法**：
  - GPTQ + LoRA（4‑bit 基础权重 + 16‑bit 适配器）；
  - QA‑LoRA（无损合并到零点因子的量化感知 LoRA）；
  - LoTA‑QAF（本文方法）。
- **超参数设置**：
  - 适配器秩：8B/14B 模型为 64，32B/70B 模型为 32。
  - 性能恢复学习率 \(1\times10^{-5}\)（8B, 14B）或 \(5\times10^{-6}\)（32B, 70B），训练 300 步。
  - 任务特定学习率 \(5\times10^{-4}\)（8B, 14B）或 \(1\times10^{-4}\)（32B, 70B），单 epoch 训练。
  - LoTA‑QAF 阈值 \(\omega\) 通常设为 \(0.75r\)，ViGGO 上为 \(0.875r\)；\(\sigma_t\) 初始 top‑5% 并在前 80% 训练中线性衰减至 0.1%，后 20% 固定为 0.01%。
- **评估指标**：准确率（MMLU、GSM8K、SQL、ViGGO），推理吞吐量和内存消耗对比。

### 4. 资源与算力

- 论文明确指出实验使用 **单块 NVIDIA A800 GPU** 完成。
- 未提供每项实验的具体训练时长，但在效率分析部分展示了针对不同数据集（Alpaca、GSM8K、SQL、ViGGO）在 Llama 3.1 8B 4‑bit 上的速度与内存对比（图 6），LoTA 相比 LoRA 训练时间增加约 14.1%–25.4%，峰值内存增加 2.6%–6.3%。
- 推理阶段效率测试详细给出了批次大小 8–128 下的吞吐量加速比（1.7×–2.0×）。

### 5. 实验数量与充分性

- **实验覆盖**：
  - 涵盖 4 种模型规模（8B 至 70B）和 3 个量化比特宽度（4、3、2 比特），共 12 种模型/量化组合。
  - 包含性能恢复（Alpaca→MMLU）和任务特定（GSM8K、SQL、ViGGO）两大场景，共计 36 组以上主要对比实验。
  - 对 LoTA‑QAF 的关键超参数 \(\omega\) 和 \(\sigma_t\) 进行了系统的消融分析，涉及多种比特宽度和数据集。
  - 对推理效率、训练效率、收敛曲线和适配器参数变化进行了深入分析。
- **充分性评价**：实验规模较大，对比方法涵盖当前最佳基线，消融研究较为全面，评估指标多维（精度、速度、内存、收敛性）。实验设置详实且可复现，整体上具备较高的充分性与客观性。

### 6. 主要结论与发现

- **性能恢复场景**：LoTA‑QAF 在所有比特宽度和模型规模下均优于 GPTQ+LoRA 和 QA‑LoRA，尤其在低比特（2‑bit）下优势显著，例如在 Qwen 2.5 14B 2‑bit 上超出 LoRA 达 5.14%。
- **任务特定微调场景**：LoTA‑QAF 性能不及保留 16‑bit 适配器的 LoRA，但稳定优于 QA‑LoRA，显示出在高效推理与任务适应性之间的良好平衡。
- **推理效率**：适配器无损合并后，推理仅使用纯低比特整型权重，相较 LoRA 在 4/3/2‑bit 下分别获得 1.9×、1.7×、2.0× 的吞吐加速。
- **适配器特性**：t‑SignSGD 使得适配器参数呈双向（正/负）等比例变化，约三分之二参数在训练过程中未更新，体现出一种选择性、有噪声过滤特性的更新机制。

### 7. 优点

- **方法论亮点**：
  - 首次实现既可直接修改量化权重、又能完全无损合并适配器的量化感知微调方法。
  - 三值适配器设计与量化栅格对齐，从原理上避免了高‑低精度合并时的误差。
  - t‑SignSGD 优化器无学习率，通过动态阈值实现离散参数空间的稳定、粗‑细粒度搜索，颇具新意。
- **实验设计亮点**：
  - 在大规模模型和多比特设置下进行广泛验证，同时涵盖通用能力恢复与下游任务特化，实用性强。
  - 详细的超参数分析与推理/训练效率剖析，提供了良好的指导价值。
  - 提供开源代码，增强可复现性。

### 8. 不足与局限

- **训练效率未达理论极限**：因 PyTorch 不原生支持三值数据类型，使用 bfloat16 模拟和 Triton 定制算子使训练开销反而略高于 LoRA（14–25% 时间增幅），未完全发挥三值运算的理论优势。
- **收敛性弱于全精度适配器**：在任务特定微调上不如 16‑bit LoRA；2‑bit 量化时，适配器调整步长较大导致收敛稳定性受限。
- **优化器探讨不够深入**：t‑SignSGD 缺乏动量机制或更先进的阈值调度策略，其设计空间尚未充分探索。
- **应用限制**：三值适配矩阵的调整强度由阈值 \(\omega\) 控制，极端低比特（如 int2）下过于保守或激进的设置均可能带来性能波动，需谨慎调参；未在更多样化的量化格式（如 int8、非对称/对称以外方案）上进行验证。
- **公平性**：与 LoRA 的比较中，LoRA 使用 16‑bit 适配器而 LoTA‑QAF 简化至三值，精度对比并非严格“同容量”，但论文已明确指出不同方法在推理效率与精度间的权衡，结论客观。

（完）
