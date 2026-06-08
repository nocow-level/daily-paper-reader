---
title: Value-Guided KV Compression for LLMs via Approximated CUR Decomposition
title_zh: 值引导的键值缓存压缩：基于近似CUR分解
authors: "Ayan Sengupta, Siddhant Chaudhary, Tanmoy Chakraborty"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=klmc4fwPLd"
tags: ["query:edge-llm"]
score: 10.0
evidence: 通过CUR分解压缩KV缓存以降低LLM推理的内存和延迟，直接面向资源受限部署
tldr: 针对大语言模型推理中键值缓存内存瓶颈，本文提出CurDKV，一种基于CUR分解的值导向压缩方法，通过选取关键值对来近似注意力输出主成分，无需仅依赖查询-键注意力分数。实验显示，CurDKV在多种模型上大幅压缩缓存，降低内存和延迟，同时保证生成质量，为Transformer模型在资源受限硬件上的运行提供了有效解决方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-klmc4fwpld/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 648, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-klmc4fwpld/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1302, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-klmc4fwpld/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1289, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-klmc4fwpld/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1445, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-klmc4fwpld/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1385, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-klmc4fwpld/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1443, \"height\": 373, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 600, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1445, \"height\": 1141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 518, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 750, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 750, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1432, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1451, \"height\": 1430, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1376, \"height\": 1347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1378, \"height\": 1082, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1360, \"height\": 765, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1386, \"height\": 1315, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1166, \"height\": 2376, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1259, \"height\": 1060, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1424, \"height\": 1198, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1311, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1426, \"height\": 1199, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1305, \"height\": 656, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1243, \"height\": 1066, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1163, \"height\": 748, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-klmc4fwpld/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1014, \"height\": 836, \"label\": \"Table\"}]"
motivation: LLM自回归推理时KV缓存占用大量内存，现有方法仅依赖注意力分数而忽略值向量的贡献。
method: 提出CurDKV方法，利用CUR矩阵分解计算重要性分数来选择关键值对，以近似注意力输出的主成分。
result: 在多个LLM上实现显著的KV缓存压缩，减少内存开销和推理延迟，并保持生成质量。
conclusion: 该方法为LLM在有限内存设备上的高效推理提供了新的缓存压缩策略，提升端侧部署可行性。
---

## Abstract
Key-value (KV) cache compression has emerged as a critical technique for reducing the memory and latency overhead of autoregressive language models during inference. Prior approaches predominantly rely on query-key attention scores to rank and evict cached tokens, assuming that attention intensity correlates with semantic importance. However, this heuristic overlooks the contribution of value vectors, which directly influence the attention output. In this paper, we propose CurDKV, a novel, value-centric KV compression method that selects keys and values based on leverage scores computed from CUR matrix decomposition. Our approach approximates the dominant subspace of the attention output $\mathrm{softmax}(QK^\top)V$, ensuring that the retained tokens best preserve the model’s predictive behavior. Theoretically, we show that attention score approximation does not guarantee output preservation, and demonstrate that CUR-based selection minimizes end-to-end attention reconstruction loss. Empirically, CurDKV achieves up to $9.6$\% higher accuracy than state-of-the-art methods like SnapKV and ChunkKV under aggressive compression budgets on LLaMA and Mistral, while maintaining compatibility with FlashAttention and Grouped Query Attention. In addition to improved accuracy, CurDKV reduces generation latency by up to 40\% at high compression, offering a practical speed-accuracy tradeoff.

---

## 论文详细总结（自动生成）

