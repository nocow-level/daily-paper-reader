---
title: "RoSTE: An Efficient Quantization-Aware Supervised Fine-Tuning Approach for Large Language Models"
title_zh: RoSTE：一种高效的大语言模型量化感知监督微调方法
authors: "Quan Wei, Chung-Yiu Yau, Hoi To Wai, Yang Zhao, Dongyeop Kang, Youngsuk Park, Mingyi Hong"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=h30EzoI3s0"
tags: ["query:edge-llm"]
score: 9.0
evidence: 量化感知微调实现LLM权重、激活和KV缓存的低位量化
tldr: 针对传统先微调后量化流程无法充分利用二者协同的问题，提出RoSTE算法，结合量化感知微调与自适应旋转，有效实现LLM权重、激活和KV缓存的低位量化。实验证明该方法在保持模型性能的前提下显著减少位宽。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1694, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 756, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 642, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1776, \"height\": 908, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1751, \"height\": 816, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 786, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 784, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-h30ezoi3s0/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 784, \"height\": 527, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1606, \"height\": 1015, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1613, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 735, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1520, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1762, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1384, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1649, \"height\": 1811, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1648, \"height\": 2031, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1757, \"height\": 756, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-h30ezoi3s0/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1239, \"height\": 480, \"label\": \"Table\"}]"
motivation: 现有量化微调流水线分别执行优化，未能挖掘微调与量化的协同效应。
method: 提出旋转直通估计器结合自适应旋转策略，在微调过程中执行量化。
result: 实现了LLM的低位量化，超越后训练量化的性能。
conclusion: RoSTE通过量化感知微调显著提升了量化LLM的精度与效率。
---

## Abstract
Supervised fine-tuning is a standard method for adapting pre-trained large language models (LLMs) to downstream tasks. Quantization has been recently studied as a post-training technique for efficient LLM deployment. To obtain quantized fine-tuned LLMs, conventional pipelines would first fine-tune the pre-trained models, followed by post-training quantization. This often yields suboptimal performance as it fails to leverage the synergy between fine-tuning and quantization. To effectively realize low-bit quantization of weights, activations and KV caches in LLMs, we propose an algorithm named Rotated Straight-Through-Estimator (RoSTE), which combines quantization-aware supervised fine-tuning (QA-SFT) with an adaptive rotation strategy that identifies an effective rotation configuration to reduce activation outliers. We provide theoretical insights on RoSTE by analyzing its prediction error when applied to an overparameterized least square quantized training problem. Our findings reveal that the prediction error is directly proportional to the quantization error of the converged weights, which can be effectively managed through an optimized rotation configuration. Experiments on Pythia, Qwen and Llama models of different sizes demonstrate the effectiveness of RoSTE. Compared to existing post-SFT quantization baselines, our method consistently achieves superior performances across various tasks and different LLM architectures. Our code is available at https://github.com/OptimAI-Lab/RoSTE.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
*   **研究动机与背景**：监督微调是将预训练大语言模型适配到下游任务的标准方法，而量化是实现模型高效部署的关键技术。传统流程先进行全精度微调，再进行训练后量化，这种“先后”分离的方式无法充分利用微调与量化之间的协同效应，常导致次优的模型性能。
*   **核心问题**：如何在单个训练阶段中，有效结合监督微调与量化过程，以生成高精度的低比特量化大语言模型，从而同时实现任务适配与高效部署。
*   **整体含义**：本文首次提出了将量化感知训练的思想系统性地应用于监督微调过程，并通过创新的自适应旋转策略解决量化中的离群值问题，为获取部署就绪的量化大语言模型提供了更优的范式。

### 2. 方法论：核心思想与关键技术
*   **核心思想：RoSTE算法**：提出了“旋转直通估计器”算法，该算法将**量化感知监督微调**与**自适应旋转策略**相结合。它通过一个双层优化框架，在微调模型权重的过程中，同步选择和优化用于消除激活值离群点的旋转矩阵。
*   **关键技术细节**：
    *   **双层优化建模**：将问题分解为上下两层。**上层**负责通过量化感知训练和直通估计器来优化量化后的权重矩阵，以最小化监督微调损失；**下层**则利用一个代理损失，以较低的复杂度为神经网络各层选择最优的旋转矩阵（是否应用旋转）。
    *   **自适应旋转策略**：针对激活值离群问题，算法在随机沃尔什-哈达玛旋转矩阵和恒等映射之间进行层级的自动选择。选择依据是**量化误差**，即选择能够最小化该层权重与激活量化误差的配置。
    *   **算法流程**：RoSTE交替执行两个阶段：1）**旋转配置阶段**：根据当前权重，以贪心方式逐层比较应用随机哈达玛矩阵与不应用旋转的量化误差，选择误差更小的配置。2）**量化感知训练阶段**：在固定旋转配置后，利用直通估计器近似量化器的梯度，对量化后的权重矩阵进行若干步的监督微调。
