---
title: Efficient Logit-based Knowledge Distillation of Deep Spiking Neural Networks for Full-Range Timestep Deployment
title_zh: 面向全范围时间步部署的深度脉冲神经网络高效逻辑蒸馏
authors: "Chengting Yu, Xiaochen Zhao, Lei Liu, Shu Yang, Gaoang Wang, Erping Li, Aili Wang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=ZvkyeUrpsA"
tags: ["query:edge-llm"]
score: 7.0
evidence: 基于logit的知识蒸馏，将教师脉冲神经网络知识迁移到学生网络，实现灵活时间步部署
tldr: 针对脉冲神经网络固定推理时间步限制灵活性的问题，提出基于logit的知识蒸馏框架，利用教师网络的知识训练学生网络，使其能在全范围时间步内推理而无需重训练。该方法提升了SNN的部署适应性和性能。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-zvkyeurpsa/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zvkyeurpsa/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1725, \"height\": 1018, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zvkyeurpsa/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 279, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zvkyeurpsa/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 851, \"height\": 1019, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1433, \"height\": 1814, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 771, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 769, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 770, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 771, \"height\": 145, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 765, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 856, \"height\": 349, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1121, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 871, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1125, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 499, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 679, \"height\": 134, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 844, \"height\": 127, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-zvkyeurpsa/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1061, \"height\": 465, \"label\": \"Table\"}]"
motivation: SNN固定推理时间步要求重训练，限制了操作灵活性。
method: 设计logit蒸馏框架，利用时空特性优化学生网络跨时间步的性能。
result: 学生网络在全范围时间步上获得提升，无需针对特定步数重新训练。
conclusion: 所提蒸馏方法增强了SNN的部署灵活性和效能。
---

## Abstract
Spiking Neural Networks (SNNs) are emerging as a brain-inspired alternative to traditional Artificial Neural Networks (ANNs), prized for their potential energy efficiency on neuromorphic hardware. Despite this, SNNs often suffer from accuracy degradation compared to ANNs and face deployment challenges due to fixed inference timesteps, which require retraining for adjustments, limiting operational flexibility. To address these issues, our work considers the spatio-temporal property inherent in SNNs, and proposes a novel distillation framework for deep SNNs that optimizes performance across full-range timesteps without specific retraining, enhancing both efficacy and deployment adaptability. We provide both theoretical analysis and empirical validations to illustrate that training guarantees the convergence of all implicit models across full-range timesteps. Experimental results on CIFAR-10, CIFAR-100, CIFAR10-DVS, and ImageNet demonstrate state-of-the-art performance among distillation-based SNNs training methods. Our code is available at https://github.com/Intelli-Chip-Lab/snn_temporal_decoupling_distillation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：脉冲神经网络（SNNs）虽具有低功耗、事件驱动的优势，但面临两大挑战：
  - **精度退化**：与传统人工神经网络（ANNs）相比，SNNs 的分类准确率仍有差距。
  - **部署僵化**：现有的 SNN 模型通常只在固定的推理时间步（timesteps）下训练，若需调整推理步数（如在能耗与精度间权衡），必须重新训练整个模型，严重限制了实际应用的灵活性。
- **研究动机**：现有的知识蒸馏（KD）方法多照搬 ANN 的端到端模式，忽略了 SNN 独特的**时空特性**。论文旨在利用这一特性，提出一种新的蒸馏框架，使得单次训练出的 SNN 模型能在**全范围时间步（Full-Range Timesteps）** 上均有优异表现，无需因步数调整而重训，从而提升部署的自适应能力。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：**时域解耦蒸馏**。
  - 将 SNN 随时间的累积投票输出视为一个**时域集成模型**。
  - 将原本只施加于最终集成输出的蒸馏损失，**解耦并独立作用于每一个时间步的输出**，确保每个时间步的子模型都能得到有效训练。
  - 引入最终集成输出作为额外的**自蒸馏软标签**，进一步正则化并指导各时间步子模型的收敛。
- **关键技术细节与损失函数**：
  - **时序交叉熵损失**（\(L_{\text{TWCE}}=\frac{1}{T}\sum_t L_{\text{CE}}(S(z_S(t)), y)\)）：将真实标签的监督信号独立作用于每个时间步。
  - **时序KL散度损失**（\(L_{\text{TWKL}}=\frac{1}{T}\sum_t L_{\text{KL}}(S(z_S(t)/\tau), S(z_A/\tau))\)）：将预训练 ANN 教师的软标签蒸馏到每个时间步。
  - **时序自蒸馏损失**（\(L_{\text{TWSD}}=\frac{1}{T}\sum_t L_{\text{KL}}(S(z_S(t)/\tau), S(z_S^{\text{ens}}/\tau))\)）：利用最终投票输出作为软标签，对各时间步进行自蒸馏。
  - **最终目标函数**：\(L_{\text{final}} = L_{\text{TWCE}} + \alpha L_{\text{TWKL}} + \beta L_{\text{TWSD}}\)。
- **理论保证**：论文证明了时序解耦损失是其对应标准损失的上界，优化该上界能够保证模型在训练步数 \(T\) 下的收敛，并能隐含地保证任意小于 \(T\) 的推理步数 \(T_k\) 下子模型的收敛。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集**：
  - 静态图像：**CIFAR-10、CIFAR-100**。
  - 大规模图像：**ImageNet**。
  - 神经形态动态视觉数据集：**CIFAR10-DVS**。
