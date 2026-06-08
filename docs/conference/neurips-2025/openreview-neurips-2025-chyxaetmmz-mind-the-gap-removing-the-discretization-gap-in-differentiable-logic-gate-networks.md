---
title: "Mind the Gap: Removing the Discretization Gap in Differentiable Logic Gate Networks"
title_zh: 弥合差距：消除可微逻辑门网络中的离散化差距
authors: "Shakir Yousefi, Andreas Plesner, Till Aczel, Roger Wattenhofer"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=chYXaetMmz"
tags: ["query:edge-llm"]
score: 5.0
evidence: 学习大型逻辑门网络实现高效图像分类，但离散化差距阻碍实际部署
tldr: 针对可微逻辑门网络在训练和推理间的离散化差距，注入Gumbel噪声以消除该差距，从而提高网络效率并实现在资源受限设备上的图像分类部署。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 664, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1440, \"height\": 984, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1455, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1425, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 699, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1453, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1456, \"height\": 354, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1452, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1315, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1421, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1453, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1467, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-chyxaetmmz/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1467, \"height\": 635, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-chyxaetmmz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1434, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-chyxaetmmz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1261, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-chyxaetmmz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 957, \"height\": 822, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-chyxaetmmz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1427, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-chyxaetmmz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 635, \"height\": 325, \"label\": \"Table\"}]"
motivation: 可微逻辑门网络存在离散化差距，导致推理时性能下降，影响实际部署。
method: 通过注入Gumbel噪声和直通估计器缩小训练与推理间的离散化差异。
result: 减少了未使用神经元的比例，提升了推理阶段的准确性。
conclusion: 该方法提高了逻辑门网络在边缘设备上部署的可行性。
---

## Abstract
Modern neural networks exhibit state-of-the-art performance on many existing benchmarks, but their high computational requirements and energy usage cause researchers to explore more efficient solutions for real-world deployment.
    Differentiable logic gate networks (DLGNs) learns a large network of logic gates for efficient image classification. However, learning a network that can solve simple problems like CIFAR-10 or CIFAR-100 can take days to weeks to train. Even then, almost half of the neurons remains unused, causing a \emph{discretization gap}. This discretization gap hinders real-world deployment of DLGNs, as the performance drop between training and inference negatively impacts accuracy.
    We inject Gumbel noise with a straight-through estimator during training to significantly speed up training, improve neuron utilization, and decrease the discretization gap. 
    We theoretically show that this results from implicit Hessian regularization, which improves the convergence properties of DLGNs. We train networks $4.5 \times$ faster in wall-clock time, reduce the discretization gap by 98\%, and reduce the number of unused gates by 100\%.

---

## 论文详细总结（自动生成）

好的，作为一名资深的学术论文分析助手，我将对这篇论文《Mind the Gap: Removing the Discretization Gap in Differentiable Logic Gate Networks》进行结构化、深入、客观的总结。

---

### **1. 论文的核心问题与整体含义**

*   **研究动机与背景**：现代深度神经网络性能强大，但计算和能耗巨大，限制了其在边缘设备等真实世界场景的部署。可微逻辑门网络是一种极具潜力的高效推理模型，因其计算可以还原为硬件原生的布尔操作，从而实现极低功耗和低延迟。
*   **核心问题：离散化差距与收敛缓慢**：作者指出当前DLGNs存在两大相互关联的关键问题，严重阻碍其实际应用。
    *   **离散化差距**：训练时，模型使用连续的、可微的“软”激活函数来组合16种逻辑门；然而，在最终推理部署时，必须将每个神经元“离散化”为唯一的、具体的逻辑门。这种训练与推理行为的不一致，导致模型在推理时精度显著下降（可达3%以上）。
    *   **收敛速度慢**：DLGNs的训练过程非常缓慢，在CIFAR-10这样的简单任务上也需要数天甚至数周才能收敛。同时，训练后大量神经元（接近50%）并未确定地选择某个逻辑门，仍处于“未使用”或不确定状态，加剧了离散化差距。
