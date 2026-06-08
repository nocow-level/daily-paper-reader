---
title: On-the-Fly Adaptive Distillation of Transformer to Dual-State  Linear Attention for Long-Context LLM Serving
title_zh: 面向长上下文大模型服务的Transformer至双状态线性注意力在线自适应蒸馏
authors: "Yeonju Ro, Zhenyu Zhang, Souvik Kundu, Zhangyang Wang, Aditya Akella"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=pqHWzviKKN"
tags: ["query:edge-llm"]
score: 9.0
evidence: 自适应蒸馏将大型Transformer知识迁移到高效双状态线性注意力学生模型，用于长上下文服务
tldr: 针对Transformer长上下文推理的计算和内存开销问题，首先提出双状态线性注意力DSLA，保持历史上下文和近期信息，缓解短程偏置；进而设计在线自适应蒸馏框架DSLA-Serve，根据动态负载将Transformer知识蒸馏到DSLA模型，在效率和精度间取得平衡。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 851, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 780, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 845, \"height\": 226, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 855, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 821, \"height\": 314, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 855, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1587, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1557, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1239, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 830, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1460, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqhwzvikkn/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1766, \"height\": 322, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1740, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 852, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 742, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 812, \"height\": 118, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1745, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqhwzvikkn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 863, \"height\": 157, \"label\": \"Table\"}]"
motivation: Transformer在处理长序列时计算和内存成本高昂，现有线性注意力方法精度下降。
method: 提出双状态线性注意力设计，并通过在线自适应蒸馏从Transformer教师模型迁移知识。
result: 实现了长上下文推理的高效与高精度权衡。
conclusion: DSLA及其自适应蒸馏为长上下文LLM服务提供了一种高效解决方案。
---

## Abstract
Large language models (LLMs) excel at capturing global token dependencies via self-attention but face prohibitive compute and memory costs on lengthy inputs. While sub-quadratic methods (e.g., linear attention) can reduce these costs, they often degrade accuracy due to overemphasizing recent tokens. In this work, we first propose *dual-state linear attention* (**DSLA**), a novel design that maintains two specialized hidden states—one for preserving historical context and one for tracking recency—thereby mitigating the short-range bias typical of linear-attention architectures. To further balance efficiency and accuracy under dynamic workload conditions, we introduce 
DSLA-*Serve*, an online *adaptive distillation* framework that progressively replaces Transformer layers with DSLA layers at inference time, guided by a sensitivity-based layer ordering. 
DSLA-*Serve* uses a chained fine-tuning strategy to ensure that each newly converted DSLA layer remains consistent with previously replaced layers, preserving the overall quality. Extensive evaluations on commonsense reasoning, long-context QA, and text summarization demonstrate that 
DSLA-*Serve* yields **2.3×** faster inference than Llama2-7B and **3.0×** faster than the hybrid Zamba-7B, while retaining comparable performance across downstream tasks. Our ablation studies show that DSLA’s dual states capture both global and local dependencies, addressing the historical-token underrepresentation seen in prior linear attentions.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将使用中文、以 Markdown 形式，对这篇论文进行结构化、深入、客观的总结。

### **1. 论文的核心问题与整体含义**

*   **核心问题**：大型语言模型（LLMs）在长序列推理任务中存在严重的计算和内存瓶颈。
    *   **计算开销**：标准自注意力机制的复杂度为 O(T²)，计算量随输入长度的平方增长。
    *   **内存开销**：存储键值（KV）缓存所需的内存随序列长度线性增长，极大限制了长上下文服务的可扩展性。
    *   **现有方案不足**：线性注意力等亚二次方方法虽然降低了开销，但存在“近因偏差”（Recency Bias），即过度关注近期词元而忽视历史信息，导致在需要长程依赖的任务上精度下降。同时，静态的混合架构无法根据动态负载灵活地在效率和精度间做权衡。
