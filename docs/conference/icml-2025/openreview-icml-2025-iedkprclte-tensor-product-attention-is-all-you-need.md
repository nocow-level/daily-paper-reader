---
title: Tensor Product Attention Is All You Need
title_zh: 张量积注意力就是你所需要的一切
authors: "Yifan Zhang, Yifeng Liu, Huizhuo Yuan, Zhen Qin, Yang Yuan, Quanquan Gu, Andrew C Yao"
date: 2025-01-17
pdf: "https://openreview.net/pdf?id=IEDkPrCLtE"
tags: ["query:edge-llm"]
score: 9.0
evidence: 利用张量分解压缩KV缓存大小，降低推理时的内存开销
tldr: 针对Transformer模型长序列推理中KV缓存内存占用过高的问题，提出张量积注意力TPA，通过将查询、键、值分解为低秩成分并与RoPE集成，大幅压缩缓存大小，在提升模型质量的同时降低内存需求，为有限内存硬件上的长上下文处理提供了新架构。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-iedkprclte/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-iedkprclte/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1563, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-iedkprclte/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1560, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-iedkprclte/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1745, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-iedkprclte/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1743, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-iedkprclte/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1711, \"height\": 512, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1770, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1625, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1570, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1285, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 885, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1772, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1773, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1772, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1773, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1773, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1768, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1774, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-iedkprclte/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1769, \"height\": 365, \"label\": \"Table\"}]"
motivation: 处理长序列时，标准注意力机制需要大型KV缓存，导致内存开销巨大。
method: 提出张量积注意力，利用张量分解紧凑表示查询、键、值，并结合RoPE。
result: 显著缩小KV缓存，同时模型质量提升，内存效率高。
conclusion: TPA为内存高效的Transformer设计提供了新范式，有助于边缘部署。
---

## Abstract
Scaling language models to handle longer input sequences typically necessitates large key-value (KV) caches, resulting in substantial memory overhead during inference. In this paper, we propose **T**ensor **P**roduct **A**ttention (TPA), a novel attention mechanism that uses tensor decompositions to represent queries, keys, and values compactly, significantly shrinking KV cache size at inference time. By factorizing these representations into contextual low-rank components (contextual factorization) and seamlessly integrating with RoPE, TPA achieves improved model quality alongside memory efficiency. Based on TPA, we introduce the **T**ensor Produc**T** A**TT**en**T**ion **T**ransformer (T6), a new model architecture for sequence modeling. Through extensive empirical evaluation of language modeling tasks, we demonstrate that T6 exceeds the performance of standard Transformer baselines including MHA, MQA, GQA, and MLA across various metrics, including perplexity and a range of renowned evaluation benchmarks. Notably, TPAs memory efficiency enables the processing of significantly longer sequences under fixed resource constraints, addressing a critical scalability challenge in modern language models.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **问题背景**：大语言模型处理长序列时，自回归推理需缓存所有历史 token 的键（Key）和值（Value）矩阵，即 **KV 缓存**。标准多头注意力（MHA）的缓存大小随序列长度和头数线性增长，成为内存瓶颈，限制上下文窗口的扩大。
- **整体含义**：本文提出 **张量积注意力（Tensor Product Attention, TPA）**，通过**上下文感知的低秩张量分解**，将 Q、K、V 表示为若干张量积之和，从而在推理时仅需缓存分解后的低维因子，大幅压缩 KV 缓存（可达 10 倍以上），同时保持甚至提升模型质量。

## 2. 论文提出的方法论

### 核心思想
- 对每个 token 的 Q、K、V 矩阵（shape: `h × d_h`）做**上下文相关**的分解，写成低秩因子向量的外积（张量积）之和：
  \[
  Q_t = \frac{1}{R_Q} \sum_{r=1}^{R_Q} a_{Q}^{(r)}(x_t) \otimes b_{Q}^{(r)}(x_t)
  \]
  类似地处理 K 和 V，其中 \(a^{(r)} \in \mathbb{R}^h\)（头维度因子），\(b^{(r)} \in \mathbb{R}^{d_h}\)（特征维度因子），均通过可学习的线性映射从当前隐藏状态 \(x_t\) 生成。
- 推理时仅缓存因子的投影结果（例如 \(A_K(x_t)\)、\(B_K(x_t)\) 而非完整 K、V），缓存大小从 \(2hd_h\) 降至 \((R_K+R_V)(h+d_h)\)，当 \(R_K,R_V \ll h\) 时节省显著。

### 与 RoPE 的兼容
- TPA 与旋转位置编码（RoPE）**原生兼容**。RoPE 对应的旋转矩阵可作用于因子 \(b^{(r)}\) 上，实现“预旋转”的键缓存，避免在解码时重复变换，保持了 TPA 的相对位置不变性（定理 1）。
- 支持更高阶分解（如三阶），并可类似地兼容 RoPE。

### T6 架构
- 将 Transformer 解码器块中的自注意力替换为 TPA，前后使用 RMSNorm，前馈网络采用 SwiGLU 激活。整体结构与 LLaMA 相似，形成**张量积注意力 Transformer（T6）**。

### 与已有注意力的统一
- 证明 MHA、MQA、GQA 均可看作 TPA 的**非上下文特例**：将头维度因子固定为 one-hot 或分组掩码，特征因子保持上下文相关。

## 3. 实验设计

