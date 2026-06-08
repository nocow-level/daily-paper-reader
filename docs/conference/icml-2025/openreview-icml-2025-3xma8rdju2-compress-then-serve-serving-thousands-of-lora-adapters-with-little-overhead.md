---
title: "Compress then Serve: Serving Thousands of LoRA Adapters with Little Overhead"
title_zh: 先压缩后服务：以极低开销服务数千个LoRA适配器
authors: "Rickard Brüel Gabrielsson, Jiacheng Zhu, Onkar Bhardwaj, Leshem Choshen, Kristjan Greenewald, Mikhail Yurochkin, Justin Solomon"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=3XMA8RDJu2"
tags: ["query:edge-llm"]
score: 8.0
evidence: 联合压缩LoRA适配器，以低内存服务数千个微调LLM
tldr: 针对服务大量LoRA微调LLM时频繁加载导致内存不足的问题，提出将LoRA联合压缩为共享基和缩放矩阵的算法，并可聚类分组，从而以极低开销同时服务数千个适配器。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-3xma8rdju2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xma8rdju2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 862, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xma8rdju2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 842, \"height\": 572, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xma8rdju2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 828, \"height\": 558, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xma8rdju2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1765, \"height\": 578, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xma8rdju2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 871, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3xma8rdju2/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 871, \"height\": 444, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 756, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1773, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1204, \"height\": 913, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1206, \"height\": 1233, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 396, \"height\": 2286, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 350, \"height\": 2297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 296, \"height\": 2308, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1399, \"height\": 540, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1396, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1775, \"height\": 1751, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1774, \"height\": 1602, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1775, \"height\": 1751, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1775, \"height\": 1608, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1775, \"height\": 1751, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1775, \"height\": 1644, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1774, \"height\": 1535, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1774, \"height\": 1669, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1770, \"height\": 517, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1771, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 816, \"height\": 638, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 816, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1785, \"height\": 566, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3xma8rdju2/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1787, \"height\": 678, \"label\": \"Table\"}]"
motivation: 数千个LoRA无法全部驻留GPU内存，频繁加载卸载影响实时服务。
method: 通过共享基与缩放矩阵联合压缩LoRA，并学习适配器聚类。
result: 实现以低内存开销同时服务大量个性化模型。
conclusion: 压缩策略显著提升了LoRA适配器的服务效率与规模。
---

## Abstract
Fine-tuning large language models (LLMs) with low-rank adaptations (LoRAs) has become common practice, often yielding numerous copies of the same LLM differing only in their LoRA updates. This paradigm presents challenges for systems that serve real-time responses to queries that each involve a different LoRA. Prior works optimize the design of such systems but still require continuous loading and offloading of LoRAs, as it is infeasible to store thousands of LoRAs in GPU memory. To mitigate this issue, we investigate the efficacy of compression when serving LoRAs. We propose a method for the joint compression of LoRAs into a shared basis paired with LoRA-specific scaling matrices. We extend our algorithm to learn clusters of LoRAs that are amenable to joint compression, allowing it to scale gracefully to large LoRA collections. Our experiments with up to 1000 LoRAs demonstrate that compressed LoRAs preserve performance while offering major throughput gains in realistic serving scenarios with over a thousand LoRAs, maintaining 80\% of the throughput of serving a single LoRA.

---

## 论文详细总结（自动生成）

好的，以下是根据论文《Compress then Serve: Serving Thousands of LoRA Adapters with Little Overhead》生成的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：在大语言模型（LLM）的实际部署中，使用低秩适配（LoRA）对单个基础模型进行定制化微调已成为主流。然而，当需要为数千个用户同时提供个性化服务时，系统面临巨大挑战：大量LoRA适配器无法同时驻留在有限的GPU内存中，必须频繁地在CPU与GPU之间进行加载和卸载，导致服务吞吐量严重下降。
*   **整体含义**：本文旨在通过压缩LoRA适配器集合来解决上述内存瓶颈，从而在保持模型性能的同时，显著提升多LoRA场景下的推理服务效率，实现以接近服务单个LoRA的吞吐量来服务上千个适配器。

### 2. 论文提出的方法论

论文的核心思想是将LoRA适配器集合进行联合压缩，并将其形式化为一个重构问题，通过寻找共享的子空间来减少LoRA特有的参数量。

*   **联合对角化（Joint Diagonalization, JD）**
    *   **核心思想**：将多个LoRA的乘积`B_iA_i`近似分解为`UΣ_iV^T`的形式。其中，`U`和`V`是所有LoRA共享的基底矩阵，而`Σ_i`是每个LoRA特有的缩放矩阵（可为全矩阵或对角阵）。这样，`U`和`V`可以预加载在GPU上，服务时只需根据请求动态加载极小的`Σ_i`矩阵。
    *   **算法类型**：
        *   **JD-Full**: 约束`U`和`V`为正交矩阵，`Σ_i`为无约束的全矩阵。
        *   **JD-Diag**: `U`和`V`无约束，但`Σ_i`被约束为对角矩阵，以实现极致的参数精简。两种方法均通过交替最小二乘法进行优化。

