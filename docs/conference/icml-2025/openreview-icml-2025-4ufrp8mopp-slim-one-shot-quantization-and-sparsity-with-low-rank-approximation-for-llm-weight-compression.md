---
title: "SLiM: One-shot Quantization and Sparsity with Low-rank Approximation for LLM Weight Compression"
title_zh: SLiM：面向LLM权重压缩的一站式量化、稀疏化与低秩近似
authors: "Mohammad Mozaffari, Amir Yazdanbakhsh, Maryam Mehri Dehnavi"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=4UfRP8MopP"
tags: ["query:edge-llm"]
score: 9.0
evidence: 集成量化、稀疏化和低秩近似以实现LLM权重压缩，降低内存并加速推理
tldr: SLiM是一种一无缝结合量化、稀疏化和低秩近似的一站式LLM压缩框架，无需再训练即可降低内存占用并加速推理，其精度可与稠密模型媲美。该框架通过概率式均匀量化和半结构化稀疏性，在硬件友好条件下实现了高效的权重压缩，为资源受限设备上的LLM部署提供了新途径。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-4ufrp8mopp/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4ufrp8mopp/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 753, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4ufrp8mopp/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 1033, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4ufrp8mopp/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1547, \"height\": 1601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4ufrp8mopp/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1679, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-4ufrp8mopp/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 912, \"height\": 645, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 583, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 869, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1423, \"height\": 918, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 862, \"height\": 495, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1566, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1644, \"height\": 638, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1630, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1276, \"height\": 893, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1622, \"height\": 850, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1644, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1664, \"height\": 941, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1666, \"height\": 938, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1602, \"height\": 632, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1387, \"height\": 891, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1632, \"height\": 812, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1639, \"height\": 636, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1474, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1468, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1486, \"height\": 421, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1427, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1429, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1430, \"height\": 420, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1325, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-4ufrp8mopp/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1389, \"height\": 153, \"label\": \"Table\"}]"
motivation: 现有LLM压缩方法需昂贵重训练，而一站式方法精度不足。
method: 提出SLiM框架，同时应用量化、稀疏化和低秩近似进行一站式权重压缩。
result: 在无需重训练的情况下实现与稠密模型可比精度，降低内存和推理延迟。
conclusion: SLiM为LLM的硬件友好压缩提供了一种高效一站式解决方案。
---

## Abstract
Conventional model compression techniques for LLMs address high memory consumption and slow inference challenges but typically require computationally expensive retraining to preserve accuracy. In contrast, one-shot compression methods eliminate retraining cost, but struggle to achieve accuracy comparable to dense models. This paper presents SLIM, a new one-shot compression framework that holistically integrates hardware-friendly quantization, sparsity, and low-rank approximation into a unified process. First, we formulate the quantization process using a probabilistic approach (SLIM-Quant) that enables us to apply uniform quantization. Then, we use an existing one-shot pruning method to apply semi-structured sparsity on top of the quantized weights. Finally, to compensate for the introduced aggregated quantization and sparsity error, we use a novel saliency function with unique invertible and additive features that enables us to
mathematically compute the value of low-rank adapters. SLIM improves model accuracy by up to 5.66% (LLaMA-2-7B) for 2:4 sparsity with 4-bit weight quantization, outperforming prior methods. Models compressed with SLIM achieve up to 4.3× and 3.8× on Nvidia RTX3060 and A100 GPUs, respectively. Additionally, they achieve up to 0.23× end-to-end memory reduction in comparison to their dense counterparts. We also propose an optional PEFT recipe that further improves accuracy
by up to 1.66% (LLaMA-2-13B) compared to SLIM without fine-tuning.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：大型语言模型（LLMs）参数庞大，导致高内存占用和慢推理速度，现有压缩技术难以在避免昂贵重训练（one-shot）的同时，保持与稠密模型（dense model）相当的精度。
*   **研究动机**：
    *   **传统压缩方法**（如需要重训练的量化、剪枝）计算成本和时间成本过高，不切实际。
    *   **现有one-shot压缩方法**虽然省去了重训练，但精度损失显著，尤其是在结合硬件友好的半结构化稀疏（如2:4稀疏）和低比特量化时，精度差距更加明显。
    *   **联合压缩的挑战**：将剪枝和量化结合使用时，两种技术引入的误差会叠加，导致性能严重下降。现有的低秩适配器（low-rank adapters）补偿方法也需要昂贵的重训练。
*   **整体含义**：SLIM旨在提出一个**统一的one-shot压缩框架**，将硬件友好的量化、稀疏性和低秩近似无缝集成，在不依赖任何重训练的情况下，最大限度地减少精度损失，实现高效、高质量的LLM部署。

