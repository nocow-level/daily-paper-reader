---
title: "R2R: Efficiently Navigating Divergent Reasoning Paths with Small-Large Model Token Routing"
title_zh: R2R：通过大小模型令牌路由高效导航分叉推理路径
authors: "Tianyu Fu, Yi Ge, Yichen You, Enshu Liu, Zhihang Yuan, Guohao Dai, Shengen Yan, Huazhong Yang, Yu Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=DpeJYRFRQY"
tags: ["query:edge-llm"]
score: 9.0
evidence: 利用蒸馏小模型和令牌路由器选择性地调用大模型，实现推理效率与精度的平衡，体现知识迁移。
tldr: 大语言模型推理开销大，而小语言模型推理快但推理路径易偏离。R2R发现大部分生成令牌差异中性，仅少数令牌导致路径分叉，为此提出神经令牌路由器，让小模型处理多数令牌，仅对关键分叉令牌调用大模型，在几乎不损失精度的前提下大幅降低推理开销。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 230, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1444, \"height\": 235, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1451, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1349, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 648, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1424, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1350, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 682, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 690, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-dpejyrfrqy/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1353, \"height\": 358, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1325, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1378, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1453, \"height\": 675, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 750, \"height\": 573, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1456, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1433, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1252, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 959, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1079, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 989, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1124, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 726, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1282, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 975, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 793, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1078, \"height\": 730, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1201, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 750, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-dpejyrfrqy/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1331, \"height\": 279, \"label\": \"Table\"}]"
motivation: 小语言模型推理高效但无法跟随大语言模型的推理路径，导致性能下降。
method: 设计神经令牌路由器，识别推理路径分叉关键令牌，动态路由至大或小模型。
result: 实验表明R2R在保持大模型推理质量的同时，显著降低了推理延迟和计算开销。
conclusion: R2R提供了一种高效的大小模型协作推理范式，为LLM轻量化部署提供了新方案。
---

## Abstract
Large Language Models (LLMs) achieve impressive reasoning capabilities at the cost of substantial inference overhead, posing substantial deployment challenges. Although distilled Small Language Models (SLMs) significantly enhance efficiency, their performance suffers as they fail to follow LLMs' reasoning paths. Luckily, we reveal that only a small fraction of tokens genuinely diverge reasoning paths between LLMs and SLMs. Most generated tokens are either identical or exhibit neutral differences, such as minor variations in abbreviations or expressions. Leveraging this insight, we introduce **Roads to Rome (R2R)**, a neural token router that selectively utilizes LLMs only for these critical, path-divergent tokens, while leaving the majority of token generation to the SLM. We also develop an automatic data generation pipeline that identifies divergent tokens and generates token-level routing labels to train the lightweight router. We apply R2R to combine R1-1.5B and R1-32B models from the DeepSeek family, and evaluate on challenging math, coding, and QA benchmarks. With an average activated parameter size of 5.6B, R2R surpasses the average accuracy of R1-7B by 1.6×, outperforming even the R1-14B model. Compared to R1-32B, it delivers a 2.8× wall-clock speedup with comparable performance, advancing the Pareto frontier of test-time scaling efficiency.

---

## 论文详细总结（自动生成）

好的，以下是根据论文《R2R: Efficiently Navigating Divergent Reasoning Paths with Small-Large Model Token Routing》生成的结构化中文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景与动机**：
    *   大型语言模型（LLM）在复杂推理任务上性能强大，但其“测试时扩展”（如生成冗长的思维链）带来了巨大的推理开销，部署成本高昂。
    *   通过知识蒸馏得到的小型语言模型（SLM）虽能大幅提升推理效率，但其生成的推理路径常与LLM产生偏差，导致显著的性能下降（例如，性能下降4-5倍）。
    *   一项关键观察是，SLM与LLM在逐令牌生成时，绝大多数（约89%）令牌是**相同**的，而剩余的**不同**令牌中，很多只是**中性**的表达差异（如缩写），只有一小部分（约5%）是真正导致推理路径分叉的**分叉令牌**。
