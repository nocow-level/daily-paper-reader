---
title: "AegisGuard: RL-Guided Adapter Tuning for TEE-Based Efficient & Secure On-Device Inference"
title_zh: AegisGuard：基于RL引导适配器调优的TEE高效安全端侧推理
authors: "CHE WANG, Ziqi Zhang, Yinggui Wang, Tiantong Wang, Yurong Hao, Jianbo Gao, Tao Wei, YANG CAO, Zhong Chen, Wei Yang Bryan Lim"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=i99ZhFw6GN"
tags: ["query:edge-llm"]
score: 9.0
evidence: 选择性保护LoRA适配器以实现安全高效的端侧大模型推理
tldr: 针对端侧大模型白盒窃取威胁，AegisGuard提出基于强化学习的适配器敏感性测量，仅将敏感部分放入TEE保护，其余在GPU上运行。该方法在降低TEE通信开销的同时维持了模型安全，为端侧大模型的安全高效部署提供了实用框架。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-i99zhfw6gn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1424, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-i99zhfw6gn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1355, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-i99zhfw6gn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 624, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-i99zhfw6gn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 625, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-i99zhfw6gn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1148, \"height\": 661, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-i99zhfw6gn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1448, \"height\": 968, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-i99zhfw6gn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1441, \"height\": 414, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1454, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1453, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1452, \"height\": 512, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1452, \"height\": 499, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1450, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1440, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1443, \"height\": 772, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1453, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1441, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-i99zhfw6gn/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1454, \"height\": 209, \"label\": \"Table\"}]"
motivation: 端侧模型面临白盒窃取攻击，全量TEE保护又引入过高通信延迟。
method: 采用RL引导的敏感性测量筛选关键适配器，选择性TEE保护，其余卸载到GPU。
result: 降低了TEE通信开销，实现了安全与效率的平衡。
conclusion: AegisGuard为端侧大模型提供了一种兼顾安全与性能的选择性保护策略。
---

## Abstract
On-device large models (LMs) reduce cloud dependency but expose proprietary model weights to the end-user, making them vulnerable to white-box model stealing (MS) attacks. A common defense is TEE-Shielded DNN Partition (TSDP), which places all trainable LoRA adapters (fine tuned on private data) inside a trusted execution environment (TEE). However, this design suffers from excessive host-to-TEE communication latency. We propose AegisGuard, a fine tuning and deployment framework that selectively shields the MS sensitive adapters while offloading the rest to the GPU, balancing security and efficiency. AegisGuard integrates two key components: i) RL-based Sensitivity Measurement (RSM), which injects Gaussian noise during training and applies a lightweight reinforcement learning to rank adapters based on their impact on model stealing; and (ii) Shielded-Adapter Compression (SAC), which structurally prunes the selected adapters to reduce both parameter size and intermediate feature maps, further lowering TEE computation and data transfer costs. Extensive experiments demonstrate that AegisGuard achieves black-box level MS resilience (surrogate accuracy around 39%, matching fully shielded baselines), while reducing end-to-end inference latency by 2–3× and cutting TEE memory usage by 4× compared to state-of-the-art TSDP methods.

---

## 论文详细总结（自动生成）

好的，下面是对论文《AegisGuard: RL-Guided Adapter Tuning for TEE-Based Efficient & Secure On-Device Inference》的详细中文总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：端侧部署大模型（LMs）虽然减少了云端依赖，但会将私有的模型权重暴露给用户，使其易受**白盒模型窃取（Model Stealing, MS）攻击**。现有的一种主流防御方案是 **TEE-Shielded DNN Partition（TSDP）**，即将所有基于私有数据微调的LoRA适配器置于可信执行环境（TEE）内。然而，这种“全量保护”策略会导致TEE与主机GPU之间产生巨大的通信延迟，严重制约了推理效率。
*   **整体含义**：本文旨在解决端侧大模型安全部署中的一个关键矛盾——**如何在保证模型安全、抵御模型窃取攻击的同时，最大限度地提升推理效率**。AegisGuard框架的提出，意味着安全保护不必以牺牲全部性能为代价，可以通过智能地选择保护目标来实现安全与效率的平衡。

