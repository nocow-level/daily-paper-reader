---
title: "GANQ: GPU-Adaptive Non-Uniform Quantization for Large Language Models"
title_zh: GANQ：面向大语言模型的GPU自适应非均匀量化
authors: "Pengxiang Zhao, Xiaoming Yuan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=pkKQGJ5d99"
tags: ["query:edge-llm"]
score: 9.0
evidence: GPU自适应非均匀量化用于LLM权重压缩
tldr: 为解决LLM量化中硬件不支持混合精度通用矩阵乘法和均匀量化无法充分捕捉权重分布的问题，提出GANQ，一种训练无关的GPU自适应层后训练非均匀量化框架。该方法利用查找表实现硬件高效推理，在保持准确率的同时显著降低内存占用，为GPU上的LLM高效部署提供了优质量化方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-pkkqgj5d99/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1739, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pkkqgj5d99/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1130, \"height\": 386, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1598, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 848, \"height\": 706, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1681, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1680, \"height\": 465, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 853, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1681, \"height\": 674, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1677, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1599, \"height\": 198, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1770, \"height\": 597, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1593, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1417, \"height\": 474, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pkkqgj5d99/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1417, \"height\": 807, \"label\": \"Table\"}]"
motivation: 硬件缺乏原生混合精度GEMM支持，均匀量化无法有效拟合权重分布。
method: 提出GPU自适应非均匀量化框架GANQ，优化基于查找表的混合精度矩阵乘法。
result: GANQ实现了训练无关的高质量量化，在硬件上高效加速。
conclusion: GANQ为LLM在GPU上的量化部署提供了兼顾效率和准确率的解决方案。
---

## Abstract
Large Language Models (LLMs) face significant deployment challenges due to their substantial resource requirements. While low-bit quantized weights can reduce memory usage and improve inference efficiency, current hardware lacks native support for mixed-precision General Matrix Multiplication (mpGEMM), resulting in inefficient dequantization-based implementations. Moreover, uniform quantization methods often fail to capture weight distributions adequately, leading to performance degradation. We propose GANQ (GPU-Adaptive Non-Uniform Quantization), a layer-wise post-training non-uniform quantization framework optimized for hardware-efficient lookup table-based mpGEMM. GANQ achieves superior quantization performance by utilizing a training-free, GPU-adaptive optimization algorithm to  efficiently reduce layer-wise quantization errors. Extensive experiments demonstrate GANQ's ability to reduce the perplexity gap from the FP16 baseline compared to state-of-the-art methods for both 3-bit and 4-bit quantization. Furthermore, when deployed on a single NVIDIA RTX 4090 GPU, GANQ's quantized models achieve up to 2.57$\times$ speedup over the baseline, advancing memory and inference efficiency in LLM deployment.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

大语言模型（LLMs）在部署时面临巨大的资源需求，尤其是在显存和推理延迟方面。虽然通过低比特（例如 3-bit / 4-bit）量化权重可以减少显存占用并提升推理效率，但现有 GPU 硬件并不原生支持混合精度通用矩阵乘法（mpGEMM），通常需要先将低精度权重反量化（dequantization）到 FP16 再计算，这在大批次场景下引入了额外开销，难以获得理想的加速效果。另一方面，主流方法大多采用均匀量化，而 LLM 的权重分布往往高度非均匀（存在大量异常值），均匀量化难以充分捕捉这种分布，导致显著的性能损失。

GANQ 正是在这一背景下提出的。它的核心思想是设计一种 **GPU 自适应的非均匀量化框架**，既能够通过基于查找表（LUT）的方式在硬件上高效实现 mpGEMM，又能够用有理论支撑的优化方法对每一层进行非均匀量化，从而在保持模型精度的同时大幅降低显存占用并提高推理速度。

## 2. 论文提出的方法论

