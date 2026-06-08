---
title: "DuoGPT: Training-free Dual Sparsity through Activation-aware Pruning in LLMs"
title_zh: DuoGPT：面向LLM的训练无关双稀疏激活感知剪枝
authors: "Ruokai Yin, Yuhang Li, Donghyun Lee, Priyadarshini Panda"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=PjbpL4brUb"
tags: ["query:edge-llm"]
score: 9.0
evidence: 结合非结构化权重剪枝与激活稀疏性以降低LLM部署的存储和计算开销
tldr: DuoGPT 解决大语言模型因高存储和计算开销难以部署的问题，提出一种训练无关的双稀疏框架，通过结合非结构化权重剪枝和激活稀疏性构建 dual-sparse 工作负载，并利用激活感知校准与输出残差校正保持精度，在十亿参数级LLM上实现高压缩比且保持性能。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-pjbpl4brub/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1096, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-pjbpl4brub/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1433, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-pjbpl4brub/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 572, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-pjbpl4brub/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1434, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-pjbpl4brub/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1130, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-pjbpl4brub/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1290, \"height\": 805, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1423, \"height\": 752, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1458, \"height\": 895, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1453, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 553, \"height\": 161, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 157, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 736, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 596, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1452, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1459, \"height\": 1611, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1128, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1192, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1242, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-pjbpl4brub/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1278, \"height\": 225, \"label\": \"Table\"}]"
motivation: LLM 部署受限于高内存和计算开销，现有剪枝方法忽略运行时激活稀疏性。
method: 提出 DuoGPT 框架，将激活稀疏性重新解释为动态结构化权重稀疏，结合非结构化剪枝与激活感知OBC校准构建双稀疏负载。
result: 在十亿参数级 LLM 上实现高压缩比，保持模型精度并优化 GPU 执行效率。
conclusion: DuoGPT 为 LLM 在资源受限环境下的高效部署提供了一种训练无关的压缩方案。
---

## Abstract
Large language models (LLMs) deliver strong performance but are difficult to deploy due to high memory and compute costs. While pruning reduces these demands, most methods ignore activation sparsity observed at runtime. We reinterpret activation sparsity as dynamic structured weight sparsity and propose DuoGPT, a unified framework that constructs dual-sparse (spMspV) workloads by combining unstructured weight pruning with activation sparsity. To preserve accuracy, we extend the Optimal Brain Compression (OBC) framework with activation-aware calibration and introduce output residuals from the dense model as correction terms. We further optimize the solution for efficient GPU execution, enabling scalability to billion-parameter LLMs. Evaluations on LLaMA-2 and LLaMA-3 show that DuoGPT outperforms state-of-the-art structured pruning methods by up to 9.17\% accuracy at an iso-speedup of 1.39$\times$ compared to the baseline dense model. Code is available at GitHub.

---

## 论文详细总结（自动生成）

好的，请查收以下基于您提供的论文内容生成的结构化中文总结。

### **1. 论文的核心问题与整体含义**
*   **研究动机与背景**：大语言模型（LLM）虽然性能强大，但其高昂的显存占用和计算量（如部署LLaMA-2-70B需约150GB显存，解码单个token需60 GFLOPs计算）给实际部署带来了巨大挑战。模型剪枝是一种常见的压缩手段，但现有方法大多忽略了LLM在运行时自然产生的“激活稀疏性”（Activation Sparsity），即激活矩阵中存在大量零值。
*   **核心问题**：如何有效结合“非结构化权重稀疏”和“动态激活稀疏”，构建一种对GPU加速友好的“双稀疏”（dual-sparse）工作负载，从而同时降低LLM的显存存储和计算开销，并在此过程中最大程度地保持模型精度。

### **2. 论文提出的方法论**
*   **核心思想**：
    *   **重新解读激活稀疏性**：将推理时的动态激活稀疏性，重新解释为一种动态的、结构化的权重稀疏，即对于零值激活对应的权重行，可以直接跳过，不参与计算。
    *   **构建双稀疏工作负载**：将上述动态结构化稀疏与非结构化权重剪枝相结合，形成“稀疏矩阵-稀疏向量”（spMspV）的运算模式，在减少显存带宽、SRAM加载、计算核心运算三个层面均获得收益。
*   **关键技术细节**：
    *   **激活感知剪枝校准**：DuoGPT将激活稀疏性直接纳入剪枝校准过程。输入校准数据被动态剪枝为稀疏版本\(\hat{X}\)，剪枝的目标是最小化剪枝后模型与原始密集模型输出的差异。
    *   **引入输出残差校正**：为解决单纯使用稀疏校准数据导致的信息损失，该方法受“非对称校准”启发，引入了原始密集模型输出\(\tilde{X}\)与稀疏校准输出\(\hat{X}\)之间的**输出残差\(\mathbf{r} = \mathbf{W}(\tilde{X} - \hat{X})\)**作为校正项，并将其整合到损失函数中。
    *   **扩展OBC框架**：DuoGPT基于最优脑压缩（OBC）框架，推导出考虑激活稀疏性和输出残差的误差函数\(\mathcal{L}\)及最优权重更新\(\Delta \mathbf{w}\)的闭式解，从而在迭代剪枝过程中动态补偿因权重移除和激活稀疏引入的误差。
    *   **高效GPU算法实现**：针对闭式解中涉及的大规模矩阵运算，作者通过假设已知剪枝掩码、海森矩阵同步、引入Cholesky分解等方法，将剪枝分数\(\mathbf{S}\)的计算复杂度从\(O(nmk^2+nk^3)\)显著降低，提出了一套可高效向量化预计算的算法伪代码（Algorithm 1），使其能够扩展到数十亿参数的模型。