### 2. 方法论

论文提出了一个名为 **AegisGuard** 的微调与部署框架，其核心思想是**选择性保护**：仅将那些对模型窃取攻击最敏感（即暴露后能显著提升攻击者模型性能）的适配器放入TEE，而将其余部分卸载到GPU上。该框架包含两大关键技术：

*   **RL-based Sensitivity Measurement (RSM)：基于强化学习的敏感性度量**
    *   **核心思想**：通过在微调过程中注入高斯噪声，观察模型损失的变化，并结合强化学习动态评估每个适配器层对私有数据的敏感程度。其逻辑是：一个包含了更多私有数据信息的敏感适配器，在参数被扰动时会引起更大的输出损失变化。
    *   **关键步骤**：
        1.  **敏感层选择（策略动作）**：将各层敏感性得分 \( S \) 作为环境状态，根据得分采样并选择一批候选敏感层进行后续微调。
        2.  **层级敏感性估计（奖励反馈）**：定期向所选层的低秩矩阵 \( A \) 中注入高斯噪声 \( \epsilon \)，计算噪声注入后的损失变化 \( \Delta L_i \)。
        3.  **敏感性得分更新（状态更新）**：根据损失变化 \( \Delta L_i \) 计算奖励 \( R_t \)，并用其更新该层的敏感性得分 \( s_i \)。使得被扰动后损失变化大的层得分增加，反之减少。

*   **Shielded-Adapter Compression (SAC)：受保护适配器压缩**
    *   **核心思想**：对RSM识别出的高敏感适配器进行**结构化剪枝**，直接减少适配器参数和中间特征图的维度，从而降低TEE内的计算量和数据传输量。
    *   **关键步骤**：
        1.  **重要性估计**：基于梯度和一阶泰勒展开，近似估计LoRA矩阵中每个参数元素的重要性 \( \hat{I}_{i,j} \)。
        2.  **动态剪枝**：提出一种与RSM模块兼容的动态剪枝率 \( \text{ratio}_i(t) \)，该比率随训练步骤 \( t \) 线性增加，并根据该层的敏感性得分 \( s_i \) 进行调整。最终，以“头”为粒度移除重要性最低的部分参数，实现结构化压缩。

### 3. 实验设计

*   **数据集与场景**：
    *   **生成式模型（NLP）**：使用`CommonSenseQA`数据集进行微调，并在六个常见问答基准上评估模型性能：`ARC-Challenge`, `ARC-Easy`, `HellaSwag`, `OBQA`, `PIQA`, `WinoGrande`。
    *   **视觉模型（CV）**：使用了六个不同领域的图像分类数据集：`CIFAR10`, `CIFAR100`, `UTKFace`, `MNIST`, `GTSRB`, `SUN397`。遵循先前工作，用`CIFAR10/100`和`UTKFace`评估防御效果。

*   **Benchmark（对比方法）**：
    *   **SOTA TSDP方案**：`TEESlice` 和 `Phantom`（发表在顶会上的近期工作）。
    *   **边界基准**：
        *   `No-Shield`：模型全部部署在非安全GPU上（效率最高，安全最差）。
        *   `Shield-LoRA`：所有适配器全部部署在TEE中（安全最高，效率最差）。

### 4. 资源与算力

*   文中明确提到的算力资源为：
    *   **微调阶段**：在一台配备单张**NVIDIA A6000 GPU**的服务器上进行。
    *   **推理评估阶段**：在一台配备**Intel SGX** 飞地（SDK 2.6, GCC 7.5）和一张**NVIDIA RTX4090D 24GB GPU**的个人电脑上搭建原型系统进行测试。
*   **不足**：论文未提及微调的总耗时、GPU内存占用量等具体细粒度的算力开销数据。

### 5. 实验数量与充分性