- **Benchmark 与方法对比**：
  - 对比了多种**直接训练方法**：STBP-tdBN, Dspike, TET, RecDis, DSR, SLTT, OS, RateBP 等。
  - 对比了多种**基于知识蒸馏的训练方法**：KDSNN, Joint A-SNN, SM, SAKD, BKDSNN, TSSD, TKS, EnOF, SuperSNN 等。
  - 在 CIFAR-10/100 上使用 ResNet-18/19 架构，在 ImageNet 上使用 ResNet-34，在 CIFAR10-DVS 上使用 ResNet-18。

### 4. 资源与算力
- **软件平台**：PyTorch 和 SpikingJelly。
- **硬件配置**：
  - **CIFAR-10/100、CIFAR10-DVS**：使用**单张 NVIDIA GeForce RTX 3090 GPU**。
  - **ImageNet**：使用**8 张 NVIDIA GeForce RTX 3090 GPU** 进行分布式数据并行训练。
- **训练时长**：文中未明确提及具体的总训练时长。

### 5. 实验数量与充分性
- **实验数量充足且全面**，包括：
  - **主流基准测试**：在 4 个不同规模和类型的数据集上进行了性能对比。
  - **消融实验**：
    - 超参数 \(\alpha\) 和 \(\beta\) 的影响分析。
    - 训练目标组合（\(L_{\text{TWCE}}\)、\(L_{\text{TWKL}}\)、\(L_{\text{TWSD}}\)）的增益对比。
    - 时域解耦对交叉熵和KL散度损失各自有效性的对比研究。
  - **深度分析实验**：
    - **损失收敛可视化**：展示了各时间步子模型损失的一致性收敛。
    - **特征聚类可视化**（t-SNE）：证明了时域解耦能学到更好、更一致的特征。
    - **全范围时间步性能分析**：验证了使用最大时间步训练的模型，在提取其内部任意更少时间步子模型时，性能最优。
  - **实际应用模拟**：结合 SEENN 框架验证了其在动态调整推理开销场景下的优势。
- **公平性**：对比方法均引用自近期顶会文章的标准结果；在“全范围性能”对比中，明确说明并未使用从大时间步模型提取小子模型的方式来获得不公平优势。

### 6. 论文的主要结论与发现
- 提出的**时域解耦蒸馏框架**能有效利用 SNN 的时空特性，显著提升模型性能，在多个基准数据集上取得了**基于蒸馏的 SNN 训练方法中最高的准确率（State-of-the-Art, SOTA）**。
- 该方法确保了模型内部所有**隐式子模型（Full-Range Timesteps）的收敛**，允许使用一个模型灵活覆盖从 \(1\) 到 \(T\) 的所有推理时间步，而无需针对特定步数重训练。
- 引入的**自蒸馏项（\(L_{\text{TWSD}}\)）** 能够作为有效的正则化，进一步拉近优化目标与原始损失间的差距，提升模型泛化能力。
- 该框架在**不引入额外前向计算分支**的情况下，实现了高效的训练。

### 7. 优点：方法或实验设计上有哪些亮点
- **问题定位精准且实用**：切中 SNN 部署中无法灵活调整时间步的实际痛点，提出的单模型覆盖全范围步数的方案极具工业应用价值。
- **方法优雅、高效**：
  - 将集成学习视角与 SNN 的时空特性自然结合，理论清晰（上界保证），实现简洁（仅调整损失函数位置）。
  - 提出的自蒸馏机制巧妙利用了模型自身的高质量输出，无需额外计算或存储开销。
- **实验论证充分扎实**：
  - 不仅有性能对比，还从损失收敛、特征可视化和全范围步数性能等多个维度深入分析了方法的有效性及原理，支撑了理论结论。
  - 结合 SEENN 框架的附加实验，进一步明确了该方法在实际动态推理场景下的现实意义。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **架构验证范围**：实验主要基于 ResNet 系列网络（ResNet-18/19/34），对近年来流行的 Transformer-based 或更为轻量级的 SNN 架构验证有限（附录中提及了 Spikingformer，但非主实验）。
- **教师模型规格**：主要使用同架构或相似架构、较大尺寸的 ANN 作为教师。对于和更大规模、异构（如ViT）的 ANN 教师进行蒸馏的极限性能探讨较少。
- **训练开销的细致对比**：虽然框架本身无额外分支，但 BPTT 训练的内存和时间开销本身就很高。论文仅提供了时间和显存的相对增量（可以忽略不计），未与 SOTA 的直接训练或蒸馏方法在达到相同精度的总训练开销上进行宏观对比。
- **极端低延迟场景**：在极低时间步（如 \(T=1\) 或 \(T=2\)）下，性能虽然已大幅优于标准方法，但与高精度 ANN 的差距依然存在，未探讨在此极限场景下的专项优化。
- **超参数敏感性**：最优的 \(\alpha\) 和 \(\beta\) 设定可能需要针对不同数据集进行微调，缺乏自适应的动态调整策略分析。

（完）
