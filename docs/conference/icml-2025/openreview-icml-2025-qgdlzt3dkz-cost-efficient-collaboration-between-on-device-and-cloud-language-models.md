---
title: Cost-efficient Collaboration between On-device and Cloud Language Models
title_zh: 端侧与云端语言模型的成本高效协同
authors: "Avanika Narayan, Dan Biderman, Sabri Eyuboglu, Avner May, Scott Linderman, James Zou, Christopher Re"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=qGDlzt3dKz"
tags: ["query:edge-llm"]
score: 10.0
evidence: 协同设备端小模型与云端大模型，在保持质量的同时降低云端推理成本
tldr: 针对端侧大模型部署中云端推理成本高的问题，提出设备端小模型与云端大模型协同方案，通过改进交互协议使小模型有效理解长文档并选择性查询云端，在保持前沿模型质量的同时显著降低云成本，为边缘场景下的大模型应用提供了经济高效的策略。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1739, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 838, \"height\": 837, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 836, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1759, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1560, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1052, \"height\": 859, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1230, \"height\": 746, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1752, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1073, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1724, \"height\": 1381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-qgdlzt3dkz/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1588, \"height\": 978, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1441, \"height\": 473, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 858, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1553, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1314, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 643, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 592, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1526, \"height\": 696, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1613, \"height\": 654, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1811, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 469, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1578, \"height\": 1523, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1578, \"height\": 1563, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1524, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-qgdlzt3dkz/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1544, \"height\": 387, \"label\": \"Table\"}]"
motivation: 设备端资源有限，直接运行大模型困难，云端推理成本高昂。
method: 设计端云协同协议，设备端模型处理全上下文并选择性调用云端模型。
result: 改进后的协议在保持前沿模型质量的同时，显著降低了云端推理成本。
conclusion: 端云协同是平衡成本与性能的有效策略，有助于大模型在边缘场景的部署。
---

## Abstract
We investigate an emerging setup in which a small, on-device language model (LM) with access to local data collaborates with a frontier, cloud-hosted LM to solve real-world tasks involving financial, medical, and scientific reasoning over long documents. 
*Can a local-remote collaboration reduce cloud inference costs while preserving quality?*
First, we consider a naïve collaboration protocol, coined MINION, where the local and remote models simply chat back and forth. Because only the local model ingests the full context, this protocol reduces cloud costs by 30.4x, but recovers only 87% of the performance of the frontier model.
We identify two key limitations of this protocol: the local model struggles to (1) follow the remote model's multi-step instructions and (2) reason over long contexts. Motivated by these observations, we propose MINIONS, a protocol in which the remote model decomposes the task into easier subtasks over shorter chunks of the document, that are executed locally in parallel. MINIONS reduces costs by 5.7× on average while recovering 97.9% of the remote-only performance. Our analysis reveals several key design choices that influence the trade-off between cost and performance in local-remote systems.

---

## 论文详细总结（自动生成）

好的，基于提供的论文内容，以下是以 Markdown 形式、使用中文生成的结构化、深入、客观的总结。

### **论文核心问题与整体含义**
*   **研究动机与背景**：当前的云端前沿大语言模型（如 OpenAI o1）虽然具备强大的数据密集型推理能力（如处理金融、法律、医疗文档），但其 API 调用成本极为高昂。与此同时，能在个人电脑和智能手机上运行的小型语言模型（1-8B 参数）正在快速进步，但目前主要用于简单任务。
*   **核心问题**：本文探索了一个新兴的协作范式：一个可访问本地数据的**设备端小语言模型**，如何与一个**云端前沿大模型**进行协作，以在解决长文档上的复杂推理任务时，**在保持质量的同时显著降低云端推理成本**。

### **论文提出的方法论**
本文提出了两种设备端与云端的通信协议，核心思想是通过让设备端模型承担大部分上下文处理工作，压缩需要发送到云端的信息，从而减少云端消耗。

1.  **基础协议：MINION**
    *   **核心思想**：一个简单的、无约束的“聊天”协议。设备端模型独享完整的长上下文，云端模型只看到用户查询。二者通过多轮对话协作，云端模型提问，设备端模型基于上下文回答，直到云端模型得出最终答案。
    *   **技术细节**：云端模型在每轮对话中生成结构化输出，包含给设备端模型的消息和“继续/终止”决策。此协议通过将全部上下文留在本地，实现了极高的云成本压缩。

2.  **改进协议：MINIONS**
    *   **核心思想**：为克服 MINION 中设备端模型难以处理多步指令和长上下文的局限，MINIONS 采用了“分而治之”的策略。云端模型充当“编曲者”，将复杂任务分解为一系列简单的子任务，并交由设备端模型在文档的短片段上并行执行。
    *   **关键技术细节与算法流程**：
        *   **分解**：云端模型在不阅读完整文档的情况下，生成一个 **Python 函数**。该函数在本地执行时，能将文档拆分成多个小块，并为每个块生成独立的“作业”（一个简单指令和对应文本块）。
        *   **本地执行与过滤**：设备端模型**并行处理**所有作业。对于不相关或无法回答的作业，模型会主动弃权，从而只将有价值的、过滤后的信息发送回云端。
        *   **云端聚合与决策**：云端模型聚合来自本地的过滤信息，判断是否能回答问题。如果能，则给出最终答案；如果不能，则进入下一轮循环，生成新的代码来创建更精准的作业。
    *   **算法流程本质**：此协议通过云端编写代码来自动化“任务分解-并行执行-结果聚合”的循环，实现了一种可扩展的、高效的人机（模型间）协作模式。

