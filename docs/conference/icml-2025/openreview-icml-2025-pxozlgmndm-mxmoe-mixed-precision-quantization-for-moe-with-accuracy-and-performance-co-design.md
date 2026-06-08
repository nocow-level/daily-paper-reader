---
title: "MxMoE: Mixed-precision Quantization for MoE with Accuracy and Performance Co-Design"
title_zh: MxMoE：面向MoE的精度与性能协同设计的混合精度量化
authors: "Haojie Duanmu, Xiuhong Li, Zhihang Yuan, Size Zheng, Jiangfei Duan, Xingcheng Zhang, Dahua Lin"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=pXoZLGMNDm"
tags: ["query:edge-llm"]
score: 9.0
evidence: 混合精度量化优化MoE模型，提升部署效率
tldr: 针对MoE模型参数量和计算量大的部署难题，利用线性块量化敏感度差异和专家激活频率异质性，提出混合精度量化框架MxMoE，联合优化精度与系统性能，自动生成高效配置。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-pxozlgmndm/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1777, \"height\": 640, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pxozlgmndm/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 707, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pxozlgmndm/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 870, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pxozlgmndm/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 702, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pxozlgmndm/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1794, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pxozlgmndm/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 866, \"height\": 488, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1761, \"height\": 1151, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 857, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 855, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1388, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 916, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1445, \"height\": 2311, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pxozlgmndm/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1444, \"height\": 679, \"label\": \"Table\"}]"
motivation: MoE部署受限于参数和计算需求，量化是关键，但不同模块敏感度不同。
method: 分析敏感度和激活模式，设计混合精度优化框架，自动生成最优位宽配置。
result: 在保持精度的同时实现更高的推理效率。
conclusion: MxMoE通过协同设计为MoE模型提供了高效的混合精度部署方案。
---

## Abstract
Mixture-of-Experts (MoE) models face deployment challenges due to their large parameter counts and computational demands. We explore quantization for MoE models and highlight two key insights: 1) linear blocks exhibit varying quantization sensitivity, and 2) divergent expert activation frequencies create heterogeneous computational characteristics. Based on these observations, we introduce MxMoE, a mixed-precision optimization framework for MoE models that considers both algorithmic and system perspectives. MxMoE navigates the design space defined by parameter sensitivity, expert activation dynamics, and hardware resources to derive efficient mixed-precision configurations. Additionally, MxMoE automatically generates optimized mixed-precision GroupGEMM kernels, enabling parallel execution of GEMMs with different precisions. Evaluations show that MxMoE outperforms existing methods, achieving 2.4 lower Wikitext-2 perplexity than GPTQ at 2.25-bit and delivering up to 3.4x speedup over full precision, as well as up to 29.4% speedup over uniform quantization at equivalent accuracy with 5-bit weight-activation quantization. Our code is available at https://github.com/cat538/MxMoE.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：Mixture-of-Experts (MoE) 模型因参数量巨大、计算开销高，难以高效部署。现有均匀量化方法未充分考虑 MoE 结构内部的异质性，导致精度损失或加速效果不佳。
- **研究动机**：发现 MoE 中不同线性块对量化的敏感度差异显著，且各专家激活频率高度不均，从而带来混合精度量化的机会；同时，需要将算法精度与系统性能进行协同设计，才能将理论加速转化为实际 wall‑clock 时间的提升。
- **整体含义**：提出一种面向 MoE 模型的精度‑性能协同设计框架 **MxMoE**，在极低位宽下兼顾模型准确度和硬件执行效率。

## 2. 论文提出的方法论

- **核心思想**：以 **线性块** 为最小分配粒度，结合参数敏感度、专家激活模式和硬件资源，通过整数线性规划（ILP）自动推导最优混合精度量化方案，并自动生成支持异构精度的并行 Group‑GEMM 内核。
- **关键技术细节**：
  - **量化损失建模**：对于 MoE 块中的每个线性块，在各硬件支持的量化方案下，利用小批量校准数据计算输出扰动 \(\Delta_{i,j,k}\) （量化前后欧氏距离）。
  - **运行时成本建模**：依据 token 分布得出每个线性块的 GEMM 形状，将其在 GPU 上分解为 tiles；预先 profiling 各 tile 的耗时 \(c_{i,j,k,t}\)，以所有 tiles 串行时间除以流多处理器（SM）数近似总执行时间 \(T\)。
  - **ILP 优化目标**：\(\min\ L^r \cdot T^{(1-r)}\)，约束为每个线性块只选一种量化方案，且总量化内存不超预算。\(r\) 为平衡精度与性能的超参数。
  - **混合精度 Group‑GEMM 内核生成**：
    - **微内核特化**：为每种量化方案定制 CTA 级设备函数，独立优化访存与计算流水线（如 W2A16 的融合反量化、W4A4‑g128 的软件流水）。
    - **资源配置**：强制所有微内核 warp 数量一致，共享内存按最大需求分配；通过 k‑dimension tiling（slice‑K）缓解小 tile 导致的共享内存浪费。
    - **Tile 调度**：采用贪心启发式，将耗时长的 tile 优先映射到 SM，近似最小化 makespan。