### 2. 论文提出的方法论（核心思想、关键技术细节、公式或算法流程）
SLIM框架通过三个核心步骤实现权重压缩，并辅以低秩适配器补偿和可选微调，其核心思想是**将非凸的优化问题转化为可高效求解的凸问题**，并使用**基于显著性的方法**直接计算低秩适配器。

#### 步骤一：SLiM-Quant量化方法
*   **核心思想**：将原本非凸的均匀量化误差最小化问题（MSE），通过**概率方式重新表述**，转化为一个可数值求解的凸优化问题。
*   **技术细节**：
    *   均匀量化虽高效，但对离群点敏感。SLiM-Quant通过最小化量化误差和截断误差之和来寻找最优缩放因子 $\alpha$。
    *   目标函数为：$\alpha^* = \arg\min_{\alpha} (E_{quant}(\alpha) + E_{clip}(\alpha))$，其中 $E_{quant}(\alpha)$ 是量化误差积分，$E_{clip}(\alpha)$ 是截断误差积分。
    *   由于权重分布不符合标准PDF，无法解析求解，SLiM-Quant采用一种基于权重直方图的**多重网格数值积分法**，高效地寻找最优 $\alpha$。
*   **激活感知变体**：SLIM-Quant O通过联合考虑激活值和权重的显著性通道，对关键通道进行缩放，以进一步降低输出误差。

#### 步骤二：剪枝
*   在量化后的权重基础上，应用现有的one-shot剪枝方法（如Wanda）引入**半结构化（如2:4）或非结构化稀疏性**。

#### 步骤三：SLiM-LoRA低秩适配器补偿
*   **核心思想**：使用低秩适配器 $L$ 和 $R$ 补偿量化误差 $E_Q$ 和稀疏误差 $E_S$ 的聚合影响。关键在于定义一个**可逆且可加**的显著性函数 $F$，通过该函数可以直接计算出最优适配器，无需迭代训练。
*   **技术细节**：
    *   **显著性函数 $F$**：定义为 $F(W) = \text{diag}(\bar{x})W$，其中 $\bar{x}$ 是校准集输入的平均绝对值。该函数满足可逆和可加属性，并能反映元素的重要性。
    *   **优化目标**：最大化补偿后权重的显著性，等同于最小化显著性误差：$L, R = \arg\min_{L,R} \|F(-(E_Q+E_S)) - F(LR)\|^2$。
    *   **解析求解**：通过计算 $F(-(E_Q+E_S))$ 的奇异值分解（SVD），并利用 $F$ 的可逆性，可以直接推导出 $L$ 和 $R$ 的精确值，无需任何优化过程。

#### 可选部分
*   **适配器量化**：对全精度低秩适配器 $L$ 和 $R$ 进行4-bit分组量化（AbsMax），以降低其引入的额外开销。
*   **参数高效微调（PEFT）**：冻结已压缩的权重，仅对（量化的）低秩适配器进行少量步骤的微调，以进一步提升精度。

### 3. 实验设计（使用数据集/场景、Benchmark、对比方法）
*   **模型与数据集**：
    *   **模型家族**：OPT（125M到13B）和LLaMA-2（7B、13B），部分实验扩展到LLaMA-2-70B和LLaMA-3.1-405B。
    *   **校准数据集**：C4数据集的128个序列。
    *   **评估基准**：在**零样本下游任务**上评估准确性，包括MMLU、Piqa、Arc-Easy、Arc-Challenge、WinoGrande和OpenBookQA。同时也使用WikiText-2数据集评估语言建模的**困惑度（Perplexity）**。
*   **实验场景**：
    *   **联合压缩**：4-bit权重量化 + 50%稀疏（2:4和Unstructured）。
    *   **单独压缩**：纯剪枝（50%稀疏）和纯量化（4-bit）。
    *   **联合稀疏与更低比特量化**：4-bit量化+50%稀疏 vs 2-bit纯量化，以比较等压缩率下的性能。
    *   **输入量化**：评估8-bit输入激活量化的影响。
*   **对比方法**：
    *   **剪枝方法**：Magnitude Pruning， SparseGPT, Wanda, MaskLLM。
    *   **量化方法**：OPTQ, AWQ, OmniQuant, AffineQuant, AbsMax, L2QER。
    *   **联合压缩方法**：JSQ（联合稀疏化与量化）。
    *   **低秩补偿方法**：Naive-LoRA（仅最小化误差的Frobenius范数）。

### 4. 资源与算力（GPU型号、数量、训练时长）
论文提到了在不同阶段的资源使用情况，具体如下：
*   **模型压缩（One-shot阶段）**：
    *   **GPU型号**：H100 GPU。
    *   **压缩时间**：例如，对于LLaMA-2-13B模型，SparseGPT+OPTQ耗时46分钟，SLiM（含LoRA）耗时68分钟。
*   **推理速度测试**：
    *   **GPU型号**：NVIDIA RTX 3060和A100-40GB GPU。