好的，作为资深学术论文分析助手，我将对提供的内容进行结构化总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：大型语言模型（LLM）在自回归推理时，需要缓存先前生成词的键（Key）和值（Value）向量，即键值（KV）缓存，以加速注意力计算。然而，KV缓存的内存占用随着序列长度线性增长，成为长上下文推理的主要瓶颈。
*   **核心问题**：现有的KV缓存压缩方法（如SnapKV、H2O）主要依赖查询-键（Query-Key）注意力分数来评估token的重要性，并驱逐得分较低的token。这种做法隐含了一个假设，即注意力分数高，语义重要性就高。
*   **问题所在与本文动机**：论文指出，上述启发式方法忽略了值（Value）向量对最终注意力输出的直接影响。理论分析（引理3.1）和实证观察（图1）均表明，高注意力分数的键并不一定对应着低输出重建损失的键，单纯依赖注意力分数进行压缩无法保证输出质量。
*   **论文的核心贡献**：为了克服这一局限性，本文提出了一种名为**CurDKV**的全新、值导向的KV缓存压缩方法。该方法基于CUR矩阵分解技术，从价值向量的角度直接筛选出最能保持模型预测行为的token，旨在最小化注意力输出的整体重建损失。

### 2. 论文提出的方法论

*   **核心思想**：将对KV缓存的压缩问题转化为一个**CUR矩阵分解**问题。目标是选择原始键矩阵K和值矩阵V的子集（即C和R矩阵），使其能够最好地重构最终的注意力输出矩阵 $\mathrm{softmax}(QK^\top)V$，从而保留模型的预测行为。
*   **关键技术细节——Leverage Score**：
    *   通过计算K和V矩阵的**leverage score**（杠杆分数）来确定各行（即各token）的重要性。
    *   对于一个矩阵，其某一行（或列）的leverage score是该行（或列）在矩阵的奇异向量中的平方$\ell_2$范数。高leverage score意味着该行（或列）对矩阵的主成分贡献更大。
    *   CurDKV分别计算K和V矩阵的leverage score，然后将二者对应元素相乘，得到一个组合分数 $\ell^{(KV)}_j = \ell^{(K)}_j \cdot \ell^{(V)}_j$，以此作为token重要性的最终度量。
*   **算法流程与加速**：
    1.  **随机高斯投影加速**：精确计算leverage score需要执行代价高昂的奇异值分解（SVD）。为了提升效率，CurDKV将K和V矩阵乘以一个随机高斯矩阵G，投影到一个低维空间，然后计算投影后矩阵的行范数平方作为近似的leverage score。
    2.  **预算分配与选择**：根据计算出的组合leverage score，为每个注意力组（头组）保留分数最高的前k个token。同时，考虑到“注意力沉没”现象的存在，强制保留初始的`s`个token。
    3.  **自适应变体**：论文还提出了**AdaCurDKV**，它不按组分配预算，而是在整个层内跨头自适应地选择总体的前k个token，以实现更灵活、更高效的压缩。
    4.  **兼容性**：CurDKV在预填充阶段运行，与FlashAttention和分组查询注意力（GQA）等高效推理技术兼容。

### 3. 实验设计

*   **模型与基准**：
    *   **模型**：在两个主流的指令微调LLM上评估：LLaMA-3.1-8B-Instruct 和 Mistral-7B-Instruct-v0.3。还在Qwen-14B和Qwen-32B上验证了可扩展性。
    *   **数据集/基准**：使用了两个广泛认可的长上下文评测基准：
        *   **LongBench**: 包含16个任务，涵盖单文档QA、多文档QA、摘要、少样本学习和代码补全等。
        *   **Ruler**: 包含8个“大海捞针”子任务，最长上下文为16K，测试模型检索关键信息的能力。
*   **对比方法**：与多种当前最优的KV压缩基线进行比较，包括三类：
    *   **非自适应方法**：SnapKV、ChunkKV、StreamingLLM、KNorm（基于键范数）。
    *   **自适应方法**：Ada-SnapKV。
    *   **注意**：H2O因不原生支持FlashAttention，在长序列上导致内存溢出，未被纳入比较。

### 4. 资源与算力

*   **明确信息**：文中提到，所有基线测试均在**单张NVIDIA A100-80GB GPU**上运行，且H2O方法因在该设置下内存不足而被排除。
*   **未明确信息**：除了提到因H2O报错而使用单张A100-80GB GPU外，论文未详细说明完成所有实验的总GPU数量（可能仅此一张）、运行的总时长或预填充/生成阶段的具体算力消耗细节。文中只在消融实验部分分析了延迟（秒），但没有给出总GPU时等算力指标。