*   **聚类（Clustering）**
    *   **核心思想**：当适配器数量`n`变得非常庞大且多样时，单一共享基底的秩`r`需要随之增大，这会增加`Σ_i`的参数量。为此，论文提出将`n`个LoRA划分为`k`个聚类`C_j`，每个簇内部独立进行联合压缩，拥有专属于该簇的共享基底`U_j`和`V_j`。
    *   **算法流程**：采用交替优化策略，一步基于当前簇的分配优化各簇的`(U_j, V_j, Σ_i)`以最小化重构误差，另一步则重新将每个LoRA分配到能使其重构误差最小的簇中。

### 3. 实验设计

*   **数据集与场景**：
    *   **训练/评估任务**：基于**Mistral-7B-Instruct-v0.2** 基础模型，在1000个多样化自然语言指令任务上训练了1000个秩为16的LoRA适配器。选择其中10个任务进行一致的性能评估。
    *   **推理场景**：使用莎士比亚十四行诗数据集作为输入，模拟异步到达的请求，测试系统在服务大量独特LoRA时的吞吐量。

*   **评估基准（Benchmark）**：
    *   **性能基准**：未压缩的原始LoRA和基础模型本身。
    *   **系统吞吐量基准**：集成Punica优化内核的先进LLM服务引擎**vLLM**的多LoRA模式。这是一个强有力的基线，因为它已采用了先进的调度和非阻塞CPU-GPU通信等优化。

*   **对比方法**：
    *   **独立SVD压缩（r-SVD）**：对每个LoRA乘积`B_iA_i`独立进行降秩SVD。
    *   **模型合并（TIES-Merging）**：将所有LoRA合并为一个单一的适配器。
    *   在不同LoRA数量（10， 50, 100, 500, 1000）和不同压缩秩（r）下，对JD-Full、JD-Diag及其聚类版本进行了全面对比。

### 4. 资源与算力

论文明确指出，吞吐量实验是在一块**NVIDIA H100 80GB GPU**上进行的。为了模拟GPU资源受限但仍需服务大量LoRA的实际情况，实验特意将GPU内存占用限制在**40%**。论文未提及完整的压缩算法训练总时长。

### 5. 实验数量与充分性

实验设计非常充分、客观且公平。

*   **实验组数庞大**：在1000个任务规模上进行实验，并针对不同LoRA数量（从10到1000）、不同压缩方法、不同秩`r`、不同聚类数目`k`进行了详尽的性能（Rouge-L等）和系统吞吐量测试。附录中包含大量实验结果表格。
*   **实验充分**：
    *   **性能-重构误差相关性分析**：深入探讨了重构误差与下游任务性能之间的非线性关系，发现适度有损压缩甚至能提升泛化能力。
    *   **多维度评估**：不仅评估任务性能（Rouge-L， Rouge-1， 准确匹配），还评估了系统吞吐量、GPU内存占用和参数节省比。
    *   **隐私消融实验**：初步探究了联合压缩是否会造成任务间信息泄露。
    *   **收敛性分析**：对比了算法不同迭代次数对结果的影响。
*   **客观公平**：在吞吐量对比中，通过调整vLLM基线允许驻留GPU的LoRA数量，确保其总GPU内存占用量与压缩方法的内存占用量精确匹配，实现了计算资源公平的比较。

### 6. 论文的主要结论与发现

*   **压缩即增益**：联合压缩（JD）不仅能大幅减少参数（超过75%），在大多数情况下其性能甚至**优于**未压缩的原始LoRA，展现出良好的泛化能力。
*   **吞吐量显著提升**：配合聚类方法，在服务超过1000个LoRA时，压缩方案能够将服务吞吐量提升至vLLM多LoRA基线的**1.6倍**，并能保持服务单个无LoRA基础模型约80%的吞吐量。
*   **聚类是关键**：当服务数百上千个LoRA时，聚类对于维持高性能至关重要。论文给出了在不同LoRA数量下选择压缩参数的实用建议。
*   **重构误差是高效代理指标**：计算高效的重构误差可以作为指导超参数选择的有效指标，避免耗时的LLM评估。经验表明，重构误差低于0.6的设置能可靠地保留99%以上的原始性能。

### 7. 优点

*   **方法论创新**：提出了联合对角化与聚类结合的压缩范式，与现有工作（如Punica， S-LoRA）正交，可以无缝集成，从另一个维度解决了多LoRA服务的内存瓶颈。
*   **理论与实验结合**：提供了关于重构误差的理论界限，并在大规模实验上验证了理论分析与实际性能的关联。
*   **实用性强**：给出了明确的超参数选择流程，并计划开源1000+个训练好的LoRA及其代码，可直接指导工业界实践。
*   **基线强且对比公平**：与高度优化的vLLM多LoRA引擎在相同GPU内存预算下对比，结论更具说服力。

### 8. 不足与局限

*   **压缩算法离线开销**：论文虽然高效，但仍需要作为预处理步骤周期性运行。当有全新LoRA持续加入时，需要将其先作为未压缩适配器服务，存在服务延迟。
*   **实验模型的单一性**：实验仅基于Mistral-7B这一款模型，对其他结构或规模的LLM泛化性有待验证。
*   **隐私分析的初步性**：虽然通过消融实验未发现信息泄露，但未就模型反转、成员推断等更复杂的隐私攻击进行深入防御性分析。
*   **CUDA内核优化潜力**：论文提到其实现只对vLLM内核进行了最小化调整，这意味着通过进一步优化自定义内核，吞吐量可能有更大的提升空间。

（完）
