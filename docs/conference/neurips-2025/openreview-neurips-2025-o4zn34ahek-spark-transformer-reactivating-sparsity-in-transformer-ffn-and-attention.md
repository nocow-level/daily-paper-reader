---
title: "Spark Transformer: Reactivating Sparsity in Transformer FFN and Attention"
title_zh: "Spark Transformer: 重新激活Transformer前馈网络与注意力中的稀疏性"
authors: "Chong You, Kan Wu, Zhipeng Jia, Lin Chen, Srinadh Bhojanapalli, Jiaxian Guo, Utku Evci, Jan Wassenberg, Praneeth Netrapalli, Jeremiah J. Willcock, Suvinay Subramanian, Felix Chern, Alek Andreev, Shreya Pathak, Felix X. Yu, Prateek Jain, David E Culler, Henry Levy, Sanjiv Kumar"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=o4zN34ahEK"
tags: ["query:edge-llm"]
score: 8.0
evidence: 重新激活Transformer中的激活稀疏性以提升效率，利于资源受限推理
tldr: 针对现代Transformer因采用非ReLU激活而丧失激活稀疏性、导致推理效率受限的问题，本文提出Spark Transformer，通过结构化稀疏设计在FFN和注意力中重新激发稀疏计算，无需回退到ReLU或使用破坏性的top-k掩码。实验表明，该方法在保持模型质量的同时大幅降低计算开销，并在CPU、GPU等硬件上实现明显加速，为Transformer模型的边缘高效部署提供了实用技术。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1376, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1113, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1132, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1404, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 577, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1179, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 730, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1180, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 572, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1400, \"height\": 618, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-o4zn34ahek/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1400, \"height\": 602, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-o4zn34ahek/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1246, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-o4zn34ahek/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1450, \"height\": 765, \"label\": \"Table\"}]"
motivation: 现代Transformer模型因放弃ReLU激活函数而失去激活稀疏性，导致推理效率下降。
method: 提出Spark Transformer，通过结构化设计在FFN和注意力中重新引入激活稀疏性，而无需退化到ReLU或使用top-k掩码。
result: 在保持模型质量的同时显著降低计算量，并在多种硬件上实现速度提升。
conclusion: 该工作为Transformer的高效推理提供了新的稀疏化思路，有助于模型在资源受限设备上的部署。
---

## Abstract
The discovery of the *lazy neuron phenomenon* (Li et al., 2022), where fewer than 10% of the feedforward networks (FFN) parameters in trained Transformers are activated per token, has spurred significant interests in *activation sparsity* for enhancing large model efficiency. While notable progress has been made in translating such sparsity to wall-time benefits across CPUs, GPUs, and TPUs, modern Transformers have moved away from the ReLU activation function crucial to this phenomenon. Existing efforts on re-introducing activation sparsity, e.g., by reverting to ReLU or applying top-k masking, often degrade model quality, increase parameter count, or complicate training. Sparse attention, the application of sparse activation to the attention mechanism, often face similar challenges.
    
This paper introduces the Spark Transformer, a novel architecture that achieves high activation sparsity in both FFN and the attention mechanism while maintaining model quality, parameter count, and standard training procedures. Our method realizes sparsity via top-$k$ masking for explicit control over sparsity level. Crucially, we introduce *statistical top-k*, a hardware-accelerator-friendly, linear-time approximate algorithm that avoids costly sorting and mitigates significant training slowdown from standard top-k operators. Furthermore, Spark Transformer reallocates existing FFN parameters and attention key embeddings to form a low-cost predictor for identifying activated entries. This design not only mitigates quality loss from enforced sparsity, but also enhances wall-time benefit. Pretrained with the Gemma-2 recipe, Spark Transformer demonstrates competitive performance on standard benchmarks while exhibiting significant sparsity: only 8\% of FFN neurons are activated, and each token attends to a maximum of 256 tokens. This translates to a 2.5x reduction in FLOPs, leading to decoding wall-time speedups of up to 1.79x on CPU and 1.40xon GPU.