*   **核心问题与整体含义**：
    *   **核心问题**：“能否仅通过替换分叉令牌，让SLM遵循LLM的推理路径？”如果可以，就能在保持LLM高质量推理的同时，获得SLM的高效率。
    *   **整体含义**：本文提出了 **R2R** 方法，一种在SLM和LLM之间进行**令牌级路由**的框架，旨在以最小的计算代价（仅对关键分叉点使用LLM）实现接近大模型的推理性能，从而推动测试时缩放效率的帕累托前沿。

### 2. 论文提出的方法论

R2R的核心思想是让SLM承担大部分令牌生成，仅在可能导致推理路径分叉的关键令牌上调用LLM进行“纠正”。该方法论包含一个自动化的**数据标注流程**和一个轻量级的**神经路由器**。

*   **模型偏好标注（数据生成）**：
    *   **问题形式化**：将推理过程定义为一系列贪婪解码的令牌预测。目标是定义一个路由函数，在每个解码步选择SLM（-θs）或LLM（-θl），以在保证与LLM生成质量一致的前提下最小化总计算成本。
    *   **路径跟随策略**：为解决巨大搜索空间，提出一种贪心的**句子级路径跟随**标注方法。
        1.  **识别差异**：用SLM对LLM的响应进行预填充，找出SLM预测与LLM不同的令牌位置。
        2.  **LLM续写与验证**：对于每个差异点，分别从SLM和LLM的预测令牌出发，用LLM继续生成直到句子结束（以句号等为界），形成两个续写序列。
        3.  **判定分叉/中性**：利用另一个强大的LLM（如Qwen-72B）作为验证器，比较两个续写序列。如果差异导致意思、逻辑或结论改变，则标注为**分叉**（首选项LLM）；否则标注为**中性**（首选项SLM）。相同的令牌自然首选SLM。
    *   该流程生成了包含“SLM”或“LLM”偏好的令牌级路由标签，用于后续路由器训练。
*   **令牌级神经路由器设计**：
    *   **架构**：一个仅含**5600万参数**的轻量级6层前馈网络（FFN），用于预测当前令牌是否为分叉令牌。
    *   **路由输入**：融合三类来自SLM的即时信号：
        1.  SLM的**输出logits**（取前100个值），捕捉预测不确定性。
        2.  当前预测**令牌的嵌入**，捕捉令牌稀有度信息。
        3.  SLM的**最后一层隐藏状态**，提供额外的语义上下文。
    *   **路由方案**：在推理时，SLM每生成一个令牌，路由器便根据上述输入输出一个分叉概率。若概率超过预设阈值，则激活LLM，利用其并行预填充能力快速生成一个新的纠正令牌，并以此为基础继续让SLM解码，实现即时纠正，避免像投机解码那样的回滚开销。

### 3. 实验设计

*   **核心设置**：以DeepSeek-R1-Distill-Qwen-1.5B作为SLM，DeepSeek-R1-Distill-Qwen-32B作为LLM。
*   **评估基准**：使用了三类具有挑战性的推理基准：
    *   **数学**：AIME 2024-2025
    *   **代码**：LiveCodeBench (2024-08至2025-01)
    *   **问答**：GPQA-Diamond
*   **对比方法**：
    *   **蒸馏缩放基线**：不同参数量的独立蒸馏模型（如R1-7B, R1-14B）。
    *   **查询级路由（QR）**：如RouteLLM框架下的相似度加权（QR-SW）、矩阵分解（QR-MF）、BERT分类器（QR-BERT）和Llama-3-8B分类器（QR-LLM）。
    *   **投机解码方法**：EAGLE2和HASS。
*   **评估指标**：
    *   **准确率**：各基准上的任务性能。
    *   **效率**：硬件无关指标——“平均激活参数量 (¯M)”和“总代价 (C = ¯M × 平均输出令牌数)”；硬件相关指标——实际“生成速度”和“延迟”。
    *   **帕累托前沿**：准确率与效率之间的最优权衡关系。

### 4. 资源与算力

