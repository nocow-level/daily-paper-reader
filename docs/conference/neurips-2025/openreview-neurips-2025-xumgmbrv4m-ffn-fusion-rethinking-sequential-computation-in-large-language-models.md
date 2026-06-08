---
title: "FFN Fusion: Rethinking Sequential Computation in Large Language Models"
title_zh: FFN Fusion：重新思考大语言模型中的顺序计算
authors: "Akhiad Bercovich, Mohammed Dabbah, Omri Puny, Ido Galil, Amnon Geifman, Yonatan Geifman, Izhak Golan, Ehud Dov Karpas, Itay Levy, Zach Moshe, Najeeb Nabwani, Tomer Ronen, Itamar Schen, Ido Shahaf, Oren Tropp, Ran Zilberstein, Ran El-Yaniv"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=XUmGMBRv4M"
tags: ["query:edge-llm"]
score: 5.0
evidence: 并行化FFN层以降低推理延迟，生成更小的模型
tldr: 该论文发现大语言模型中多轮FFN层可并行化，提出FFN Fusion方法将其融合为并行操作，以显著减少推理延迟。在Llama-3.1-405B上应用后得到253B模型，性能几乎不受影响。该方法提供了一种通用的LLM推理加速策略，有助于模型在资源受限环境下的高效运行。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 740, \"height\": 894, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 476, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1167, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 689, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1063, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1164, \"height\": 1035, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1276, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1348, \"height\": 1013, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 745, \"height\": 778, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-xumgmbrv4m/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1141, \"height\": 1109, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1374, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 660, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 598, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 728, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 588, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 586, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 590, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-xumgmbrv4m/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 840, \"height\": 364, \"label\": \"Table\"}]"
motivation: 大语言模型中FFN层的顺序执行导致推理延迟高。
method: 识别并融合可并行化的FFN层序列，转化为并行操作。
result: 将405B模型压缩为253B，推理延迟显著降低，性能保持。
conclusion: FFN Fusion通过挖掘并行机会有效加速LLM推理，为模型压缩提供新思路。
---

## Abstract
We introduce \textit{FFN Fusion}, an architectural optimization technique that reduces sequential computation in large language models by identifying and exploiting natural opportunities for parallelization. Our key insight is that sequences of Feed-Forward Network (FFN) layers, particularly those remaining after the removal of specific attention layers, can often be parallelized with minimal accuracy impact. We develop a principled methodology for identifying and fusing such sequences, transforming them into parallel operations that significantly reduce inference latency while preserving model behavior. Applying these techniques to Llama-3.1-405B-Instruct, we create a 253B model (253B-Base), an efficient and soon-to-be publicly available model that achieves a 1.71$\times$ speedup in inference latency and 35$\times$ lower per-token cost while maintaining strong performance across benchmarks. Most intriguingly, we find that even full transformer blocks containing both attention and FFN layers can sometimes be parallelized, suggesting new directions for neural architecture design.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：大语言模型（LLM）的规模扩展带来高昂的推理延迟与资源消耗，虽然量化、剪枝、专家混合（MoE）等优化方法被广泛使用，但各有局限（如量化精度损失、剪枝难发现冗余、MoE在中小批次下吞吐不佳）。
- **核心问题**：能否从架构层面挖掘顺序计算中的并行性，从而在保持模型能力的同时大幅降低推理延迟？
- **整体含义**：本文证实，移除部分注意力层后留下的连续FFN层之间存在大量可并行化的机会，通过将它们“融合”为更宽的并行层，可以实质性加速推理，同时几乎不影响性能。这一发现挑战了Transformer必须严格顺序执行的传统认知，为高效部署开辟了新方向。

### 2. 论文提出的方法论

- **核心思想**：在注意力已被剪枝的区块中，多个顺序FFN层可以改写为共享同一输入的并行形式，其输出之和等价于一个宽度更大的单层FFN（定理3.1）。
- **FFN融合公式**：
  - 对无注意力的块 \( \hat{f}(X) = X + \text{FFN}(\eta_2(X)) \)。
  - 并行版本：\( \hat{f}_{[i,i+c]}(X) = X + \sum_{j=0}^c \text{FFN}_{i+j}(\eta_2(X)) \)。
  - 融合实现：通过将对应权重矩阵沿隐藏维度拼接，得到一个 \( nd_h \times d_e \) 的大FFN层（其中n为融合的层数），从而消除层间同步并提高GPU利用率。
- **识别可融合序列的方法**：
  - **块间依赖分析**：计算各层输出之间的余弦距离矩阵 \( M_{ij} = \text{CosineDist}(h_j(X), \tilde{h}_{ji}(X)) \)，其中 \( \tilde{h}_{ji}(X) \) 为移除层i后层j的输出。值越小表示依赖越弱，越适合融合。
  - **与Puzzle结合**：先使用Puzzle框架搜索并移除大量注意力层，形成长连续FFN序列，再根据依赖分析和内存约束将序列分割成若干组进行融合。