*   **可选微调阶段**：
    *   **GPU型号**：H100 GPU。
    *   **训练时长**：在30万C4 tokens上进行PEFT微调，LLaMA-2-13B模型约需14小时，而传统全权重微调则需36天以上，突显了SLiM微调的高效性。
*   **校准与微调数据集**：C4数据集。

### 5. 实验数量与充分性
实验设计**非常全面且充分**，系统性地验证了方法的优越性和鲁棒性。
*   **主要精度对比**：在不同模型家族（OPT， LLaMA-2）、不同大小（7B， 13B）和两种稀疏模式（2:4， Unstructured）下，与多种SOTA方法进行了零样本精度和困惑度的对比。
*   **消融研究**：
    *   对比了Naive-LoRA与SLiM-LoRA，验证了显著性设计的有效性。
    *   对比了SLiM-Quant W与SLiM-Quant O，验证了激活感知量化的收益。
    *   分析了有无适配器量化（SLiM-LoRA vs SLiM-LoRA Q）的影响。
    *   对适配器秩（rank）、校准样本数量、校准数据集种类进行了敏感性分析。
    *   分析了不同稀疏度比率对性能的影响。
*   **资源效率分析**：提供了详细的内存减少和计算量（FLOPs）减少的理论分析，并报告了在RTX 3060和A100 GPU上的实际加速比。
*   **扩展性测试**：实验扩展到包括LLaMA-2-70B和LLaMA-3.1-405B在内的超大规模模型，验证了方法的可扩展性。
*   **对比公平性**：实验设定（如校准样本数、适配器秩）与基线方法保持一致。

### 6. 论文的主要结论与发现
*   **精度优越**：SLiM在one-shot设置下，将量化、剪枝和低秩近似结合，在多种模型和数据集上**均达到了最优精度**，显著优于现有one-shot方法。例如，在LLaMA-2-7B的2:4稀疏+4-bit量化场景下，平均准确率比最佳基线方法提升了**高达5.66%**。
*   **效率提升显著**：SLiM压缩的模型在A100和RTX 3060 GPU上分别实现了最高**3.8倍和4.3倍**的逐层加速，同时实现了高达**0.23倍**的端到端内存占用降低。
*   **有效突破Pareto前沿**：在相同比特预算下，SLiM压缩的模型精度**甚至能超过同等大小的稠密模型**（最高提升0.6%），打破了精度与效率的固有平衡。
*   **组件有效性**：SLiM-Quant的概率式均匀量化、SLiM-LoRA的基于显著性解析求解的低秩适配器，以及适配器量化，每个组件都对最终性能有正面贡献，且计算开销可控。
*   **灵活的可选微调**：提出的PEFT方法能以极低的计算成本，在SLiM的基础上进一步提升模型精度（最高再提升1.66%）。

### 7. 优点（方法或实验设计上的亮点）
*   **统一的One-shot框架**：首次将硬件友好的均匀量化、半结构化稀疏和低秩补偿无缝集成到一个**无需任何迭代训练**的流程中。
*   **方法创新性强**：
    *   **SLiM-Quant**：通过概率建模将非凸量化问题转化为可高效数值求解的凸问题，巧妙避开了梯度优化。
    *   **SLiM-LoRA**：提出**可逆且可加的显著性函数**，使得低秩适配器的值可以通过一次SVD分解**直接数学计算得出**，省去了成本高昂的迭代训练，是理论上的一个亮点。
*   **实验极其详尽**：覆盖了多个模型、多个任务、多种压缩模式，并且进行了充分的消融实验、资源分析和超大规模模型的扩展性验证，结论非常有说服力。
*   **实用导向**：方法设计充分考虑了硬件友好性（均匀量化、2:4稀疏），并给出了在真实GPU上的加速和内存节省数据，证明其有很高的实用价值。

### 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）
*   **可选微调成本**：尽管PEFT轻量，但文中提到可选微调对于超越稠密模型至关重要，这部分的成本（14小时/13B模型）仍可能是某些场景下的障碍。
*   **适配器秩灵敏度**：虽然秩越大精度越高，但仍需人为在精度和开销之间做权衡，缺乏自适应机制。
*   **未与训练感知方法对比**：论文主要与one-shot方法对比，未详细讨论SLiM的精度与需要**完整重训练**的压缩方法（如某些量化感知训练QAT方法）之间的差距。
*   **校准数据集影响**：虽敏感性分析显示影响不大，但其性能仍依赖于校准数据集的质量和代表性，在极端分布外数据上的鲁棒性有待进一步验证。
*   **特定硬件依赖**：其速度提升部分依赖于针对NVIDIA GPU优化的专用内核（如Sparse Marlin），在其他硬件平台上的通用性和效率未得到验证。

（完）