*   **整体含义**：本文的目的是消除这一离散化差距，从而显著加速DLGNs的训练过程、提升神经元利用率，使其在保持高效推理优点的同时，也能进行高效且可靠的训练，推动其走向实际部署。

### **2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程**

*   **核心思想**：通过在训练过程中注入Gumbel噪声并采用直通估计器，使得模型的训练行为与最终的离散推理行为对齐，并隐式地将损失景观平滑化，从而引导优化过程走向更平坦的极小值点。
*   **提出的模型：Gumbel Logic Gate Networks**
    *   **Gumbel-Softmax重参数化**：在标准的DLGN中，一个神经元的输出是16个逻辑门输出的加权平均，权重由softmax(logits)给出。Gumbel LGNs参照Gumbel-Softmax技巧，在前向传播时，对每个神经元的16个逻辑门logits `z_i` 注入标准Gumbel噪声 `g_i`，然后执行 `argmax` 操作，即硬性地选择一个逻辑门 `h_k(a,b)`。这模仿了推理时的离散行为。
    *   **直通估计器**：由于 `argmax` 操作不可微，作者在其反向传播阶段，使用“软”的Gumbel-Softmax（公式3）输出来近似梯度，从而实现了端到端的梯度下降训练。即前向用离散选择，反向用连续近似。
    *   **隐式正则化理论**：
        *   作者从理论上证明了，注入Gumbel噪声进行训练，等价于在原始的损失函数 `L` 上增加了一个关于Hessian矩阵迹的正则化项。
        *   **核心引理 (Lemma 1)**：期望损失 \(J(z) = L(\text{softmax}(z/\tau)) + \frac{\pi^2}{12\tau^2} \text{tr}(H_f(z/\tau)) + O(\tau^{-3})\)，其中 `τ` 是温度参数，`H_f` 是Hessian矩阵。这表明，最小化这个带噪声的损失函数会**隐式地最小化损失曲面的Hessian迹（曲率）**，从而鼓励优化器找到更平坦的极小值。
    *   **效果**：平坦的极小值对参数的小幅扰动（如离散化过程中的参数变化）不敏感，因此从“软”模型到“硬”模型的切换几乎不会造成精度损失，从而从根本上消除了离散化差距。同时，更平滑的损失景观也提供了更好的梯度信号，加速了收敛。

### **3. 实验设计**

*   **数据集**：主要在图像分类基准数据集CIFAR-10和CIFAR-100上进行实验。次要实验使用了MNIST等数据集。
*   **基准对比方法**：核心对比对象是原始的**可微逻辑门网络**。
*   **对比维度与场景**：
    *   **收敛速度与精度**：对比Gumbel LGNs和DLGNs在训练过程中的“软”精度（连续模式）和“硬”精度（离散模式），并计算二者之差（离散化差距）。
    *   **网络深度的影响**：测试在不同网络深度（6， 8， 10， 12层）下，两种方法的离散化差距变化。
    *   **网络宽度的影响**：在浅层（深度6）但极宽（宽度2048k）的网络配置下进行测试。
    *   **消融研究**：
        *   **直通估计器消融**：对比“Gumbel + ST”（硬前向，软反向）和“Soft Gumbel”（前后向均软）的效果，以分离ST的贡献。
        *   **温度参数 `τ` 的消融**：测试 \(τ \in [0.01, 2.0]\) 范围内的不同取值，研究其对收敛速度和Hessian迹的影响。
    *   **损失景观分析**：
        *   **Hessian迹估计**：使用Hutchinson随机迹估计器，估算不同 `τ` 值下模型参数的Hessian矩阵迹。
        *   **损失曲面可视化**：将高维参数空间投影到二维平面，绘制损失景观，直观对比DLGNs和Gumbel LGNs的最优解附近平坦程度。
    *   **神经元利用率分析**：通过计算训练后每个神经元选择逻辑门分布的熵，来量化神经元的“确定”程度，并定义“未使用神经元”的比例。

### **4. 资源与算力**