*   **数据生成**：使用 **8 块 NVIDIA A800-80GB GPU**，耗时约 **2.3 天**（共约56小-时，总计448 GPU时），生成了760万个令牌级路由标签。
*   **推理评估**：所有方法（包括R2R和所有基线）的端到端推理性能均在 **2 块 NVIDIA A800-80GB GPU** 上进行评估 ，使用SGLang框架和Tensor并行。
*   文中明确描述了数据生成和评估阶段的算力细节。

### 5. 实验数量与充分性

*   **实验数量**：论文进行了广泛且充分的实验。
    *   **主实验**：在3个不同领域的基准上，与3大类（蒸馏、查询路由、投机解码）共超过10种方法进行了性能与效率的全面比较。
    *   **消融实验**：针对路由目标（分叉 vs. 简单不同）和路由器输入特征（逐步移除logits、令牌嵌入）进行了4组消融研究。
    *   **泛化性实验**：验证了R2R在**不同模型家族**（Qwen3，包括MoE模型）、**非训练领域任务**（对话、哲学）以及**随机采样**（top-p / temperature）下的有效性。
    *   **深入分析**：展示了LLM使用率在思考过程和不同“念头”阶段的分布，对比了与投机解码的计算和内存访问量，分析了路由阈值的影响、SLM-LLM组合选择、以及系统的失效模式。
*   **公平性与客观性**：
    *   所有对比方法均基于统一的SGLang推理框架，并在相同GPU上进行测试，保证了硬件效率对比的公平性。
    *   路由器在固定验证集上选定阈值后，**路由权重在所有评估中保持不变**，仅通过调整阈值来控制效率-性能权衡，避免了针对特定基准的调优偏差。

### 6. 论文的主要结论与发现

*   **极致效率与性能平衡**：R2R以平均**56亿**激活参数（LLM使用率11%-15%），超越了**70亿**参数的R1-7B模型**1.6倍**的平均准确率，甚至超越了**140亿**参数的R1-14B模型。相比32B大模型，在取得可比性能的同时，实现了**2.8倍**的实际推理加速。
*   **新帕累托前沿**：R2R在准确率-效率的权衡曲线上，全面优于蒸馏模型和查询级路由方法，确立了新的帕累托最优。
*   **路由目标至关重要**：消融实验证明，容忍中性差异、仅路由**分叉**令牌，比直接路由所有与LLM不同的令牌，在同等计算代价下性能大幅提升。
*   **路由行为可解释**：路由器学到了可解释的模式，如在每个“念头”段落的开端和结尾更多地依赖LLM，表明这些位置对于设定思考方向和决定是否深入/切换思路更为关键。

### 7. 优点

*   **粒度巧妙**：首次在令牌级别实现精细化路由，准确抓住了性能损失的关键（分叉令牌），而非粗粒度的查询级切换或过于严苛的令牌级一致（投机解码）。
*   **自动化数据流水线**：提出的“路径跟随”数据标注策略，通过并行操作和前缀缓存，高效且自动地生成了高质量的训练标签，避免了昂贵的人工标注。
*   **路由器设计强大且高效**：利用SLM即时的不确定性信号（logits、令牌嵌入、隐藏状态）预测分叉，轻量级路由器几乎不增加推理时延，且无需任何回滚操作，天然优于投机解码的回滚机制。
*   **泛化能力强**：证明了该方法可泛化至不同模型家族、不同任务领域及随机解码策略，展现了作为通用方法的潜力。

### 8. 不足与局限

*   **采样方法支持有限**：主要针对贪婪解码进行了优化和验证，虽然展示了在随机采样下的初步扩展，但探索不够深入，可能影响其通用性。
*   **标注策略的局部性**：句子级路径跟随策略可能在某些情况下（如SLM重组段落但仍为有效推理）产生误报，虽然不会降低性能，但会造成不必要的LLM调用，降低效率上限。
*   **长推理循环问题**：主要失败模式之一是R2R在遇到训练时未见的重复推理模式时，可能无法在最大令牌数限制内完成推理。
*   **系统级优化**：论文提到在SGLang框架下的实现仍有进一步优化的空间，以达到更优的端到端成本效益。

（完）
