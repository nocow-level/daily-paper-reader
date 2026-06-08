---
title: Retraining-free Merging of Sparse MoE via Hierarchical Clustering
title_zh: 基于层次聚类的稀疏MoE免重训练合并
authors: "I-Chun Chen, Hsu-Shen Liu, Wei-Fang Sun, Chen-Hao Chao, Yen-Chang Hsu, Chun-Yi Lee"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=hslOzRxzXL"
tags: ["query:edge-llm"]
score: 9.0
evidence: 通过层次聚类合并稀疏MoE中的专家，无需重新训练即可减少参数以适应资源受限部署
tldr: 针对稀疏MoE模型在资源受限环境中因专家组件带来的巨大内存需求，提出免重训练的专家合并框架HC-SMoE，通过基于专家输出的层次聚类确保稳健合并，显著降低参数量，便于在有限资源设备上部署高性能MoE模型。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 771, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 855, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 849, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1768, \"height\": 1868, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1418, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1782, \"height\": 1046, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1783, \"height\": 1052, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1778, \"height\": 1027, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1780, \"height\": 1052, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1776, \"height\": 1046, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1779, \"height\": 814, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1750, \"height\": 834, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hslozrxzxl/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1760, \"height\": 748, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1776, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1773, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 863, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1773, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1774, \"height\": 486, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1775, \"height\": 429, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1772, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1770, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1770, \"height\": 406, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1771, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1769, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1760, \"height\": 274, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1199, \"height\": 532, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1772, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1771, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1773, \"height\": 467, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1773, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1345, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1050, \"height\": 553, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1050, \"height\": 556, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hslozrxzxl/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1774, \"height\": 618, \"label\": \"Table\"}]"
motivation: 稀疏MoE模型参数效率高但专家组件内存占用大，难以在资源有限环境部署。
method: 提出HC-SMoE，基于专家输出进行层次聚类，任务无关地合并专家以压缩模型。
result: 无需重新训练即可显著减少参数，同时保持模型性能。
conclusion: 为稀疏MoE模型在边缘设备上的高效部署提供了实用的压缩方案。
---

## Abstract
Sparse Mixture-of-Experts (SMoE) models represent a significant advancement in large language model (LLM) development through their efficient parameter utilization. These models achieve substantial performance improvements at reduced
inference costs. However, the deployment of SMoE models faces constraints from extensive memory requirements of expert components in resource-limited environments. To address these limitations, this paper introduces Hierarchical Clustering for Sparsely activated Mixture of Experts (HC-SMoE), a task-agnostic expert merging framework for parameter reduction without retraining. HC-SMoE introduces a novel hierarchical clustering approach based on expert outputs to ensure merging robustness independent of routing decisions. The proposed output-based clustering method enables effective capture of functional relationships between experts for large-
scale architectures. We provide theoretical analysis and comprehensive evaluations across multiple zero-shot language tasks to demonstrate HC-SMoE’s effectiveness in state-of-the-art models including Qwen and Mixtral. The experimental results validate HC-SMoE’s superior performance and practical applicability for real-world deployments. Our implementation is available at https://github.com/wazenmai/HC-SMoE.

---

## 论文详细总结（自动生成）

好的，我将以资深学术论文分析助手的身份，使用中文、Markdown格式，对这篇论文《Retraining-Free Merging of Sparse MoE via Hierarchical Clustering》进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：稀疏混合专家模型（SMoE）在推理时通过选择性激活部分“专家”网络，实现了高效扩展。然而，其巨大的总参数量（所有专家之和）导致了高昂的显存占用，阻碍了模型在资源受限环境下的部署。
*   **研究动机**：现有解决方案如专家剪枝（Pruning），虽然能减少参数，但会永久性丢弃被剪枝专家的知识，可能导致不可逆的性能损失。另一种方案是专家合并（Merging），但其先前的任务无关通用性不足，或依赖特定任务数据。
*   **整体含义**：本文旨在提出一种 **任务无关、无需重新训练的专家合并框架**，在减少SMoE模型参数量的同时，最大限度地保留其通用语言能力，为SMoE模型在现实世界的高效部署提供实用方案。

### 2. 论文提出的方法论

核心思想是通过基于专家功能相似性的层次聚类，将相似专家分组后再进行合并，从而减少专家总数。