*   **硬件环境**：实验在内部集群上进行，使用了NVIDIA RTX 3090和RTX 2080 Ti显卡。
*   **总计算量**：论文明确报告，全部实验与测试共消耗了1284个GPU小时。

### **5. 实验数量与充分性**

*   **实验数量充足**：论文设计了多种实验，从核心指标对比、架构缩放（深度、宽度）、多层次的消融研究（ST、温度）、到定量的曲面分析（Hessian迹）和定性的可视化（损失景观、熵分布），实验维度非常全面。
*   **实验不够充分之处**：
    *   **数据集覆盖**：评估主要集中在CIFAR-10和CIFAR-100，未在更大规模、更复杂的ImageNet等数据集上验证方法的泛化性。作者在局限性中也承认了这一点。
    *   **公平性**：对比DLGNs时，核心超参数（如学习率）沿用了原论文的设定，这保证了公平性。消融实验设计精巧，有效地分离了不同组件（Gumbel噪声 vs. ST）的贡献。
    *   **统计显著性**：论文坦诚指出，由于计算资源限制，未能使用不同随机种子进行多次运行，因此实验图表中缺少误差线和统计显著性检验结果，结论的可靠性略受影响。

### **6. 论文的主要结论与发现**

*   **显著加速收敛**：Gumbel LGNs比DLGNs在迭代次数上快4.75倍，在总训练墙钟时间上快4.5倍。
*   **几乎消除离散化差距**：相比DLGNs，Gumbel LGNs的离散化差距减少了98%，在训练曲线图上，软、硬精度线几乎重合。
*   **完全消除未使用神经元**：训练后，DLGNs有约49.81%的神经元未收敛到确定的门上，而Gumbel LGNs的这一比例为0.00%，实现了100%的神经元利用率。
*   **优越的深度缩放性**：随着网络深度增加，DLGNs的离散化差距会急剧增大，而Gumbel LGNs的离散化差距始终保持极低水平，显示出更好的缩放特性。
*   **理论基础与实证一致**：理论推导（Hessian迹最小化）与实验观察（更小的Hessian迹、更平坦的损失景观）相互印证，解释了方法有效性的内在机理。
*   **温度参数存在“金发姑娘区”**：温度 `τ` 过高或过低都会导致收敛变慢，存在一个适中范围（如 \(τ \approx 0.25\)）能实现最快的收敛。

### **7. 优点**

*   **问题导向清晰，解决方案简洁有效**：精准识别了DLGNs的“离散化差距”这一关键瓶颈，提出的Gumbel噪声注入方法理论扎实，无需复杂架构修改，效果惊人。
*   **理论与实验紧密结合**：不仅给出了有效的方法，还提供了Lemma 1从理论上解释了为什么Gumbel噪声能平滑损失景观、消除离散化差距，理论结果得到了Hessian迹估计等实验的有力支持。
*   **分析全面深入**：实验设计不仅仅关注精度，还系统性地分析了收敛速度、曲率、神经元利用率、温度参数影响，并提供了直观的损失景观可视化，分析维度立体且深刻。
*   **方法独立性强**：该方法的改进与具体的网络架构（如卷积DLGNs）正交，因此理论上可以推广到其他DLGNs变体中。

### **8. 不足与局限**

*   **数据集评估范围有限**：实验主要局限于CIFAR-10/100等小型数据集，未在更广泛、更具挑战性的基准上验证，泛化能力有待证明。作者已将此作为局限性提出。
*   **缺少统计显著性检验**：由于计算资源所限，实验多为单次运行，结果的随机波动影响未知，结论的稳健性需要进一步通过多种子实验验证。
*   **温度参数 `τ` 需要手动调整**：`τ` 值对性能有影响，且最优值可能需要针对不同任务或架构进行调整，这引入了额外的超参数调优负担。
*   **理论假设的简化**：理论分析基于Lipschitz连续的Hessian等假设，与复杂的真实训练场景可能存在差距。
*   **综合缩放性未充分探索**：论文未深入探索模型宽度、深度与性能之间的全面关系，比如在极深或极宽配置下的综合表现。

（完）