### **3. 实验设计**
*   **数据集/场景**：
    *   校准数据集：从C4训练集中随机选取128个长度为2048 token的样本。
    *   评估数据集：使用WikiText2评估困惑度（PPL）；使用PIQA, HellaSwag, WinoGrande, ARC-e, ARC-c, OBQA, BoolQ共7个数据集进行零样本（0-shot）任务评估。
*   **Benchmark模型**：实验主要针对LLaMA-2（7B, 13B, 70B）和LLaMA-3（8B, 70B）系列模型。在后续消融中也涵盖了Mistral, Qwen2, OPT等架构。
*   **对比方法**：
    *   **非结构化剪枝方法**：在双稀疏（W50% + X50%）和2：4半结构化稀疏（W2：4 + Xdense）两种设置下，与SparseGPT和Wanda进行了全面比较。
    *   **结构化剪枝方法**：与ShortGPT, 2SSP, BlockPruner, SliceGPT在近似加速比下进行比较。
    *   **激活稀疏方法**：与R-Sparse, TEAL, CATS等进行了比较或兼容性测试。

### **4. 资源与算力**
*   **硬件配置**：所有校准和实验均在80GB显存的NVIDIA A100 GPU上执行。对于70B模型的零样本评估，使用了2块A100 GPU并启用了offloading技术。
*   **计算开销**：DuoGPT的标定过程效率较高。例如，根据表1的数据，校准一个LLaMA-3-70B模型大约需要**2.28 GPU小时**，一个LLaMA-2-7B模型约需0.22 GPU小时。

### **5. 实验数量与充分性**
*   论文进行了相当数量的实验来验证其方法的有效性和鲁棒性。
    *   **多模型尺度实验**：覆盖了7B/8B, 13B, 70B等不同参数规模的模型。
    *   **多稀疏度消融实验**：系统评估了从30%到65%不等、共5个等级的双稀疏率下的性能变化，并与两个基线方法进行了详尽对比。
    *   **方法内对比**：全面比较了与非结构化剪枝、结构化剪枝、纯激活稀疏化等不同技术路线的代表性方法。
    *   **兼容性研究**：探索了与激活阈值技术（TEAL）、权重量化（INT8/INT4）等其他压缩方法的正交叠加效果。
    *   **额外分析**：包括了不同LLM架构的泛化性测试、校准数据量和序列长度的影响分析、算法效率分析等。
*   整体来看，实验设计全面，对比公平，在多个维度上证明了DuoGPT的优势。

### **6. 论文的主要结论与发现**
*   DuoGPT能够成功构建双稀疏LLM，在内存、数据传输和计算量上均获得收益。
*   相比于其他双稀疏基线（SparseGPT, Wanda），DuoGPT在相同稀疏度下（如50%权重+50%激活）能显著提升模型性能（困惑度和零样本准确率），且性能优势在极高稀疏度（60%+）下更为明显。
*   在等速度比约为1.39倍的情况下，DuoGPT的精度比最先进的结构化剪枝方法高出9.17%。
*   与激活稀疏化方法相比，DuoGPT在等精度下可实现最高1.97倍的模型体积压缩。
*   DuoGPT提出的校准方法是高效且可扩展的，能够在合理的时间内完成超大规模模型的压缩。

### **7. 优点**
*   **视角新颖**：创造性地将动态激活稀疏性重新定义为动态结构化权重稀疏，为解决LLM部署效率问题提供了新思路。
*   **方法创新且完备**：提出的DuoGPT框架不仅有扎实的理论推导（OBC框架扩展、闭式解），还考虑到了实际工程落地，给出了高效的GPU算法实现。
*   **性能卓越**：在多个模型、多个尺度和任务上，DuoGPT均展现出超越同类基线方法的性能，尤其在极端稀疏条件下具有明显优势。
*   **工程价值高**：校准过程无需重新训练，且能与量化、阈值激活修剪等其它压缩技术正交结合，为实际部署提供了灵活且强大的解决方案。

### **8. 不足与局限**
*   **缺乏定制化GPU内核**：论文明确指出，目前并未实现一个完整的双稀疏（spMspV）GPU内核来充分发挥其潜力。当前测速主要利用激活稀疏性（spVM），展示了效率提升的下限，但未能完全证实其理论加速优势。
*   **双稀疏仅应用于线性层**：目前的工作仅在线性层中引入双稀疏，尚未覆盖注意力层。如何与KV缓存剪枝等技术结合是未来的研究方向。
*   **激活稀疏模式简化**：在校准和评估中，主要采用基于量级的动态稀疏化和均匀的稀疏度分配，未对层间差异化的最优激活稀疏度进行搜索，这可能限制了性能的上限。
*   **部分实验可复现性细节**：由于大模型校准耗时较长，文中未提供多轮实验的误差棒，仅通过固定随机种子来保证可复现性。

（完）