*   **核心思想与关键技术细节**：
    1.  **相似性度量指标（Expert Outputs as Similarity Metric）**：
        *   传统方法使用路由得分或专家权重作为相似性依据，但这会引入任务特定偏差或面临高维计算挑战。
        *   本方法创新性地提出**基于专家输出的平均向量**作为相似性度量。对于一个专家 \(E_j\)，其代表性向量 \(o_j\) 通过在通用校准数据集 \(\mathcal{D}_{cal}\) 上计算其输出的平均值得到：
            \[ o_j := \mathbb{E}_{x \sim \mathcal{D}_{cal}} [E_j(x)] \]
        *   该方法能更直接地反映专家的功能等价性，且计算效率高，与合并目标一致。
    2.  **层次聚类分组（Hierarchical Clustering of Experts）**：
        *   采用自底向上的层次聚类算法，初始时将每个专家视为一个独立聚类。
        *   迭代合并功能最相似的聚类，每次合并后重新计算聚类间距离（采用**平均链接法**），克服了K-means等分区方法对初始化和聚类几何形状敏感的缺点。
        *   聚类距离使用欧几里得距离计算：\(d(e_i, e_j) = ||e_i - e_j||_2\)。链接策略上，理论分析和实验表明**平均链接**在簇内相似度和簇间差异度之间取得了最佳平衡。
    3.  **专家合并与路由保持**：
        *   对于形成的每个聚类，将其内部的专家合并为一个新专家。合并方式为权重空间的参数聚合：\(\hat{E}_i = \sum_{j=1}^{|C_i|} \alpha_j E_j\)，其中 \(\sum \alpha_j = 1\)。
        *   由于优秀的聚类结果保证了组内专家的功能相似性，合并策略（如平均合并、频率加权合并）的选择对最终性能影响**较为温和**。框架默认采用基于专家使用频率的加权合并。
        *   **关键技巧**：在合并专家后，路由网络 \(R\) **保持不变**。原先路由到某个聚类中任何专家的输入，都会被导向该聚类合并后的唯一专家，从而在不改变路由维度的情况下实现专家缩减。

*   **算法流程概要**：
    1.  **输入**：校准数据集 \(\mathcal{D}_{cal}\)，目标聚类数 \(r\)。
    2.  **计算专家输出**：对于每一层，计算所有专家在 \(\mathcal{D}_{cal}\) 上的平均输出向量 \(o_j\)。
    3.  **层次聚类**：以每个专家为单独的簇开始，重复计算成对簇间的平均距离，并合并距离最近的两个簇，直到簇的数量减少至 \(r\)。
    4.  **专家合并**：在每个簇内，根据专家在 \(\mathcal{D}_{cal}\) 上的激活频率进行加权平均，合并成新的专家参数。
    5.  **输出**：专家数减少后的新SMoE模型。

### 3. 实验设计

*   **数据集/场景**：
    *   **校准数据集**：所有方法统一从C4语料库中抽取文本，构建32个长度为2048的序列作为校准数据，用于计算专家输出或路由得分等统计信息。同时也测试了从MATH和CodeQA等不同领域构建的校准集。
    *   **评估基准**：在8个具有代表性的零样本语言任务上进行评估，覆盖常识推理、知识问答和语义理解。基准包括：**ARC-c, ARC-e, BoolQ, HellaSwag, MMLU, OpenBookQA, RTE, Winogrande**。使用EleutherAI LM Harness框架评测，报告零样本准确率。
    *   **额外评估**：在医学领域的**MedMCQA**数据集上进行了领域适应性评估；在**DeepSeek-MoE-16B**模型上评估了可扩展性。

*   **对比方法**：
    *   **3种裁剪基线**：
        *   **O-prune**: 基于输出损失比较的裁剪。
        *   **S-prune**: 基于路由得分的裁剪。
        *   **F-prune**: 基于专家激活频率的裁剪。
    *   **1种合并基线**:
        *   **M-SMoE**: 基于路由得分进行分组和合并的先前方法。
    *   **原始未裁剪模型**作为性能上界参考。

*   **模型与削减比例**：
    *   **Qwen1.5-MoE-A2.7B-Chat (60专家/层)**：削减至45专家（25%）、30专家（50%）。
    *   **Mixtral 8x7B (8专家/层)**：削减至6专家（25%）、4专家（50%）。

### 4. 资源与算力

