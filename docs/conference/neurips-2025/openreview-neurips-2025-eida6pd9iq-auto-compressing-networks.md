---
title: Auto-Compressing Networks
title_zh: 自压缩网络
authors: "Vaggelis Dorovatas, Georgios Paraskevopoulos, Alexandros Potamianos"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=eIDa6pd9iQ"
tags: ["query:edge-llm"]
score: 4.0
evidence: 提出自压缩网络，通过结构设计在训练中自动减少冗余，与模型压缩相关。
tldr: 深度神经网络随层数增加计算冗余加剧，性能提升却有限。本文提出自压缩网络（ACN），通过将每层与输出直接相连的长前馈连接替代短残差连接，使得梯度下降训练时信息动态“挤压”到浅层，增强浅层表征能力，从而实现网络自压缩。实验表明，这种架构可减少网络深度与计算开销，同时保持甚至提高模型精度，为模型压缩和加速提供了新的结构设计思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-eida6pd9iq/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1430, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-eida6pd9iq/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1433, \"height\": 497, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-eida6pd9iq/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 449, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-eida6pd9iq/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 528, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-eida6pd9iq/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 603, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-eida6pd9iq/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 487, \"height\": 399, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-eida6pd9iq/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 873, \"height\": 710, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-eida6pd9iq/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1422, \"height\": 859, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-eida6pd9iq/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1458, \"height\": 187, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-eida6pd9iq/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1436, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-eida6pd9iq/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 443, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-eida6pd9iq/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1167, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-eida6pd9iq/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1260, \"height\": 476, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-eida6pd9iq/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 906, \"height\": 341, \"label\": \"Table\"}]"
motivation: 深网络增加深度带来计算冗余，性能提升有限，亟需更高效的网络结构。
method: 设计自压缩网络架构，用长前馈连接替代短残差连接，利用训练动态自动压缩信息。
result: 实验显示自压缩网络在多个任务上以更浅结构达到甚至超越传统深网络性能。
conclusion: 自压缩网络提供了一种结构驱动的模型压缩范式，有助于开发更高效的网络模型。
---

## Abstract
Deep neural networks with short residual connections have demonstrated remarkable success across domains, but increasing depth often introduces computational redundancy without corresponding improvements in representation quality. We introduce Auto-Compressing Networks (ACNs), an architectural variant where additive long feedforward connections from each layer to the output replace traditional short residual connections. By analyzing the distinct dynamics induced by this modification, we reveal a unique property we coin as *auto-compression*—the ability of a network to organically compress information during training with gradient descent, through architectural design alone. Through auto-compression, information is dynamically "pushed" into early layers during training, enhancing their representational quality and revealing potential redundancy in deeper ones. We theoretically show that this property emerges from layer-wise training patterns found only in ACNs, where layers are dynamically utilized during training based on task requirements. We also find that ACNs exhibit enhanced noise robustness compared to residual networks, superior performance in low-data settings, improved transfer learning capabilities, and  mitigate catastrophic forgetting suggesting that they learn representations that generalize better despite using fewer parameters. Our results demonstrate up to 18\% reduction in catastrophic forgetting and 30-80\% architectural compression while maintaining accuracy across vision transformers, MLP-mixers, and BERT architectures. These findings establish ACNs as a practical approach to developing efficient neural architectures that automatically adapt their computational footprint to task complexity, while learning robust representations suitable for noisy real-world tasks and continual learning scenarios.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：深度神经网络通过堆叠大量带有短残差连接（short residual connections）的层获得强大性能，但深度增加常常引入计算冗余，而表征质量并未相应提升。现有的残差网络虽然训练稳定，但存在部分层被绕过或欠训练、参数冗余、泛化受限等问题。
- **研究动机**：探索一种新的网络架构，既能保持残差网络多信号通路和梯度流畅的优点，又能自动识别并压缩冗余层，从而提升参数利用效率与泛化能力。
- **整体含义**：提出 **自压缩网络（Auto-Compressing Networks, ACNs）**，通过结构设计（而非外部正则化或辅助损失）使网络在训练过程中自然地将信息“推”向浅层，深层自动变为冗余，实现压缩。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：用从每一层直接连接到最终输出的 **加性长前馈连接（additive long feedforward connections）** 替代传统的短残差连接。这种单一的“层到输出”的直连通路，使网络表现出 **自压缩（auto-compression）** 特性。
- **关键技术细节**：
  - 对于深度为 `L` 的网络，定义层输出 `x_i = f_i(x_{i-1})`，最终输出 `y = \sum_{i=0}^{L} x_i`。每一层的输出直接接受最终目标的优化。
  - 与 ResNet 和 DenseNet 的区别：ResNet 是隐式的“层间加法 + 身份映射”，DenseNet 是“每层连接到所有后续层”的拼接；ACN 则是“每层只连接到最终输出”，路径数量为 `L`，远少于 ResNet 的 `2^L` 条。
  - **梯度传播分析**（1D线性情形）：
    - ACN 的梯度分解为 **直接梯度（DG，Direct Gradient）** 和 **网络介导梯度（NG，Network-mediated Gradient）** 两部分。DG 提供从输出直接到每一层的“信息高速公路”，使浅层获得更强的训练信号。
    - 在训练早期，由于权重通常初始化为接近零，DG 在 ACN 中的相对贡献远高于 ResNet（因为 ResNet 有指数级的梯度路径，削弱了 DG 的作用）。
    - ACN 的前向项与传统前馈网络相同（单路径），后向项更接近 ResNet（多路径），形成 **隐式的逐层训练动态**：浅层先被充分训练，信息自然集中在浅层，深层逐渐变为恒等映射（冗余）。