### 2.1 核心思想：基于码本的非均匀量化
GANQ 对权重矩阵 $W \in \mathbb{R}^{m\times n}$ 的每一行（通道）维护一个码本 $T_i = \{t_{i,0}, t_{i,1}, \dots, t_{i,2^N-1}\}$，存储 $2^N$ 个可能的量化值（例如 $N=4$ 时有 16 个值）。同时用一个低比特查询矩阵 $Q \in \{0,1,\dots,2^N-1\}^{m\times n}$ 指示每个权重对应码本中的哪一个值，即 $\tilde{W}_{i,j}=T_{i,Q_{i,j}}$。推理时，LUT 内核直接查表完成计算，省去反量化开销。

### 2.2 优化模型
对每一层，最小化量化前后输出的误差：
\[
\min_{Q,T} \|W X - \tilde{W} X\|_F^2 \quad \text{s.t.} \ \tilde{W}_{i,j}=T_{i,Q_{i,j}}
\]
利用行独立性，可将原问题分解为 $m$ 个相互独立的子问题，每个子问题是一个关于码本 $T_i$ 和 one-hot 编码矩阵 $S_i \in \{0,1\}^{2^N \times n}$ 的混合整数二次规划：
\[
\min_{S_i,T_i} \|W_i X - T_i S_i X\|^2 \quad \text{s.t.} \ \mathbf{1}^\top S_i = \mathbf{1}^\top
\]

### 2.3 GPU 自适应交替优化
由于问题复杂（离散、非凸、非光滑），GANQ 采用交替方向优化：
- **更新码本 $T_i$**：固定 $S_i$，此时为无约束二次规划，有闭式解：
  \[
  T_i^{k+1} = W_i X X^\top (S_i^{k+1})^\top \big( S_i^{k+1} X X^\top (S_i^{k+1})^\top \big)^\dagger
  \]
  该计算仅涉及矩阵–矩阵乘法，且 $(S_i X X^\top S_i^\top)$ 维度仅为 $2^N \times 2^N$，非常小，适合 GPU 并行批处理。

- **更新分配矩阵 $S_i$**：固定 $T_i$，原问题仍为离散组合优化。GANQ 使用 Cholesky 分解 $X X^\top = L L^\top$，将目标转化为 $\|W_i L - T_i S_i L\|^2$，再利用 $L$ 的下三角结构，从最后一列向前进行**反向代入**（back‑substitution）逐列贪婪确定 $S_i$ 的每一列，避免了指数复杂度。所有行的 $S_i$ 同样可以组织成张量，利用 GPU 并行完成。

完整的层量化流程如 Algorithm 1 所示，迭代 $K$ 次（例如 10 次）。

### 2.4 兼容异常值处理
GANQ 可以直接与现有异常值处理技术结合。论文实现了简单的异常值提取方法：按行找出对称的上下分位数之外的元素作为稀疏成分 $W_{\text{sparse}}$，剩余部分作为 $W_{\text{dense}}$，仅对 $W_{\text{dense}}$ 应用 GANQ，进一步提升量化质量。

## 3. 实验设计

### 3.1 数据集与评测指标
- **语言建模困惑度**：在 WikiText‑2、C4、PTB 上报告困惑度（序列长度 2048）。
- **零样本任务准确率**：HellaSwag、BoolQ、RTE、WinoGrande、ARC‑e、ARC‑c、GSM8K。
- **长上下文能力**：LongBench（标准协议，无 Chain‑of‑Thought）。
- **推理效率**：在单张 NVIDIA RTX 4090 上测量生成 1024 token（batch size=1）的 CUDA 耗时和峰值显存。

### 3.2 模型覆盖
涵盖 OPT‑125M/350M/1.3B/2.7B/6.7B，LLaMA‑7B，LLaMA‑2‑7B，LLaMA‑3‑8B，LLaMA‑3.2‑1B/3B 及其 Instruct 版本。

### 3.3 对比方法
- **基础权重量化**：RTN、GPTQ、OmniQuant。
- **带异常值处理的权重量化**：GPTQ (group‑128)、AWQ (group‑128)、OmniQuant (group‑128)、SqueezeLLM。
- 量化位宽：4‑bit 和 3‑bit。

