---
title: Prompt-based Depth Pruning of Large Language Models
title_zh: 基于提示的大语言模型深度剪枝
authors: "Juyun Wee, Minjae Park, Jaeho Lee"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=hRxHF1xPYB"
tags: ["query:edge-llm"]
score: 9.0
evidence: 基于提示的动态深度剪枝，通过省略不重要Transformer块降低LLM推理成本
tldr: 针对LLM推理成本高的问题，观察到Transformer块的重要性高度任务依赖，提出PuDDing算法，通过训练轻量路由器根据输入提示动态选择省略的块集合，无需硬件特定修改即可降低推理开销。实验表明该方法在保持精度的同时有效减少了计算量。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-hrxhf1xpyb/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hrxhf1xpyb/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 840, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hrxhf1xpyb/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1677, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hrxhf1xpyb/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1759, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hrxhf1xpyb/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1771, \"height\": 822, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1718, \"height\": 905, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 869, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1614, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 871, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 593, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 868, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 703, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1264, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 726, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 939, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1264, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1704, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hrxhf1xpyb/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1252, \"height\": 263, \"label\": \"Table\"}]"
motivation: 不同任务对Transformer块的依赖程度不同，静态深度剪枝无法适应任务变化。
method: 训练轻量路由器根据输入提示预测最佳省略块集合，实现动态深度剪枝。
result: 在多种任务上实现推理加速，同时保持模型精度。
conclusion: PuDDing提供了一种简单有效的动态深度剪枝方案，使LLM推理更高效。
---

## Abstract
Depth pruning aims to reduce the inference cost of a large language model without any hardware-specific complications, by simply removing several less important transformer blocks. However, our empirical findings suggest that the importance of a transformer block may be highly task-dependent---a block that is crucial for a task can be removed without degrading the accuracy on another task. Based on this observation, we develop a dynamic depth pruning algorithm, coined PuDDing (**P**rompt-ro**u**ted **D**ynamic **D**epth Prun**ing**), which determines which blocks to omit from the model based on the input prompt. PuDDing operates by training a lightweight router to predict the best omission set among a set of options, where this option set has also been constructed in a data-driven manner. Empirical results on commonsense reasoning benchmarks demonstrate that PuDDing effectively accelerates the inference language models, and achieves better on-task performance than static depth pruning baselines.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **核心问题**：大语言模型（LLM）推理成本高，深度剪枝通过直接移除不重要的 Transformer 块来降低开销，但在资源受限设备上，静态剪枝（对所有输入固定省略同一组块）无法适应不同任务对底层模块的差异化需求。
- **研究动机**：实证观察发现，Transformer 块的重要性高度任务依赖——在某任务上剪掉至关重要的块，在另一任务上可能无损准确率。这引出动态深度剪枝的需求：根据用户提示自适应地决定移除哪些块，既减少内存访问与计算，又保持任务性能。
- **整体含义**：提出 **PuDDing**（Prompt‑routed Dynamic Depth Pruning），用轻量路由器动态选择省略块集合，使 LLM 在内存受限设备上实现高效推理，无需硬件定制支持。

### 2. 方法论核心思想与关键技术

#### 2.1 核心思想

- 将深度剪枝形式化为根据提示 \(x\) 选择省略集 \(b(x)\) 的问题，要求被剪枝模型始终不超过规定的块数 \(d-k\)（满足峰值内存约束）。
- 采用“候选集生成 + 路由器训练”的两阶段策略：先构造少量多样且高性能的候选省略集，再训练一个分类器/回归器根据提示预测最佳省略集。

#### 2.2 候选省略集生成

- **数据集构建**：从多个下游任务的训练集中采集样本，构成 \(t\) 个校准数据集。
- **损失函数**：提出 **task likelihood (tl)** 和 **task likelihood difference (tld)** 两种指标。  
  - tl：仅计算答案部分的对数似然，避免流畅度主导。  
  - tld：在有限答案选择的任务中，使用正确与错误答案的似然差值。
- **省略集搜索**：对每个校准数据集按两种损失分别进行贪婪搜索，共得到 \(m = t \times l\) 个候选省略集 \(B = \{b_1, \dots, b_m\}\)。
- 设计目标：覆盖广泛任务（coverage）且候选数不太多（cardinality）。

#### 2.3 路由器训练与推理

- **训练数据构造**：对每个样本 \((x_i, y_i)\)，计算其在所有候选省略集上的 tl 损失，形成软标签向量 \(s_i\)。
- **路由器**：在预训练 BERT‑base 上接一个线性层，用 MSE 损失逼近 \(s_i\)（即预测每个候选集的损失）。  
  - 损失函数：\(\text{MSE}(s, \hat{s}) = \|s - \hat{s}\|_2^2\)。
- **推理**：对输入提示，路由器输出预测损失向量，选择最小损失对应的省略集，从存储加载所需参数（不包括被省略块），执行前向传播。
- 一句话区别：路由器仅按提示（prompt‑level）路由一次，而非逐 token 路由，适应内存受限设备。

#### 2.4 主要公式

- 深度剪枝优化目标：\(\min_{\hat{b}(\cdot)} \mathbb{E}[\ell((x,y); W_{\setminus \hat{b}(x)})]\)，同时 \(\Pr(|\hat{b}(x)| \ge k) = 1\)。
- 任务似然损失：\(tl(z;W) = -\frac{1}{T-S}\sum_{i=S+1}^T \log p_i(z_i|z_{<i}; W)\)。（略去指数化，经验更佳）
- 路由器训练：最小化 \(\text{MSE}(s, \hat{s})\)。