- **公式描述**：
  - ACN 前向：`y = x_0 + \sum_{i=1}^{L} \left(\prod_{j=1}^{i} w_j \right) x_0`
  - ACN 梯度（对权重 `w_i`）：`∂y/∂w_i = (1 + \sum_{j=i+1}^{L} \prod_{k=i+1}^{j} w_k) · (\prod_{m=1}^{i-1} w_m) · x_0`，其中括号内的第一项 `1` 即为 DG。

### 3. 实验设计：数据集与对比方法
- **数据集/场景**：
  - 图像分类：CIFAR-10、CIFAR-100、ImageNet-1K（ILSVRC-2012）。
  - 自然语言处理：GLUE 基准中的 SST-2、QQP、QNLI 任务，使用 BERT 架构，在 BooksCorpus 与 Wikipedia 上预训练后微调。
  - 连续学习（Continual Learning）：Split CIFAR-100 基准（20个顺序的5类分类任务）。
- **对比基准与方法**：
  - 主要对比 **ACN 变体 vs. 残差网络（ResNet）变体**，涉及 ViT、MLP-Mixer、BERT。
  - 还与其它残差变体比较：DenseNet-Mixer、DenseFormer-Mixer。
  - 在迁移学习实验中比较了 Aligned、LayerSkip 等基于正则化的层压缩方法。
  - 连续学习中使用 Naive Fine-tuning 和 Synaptic Intelligence (SI) 方法。
  - 后训练剪枝实验中结合了 Magnitude Pruning 和 Movement Pruning。

### 4. 资源与算力
- 论文中 **未显式提供 GPU 型号、数量及具体训练小时数**。
- 部分细节提及：ViT 实验使用 batch size 256（受显存限制）；AC-ViT 训练 700 epoch 收敛，Residual ViT 约 300 epoch；CIFAR 上的 Mixer 实验训练 300-420 epoch；BERT 预训练 AC 版本需要 2 epoch vs. 残差版 1 epoch 达到相同损失。这些信息暗示训练时间较残差网络更长，但未提供具体计算资源开销。

### 5. 实验数量与充分性
- **实验规模**：论文涵盖了 **图像分类、语言理解、连续学习、迁移学习、剪枝加速、早退（Early Exit）协同** 六大类实验，每种实验均使用多个网络架构（ViT, Mixer, BERT）和不同深度。
- **消融与分析**：
  - 梯度热力图（ACN vs. ResNet 梯度分布）
  - DG/FG 比率随训练进程的变化
  - 仅使用 DG 的 ACN 变体验证 DG 的关键性
  - 考察不同任务难度（类别数 2,5,10）下有效深度的变化
- **公平性**：尽量保持训练配置一致（epoch 数量在必要时延长以保证收敛），并与近期正则化方法进行公平对比（如 Aligned, LayerSkip）。但部分实验（如 CIFAR-10 上的 Mixer）中 ACN 训练 epoch 数多于基线，作者通过延长所有模型训练时间的额外实验排除了过拟合疑虑。
- **整体充分性**：实验维度丰富，覆盖多个模态与任务，对核心主张的验证较为系统。不过，大规模模型级别的比较依然缺乏。

### 6. 论文的主要结论与发现
- ACN 具有 **自压缩** 特性：训练过程中自然降低深层重要性，使网络在较少层数下达到与完整深度相当的性能（例如 ViT 仅需 6/12 层，BERT 仅需约 1/4 层数）。
- 梯度分析证实 **较高的 DG/FG 比例** 是自压缩的关键驱动力。
- ACN 学习到的表征 **更鲁棒、泛化性更强**：在图像加噪、低数据量、迁移学习和连续学习中均表现出显著优势（噪声下准确率更高，小样本下收敛更快，灾难性遗忘降低最高 18%）。
- 结构压缩与性能保持：在 ViT、Mixer、BERT 等多种架构上，在保持或略微提升准确率的同时，实现 30–80% 的层数压缩，且无需额外超参数调优。
- ACN 可与早期退出方法、剪枝等技术天然协同，进一步提升推理加速比（如配合早退头达 3.3× 加速）。

### 7. 优点
- **方法简洁且硬件友好**：仅改变连接方式，无需复杂的辅助损失或路由模块，易于实现，不依赖专门软件。
- **极强的可解释性**：通过梯度流和逐层性能贡献图清晰揭示了自压缩的机制。
- **多任务和多架构验证**：在视觉和语言两大领域，覆盖 MLP、Transformer 等典型骨干，证明了方法的普适性。
- **附带泛化与鲁棒性收益**：自动信息集中不仅带来压缩，还提升了噪声鲁棒性、迁移能力和连续学习能力。
- **与现有技术的正交性**：可与剪枝、早期退出等结合，大幅提升整体效率。

### 8. 不足与局限
- **训练时间较长**：ACN 通常需要比残差网络更多的训练 epoch 才能收敛（如 ViT 700 vs 300 epoch），且未给出具体优化策略来缓解此问题。
- **大规模模型验证缺失**：评测限于中等规模的数据集和模型（如 CIFAR, ImageNet-1K, BERT-base），未在数十亿参数级别的大模型上检验。
- **任务范围局限**：主要聚焦于分类和掩码语言建模，缺少生成、自监督预训练等更广泛场景的评估。
- **训练不均衡风险**：逐层训练动态可能导致深层“过早停滞”，需要进一步初始化或调度策略的研究。
- **比较公平性**：部分实验训练周期不一致，尽管补充了控制实验，但读者仍需谨慎解读效率对比。

（完）