- **训练数据**：FineWeb-Edu 100B 数据集（100B 训练 token，0.1B 验证 token）。
- **基线方法**：MHA、MQA、GQA、MLA（DeepSeek-V2 的多头潜在注意力），以及 TPA 的多个变体（TPA-KVonly、Non-contextual A 等）。
- **模型规模**：small（124M）、medium（353M）、large（773M）、XL（1.5B）四种参数级别。保证同等参数数量比较（调整各注意力的头数）。
- **训练设置**：基于 nanoGPT 代码库，使用 AdamW（β1=0.9,β2=0.95）、余弦退火学习率、warmup 2000 步、全局批次 480。学习率和模型深度等见原文表 4、表 5。
- **评测基准**：在验证集上报告训练/验证 loss 和困惑度；使用 `lm-evaluation-harness` 进行零样本和两样本下游任务评估，涵盖 **ARC-E, ARC-C, BoolQ, HellaSwag, OBQA, PIQA, WinoGrande, MMLU, SciQ** 等。

## 4. 资源与算力

- **GPU**：small 模型用 4 张 A100，medium、large、XL 用 8 张 A100。
- **训练细节**：给出了微型批次大小（micro batch size）和梯度累积步数（表 4），未明确报告总训练 wall-clock 时间或训练 token 数是否处理完整个数据集（图中显示约 50B token 左右的训练曲线）。XL 模型 batch size 较小（micro 6, accumulation 10）。
- 整体来说，算力消耗与同等参数量的标准 Transformer 训练相当，但受益于 TPA 的推理端内存压缩。

## 5. 实验数量与充分性

- **规模覆盖**：四个参数级别，充分考察不同模型容量下的行为。
- **对比方法全面**：包括 MHA、MQA、GQA、MLA 及 TPA 的多个消融变体（如 TPA-KVonly、Non‑contextual A/B、不同 rank）。
- **下游任务多样**：9 个常用语言理解/常识推理基准。
- **消融实验**：
  - 针对 XL 模型改变 rank（\(R_K=R_V=2,4,6\)），展示随 rank 增加的性能变化（图 5、表 7）。
  - 针对 medium 模型使用不同初始学习率（3e‑4）重复训练，验证结论稳健性（图 6、表 12‑13）。
- **公平性**：调整各方法的头数以保证参数量一致；使用相同训练配置。实验相当充分且客观。
- **潜在不足**：未见在更大规模模型（>1.5B）、更长上下文长度、不同架构（如 MoE）上的实验。

## 6. 论文的主要结论与发现

- **性能优势**：TPA（尤其是 KV‑only 变体或适度 rank 的全分解）在验证损失和困惑度上优于 MHA、MQA、GQA 和 MLA；在下游基准的平均准确率也最高或持平，尤其在 medium 和 large 模型上显著。
- **内存效率**：TPA 使推理时的 KV 缓存大小减少一个数量级（具体为 \((R_K+R_V)(h+d_h)\) vs \(2hd_h\)），理论上支持在固定内存下处理更长上下文。
- **RoPE 集成**：TPA 天然支持 RoPE，无需像 MLA 那样增加额外的位置嵌入头。
- **统一视角**：MHA、MQA、GQA 可视为 TPA 的非上下文退化形式，增强了理论的统一性。
- **高效解码**：在特定 rank 设定下，TPA 推理时计算 \(QK^\top\) 的浮点数更低（如示例中 4096T vs 8192T），结合不显式构建 Q、K、V 的实现可进一步加速。

## 7. 优点

- **显著的缓存压缩**：在保持或提高模型质量的前提下，KV 缓存减少 10 倍以上，直接缓解长序列推理瓶颈。
- **即插即用**：与 RoPE 兼容，可作为 MHA 的直接替换，易于集成到 LLaMA 等现有架构中。
- **理论与实验并重**：通过定理证明了 RoPE 兼容性，并提供了全面的实验对比，包括消融和变体。
- **统一框架**：将多种主流注意力机制归入同一张量分解范式，便于理解和改进。
- **低秩拟合是上下文相关的**：不同于 LoRA 那样的静态权重分解，TPA 的分解依赖于输入内容，表达能力更强。

## 8. 不足与局限

- **长上下文实测缺失**：虽然分析显示缓存大幅缩小，但论文未报告在极长序列（例如 32k 以上）上实际的推理延迟、吞吐量或困惑度性能，无法直接验证端侧收益。
- **尺度局限性**：最大模型仅 1.5B 参数，与当今动辄 7B/13B/70B 的实用 LLM 存在很大差距，该方法在更大规模下的表现有待验证。
- **训练计算开销**：因子化引入了额外参数（\(R_Q+R_K+R_V\) 个线性投影），可能增加训练 FLOPs，尽管论文声称通过合并计算可以控制，但未给出详细的训练速度对比。
- **硬件适配**：提到的“不物化 Q、K、V”的推理计算依赖高效的 kernel 实现，文中并未提供实测的 wall‑time 加速结果，实际部署可能受限。
- **数据集单一**：仅使用 FineWeb‑Edu100B 进行预训练，模型的泛化能力、在其他领域数据（代码、数学、多语言）的表现未知。
- **无超参数敏感度分析**：除了 rank 和学习率，未探究 \(d_h\)、头数比例、分解阶数等对性能和缓存压缩的敏感性。
- **上下文因子选择**：因子分解中头维度和特征维度的角色设定可能带来归纳偏置，对某些任务可能存在负面影响，但论文未深入讨论。

（完）