*   **整体含义**：本文旨在解决上述挑战，提出一种能够**根据实时系统负载，动态、在线地将高成本的Transformer层自适应地替换为高效、高精度的线性注意力层**的推理框架，从而在几乎不损失性能的前提下，大幅提升长上下文LLM服务的效率。

### **2. 论文提出的方法论**

论文方法论主要包含两个核心部分：**双状态线性注意力（DSLA）模块**和**在线自适应蒸馏框架（DSLA-Serve）**。

*   **双状态线性注意力（DSLA）**
    *   **核心思想**：针对单状态线性注意力（如GLA）的“近因偏差”问题，设计两个专门化的隐藏状态，分别用于捕获全局历史信息和近期局部信息。
    *   **关键技术细节**：
        *   **双状态更新**：在每一时间步，分别用两个不同的门控矩阵（G₁_t, G₂_t）更新历史状态 S₁_t 和近期状态 S₂_t。公式为 `S₁_t = G₁_t ⊙ S₁_{t-1} + kᵀ_t v_t`， `S₂_t = G₂_t ⊙ S₂_{t-1} + kᵀ_t v_t`。
        *   **状态混合输出**：最终的注意力输出由两个状态加权混合得到：`o_t = q_t (γ·S₁_t + (1-γ)·S₂_t)`。其中γ是一个可学习的、每层独立的系数。
        *   **状态专门化**：为了使两个状态各司其职，引入了一个**对比正则化项** `L_cont = sim(G₁_t, G₂_t)`。通过最小化两个门控矩阵的相似度，迫使它们学习到差异化的上下文模式。总损失函数为蒸馏损失与对比损失之和：`L = L_dist + λ L_cont`。
*   **在线自适应蒸馏框架（DSLA-Serve）**
    *   **核心思想**：在推理阶段，根据实时系统资源状况（如GPU内存压力），动态地将Transformer的自注意力层逐步替换为预先蒸馏好的DSLA层，实现“即用即付”的弹性效率-精度权衡。
    *   **关键技术流程**：
        1.  **灵敏度排序**：离线评估模型中每一层对线性化的“灵敏度”（使用注意力熵作为度量，熵越低表示该层注意力越集中，对线性化越不敏感），并按灵敏度从低到高排序。
        2.  **链式微调**：为保证层替换的兼容性，采用一种递进式蒸馏策略。即按照灵敏度排序，先蒸馏并固定第一个DSLA层，然后在此新架构上蒸馏并固定第二个DSLA层，以此类推。这确保了后续层在训练时能看到前面层已被替换的状态，避免了训练-推理架构失配。
        3.  **自适应转换**：在线推理时，当监测到系统负载超过阈值，DSLA-Serve便从灵敏度最低的层开始，将Transformer层转换为对应的DSLA层。转换过程持续进行，直到内存压力得到缓解或性能面临不可接受的风险。此策略优先应用于长上下文请求，因为它们是KV缓存膨胀的主要来源。

### **3. 实验设计**

*   **使用数据集/场景**：
    *   **长上下文理解**：Multi-Document QA (HotpotQA, 2WikiMQA), Code Understanding (LCC, Repobench), Few-shot Learning (TREC, Samsum, TriviaQA)。
    *   **语言建模**：WikiText-2, Lambada。
    *   **文本摘要**：CNN/DailyMail, XSum。
    *   **常识推理（短上下文）**：lm-eval 套件（WG, HS, PIQA, ARC-E, ARC-C, MMLU, LogiQA）。
    *   **系统性能**：基于增强的Azure推理服务跟踪数据模拟真实负载。
*   **Benchmark 与方法**：
    *   **教师模型**：Llama2-7B。
    *   **对比方法**：
        *   **纯二次方模型**：Llama2-7B。
        *   **纯线性复杂度模型**：RetNet-6.7B, GLA-7B, Mamba-7B。
        *   **混合模型**：Zamba-7B。
        *   **其他线性化方法**：LoLCATs。
    *   **自身变体**：DSLA（25%层转换）和 DSLA（50%层转换）。