---

## 论文详细总结（自动生成）

# Spark Transformer: 重新激活 Transformer 前馈网络与注意力中的稀疏性

## 1. 论文的核心问题与整体含义

- **背景与动机**：现代大型 Transformer 模型在语言理解与生成任务中取得了显著突破，但其高昂的计算开销（尤其在长序列场景）严重制约了模型的部署与应用。  
- **关键发现**：早期研究（如 Li et al., 2022）观察到**惰性神经元现象**——训练后的 Transformer 中，每个 token 仅激活前馈网络（FFN）中不到 10% 的参数。这种**激活稀疏性**可在 CPU、GPU 等设备上转化为实际推理提速。  
- **核心矛盾**：当前主流模型（如 Mistral、Gemma、LLaMA）普遍采用**非 ReLU 的门控激活函数**（如 GELU、SiLU），导致自然存在的激活稀疏性几乎消失，使得先前的稀疏加速方案难以直接迁移。  
- **现存方案的不足**：强行回归 ReLU 或使用 top-$k$ 掩码会损害模型质量；引入稀疏预测器又会增加训练复杂度与额外参数。稀疏注意力（sparse attention）也面临类似挑战。  
- **论文目标与整体含义**：重新在现代 Transformer 中**引入高水平的激活稀疏性，同时不牺牲模型质量、不增加参数规模、且维持标准训练流程**，从而在保证性能的前提下大幅降低推理计算量。

## 2. 论文提出的方法论

Spark Transformer 从 FFN 和 Attention 两个核心组件进行稀疏化设计，核心思路是将传统前向计算重新解释为**键-值查找表**，并借助**低秩预测器**与**近似 top-k 算法**实现高效稀疏激活。

### 2.1 Spark FFN（稀疏前馈网络）
- 将标准 FFN 的输入 $q$ 拆分为两部分：$q[:r]$（前 $r$ 维）和 $q[r:]$（剩余维度）。
- 第一个线性变换 $K_1^\top q[:r]$ 作为**低秩预测器**，输出经 GELU 激活后通过 **Statistical-Top-k** 选择出重要的 $k$ 个神经元。
- 基于该稀疏掩码，仅对 $K_2^\top q[r:]$ 和最终价值矩阵 $V$ 执行稀疏矩阵乘法，跳过被掩码的列/行。
- **计算量优化**：当 $r \approx d_{\text{model}}/2$ 时，FFN FLOPs 从 $4 d_{\text{model}} d_{ff}$ 降至约 $d_{\text{model}} d_{ff} + 3 d_{\text{model}} k$，在 $k$ 很小时可实现约 4 倍理论加速。

### 2.2 Spark Attention（稀疏注意力）
- 类比 FFN 设计，将查询 $q$ 与键 $K$ 也划分为低秩部分与剩余部分。
- 使用 Softmax 作为 $\sigma_1$，Softplus 作为 $\sigma_2$，对 $K_1^\top q[:r]$ 施加 **Statistical-Top-k** 并保留前 $k$ 个注意力分数（其余置为 $-\infty$），产生稀疏注意力分布。
- 仅对选中的键-值对计算后续乘法，显著降低长上下文的点积与加权求和开销。

### 2.3 Statistical Top-k（统计 Top-k）
- **核心公式**：  

  1. 计算阈值 $\theta(\mathbf{x}, k) = \text{mean}(\mathbf{x}) + \text{std}(\mathbf{x}) \cdot Q(1 - k/d)$，其中 $Q(\cdot)$ 为标准正态分位数函数。  
  2. 应用**软阈值算子** $\text{Soft-Threshold}(\mathbf{x}, \theta) = \max(\mathbf{x} - \theta \cdot \mathbf{1}, \mathbf{0})$，得到近似包含 $k$ 个正值的稀疏向量。
