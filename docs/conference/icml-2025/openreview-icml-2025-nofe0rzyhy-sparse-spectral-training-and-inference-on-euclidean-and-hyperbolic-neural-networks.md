---
title: Sparse Spectral Training and Inference on Euclidean and Hyperbolic Neural Networks
title_zh: 稀疏谱训练与欧几里得及双曲神经网络推理
authors: "Jialin Zhao, Yingtao Zhang, Xinghang Li, Huaping Liu, Carlo Vittorio Cannistraci"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Nofe0rzyhY"
tags: ["query:edge-llm"]
score: 4.0
evidence: 通过稀疏谱更新实现内存高效训练，可能减少推理内存
tldr: 针对神经网络参数增长导致GPU内存需求增加的问题，提出稀疏谱训练方法(SST)，通过更新全部奇异值并依据幅度采样选择性地更新奇异向量，降低预训练内存占用，可推广至双曲神经网络。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1788, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1687, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 871, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 809, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1224, \"height\": 722, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1353, \"height\": 1345, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1380, \"height\": 1377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nofe0rzyhy/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1580, \"height\": 2045, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1452, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1771, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1748, \"height\": 814, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1768, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1347, \"height\": 143, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1437, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1023, \"height\": 751, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 986, \"height\": 622, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1192, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 952, \"height\": 536, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 745, \"height\": 529, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1018, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 954, \"height\": 818, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1238, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1246, \"height\": 144, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1277, \"height\": 144, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1079, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1063, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1003, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1178, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1017, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1135, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1220, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nofe0rzyhy/table-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 902, \"height\": 317, \"label\": \"Table\"}]"
motivation: 现有低秩适应方法如LoRA局限于低秩结构，ReLoRA易陷入鞍点，需要更通用的内存高效训练方法。
method: 采用稀疏谱训练，更新所有奇异值，通过基于奇异值幅度的多项采样选择性更新奇异向量。
result: 在预训练任务上相比LoRA等方法进一步降低内存消耗，同时保持性能。
conclusion: SST为大规模神经网络的内存高效训练提供了一种新范式。
---

## Abstract
The growing demands on GPU memory posed by the increasing number of neural network parameters call for training approaches that are more memory-efficient. Previous memory reduction training techniques, such as Low-Rank Adaptation (LoRA) and ReLoRA, face challenges, with LoRA being constrained by its low-rank structure, particularly during intensive tasks like pre-training, and ReLoRA suffering from saddle point issues. In this paper, we propose **S**parse **S**pectral **T**raining **(SST)** to optimize memory usage for **pre-training**. SST **updates all singular values** and **selectively updates singular vectors** through a multinomial sampling method weighted by the magnitude of the singular values. Furthermore, SST employs **singular value decomposition to initialize and periodically reinitialize** low-rank parameters, reducing distortion relative to full-rank training compared to other low-rank methods. Through comprehensive testing on both Euclidean and hyperbolic neural networks across various tasks, SST demonstrates its ability to outperform existing memory reduction training methods and is comparable to full-rank training in various cases. On LLaMA-1.3B, with only 18.7\% of the parameters trainable compared to full-rank training (using a rank equivalent to 6\% of the embedding dimension), SST reduces the perplexity gap between other low-rank methods and full-rank training by **97.4\%**. This result highlights SST as an effective parameter-efficient technique for model pre-training.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型参数量激增，全参数训练需要巨大的 GPU 内存，严重制约了从头预训练的可行性。
- **现有方法局限**：
  - **LoRA**（低秩适应）：仅更新固定的低秩子空间，在复杂任务（如预训练）中表达能力受限，无法捕捉非主导奇异值对应的方向。
  - **ReLoRA/COLA/PLoRA**：通过周期性合并低秩矩阵来突破固定低秩的限制，但每次合并后梯度消失（鞍点问题），导致收敛慢且效果不如全秩训练。
  - **GaLore**：对梯度进行低秩投影，但在小秩情况下不稳定。