### **4. 资源与算力**

*   **GPU型号与数量**：
    *   微调7B模型及延迟测量：**4块NVIDIA A100 (80GB) GPU**。
    *   下游任务评估、端到端性能测试及消融研究：**NVIDIA A6000 (49GB) GPU**。
*   **训练时长**：使用1.6B词元，在4块A100上微调7B模型的单个层大约需要**5小时**。这相比从头训练（如Llama 2的858天）成本极低，仅为0.07%。

### **5. 实验数量与充分性**

*   **实验数量**：论文进行了相当全面的实验，涵盖超过10个下游任务、4类对比模型、多组自身配置，并从精度、延迟、吞吐、内存等多个维度进行评估。
*   **充分性评估**：
    *   **任务覆盖充分**：涵盖了长上下文理解、短上下文推理、文本摘要和语言建模等典型LLM评测场景，能较全面反映模型性能。
    *   **对比客观公平**：选择了当时主流的纯线性、纯二次方和混合模型作为基线，并与同是线性化蒸馏方法的LoLCATs进行了对比，确保了比较的公平性。
    *   **分析深入**：包含了对注意力模式、状态权重γ、灵敏度度量、状态数量和架构泛化能力等的详细消融研究和分析，为自己的每个设计选择提供了有力支撑。
    *   **系统验证真实**：通过重放真实的Azure服务跟踪数据来验证系统端到端性能，使其实用性论证更具说服力。

### **6. 论文的主要结论与发现**

1.  **双状态设计有效**：DSLA通过历史和近期双状态设计，成功缓解了单状态线性注意力的“近因偏差”，能更忠实地近似标准自注意力模式。
2.  **性能显著提升**：与Llama2-7B相比，DSLA-Serve实现了 **2.29倍**的端到端延迟降低；与混合模型Zamba-7B相比，加速比达到**3.0倍**，同时在下游任务上保持相当的精度。
3.  **长上下文优势**：在多文档QA等需要长程依赖的任务上，25%层数被转换的DSLA模型甚至**超越了原始的纯自注意力模型**，同时显著降低了内存占用。
4.  **自适应策略成功**：DSLA-Serve框架能够有效地根据动态负载进行自适应转换，在不牺牲服务质量的前提下，大幅提升系统效率和资源利用率。

### **7. 优点**

*   **创新性强**：提出了双状态线性注意力和在线自适应蒸馏两个新颖点，系统地解决了线性注意力模型的固有缺陷和静态模型架构的局限性。
*   **实用价值高**：DSLA-Serve直接面向真实的LLM动态服务场景，通过在线自适应调整，提供了一种非常灵活的“效率-精度”折中方案，具有很强的落地潜力。
*   **论证严谨扎实**：
    *   从动机分析（近因偏差可视化、服务负载波动）到方法设计（双状态、对比正则、链式微调），再到实验验证，逻辑链条完整。
    *   消融研究透彻，充分证明了注意力熵作为灵敏度指标的有效性，以及双状态设计的充分性。

### **8. 不足与局限**

*   **模型加载开销**：论文承认，DSLA-Serve需要将Transformer和DSLA两组权重都加载到内存中，这会增加模型的权重的内存占用。虽然提出了通过offloading/prefetching技术来缓解，但这会引入实现复杂性和潜在的延迟。
*   **转换上限**：经验表明，当超过75%的层被转换后，模型性能开始显著下降，这对于极端追求效率的场景可能是一个限制。
*   **批量推理开销**：在混批推理时，不同请求可能需要不同类型的层，这会导致路径分叉和重新批处理（Re-Batching）的开销。尽管论文认为KV缓存节省的效果占主导，但这仍是一个需要考虑的工程复杂性。
*   **缺乏更多模型架构验证**：实验主要集中在基于Llama架构的模型上，虽然也在小模型Phi-1.5上进行了验证，但其在其他流行架构（如纯Mamba、GPT-NeoX等）上的泛化效果尚不明确。

（完）