### 5. 实验数量与充分性

论文的实验设计**非常充分且客观**，主要体现在以下几个方面：
*   **多维度评估**：在多个模型（至少4个）、两个综合性长上下文基准、两种压缩策略（静态和自适应，即CurDKV和AdaCurDKV）上进行了评测。
*   **宽范围压缩比**：在30%、50%、70%、90%这4个迥异的压缩比下全面测试，充分验证了方法在不同内存压力下的性能。
*   **丰富的对比**：与至少5种代表性的基线方法（涵盖基于注意力、基于范数、自适应等不同类型）进行了头对头比较，确保了对比的公正性。
*   **深入的消融研究**：
    *   **Leverage Score来源**：对比了仅用键、仅用值、键-值组合三种方式计算分数的影响。
    *   **随机投影的作用**：对比了使用和不使用高斯随机投影的性能与稳定性。
    *   **超参数敏感性**：分析了自适应方法的保护参数 $\alpha$ 和投影维度 $r$ 对结果的影响。
    *   **效率分析**：全面分析了不同方法在预填充和生成阶段延迟、KV缓存内存占用上的表现。
*   **统计显著性检验**：论文报告了Friedman统计量和p值，以证实实验结果（尤其是CurDKV相对于基线的优势）具有统计显著性。

### 6. 论文的主要结论与发现

*   **性能优越**：在LLaMA和Mistral模型上，CurDKV在各种压缩比（尤其激进压缩）下，在LongBench和Ruler基准上的平均准确性均显著超越了所有基线方法。例如，在LLaMA-8B的LongBench上以90%压缩时，CurDKV比SnapKV高出2.0个百分点，比最佳非自适应基线高出更多。
*   **值导向策略更有效**：消融实验证实，在高压缩率下，基于值或键-值组合的leverage score选择，比仅基于键的选择更为鲁棒，验证了“值导向”的核心思想。
*   **出色的检索能力**：在Ruler的长上下文检索任务中，CurDKV保持高性能，表明其能有效保留对语义至关重要的token。
*   **效率与性能的权衡**：虽然预填充阶段因计算leverage score而增加了少量延迟，但在生成阶段，CurDKV由于处理更小的KV缓存，显著降低了延迟（最高达40%），实现了更好的整体推理效率，尤其在长序列场景下优势明显。
*   **良好的可扩展性和兼容性**：在更大模型（Qwen-32B）上优势更加显著，且能无缝适配FlashAttention和GQA等现代LLM推理技术。

### 7. 优点

*   **理论基础坚实**：将KV压缩问题优雅地建模为CUR分解问题，并用理论界限证明了值向量在输出重建中的关键作用，区别于普遍的启发式方法。
*   **方法创新**：首次将leverage score引入KV缓存压缩，创造性地通过组合键值分数来直接优化对最终注意力输出的重建。
*   **高效工程实现**：通过随机高斯投影巧妙地避免了高昂的SVD计算，使得算法在保持效果的同时具备实际可行性。
*   **评估全面扎实**：实验涵盖了多个模型、基准、压缩比和对比方法，并配以消融研究、效率分析和统计检验，结论极具说服力。

### 8. 不足与局限

*   **预填充阶段开销**：CurDKV在预填充阶段引入了额外的计算开销（计算leverage score），导致预填充延迟有所增加，这在一些对首token延迟要求极高的场景下可能是一个劣势。
*   **静态选择策略**：该方法在预填充阶段一次性决定保留哪些token，是一种静态策略。在生成过程中，当新的查询需求出现时，它无法动态调整缓存以应对信息需求的变化。
*   **低压缩率下增益不明显**：消融研究显示，在低压缩率（如30%）下，不同leverage score计算方式（键、值、组合）的差距不大，CurDKV的优势相比基线可能不如高压缩率下那样显著。
*   **特定架构下的潜在弱点**：文中指出，在Mistral模型的某些任务上，由于滑动窗口注意力减少了头的特化，自适应策略有时会表现不佳，这可能暗示该方法在与特定注意力机制结合时需要更多考量。

（完）