- **优势**：  
  – 仅需 $O(d)$ 计算量（与 LayerNorm 相当），远低于基于排序的 $O(d\log d)$。  
  – 软阈值化连续且几乎处处可微，保证梯度流，易于训练。  
  – 理论保证：在输入服从高斯分布时，超过阈值的元素数量与 $k$ 的相对误差随维度增加快速收敛。
- 对于 Spark Attention，变体改为将低于阈值的元素直接置为 $-\infty$。

### 2.4 低秩预测器与参数复用
- 预测器（$K_1$）由原有 FFN 和 Attention 的权重维度拆分而来，**不引入额外参数**，且与主网络在单一阶段内共同训练。
- 这种设计既避免了预测器单独训练的复杂性，又缓解了强制稀疏带来的质量损失，在实际中兼具更好效果与更高效率。

## 3. 实验设计

### 3.1 基础模型与训练配置
- **主模型**：以 **Gemma-2 2B** 为基准（解码器架构、2B 参数，已用 2T tokens 预训练）。
- **Spark 变体**：将 Gemma-2 2B 的 FFN 和 Attention 直接替换为 Spark FFN 与 Spark Attention，保持等参数规模。
- **训练流程**：完全沿用 Gemma-2 的预训练 recipe（数据、优化器、迭代次数）**从零训练一个完整的 Spark Transformer**（无微调范式）。

### 3.2 对比方法（含消融实验）
- **内部消融**：  
  - **ReLU 版本**：将激活函数由 GELU 改为 ReLU 以恢复稀疏性。  
  - **ReLU²**：采用平方 ReLU 变体（Zhang et al., 2024）。  
  - **Topk**：在 GELU 前应用标准 top-k 掩码但不引入预测器。  
  - **Gemma-2 + Spark Attention**：仅将注意力改为 Spark Attention。  
  - **Gemma-2 + Top-k**：在 FFN 和 Attention 中同时使用统计 Top-k，但不引入低秩预测器。  
  所有消融模型仅训练了全流程的 1/6，以控制成本。
- **与外部工作对比**：在文本中概括性地引用 ReLUification、ProSparse、HiRE、CATS 等方法，并在附录表格中比较稀疏度、质量损失与计算节省。

### 3.3 评估指标与任务
- **预训练质量**：训练损失曲线（相对标准 Gemma-2 的偏差）。
- **下游任务**：一组 Gemma-2 论文采用的标准基准，涵盖了语言理解、常识推理等多种测试。
- **推理效率**：  
  - **CPU**：在 4 核与 16 核 CPU 上使用 gemma.cpp 引擎，测量 prefill 和 decode 阶段的毫秒/ token 或解码速度（tokens/sec）。  
  - **GPU**：在 NVIDIA T4 GPU 上使用 llama.cpp，测量不同 prompt 长度下的解码速度。  
  - **FLOPs 分析**：理论计算每 token 的浮点运算量。

## 4. 资源与算力

- **训练成本**：文中明确说明 Spark Transformer 使用与 Gemma-2 2B 相同的**完整预训练流程**（2 万亿 tokens），但并未给出具体的 GPU 型号、数量或训练总时长。  
- **推理效率评测**：在 **4-Core / 16-Core CPU** 和 **NVIDIA T4 GPU** 上进行，提供了具体的硬件环境描述。  
- **总体来看**，虽然未公布训练 GPU 算力的具体规模，但从“完整 Gemma-2 训练流水线”可推断其训练投入极高（千卡级 GPU 月量级），属于典型大模型训练场景。

## 5. 实验数量与充分性