### **实验设计**
*   **数据集**：评估使用了三个需要长文档数据密集型推理的基准测试集：
    1.  **FINANCE BENCH**：金融文档理解与推理。
    2.  **LONG HEALTH**：长篇幅临床文档的问答。
    3.  **QASPER**：针对密集科学论文的问答。
    *   为增加难度，研究者对 LONG HEALTH 和 QASPER 数据集进行了处理，为每个问题混入了其他无关文档，以构造更长的上下文。
*   **对比方法**：
    *   **远程（云端）单独运作**：直接向云端大模型提供完整上下文（性能和成本的上限基准）。
    *   **本地（设备端）单独运作**：只使用本地小模型处理完整上下文（性能的下限基准）。
    *   **MINION 协议**。
    *   **MINIONS 协议**。
*   **评估指标**：
    *   **质量**：准确率。
    *   **成本**：处理单个查询的平均美元成本，基于 GPT-4o 的 API 定价（输入 $2.50/1M tokens，输出 $10.00/1M tokens），并假定本地模型调用免费。

### **资源与算力**
*   **云端模型**：实验主要使用 GPT-4o 作为云端远程模型。
*   **设备端模型**：使用了不同规格的开源小模型，包括 LLAMA 系列（1B、3B、8B）和 QWEN 2.5 系列（1.5B、3B、7B）。
*   **硬件**：用于本地模型延迟测试的硬件是单个消费级 GPU（Nvidia RTX 4090）及专业级 GPU（Nvidia RTX 6000 Ada）。论文没有提及专门的训练过程，其方法论基于提示工程与模型调用编排，因此**未涉及大规模训练算力（如 GPU 时）的描述，也未明确训练所需的具体时长**。

### **实验数量与充分性**
*   **实验数量**：研究进行了大量、细致的实验，旨在全面评估并提出洞见。
    *   **主实验**：在三个数据集上对比了 4 种方法（本地单独、云端单独、MINION、MINIONS），使用了至少 3 种不同大小的本地模型。
    *   **消融与分析实验**：
        1.  **模型选择分析**：探讨了本地模型大小、模型家族和不同远程模型的配对效果，以及对历年模型能力演进的回顾性分析。
        2.  **并行扩展实验**：分别研究了增加子任务数量、增加每个子任务的采样次数、减小文档块大小这三个“旋钮”对性能和成本的影响。
        3.  **顺序通信分析**：研究了增加通信轮次上限和多轮上下文保持策略（简单重试/草稿本）的影响。
        4.  **延迟分析**：在真实硬件上测量了端到端延迟，并提出了一个理论延迟估算框架。
        5.  **其他分析**：与检索增强生成（RAG）进行了对比，并进行了能耗分析、扩展至多模态任务、工具使用和模型微调的初步实验。
*   **充分性与公平性**：实验设计**非常充分、客观且公平**。它在多个标准化的、公开的基准数据集上，通过统一、可量化的成本模型和准确率指标，系统性地对比了所提方法与强有力的基线（尤其是云端全量处理）。大量的消融研究不仅验证了方法的有效性，还深入剖析了协议中各个设计选择如何影响“成本-质量”的权衡，提供了极具价值的工程指导。

### **论文的主要结论与发现**
1.  **MINION 的效率与瓶颈**：该协议能以 30.4 倍的巨大成本削减，恢复前沿模型 87% 的性能。瓶颈在于设备端小模型难以处理复杂的多步指令和超长上下文。
2.  **MINIONS 的优越性**：通过基于代码生成的任务分解和本地并行执行，MINIONS 平均降低 5.7 倍成本，同时恢复远程单独模型 97.9% 的性能，实现了更好的成本-效益平衡。
3.  **本地模型是关键**：MINIONS 的可行性在很大程度上依赖于本地模型的进步。实验表明，从 2023 年到 2024 年中，随着模型能力的提升（如 LLaMA 3.1 的发布），协议的性能才真正接近前沿水平。
4.  **可调节的“成本-质量”权衡**：论文识别了多个关键超参数（如并行任务数、采样数、上下文分块大小、通信轮次），通过调整它们，可以灵活地在成本和准确率之间滑动，以适应不同的应用需求。

### **优点**
*   **问题导向清晰，实用性强**：直接针对当前大模型应用的高昂推理成本这一核心痛点，提出的解决方案具有很高的实际部署价值。
*   **方法论创新且优雅**：MINIONS 协议巧妙地克服了小模型的认知界限。让云端大模型作为“编码者”来编排本地小模型，这种非对称协作方式比单纯的“聊天”更稳健、高效。
*   **分析极其深入透彻**：论文不仅报告了最终结果，还通过详尽的消融实验和理论框架（如从信息瓶颈视角理解模型压缩效率），深刻剖析了系统各组件的作用，为未来的系统设计提供了宝贵洞见。
*   **实验基准坚实**：选择金融、医疗、科研三个复杂领域的真实长文档任务进行评估，使得结论更有说服力和泛化性。

### **不足与局限**
*   **云成本模型的简化**：成本计算基于特定时间点的 API 定价，且假设本地模型调用成本为零（忽略硬件折旧、能耗等）。虽然便于比较，但可能与实际总拥有成本（TCO）存在差异。
*   **任务类型的局限**：尽管覆盖了三个重要领域，但主要聚焦于“基于长文档的问答”。对于其他类型的数据密集型任务（如大规模代码重构、多轮对话等），其有效性有待进一步验证。
*   **对云端模型的依赖**：协议的性能高度依赖于一个强大的云端“编曲者”模型来生成准确的分解代码。如果云端模型在无上下文的情况下理解任务产生偏差，整个流程可能失败。
*   **安全性风险**：云端模型生成代码并在本地执行，引入了潜在的安全隐患。论文虽然在影响声明中提及了此点，但并未在协议设计中提出具体的防御措施。

（完）
