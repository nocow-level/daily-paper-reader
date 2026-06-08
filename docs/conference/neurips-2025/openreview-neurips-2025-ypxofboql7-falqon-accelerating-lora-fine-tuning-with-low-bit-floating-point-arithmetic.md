---
title: "FALQON: Accelerating LoRA Fine-tuning with Low-Bit Floating-Point Arithmetic"
title_zh: FALQON：利用低位浮点运算加速LoRA微调
authors: "Kanghyun Choi, Hyeyoon Lee, SunJong Park, Dain Kwon, Jinho Lee"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yPXOfBoQL7"
tags: ["query:edge-llm"]
score: 4.0
evidence: 将低位浮点运算（FP8）用于加速LoRA微调，与降低数值精度加速边缘硬件相关。
tldr: 低位浮点格式（如FP8）在矩阵乘法上有硬件加速优势，但对于使用小维度矩阵的LoRA微调，量化开销却抵消了加速效果。FALQON提出将LoRA适配器在微调过程中直接合并到FP8量化的骨干网络中，消除了独立LoRA路径带来的量化开销，并通过重构前向过程保持精度，在LLM微调中实现了显著的训练加速和内存节省。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-ypxofboql7/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ypxofboql7/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1451, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ypxofboql7/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1322, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ypxofboql7/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1322, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ypxofboql7/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 884, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ypxofboql7/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 849, \"height\": 535, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 694, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1419, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1441, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 693, \"height\": 524, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 519, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1444, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 699, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 590, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1451, \"height\": 1283, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1443, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1432, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1435, \"height\": 404, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1440, \"height\": 1067, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 878, \"height\": 848, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ypxofboql7/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 878, \"height\": 720, \"label\": \"Table\"}]"
motivation: 低精度量化用于LoRA微调时，小矩阵计算产生高量化开销，抵消了硬件加速潜力。
method: 设计FALQON框架，在微调时将LoRA适配器融合进FP8量化骨干，消除独立路径，优化前向过程。
result: 实验表明FALQON在LLM微调任务上实现线性加速，且几乎不损失精度。
conclusion: FALQON为低精度量化在参数高效微调中的应用提供了可行方案，拓宽了边缘训练的可能性。
---

## Abstract
Low-bit floating-point (FP) formats, such as FP8, provide significant acceleration and memory savings in model training thanks to native hardware support on modern GPUs and NPUs. However, we analyze that FP8 quantization offers speedup primarily for large-dimensional matrix multiplications, while inherent quantization overheads diminish speedup when applied to low-rank adaptation (LoRA), which uses small-dimensional matrices for efficient fine-tuning of large language models (LLMs). To address this limitation, we propose FALQON, a novel framework that eliminates the quantization overhead from separate LoRA computational paths by directly merging LoRA adapters into an FP8-quantized backbone during fine-tuning. Furthermore, we reformulate the forward and backward computations for merged adapters to significantly reduce quantization overhead, and introduce a row-wise proxy update mechanism that efficiently integrates substantial updates into the quantized backbone. Experimental evaluations demonstrate that FALQON achieves approximately a 3$\times$ training speedup over existing quantized LoRA methods with a similar level of accuracy, providing a practical solution for efficient large-scale model fine-tuning. Moreover, FALQON’s end-to-end FP8 workflow removes the need for post-training quantization, facilitating efficient deployment. Code is available at https://github.com/iamkanghyunchoi/falqon.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：低比特浮点格式（如 FP8）在现代 GPU 和 NPU 上能显著加速大矩阵乘法，但用于**小维度矩阵**时会因量化开销（reduction + element‑wise scaling）抵消加速效果。
- **核心问题**：参数高效微调方法 **LoRA** 使用了极小的适配器矩阵，直接对其应用 FP8 量化会导致量化开销远大于计算收益，导致微调速度反而慢于 FP16。
- **研究动机**：在个性化、多任务学习等场景中需要训练大量 LoRA 适配器，因此急需一种能真正利用硬件低比特加速的 LoRA 微调方案。

## 2. 论文提出的方法论