- **并行化扩展**：初步尝试将完整的Transformer块（含注意力）做全块并行，通过贪心选取4块序列进行实验（暂未在高效推理框架上实现）。

### 3. 实验设计

- **主要衍生模型**：从Llama-3.1-405B-Instruct出发，通过Puzzle搜索出一个253B参数模型，再应用FFN Fusion生成**Ultra-253B-Base**。
- **数据集与基准**：
  - **训练/蒸馏数据**：Distillation Mix（来自FineWeb、Dolma、Buzz-V1.2等，约224B tokens），以及用于知识蒸馏（KD）和继续预训练（CPT）的合成数据。
  - **评测基准**：MMLU、MMLU-Pro、Arena Hard、HumanEval、MT-Bench、MATH500、RULER 128K等，覆盖知识、代码、对话、长文本能力。
- **对比方法**：
  - 与原始Llama-405B、Llama-3.3-70B-Instruct等模型比较精度与延迟。
  - 在不同规模（8B、49B、70B、253B-405B）和不同家族（Mistral Large 2）上验证融合效果。
  - 消融实验对比“融合FFN”与“直接移除FFN”，以及反向顺序FFN的效果。

### 4. 资源与算力

- **硬件配置**：推理效率测试在单节点8×H100（640 GB）上进行，部分显存要求提到单B100 GPU 192 GB。
- **训练细节**：
  - **KD阶段**：54B tokens（8k上下文）+ 5B tokens（16k）+ 5B tokens（32k）+ 0.8B tokens（128k）。
  - **可选CPT**：73B tokens（8k）+ 15B tokens（258k）。
  - 对49B模型的KD实验仅需25B tokens。
- **局限性**：论文未明确给出训练阶段所需的GPU卡数/总GPU小时数，也未计算总浮点运算量。由于模型规模巨大，训练资源消耗必然极高。

### 5. 实验数量与充分性

- **多组实验设置**：
  - 主实验：从405B→253B的端到端流程，含精度与延迟全面测量。
  - 多尺度验证：在8B、49B/70B、253B模型上进行不同融合强度（1/2/3/4步融合）的比较。
  - 消融分析：FFN融合 vs 直接移除FFN、反向顺序、是否包含序列末尾FFN等。
  - 泛化测试：在Mistral Large 2和Llama-3.1-8B上复现融合效果。
  - 可解释性实验：依赖热力图、层间余弦距离、残差范数比等。
  - 全块并行尝试：选取4块序列进行初步效果测量。
- **充分性评价**：实验设计覆盖了不同规模、不同模型家族、多种融合策略和丰富的消融对比，并配有延迟与成本的实测数据，整体系统且充分，结论客观。

### 6. 论文的主要结论与发现

- **FFN序列可大幅并行化**：连续FFN层融合为单层后，精度损失极小（例如253B模型融合后MMLU从84.23→82.76未经额外训练），且可通过轻量KD完全恢复甚至超越原模型。
- **Ultra-253B-Base实现极致效率**：相较Llama-405B，推理延迟降低1.71倍，每token成本降低35倍（batch=32），参数量减少至253B，KV缓存减半，在Arena Hard、HumanEval等多个基准上维持或提升性能。
- **末尾FFN具有特殊敏感性**：融合长序列时，跳过最后一个FFN通常能避免较大精度下降。
- **方法具有通用性**：在49B模型、Mistral Large 2、Llama-8B上均能成功应用。
- **全块并行存在可能**：初步结果表明，部分完整的Transformer块也可并行，但依赖更复杂，尚未在高效框架中实现。

### 7. 优点

- **理论基础扎实**：定理3.1为融合操作提供了严格的数学保障。
- **落地性强**：直接生成可部署的253B高效模型，并即将公开。
- **系统性分析**：依赖矩阵、残差分析等提供了可解释性，帮助理解为何融合可行。
- **兼容现有技术**：与Puzzle剪枝、知识蒸馏无缝衔接，构成推理优化的完整流水线。
- **效率提升显著**：在保持或超越原模型精度的前提下，实现真实场景下的延迟与成本大幅降低。

### 8. 不足与局限

- **前提依赖**：需要先通过Puzzle等方法移除注意力层，形成长FFN序列，原始密集模型中可融合的区域有限。
- **并行化实现约束**：全块并行受限于现有推理框架，速度优势未能实测。
- **计算成本未披露**：大规模KD/CPT的训练资源需求未量化，可能成为复现障碍。
- **模型规模有限**：虽测试了253B级模型，但未在更大规模的MoE或其他非Llama架构上深入验证（仅Mistral、8B）。
- **最终FFN的敏感性问题**：需要人工决定是否保留尾部层，缺乏自动化的判断准则。
- **融合粒度受硬件限制**：受GPU内存影响，融合序列的长度需分组合并，未能验证更长融合的效果。

（完）