*   **实验类型与数量丰富**：实验涵盖了多个维度的评估，包括：
    1.  **端侧推理效率**：在不同模型（ViT-Base, LLaMA-7B）上分解并测试了GPU计算、TEE计算和跨域数据传输的延迟及内存占用。
    2.  **防御有效性**：模拟灰盒模型窃取攻击，评估了攻击者复制的替代模型在不同数据集和模型（ViT-Base, LLaMA-7B, ViT-Large, OPT-2.7B）上的准确率。
    3.  **下游任务精度**：评估了在多个NLP和CV基准上AegisGuard及其变体（消融版本）的原始任务准确率。
    4.  **敏感性可视化**：可视化了不同模型、不同层的敏感性得分分布。
    5.  **消融研究**：对比了 `Shield-LoRA`、`+RL sens`、`+SAC` 和完整的 `AegisGuard`，以验证各模块的作用。
    6.  **同类型模型分析**：在更多模型（ViT-Large, OPT-2.7B）上验证了效率、安全和精度表现的泛化性。
*   **充分性与公平性**：实验设计较为全面和系统。从效率、安全、精度三个核心目标出发，进行了充分的横向对比和内部消融分析。对比基线具有代表性，攻击模拟和测试基准遵循了领域惯例，确保了客观性和公平性。

### 6. 主要结论与发现

1.  **效率显著提升**：与最高安全级别的`Shield-LoRA`相比，AegisGuard可将端到端推理延迟降低 **2-3倍**（LLaMA-7B上达3.33倍加速），并将TEE内存占用减少约 **4倍**。这主要得益于降低了TEE计算量和数据传输量。
2.  **防御效果相当**：AegisGuard在降低效率开销的同时，提供了与全量保护（`Shield-LoRA` / `TEESlice`）**同级别**的黑盒模型窃取防御能力，攻击者替代模型的准确率被压制在约39%。
3.  **精度损失可忽略不计**：AegisGuard引入的额外模块对下游任务精度的影响微乎其微，平均准确率浮动仅 **0.12%**。
4.  **敏感性分布非均匀**：不同层级对模型窃取的敏感性差异很大，证明了**动态选择**敏感层进行保护的必要性，固定策略难以全面兼顾。

### 7. 优点

*   **创新的问题视角**：首次在TSDP框架下，从适配器“敏感性”差异的角度出发，突破了“全量保护”的思维定式，实现了安全与效率的有效平衡。
*   **方法论设计巧妙**：将强化学习（建模为多臂老虎机问题）与基于噪声注入的敏感性评估相结合，能动态、高效地识别关键保护目标，方法新颖且开销可控。
*   **双管齐下的优化**：RSM和SAC两个模块分别从**减少保护目标数量**和**压缩单一目标体积**两个维度，系统性地降低了TEE的开销。
*   **实验全面扎实**：涵盖了多种模型、多个数据集、多维度的评估指标，验证了方法的有效性、泛化性和各部分设计的合理性。

### 8. 不足与局限

*   **威胁模型受限**：论文明确声明不防御基于特征泄露的输入重构或训练数据反演攻击，仅关注保护微调知识免于功能性模仿，这是一个有意为之的设定，但与更全面的端侧安全需求相比存在局限。
*   **实验精度分析**：在特定情况下，如LLaMA-7B的`PIQA`任务，完整AegisGuard（77.85%）相比Shield-LoRA（77.92%）出现了微小的精度下降，文中的“可忽略不计”描述略显绝对，且对微调稳定性的影响分析不够深入。
*   **训练成本对比缺失**：虽然推理端效率提升显著，但未明确量化RSM和SAC模块在微调阶段引入的**额外训练时间成本**，这对于实际应用是一个重要权衡因素。
*   **RL代理设计**：目前的RL状态仅考虑层敏感性的连续打分，动作空间为基于此打分的采样，设计相对简单。未来或可引入模型结构、参数规模等更丰富的状态信息，设计更复杂的策略。

（完）