- **核心对比**：图 1a 展示了 6 种模型（Gemma-2、ReLU、ReLU²、Topk、Spark FFN、Spark Transformer）在 1/6 训练时的损失-FLOPs 权衡。
- **完整训练结果**：一个全训练的 Spark Transformer，与其对比的完整 Gemma-2 在下游任务上的表现（图 1b）。
- **稀疏性监控**：训练过程中多个层（26 层）的 FFN 激活非零比例及注意力参与 token 数量的动态变化（图 3）。
- **推理性能**：三种硬件平台（16 核、4 核 CPU、T4 GPU）下，不同 prompt 长度（256~4096 tokens）的解码速度，以及 chunked prefill 测评（图 5、图 1c）。
- **消融实验**：关于参数 $r$ 和 $k$ 的敏感度分析（附录图 C.3），以及组件拆解（Spark FFN vs. Spark Attention 分别加入的效果，附录图 C.6）。
- **理论分析**：对 Statistical Top-k 提供概率保证（Theorem 3.1）与可微性证明（Theorem 3.2）。
- **公平性与充分性**：由于训练成本极高，部分对比仅进行了 1/6 或 1/20 训练步数，但对主要结论的验证已相对充分；推理效率测试覆盖了典型的 CPU 与低端 GPU，具有实际参考价值。

## 6. 论文的主要结论与发现

- Spark Transformer 在 **FFN 中仅激活 8% 的神经元**，在**注意力中每 token 最多关注 256 个上下文 token**，实现了约 **2.5 倍的 FLOPs 压缩**。
- 在标准下游任务上，全训练的 Spark Transformer 与基准 Gemma-2 2B 性能几乎持平（质量近乎中性）。
- 与近期其他稀疏化方案相比（ReLU、ReLU²、Topk 等），Spark Transformer 在更激进的 FLOPs 节省下保持了更小的质量损失。
- 推理墙钟时间在 CPU 上取得 **1.79× 解码加速**（16 核），在 **NVIDIA T4 上达到 1.40× 加速**，prefill 阶段亦有显著提升（1.86×）。
- Statistical Top-k 近似算法仅带来极小的训练减速（相较排序 top-k 的 10× 减速），且几乎不损害精度。
- 激活分布经训练后仍近似高斯，保证了统计 top-k 阈值长期有效。

## 7. 优点

- **设计与方法论**：  
  – 巧妙地将 FFN 和 Attention 统一为键-值查找框架，使稀疏化方案在两个组件上高度对称，结构简洁。  
  – 通过拆分输入维度构建“无参数化”的低秩预测器，避免额外存储与复杂的多阶段训练。  
  – Statistical Top-k 同时解决了排序算子的硬件不友好性、非可微性和训练减速问题，且理论可靠。
- **实验验证**：  
  – 采用完全预训练而非轻量微调，结果更具说服力。  
  – 从损失曲线、下游分数、FLOPs 理论值到实际 CPU/GPU 墙钟时间，多层次评估，覆盖了模型质量与部署效率全链条。  
  – 消融分析清晰，逐渐剥离预测器和稀疏强制，揭示了各组件的贡献。
- **实用性**：  
  – 在不改变主训练框架的前提下大幅降低推理计算，有利于在 CPU、消费级 GPU 等低算力设备上运行高质量模型，对边缘推理友好。

## 8. 不足与局限

- **仅在一个模型规模上验证**：实验全部基于 Gemma-2 2B，未展示在更大尺寸（如 7B、13B 等）模型上的可扩展性，无法直接断言其泛化能力。  
- **预训练范式限制**：需从零开始训练，无法直接应用于已预训练的模型进行稀疏化改造，增加了落地成本。  
- **训练资源细节缺失**：论文未披露 GPU 类型、数量和训练时长，难以评估实际预训练的经济成本。  
- **batching 场景下的效率**：当 prefill 或 decode 的 batch 较大时，由于各 token 激活子集差异，稀疏性带来的内存带宽节省会打折扣（文中虽有分析，但未在更大 batch 下给出充分实验）。  
- **理论假设的局限性**：Statistical Top-k 依赖激活近似高斯分布，尽管实验表明该假设在训练全程基本成立，但在极端分布或特殊激活函数下可能失效。  
- **与传统稀疏方法系统的公平对比不足**：与 HiRE、CATS 等同期工作的比较仅在附录表格中简要总结，缺乏在统一基准上的直接复现或数量化 head-to-head 比较。

（完）