- **核心问题**：如何设计一种参数高效的预训练方法，既能大幅减少内存，又能紧密逼近全秩训练的学习动态与最终性能。
- **整体含义**：本文提出 Sparse Spectral Training（SST），直接在权重矩阵的谱分解域（奇异值及奇异向量）上进行稀疏更新，平衡“利用”（持续更新所有奇异值并周期性回访主导方向）与“探索”（基于幅度采样的动态选择），最终在欧氏和双曲神经网络上均取得显著优于现有低秩方法的性能，并逼近全秩训练。

## 2. 方法论：Sparse Spectral Training (SST)

SST 将线性层的操作从 \( h = Wx \) 替换为 \( h = U\Sigma V^T x \)，其中 \( U\Sigma V^T = \text{SVD}(W) \)，权重矩阵原体被移除。训练过程中采用以下关键技术：

- **更新所有奇异值（Σ）**：  
  每步都对对角矩阵 Σ（视为长为 m 的向量）进行梯度更新，并用 `max(·, 0)` 保证非负，因此所有奇异值都持续调整。梯度公式为 \(\nabla\mathcal{L}_{\Sigma_i} = U_{\cdot i}^T \frac{\partial\mathcal{L}}{\partial W} V_{\cdot i}\)。

- **基于多项式采样的选择性奇异向量更新**：  
  每轮迭代（iteration）根据奇异值幅度定义多项式分布（含均匀混合，\(p(i) = \frac{1}{2}(\frac{1}{m} + \frac{\Sigma_i}{\sum_j \Sigma_j})\)），采样 r 个索引，仅对选中的列向量 \(U_{\cdot i}\) 和 \(V_{\cdot i}\) 进行梯度更新，更新后进行归一化以保持单位范数（幅度信息完全由 Σ 承载）。未选中的向量冻结。

- **增强梯度**：  
  为避免小奇异值对应的向量梯度被 Σ 的幅度削弱，使用解耦方向的增强梯度：
  \[
  \widetilde{\nabla}_{\mathcal{L}}U_{\cdot i} = \frac{\partial\mathcal{L}}{\partial W} V_{\cdot i}, \quad
  \widetilde{\nabla}_{\mathcal{L}}V_{\cdot i} = \left(\frac{\partial\mathcal{L}}{\partial W}\right)^T U_{\cdot i}
  \]

- **周期性重初始化（re-SVD）**：  
  每完成一轮（round，即遍历所有采样模式一次）后，对当前权重 \(U\Sigma V^T\) 重新执行 SVD，恢复正交性并更新 U、Σ、V。这避免了训练过程退化为低秩子空间，并确保 SST 的投影方向始终与当前权重的最新谱结构对齐。

- **内存高效实现**：  
  将 U 和 V 分为活跃段（存储优化器状态）和冻结段（无状态）。采样后通过交换操作将新选中的向量移到活跃段，未被选中的向量移入冻结段，实现了类似分时操作系统的资源分配，优化器状态仅维护 r 个向量。

- **与 LoRA/ReLoRA* 的对比**：  
  - LoRA：仅学习 ΔW 的 top-r 奇异值，忽略其余。
  - ReLoRA*：零初始化 A/B 且重置动量，每次合并后梯度为 0，出现鞍点。
  - SST：以 SVD 分解的原权重作为 U、V 的初始化和周期性重初始化，避免了零初始化引发的梯度消失；通过采样策略探索全部奇异向量，而非固定 top-r；全 Σ 更新保证所有奇异值参与优化。

## 3. 实验设计

实验覆盖了欧氏空间和双曲空间下的多种架构与任务，对比基准为全秩训练、LoRA、ReLoRA*（统一化的端到端参数高效预训练框架）。部分实验还对比 GaLore、DoRA、VeRA。