*   **理论支撑**：论文通过分析一个过参数化最小二乘量化训练问题，从理论上证明预测误差与收敛权重的量化误差成正比，而后者可通过优化的旋转配置有效降低，为使用量化误差作为代理损失提供了依据。

### 3. 实验设计
*   **数据集与场景**：
    *   **实验一（Exp.1）**：使用**Reddit TL;DR摘要数据集**对Pythia和Qwen系列模型进行微调，并在TL;DR测试集上以**ROUGE**分数作为评价指标。
    *   **实验二（Exp.2）**：使用**Tulu 3 SFT混合数据集**对Llama 3.1 8B模型进行微调，在包括**TruthfulQA、MMLU-Pro、BigBenchHard、AGIEval、GSM8K和MATH**在内的多个下游任务基准上评估准确性。
*   **对比方法**：
    *   **传统两步法基线**：先进行全精度监督微调，后进行训练后量化，如**RTN、GPTQ、QuaRot、SpinQuant**。
    *   **量化感知训练基线**：直接将**直通估计器**应用于监督微调过程。

### 4. 资源与算力
论文明确指出所有实验均在配备**8块NVIDIA A100 GPU**的服务器集群上完成。文中提供了详细的训练时间对比图，例如，对Qwen2.5 7B模型进行4比特量化感知微调（RoSTE）的总训练时间约为2.8小时，略高于全精度微调的2.1小时和STE方法的2.4小时，但在可接受范围内。

### 5. 实验数量与充分性
*   **实验数量**：实验覆盖了多种模型（Pythia、Qwen、Llama）的不同参数规模，共涉及数十组对比实验。
*   **实验充分性**：
    *   **多架构与多规模**：验证了RoSTE在不同模型架构和多种参数规模下的有效性，结论具有普适性。
    *   **多任务评估**：不仅评估了文本摘要能力，还评估了在数学、推理、常识等多种下游任务上的表现，评估维度全面。
    *   **消融实验**：通过对比“无旋转”、“全旋转”和“自适应旋转”策略，清晰证明了自适应旋转策略的关键作用。
    *   **多比特位宽验证**：提供了W4A4KV4、W4A8KV4等多种量化配置下的实验结果。
*   **客观性与公平性**：所有基线方法均采用公开代码和论文推荐的设置进行复现，训练和评估设置清晰透明，保证了对比的客观与公平。

### 6. 主要结论与发现
*   **性能优越**：RoSTE算法在多个模型和任务上一致地优于所有现有基线方法，能够以极小的性能损失（与全精度微调模型相比）实现4比特权重、激活值和KV缓存的量化。
*   **旋转策略至关重要**：自适应地在模型各层应用旋转矩阵，是获得高性能量化微调模型的关键，盲目的全局应用旋转反而会损害性能。
*   **理论指导实践**：理论分析揭示的量化误差与最终性能的关联，成功地指导了高效的旋转矩阵选择策略。

### 7. 优点
*   **方法新颖**：首次将量化感知训练与自适应旋转策略系统性地结合到监督微调中，提供了一种获取高性能量化推理模型的一体化解决方案。
*   **理论与实验并重**：不仅提出了有效算法，还提供了坚实的理论依据，增强了方法的可信度与可解释性。
*   **计算效率高**：算法设计巧妙，旋转矩阵的选择和量化感知训练过程计算开销适中，训练时间与全精度微调或传统量化感知训练相比仅略微增加。
*   **实用性强**：专注于在主流GPU硬件上实现高效的4比特量化推理，现实意义明确。

### 8. 不足与局限
*   **旋转策略的启发性**：论文中旋转配置的搜索被简化为一组离散选择的组合优化，并通过启发式方法求解，虽然有效，但并非精确最优解，其在更复杂的网络结构或任务下的泛化能力有待进一步探索。
*   **激活量化位宽的假设**：理论分析部分假定了一个简化的线性模型和特定的插值条件，与现实中的复杂大语言模型微调场景存在差距。
*   **应用场景有待扩展**：实验目前集中在语言模型和文本任务上，其在多模态模型等更广泛领域的适用性尚未得到验证。
*   **未探索与其他高效微调技术的结合**：论文并未探讨RoSTE与LoRA等流行的参数高效微调技术结合的可能性与效果，这可能是一个有价值的后续方向。

（完）