- **公式/算法流程**：整体流程为 “离线统计 → ILP 求解 → 方案应用 → 内核生成与调度”，公式 (7) 给出了完整的 ILP 约束形式。

## 3. 实验设计

- **数据集/场景**：
  - 校准集：Wikitext‑2 训练集中抽 128 条长度 4096 的序列。
  - 评测集：Wikitext‑2（PPL）和 7 个常识推理任务（Arc‑Challenge, Arc‑Easy, HellaSwag, LAMBADA‑openai, LAMBADA‑standard, PIQA, WinoGrande）。
  - 性能测试：在 RTX‑4090 上测试单 MoE 块的吞吐量（token 数 512 和 8192，覆盖 memory‑bound 与 compute‑bound）。
- **对比方法**：
  - **Weight‑only**：GPTQ（带随机 Hadamard 变换），位宽 3.25‑bit、2.25‑bit。
  - **Weight‑activation**：QuaRot（4‑bit 均匀），MxMoE 平均 5‑bit 混合精度。
  - 吞吐量对比：FP16 CUTLASS、HQQ、VLLM‑Marlin‑MoE、MxMoE 自有统一精度及混合精度内核。
- **模型**：DeepSeek‑V2‑Lite、Qwen1.5‑MoE、Qwen2‑MoE、Mixtral‑8×7B。

## 4. 资源与算力

- **GPU 型号**：所有实验均在 **Nvidia RTX‑4090** 上执行。
- **校准开销**：根据模型大小，离线统计时间从几分钟到几小时不等，论文未报告具体 GPU 时数或训练时长。量化方法采用 GPTQ（校准集同上），无需额外重训练。
- **算力未完全明确**：未提及 GPU 数量（推测为单卡），也未给出训练/校准的具体 wall‑clock 时间。

## 5. 实验数量与充分性

- **实验组数**：
  - 4 个 MoE 模型 × 3 种位宽配置（2.25‑bit、3.25‑bit、5‑bit）的精度对比，共 12 组主要结果。
  - 吞吐量测试：覆盖 4 个模型、两种 batch 场景（512/8192 tokens）、FP16、多种均匀量化和 MxMoE 混合精度，合计超过 20 条柱状图数据点。
  - 消融实验：两种分配粒度（线性块 vs. 专家级），以及超参数 \(r\) 在 0~1 间的精度‑性能权衡曲线。
  - 案例分析：单独分析 W5A5 方案中不同位宽组合的 PPL 影响。
- **充分性评价**：实验覆盖主流 MoE 架构，同时评估了精度和实际加速，消融实验解释了关键设计选择，整体较为充分。比较对象均为公开方法，基准一致，公平性较好。
- **潜在不足**：仅在单张 RTX‑4090 上测试，未涉及 A100/H100 等数据中心 GPU；跨层误差传播的影响仅简单提及，未做深入消融。

## 6. 论文的主要结论与发现

- MxMoE 在极低位宽（2.25‑bit）下的 Wikitext‑2 PPL 相比 GPTQ 降低 2.4（DeepSeek‑V2‑Lite），3.25‑bit 时多数模型也有提升。
- 在 5‑bit 权‑激活混合量化下，MxMoE 显著优于 QuaRot 的 4‑bit 均匀量化，且仅需约 1‑bit 额外平均位宽即可取得接近 FP16 的精度。
- 性能方面，混合精度方案实现 1.6‑3.4× 的吞吐量提升，且在同等精度下可比 8‑bit 均匀量化再加速 29.4%。
- 线性块级别的位宽分配明显优于专家级别分配；联合优化目标超参数 \(r\) 可有效平衡精度与速度。
- 自动化内核生成成功消除了多精度计算的内核启动开销，使异构 Group‑GEMM 高效并行。

## 7. 优点

- **细粒度混合精度**：首次在 MoE 中以线性块为粒度进行硬件感知的位宽优化，充分挖掘不同组件敏感度的差异。
- **算法‑系统协同**：将精度损失与实际执行时间统一到 ILP 框架中，保证了方案在真实硬件上的加速有效性。
- **自动化内核支持**：通过微内核特化与资源配置约束，自动生成异构精度并行 Group‑GEMM 内核，避免了手工为每种组合编写内核的巨大工程量。
- **实验扎实**：多模型、多位宽、多任务评测，同时兼顾精度与吞吐量指标，消融分析解释性强。

## 8. 不足与局限

- **跨层误差累积**：灵敏度指标基于单层扰动，可能低估深层误差传播；在 Qwen2‑MoE 上精度略逊于 GPTQ，作者推测与此相关。
- **硬件平台单一**：所有实验均在 RTX‑4090 上进行，未验证在不同架构（如 A100、H100）或不同厂商 GPU 上的泛化能力。
- **校准依赖**：最优位宽分配需离线收集统计和 profiling，对模型和硬件的变动需重新校准，灵活性受限。
- **Mixtral 收益有限**：当专家数较少（如 Mixtral‑8×7B）时，混合精度的设计空间缩小，改进幅度相对不明显。
- **量化方案集合受限**：只考虑现有硬件原生支持的量化类型，未探索更激进的位宽组合（如 6‑bit 激活）或非均匀量化。

（完）