- **数据集与任务**：
  - 机器翻译：IWSLT’14 英德、IWSLT’17 德英、Multi30K 德英；使用 vanilla Transformer（欧氏）和 HyboNet（双曲 Transformer）。
  - 语言建模：在 OpenWebText 上预训练 OPT 系列（125M/350M/1.3B）和 LLaMA 系列（130M/1.3B），并额外在 C4 数据集上测试 LLaMA-130M。
  - 零样本下游评估：对 OPT 预训练模型在 16 个 NLP 任务上评估（ARC、BoolQ、HellaSwag、PIQA 等）。
  - 双曲图神经网络：节点分类和链接预测，数据集包括 Airport、Cora、Disease、PubMed；模型采用 HyboNet。
  - 图像分类：MLP 模型在 MNIST、EMNIST、Fashion MNIST 上补充实验。
  - 采样机制消融：在 IWSLT’14 上对比多项式、均匀、顺序、Top-R 采样。

- **评价指标**：
  - 机器翻译：BLEU 分数。
  - 语言建模：验证困惑度（PPL），以及零样本任务的准确率/F1。
  - 图任务：节点分类（F1）、链接预测（精度）。
  - 额外指标：效率比（Memory Reduction% / PPL Increase%）。

- **秩及参数效率对比**：所有低秩方法替换全部线性层，保持类似的可训参数数量（SST 略高于 LoRA，如 r=64 时 SST 约 18.7% 可训练参数），保证公平。

## 4. 资源与算力

- **GPU 与训练时长**：
  - 机器翻译实验（IWSLT’14、Multi30K 等）在单张 A100 上完成。
  - OPT 系列预训练采用 4 张 A100，利用 Accelerate 库分布式训练，训练 19.7B tokens（约 2 个 epoch 的 OpenWebText），总时长：OPT-125M 约 65 小时（SST），OPT-350M 约 170 小时，OPT-1.3B 约 387 小时。
  - LLaMA 系列在 4 张 A100 上预训练，LLaMA-130M 2.6B tokens，LLaMA-1.3B 13.1B tokens。
  - 双曲图神经网络和图像分类实验在单张 A100 上完成。
- **未完全说明的部分**：文中未列出所有实验的精确 GPU 显存峰值及每步训练时间，但提供了内存消耗表格（表 20-22），显示 SST 比全秩大幅减少内存（如 OPT-1.3B 从 ~20 GB 降至 ~9.3 GB），训练时间略高于 LoRA（主要由于 \(U\Sigma V^T\) 的计算和周期性 SVD，但 SVD 耗时占比仅 0.5%–0.8%）。

## 5. 实验数量与充分性

- **实验规模**：
  - 多个模型尺寸：OPT 三种规模，LLaMA 两种规模，Transformer 多种维度（64/128/256/512）和不同秩（r/4 至 r/128）。
  - 超过 5 类任务（翻译、语言建模、零样本推理、图节点分类/链接预测、图像分类），数据集 ≥ 10 个。
  - 比较方法至少包含全秩、LoRA、ReLoRA*，部分加入 GaLore、DoRA、VeRA。
  - 消融实验：Σ 更新方式（全量 vs 采样）、初始化方式（SVD vs 随机/零）、迭代间隔 T3、每轮迭代数、秩的影响、训练步数影响。
  - 额外分析：奇异值剪枝测试模型可压缩性、Singular Value 分布可视化、梯度范数相关性分析、效率比分析、内存吞吐与性能权衡图表。
- **充分性与公平性**：
  - 所有低秩方法在相同秩和最大可训参数限制下进行比较，超参数与全秩训练保持一致（或对低秩方法单独调节学习率并选择最佳），且均使用统一框架（全部线性层替换），避免了仅在部分层应用的低秩偏差。
  - 进行多随机种子（图任务 3 种子，翻译实验未明确但提及 checkpoint 选择策略），零样本评估涵盖多种任务，减少偶然性。
  - 在更大数据集 C4（比 OpenWebText 大约 25 倍）复现，并有不同学习率对比，证明鲁棒性。
  - 局限性：未在更大规模模型（>1.3B）上验证；未详细研究不同优化器、量化技术的联合影响。