### 3. 实验设计

#### 3.1 模型与基准

- **主模型**：LLaMA‑3.1‑8B；额外测试 Vicuna‑1.5‑7B、OPT‑6.7B，均为 32 层。
- **基线方法**：
  - 静态深度剪枝：SLEB（迭代困惑度选择）、Shortened LLaMA（单步困惑度选择）。
  - 宽度剪枝：FLAP、SliceGPT。
  - 动态 naïve 基线：SLEB per prompt（用当前提示作为校准数据做静态剪枝，效果差且耗时）。
- 所有方法统一使用 FP16 精度，对比在相同块剪枝率（21.88%、15.62%、9.38%）下的表现。

#### 3.2 任务与数据集

- **零样本常识推理**（6 个）：ARC‑C、ARC‑E、BoolQ、HellaSwag、PIQA、WinoGrande。
  - 其中 BoolQ 未参与候选集生成，用于测试分布外泛化。
- **更复杂任务**（5 个）：OpenBookQA、MathQA、MMLU、PubMedQA、SciQ。
- **校准/训练数据**：候选集生成时从 ARC‑C、ARC‑E、HellaSwag、PIQA、WinoGrande 训练集各抽取 128 条；路由器训练使用全部训练集。

#### 3.3 评估维度

- 准确率对比表（不同剪枝率、不同模型）。
- LoRA 微调后的对比（使用 Alpaca 数据集，每候选集训练一份 LoRA）。
- 推理速度：壁钟时间（pre‑fill、生成、total），在 A100、RTX 6000 Ada、Apple M3 Pro 上测试。
- 参数加载时间估计（PCIe、NVLink）。
- 可视化：不同任务下各块的省略频率热力图。
- 消融实验（附录 B）：候选集数量、tl vs. 困惑度、MSE vs. CE、多域校准集、结合 AWQ 量化。

### 4. 资源与算力

- **使用硬件**：主要在 NVIDIA RTX 6000 Ada 上训练与评估；部分评估用 NVIDIA A100 云实例。
- **训练细节**：路由器训练使用 AdamW，学习率 \(10^{-5}\)，权重衰减 0.01，批次大小 32，训练 10 epoch，warm‑up 500 步。没有报告训练时长或 GPU 数量。
- **参数加载分析**：给出加载 8B 模型到 A100 的带宽估计（PCIe Gen4 x4 约 250 ms），但未给出具体实验占用的 GPU 时。

### 5. 实验数量与充分性

- **实验组数较多**：覆盖 3 个模型、3 种剪枝率、11 个任务、静态/动态/宽度剪枝对比、LoRA 微调、推理速度测试、多种消融。从不同维度验证了方法的有效性和适用性。
- **公平性**：所有方法使用相同模型与任务，基线严格按原论文设定（校准数据、超参数等），PuDDing 的测试任务包含未见的 BoolQ 和更复杂任务。
- **充分性**：消融实验剖析了候选集数量、tl 损失的优势、MSE 优于 CE 等关键设计选择，并结合量化展示了与其它压缩技术的兼容性，论证充分。

### 6. 主要结论

- PuDDing 在零样本常识推理任务上显著优于静态深度剪枝基线，在 20% 稀疏度下平均准确率提升 4.7%p，在更低稀疏度下仍有增益。
- 动态路由能有效利用任务间的块重要性差异：某些块在所有任务中普遍不重要（如第 20、26、27 块），另一些块（如第 4 块）则高度任务依赖。
- 路由器仅带来 4‑8 ms 额外开销（占总 pre‑fill 的 2‑4%），整体推理加速约 1.2‑1.28 倍，适合边缘设备。
- LoRA 微调后 PuDDing 仍保持优势，且与 AWQ 等量化方法可组合，进一步压缩。

### 7. 优点

- **首次提出基于提示的动态深度剪枝**，填补任务自适应与内存受限推理的空白。
- **方法简洁高效**：仅需训练轻量路由器（单次 per prompt），无需逐 token 路由，避免多次加载参数；保持原始 Transformer 块形状，硬件兼容性好。
- **损失函数设计合理**：提出 tl/tld 损失，专门针对任务答案而非常规困惑度，更能捕捉任务相关模块的重要性。
- **实验设计全面**：多模型、多稀疏度、多任务，包含分布外和复杂任务测试，与宽度剪枝、微调、量化等基线对比，并提供速度及可视化分析。
- **可扩展性**：结合 LoRA 或量化后仍能保持优势，易于集成到现有压缩流程中。

### 8. 不足与局限

- **依赖有监督任务数据**：候选集生成和路由器训练需要标注（提示‑答案对），难以直接迁移到开放式生成场景。虽有初步的多域实验，但未利用海量无标注文本（如 C4）来构建更通用的省略集。
- **固定剪枝比率**：所有提示均移除相同数量的块，未考虑任务难度自适应（简单任务少用层，难任务多用层），可能损失灵活性。
- **路由器存储与计算开销**：BERT‑base 路由器约有 110M 参数，虽只执行一次，但对极低功耗设备可能仍偏重。
- **泛化边界**：未见任务（如 BoolQ）上表现优于静态基线但仍有差距，更多样化域（如数学、生物）上虽有所提升，但提升幅度有限。
- **未充分报告训练成本**：缺少路由器训练的实际耗时估算，影响资源规划。
- **多 LoRA 副本存储量增加**：虽称仅约 2.5% 增长，但每增加一个候选集都需要额外适配器参数。

（完）