*   **硬件**: 论文明确提到，Mixtral 8x7B 实验在 **8块 NVIDIA A100 GPU** 上运行，Qwen 实验在 **4块 NVIDIA V100 GPU** 上运行。
*   **效率**: 论文在附录中报告了算法运行时间。例如，对Qwen模型的压缩，HC-SMoE算法耗时约290-323秒（约5分钟），内存占用约48.7GB；对Mixtral 4x7B的压缩耗时约112秒。这表明方法本身的计算开销是较小的，主要开销源于模型推理。

### 5. 实验数量与充分性

*   **实验数量**：实验设计较为系统和充分。主要包括：
    *   **主实验**：在2个主流SMoE模型（Qwen, Mixtral）上，分别在2种削减比例（25%, 50%）下，与4个基线方法在8个语言任务上的性能对比，共计 \(2 \times 2 \times 4 \times 8\) 等多项结果。
    *   **消融研究**：对方法的核心组件进行了详细消融。
        *   **聚类方法对比**：与K-means聚类进行对比，验证层次聚类的稳定性和有效性。
        *   **相似性度量对比**：对比了基于路由得分、权重和专家输出的度量效果。
        *   **链接方法对比**：对比了单链接、全链接和平均链接。
        *   **合并策略对比**：对比了平均、频率加权和固定主导合并。
        *   **聚类流程对比**：与非均匀聚类、单次分组法进行对比。
    *   **鲁棒性验证**：评估了不同校准数据集（C4, MATH, CodeQA）的影响，验证方法的任务无关性。
    *   **极端压缩与领域测试**：在高达75%削减率下测试，并在医学问答领域进行验证。
*   **公平性**: 实验设计是公平的。所有对比方法均在**任务无关的零样本设定**下进行，使用相同的校准数据集来获取必要统计信息，并在同样的基准上进行评估。

### 6. 论文的主要结论与发现

*   **优越性能**：HC-SMoE在所有实验设置下均**一致性地优于**现有的免重训练裁剪和合并基线方法，在25%和50%的参数削减后性能下降最小，甚至在某些任务上由于合并减少了冗余而超越原始模型。
*   **稳定性与鲁棒性**：相比K-means等方法，层次聚类由于是确定性算法，对初始化不敏感，聚类结果更稳定。专家输出作为相似性度量优于路由得分和权重，并且对校准数据集的选择不敏感，展现出强大的任务无关泛化能力。
*   **聚类质量优先**：研究表明，一旦通过高质量聚类将功能相似的专家正确分组，具体的合并策略（如平均或加权平均）对最终性能的影响较小。聚类质量是压缩效果的关键。
*   **实用性强**：方法无需重新训练，计算开销小，能在数分钟内完成大型MoE模型的压缩，为在资源受限设备上部署高性能SMoE模型提供了切实可行的路径。

### 7. 优点

*   **方法创新性**：
    *   提出了**基于专家输出的层次聚类合并**这一新颖且有效的框架，从根本上解决了SMoE模型的参数冗余问题。
    *   证明了**专家平均输出**是衡量专家功能相似性的一个简单、高效且鲁棒的度量。
*   **实用价值高**：
    *   **完全免重训练、任务无关**，可直接应用于任何SMoE模型，无需下游任务数据和额外训练成本。
    *   **可扩展性强**，能有效处理拥有大量专家的模型（如Qwen的60个专家）。
*   **理论分析**：提供了聚类算法有效性的理论证明，从近似误差界定的角度阐述了层次聚类的优势。
*   **实验扎实**：消融实验全面、透彻，清晰地论证了各个设计选择的合理性，并验证了方法的鲁棒性。

### 8. 不足与局限

*   **未修改路由网络**：论文指出，为了保持性能，合并后保留了原始路由权重。这导致虽然计算量（GFLOPs）减少，但**理论上路由器带来的延迟没有得到优化**，这是一个性能和效率的折中。
*   **合并策略探索有限**：虽然证明了聚类质量的重要性，但对更高级的合并策略（如基于优化的合并）探索较少，固化的频率加权合并可能在特定场景下并非最优。
*   **专家输出度量潜在局限**：使用专家输出的平均值作为相似性度量，可能无法捕获专家在不同上下文中的细粒度功能差异。若专家行为对输入变化非常敏感，这种静态表征方式可能有信息损失。
*   **应用场景限制**：该方法主要面向**零样本通用语言能力的保留**，对于需要将模型压缩后用于某个特定下游任务进行微调的场景，其优势可能不如任务相关的剪枝方法。

（完）