- **总体思路（FALQON）**：将 LoRA 适配器在微调开始时就**直接合并到 FP8 量化的骨干网络**中，消除独立的低秩适配器路径，从而避免因小矩阵引入的额外量化开销。
- **关键技术步骤**：
  - **Melded LoRA 初始化（§5.1）**
    - 将高精度骨干权重 \(W\) 量化为 FP8 格式 \(\tilde{W}\)，计算量化误差 \(\Delta W = W - \tilde{W}\)。
    - 对 \(-\Delta W\) 进行秩为 \(r\) 的 SVD，得到 \(\hat{B}\hat{A}\)，将 \(\hat{A}\) 量化并拼接到 \(\tilde{W}\) 形成 \(\tilde{W}'\)，从而让单次前向计算直接输出 \(Wx + \hat{B}\hat{A}x\)，无需额外路径。
  - **高效梯度计算（§5.2）**
    - 前向时同时计算骨干输出 \(O\) 和中间结果 \(O_{\hat{A}} = \hat{A}x\)，保存 \(O_{\hat{A}}\) 供反向传播使用。
    - 利用 \(\frac{\partial \mathcal{L}}{\partial B} = \frac{\partial \mathcal{L}}{\partial O} (Ax)^\top\)，仅需计算 \(B\) 的梯度，冻结 \(A\) 以减少量化与计算开销。
  - **逐行代理更新机制（§5.3）**
    - 维护代理更新缓冲区 \(\Delta_{\text{Buffer}}\) 来记录 \(B\) 的变化，而非直接更新高精度 \(B\)。
    - 每次更新时选择 \(\Delta_{\text{Buffer}}\) 中变化最大的 top‑\(k\) 行，将其更新量作用到量化骨干权重 \(\tilde{W}\) 的对应行，避免无效的微小更新。
- **算法流程**：以伪代码（Algorithms 1‑3）给出初始化、前向计算、梯度反向与选择性权重更新的完整过程。

## 3. 实验设计

- **数据集与任务**：
  - 微调数据集：Alpaca（指令微调）、OASST1（对话）。
  - 评测基准：**MMLU**（知识推理）、**HellaSwag / PIQA / WinoGrande / ARC / BoolQ / OpenBookQA**（常识推理，五样本评估）。
- **对比方法**：
  - 量化 LoRA 基线：**QLoRA (NF4)**、**QA‑LoRA (INT4)**、**IR‑QLoRA**。
  - 低比特浮点量化方法：**FP6‑LLM (E2M3/E3M2)**、**TorchAO (FP8)**、**Fishman et al. (FP8)**。
  - 标准 FP16 LoRA 作为参照。
- **实验配置**：Paged AdamW，batch size 16，学习率 \(2\times10^{-5}\)，训练 1875 步，总训练 token 数约 3M。

## 4. 资源与算力

- **主要 GPU**：单张 24 GB 显存的 **NVIDIA RTX 4090**，搭配双路 Intel Xeon Gold 6442Y CPU、1 TB DDR5 ECC 内存。
- **额外 GPU 测试**：在 **L40S** 和 **H100** 上进行了跨硬件速度评估。
- **训练时常**：例如 LLaMA‑7B 在 Alpaca 上调 1875 步，FALQON 耗时约 0.94 小时（1.80 秒/步），QLoRA 约 2.84 小时（5.45 秒/步）。
- **成本估算**：在多适配器场景中（6040 个用户），基于云 GPU 价格估算了训练费用，FALQON 相比基线可节省数千美元。

## 5. 实验数量与充分性

论文进行了**大量且多维度**的实验，涵盖：
- 2 个模型规模（7B、13B） × 2 个微调数据集 → **4 组主要实验结果**。
- 7 个常识推理基准的详细对比。
- 与 6 种量化/低精度方法的横向比较。
- **消融实验**：是否更新矩阵 A、不同 top‑k 行数的影响、不同学习率下的表现。
- **效率分析**：不同 LoRA 秩的速度变化、各算子的时间分解、batch size 对吞吐量的影响。
- **跨硬件实验**：3 款不同 GPU 上的延时对比。
- **规模化成本分析**：基于真实价格的云端训练费用估算。

实验设置公开、基线实现引自官方仓库，且使用固定随机种子，保证了**公平性与可复现性**。覆盖范围广，足以支撑论文核心结论。

## 6. 论文的主要结论与发现

- FALQON 在 **LLaMA‑7B / 13B** 上取得了约 **3 倍**的训练加速（相比 QLoRA、QA‑LoRA 等量化 LoRA 方法），同时在 MMLU 与常识推理基准上保持**可比的准确率**。
- 相比于其他 FP8 量化训练方法，FALQON 不仅速度更快，而且**内存占用更低**，能够支持 13B 模型在消费级 GPU 上微调（其他方法 OOM）。
- 分解分析证实，加速主要来源于**量化开销的大幅削减**以及 FP8 矩阵乘法的高效利用。
- 端到端的 FP8 工作流**免去了后训练量化**，便于直接部署。

## 7. 优点

- **创新性强**：首次将 LoRA 适配器“融入”到 FP8 量化骨干中，从根本上回避了小矩阵量化开销，思想新颖。
- **系统级优化**：不仅重构了前后向计算路径，还引入 top‑k 逐行代理更新，层层递进减少无用操作。
- **实验全面扎实**：覆盖多个模型、数据集和基线，配有详细的分解分析和消融实验，证明加速不牺牲精度。
- **实用性强**：在消费级 GPU 上实现可观的加速与内存节省，并提供了跨 GPU 成本分析，具有工业落地潜力。
- **可复现性**：提供了完整代码和超参数，遵循 NeurIPS 清单。

## 8. 不足与局限

- **架构覆盖有限**：目前仅在解码器架构 Transformer（LLaMA）上验证，未扩展到编码器模型或扩散模型。
- **模型规模受限**：受计算资源限制，仅测试到 13B，更大规模（70B+）的效果尚待验证。
- **精度与部分基线的差距**：在某些常识推理任务（如 OpenBookQA）上，FALQON 的得分略低于 QLoRA、TorchAO 等方法。
- **top‑k 选择的风险**：选择性更新可能丢失部分具有长期价值的微小梯度，在更高精度或更长训练中可能累积影响。
- **依赖 FP8 硬件**：加速依赖原生 FP8 支持，不能享受该特性的旧硬件上效果会打折。

（完）