## 6. 主要结论与发现

- SST 在预训练场景全面超越 LoRA、ReLoRA* 等低秩方法，并在许多配置下逼近甚至超过全秩训练（如双曲 Transformer 上 SST 常优于全秩；OPT-125M 零样本平均得分略超全秩）。
- 在 LLaMA-1.3B 上，SST 以 18.7% 可训参数，将与其他低秩方法的困惑度差距缩小 97.4%；在其他模型上缩小 50%–67%。
- 在机器翻译中，SST 平均降低 BLEU 差距 66.7%（欧氏）且双曲场景下稳定性远优于其他低秩方法。
- 在双曲图神经网络上，节点分类平均降低性能差距 73.7%，链接预测降低 82.5%，且在疾病数据集的链接预测上超越全秩。
- SST 的奇异值分布更接近全秩训练，且剪枝实验表明其权重信息更集中于少数奇异值，利于模型压缩。
- 多项式采样且混合均匀分布的策略优于纯 Top-R 采样，证实了平衡探索与利用的重要性。
- SVD 初始化和周期性重初始化是核心要素，若换为随机初始化则性能骤降至接近 LoRA/ReLoRA* 水平。

## 7. 优点

- **新颖的参数高效预训练范式**：直接在谱域操作，更新所有奇异值并结合采样选择奇异向量，未受限于固定低秩子空间。
- **理论支撑扎实**：利用 Eckart–Young–Mirsky 定理分析低秩方法的局限性，并通过梯度推导和优化器动量分析阐明重初始化意义。
- **泛化能力强**：统一适用于欧氏与双曲神经网络，覆盖多种任务（文本、图、图像），是首个将参数高效预训练引入双曲空间的工作。
- **高效且逼近全秩**：内存与 LoRA 相当，额外计算开销小（SVD 占比 <1%），但性能大幅领先其他低秩方法，多任务逼近甚至超越全秩。
- **良好的收敛特性**：梯度范数与全秩训练高度相关（相关系数 0.85），避免 ReLoRA* 的周期性鞍点。
- **内存-性能权衡优秀**：提出的效率比指标显示 SST 在同等内存缩减下带来的性能损失远小于 ReLoRA*（提升 65%–4434%）。
- **实用性设计**：提供了分块、交换的内存高效实现，支持现有优化器；推理时可合并回标准权重矩阵，无额外推理时延。

## 8. 不足与局限

- **模型规模验证有限**：预训练只做到 1.3B 参数，未在更大规模（如 7B、13B）上验证，其在大规模模型上的可扩展性和收益边界尚不明确。
- **训练步数依赖**：低秩配置（如 r=4）需要更多训练步数才能逼近全秩性能，实际时间收益可能被部分抵消（尽管文中显示即使步数减少 20%，SST 仍优于其他方法）。
- **优化器和超参数敏感性**：每次迭代重置动量需要 warmup，且对迭代间隔 T3、每轮迭代数等超参数有一定依赖性，虽实验显示一定鲁棒性，但未在所有配置下调优。
- **仅限于线性层替换**：当前仅替换全部线性层，未探索嵌入层或其它模块的参数高效化（论文指出作为未来方向）。
- **双曲实验的局限性**：双曲模型及图神经网络是在较小规模的数据集上测试，且对 dropout 等进行了调整，可能不够全面。
- **缺少与更多参数高效方法的深入比较**：虽然补了 DoRA、VeRA，但主实验仅以 LoRA、ReLoRA*、GaLore 为主，与其他新兴方法（如 PiSSA、AdaLoRA 等）的对比尚不充分（注：正文将 PiSSA 放在了示意图中，未作为基准）。
- **潜在实现复杂度**：相比于 LoRA，SST 涉及动态采样、分块交换、周期性 SVD 等操作，工程实现上更复杂。

（完）