## 4. 资源与算力

所有实验均在**单张 NVIDIA RTX 4090 GPU** 上完成。校准数据使用 128 个样本（LLaMA 系列）或 32 个样本（OPT），每个样本 2048 tokens，取自 C4 数据集。例如，GANQ 在 LLaMA‑2‑7B 上量化（10 次迭代）耗时约 **1 小时**，显著低于需要梯度的 OmniQuant（3 小时以上）和无法运行更大模型的 SqueezeLLM。这体现了方法的高资源效率。

## 5. 实验数量与充分性

论文进行了非常广泛的实验，总数超过 **15 组对比表格**，覆盖：
- 多个模型家族、多种规模、两种位宽的 perplexity（WikiText‑2、C4、PTB）。
- 零样本任务（6 个任务）的准确率对比。
- 长文本与推理任务（LongBench、GSM8K）的对比。
- 带异常值处理（GANQ⋆）与 SqueezeLLM 等的直接比较。
- 推理延迟与峰值显存的真实测量。
- 对正定性预处理策略的消融实验（固定 λ vs 自适应对角占优），验证方法鲁棒性。

所有对比均基于公开统一的设置（相同校准数据、序列长度、评测协议），基线方法均使用原作者实现或官方模型。整体实验设计**客观、公平且充分**。

## 6. 主要结论与发现

- **量化质量显著优于均匀方法**：在 4‑bit 和 3‑bit 下，GANQ 在 OPT、LLaMA、LLaMA‑2、LLaMA‑3 等模型上的 WikiText‑2、C4、PTB 困惑度均最低，且与 FP16 基线的差距大幅缩小，例如 OPT‑2.7B 4‑bit 甚至优于 FP16。
- **零样本任务性能保持良好**：LLaMA‑2‑7B 4‑bit 量化后平均准确率 64.23%，接近 FP16 的 64.47%；3‑bit 下 62.22%，远高于 RTN、GPTQ、OmniQuant。
- **实际加速显著**：在 RTX 4090 上，GANQ 4‑bit 量化模型生成速度可达 FP16 的 2.24×（OPT‑6.7B）和 2.11×（LLaMA‑7B）；3‑bit 下加速比分别达到 2.57× 和 2.39×，同时峰值显存大幅降低（OPT‑6.7B 仅 4.10 GB）。
- **兼容异常值处理**：结合 0.5% 异常值提取后，GANQ⋆ 比 SqueezeLLM 等方法更优，且性能提升明显。

## 7. 优点

- **有原则的优化模型**：首次将 LUT 非均匀量化建模为混合整数二次规划，并提供有效的数值求解方案，理论清晰。
- **硬件友好与高效**：完全兼容现有的 LUT 推理内核，无需反量化；量化过程利用 GPU 大规模并行，速度快，资源占用低。
- **即插即用且鲁棒**：训练免费、易于实现，可直接替换层量化步骤；自适应对角占优预处理保证了数值稳定性。
- **广泛验证**：在大量模型、数据集、位宽和任务上进行了充分验证，结果一致且领先。

## 8. 不足与局限

- **存储开销略有增加**：与基础均匀量化相比，每行需要存储 $2^N$ 个浮点码本值（例如 4‑bit 通道需要 16 个 FP16），但从论文的表 1 看，额外开销很小（≈0.2%），可以接受。
- **异常值处理增加推理开销**：GANQ⋆ 需要额外的稀疏矩阵运算，会导致推理延迟轻微上升，需在精度与速度间权衡。
- **当前仅支持权重量化**：未涉及激活量化，压缩率上限受限于权重部分；对于某些场景，权重–激活联合量化可能更有效。
- **实验硬件单一**：所有实验均在 RTX 4090 上进行，更大模型（如 70B 级别）和不同架构 GPU（如 A100、H100）上的验证缺失。
- **非均匀量化的泛化性**：虽然方法理论上适配各种权重分布，但码本初始值依赖均匀抽样，可能对极端分布需要更谨慎的初始化策略。

（完）
