---
title: "MoE-Infinity: Efficient MoE Inference on Personal Machines with Sparsity-Aware Expert Cache"
title_zh: MoE-Infinity：利用稀疏感知专家缓存在个人机器上实现高效的MoE推理
authors: "Leyang Xue, Yao Fu, Zhan Lu, Chuanhao Sun, Luo Mai, Mahesh K. Marina"
date: 2025-01-09
pdf: "https://openreview.net/pdf?id=BL7WMLJKZM"
tags: ["query:edge-llm"]
score: 10.0
evidence: 稀疏感知专家缓存使MoE-LLM在有限GPU内存的个人机上高效推理
tldr: MoE-Infinity利用MoE模型在个人机器单用户场景下的激活稀疏性，设计稀疏感知专家缓存，动态管理有限GPU内存中的专家，从而实现无需高端硬件的MoE-LLM高效推理。在资源受限环境下，该系统显著提升了推理速度并降低了内存占用。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 702, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 821, \"height\": 275, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 834, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 836, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 853, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 781, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 777, \"height\": 241, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-bl7wmljkzm/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 784, \"height\": 264, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-bl7wmljkzm/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 857, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bl7wmljkzm/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 136, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-bl7wmljkzm/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 763, \"height\": 247, \"label\": \"Table\"}]"
motivation: 个人机器GPU内存有限，无法高效运行大型MoE-LLM。
method: 设计稀疏感知专家缓存，追踪并缓存经常激活的专家到GPU内存。
result: 在个人机器上实现MoE-LLM快速推理，内存占用显著降低。
conclusion: MoE-Infinity为在个人设备上部署MoE大模型提供了有效解决方案。
---

## Abstract
This paper presents MoE-Infinity, an efficient MoE inference system designed for personal machines with limited GPU memory capacity. The key idea for MoE-Infinity is that on personal machines, which are often single-user environments, MoE-based LLMs typically operate with a batch size of one. In this setting, MoE models exhibit a high degree of activation sparsity, meaning a small number of experts are frequently reused in generating tokens during the decode phase. Leveraging this idea, we design a sparsity-aware expert cache, which can trace the sparse activation of experts during inference and carefully select the trace that represents the sparsity pattern. By analyzing these selected traces, MoE-Infinity guides the replacement and prefetching of the expert cache, providing 2.7–13.7× per-token latency improvements over numerous state-of-the-art systems, including vLLM, Ollama, DeepSpeed and BrainStorm across various MoE models (DeepSeek and Mixtral) when handling different LLM tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：混合专家（MoE）架构的大语言模型（LLM）参数量巨大（可达数百GB），个人机器通常仅搭载单张消费级GPU（24–48GB显存），必须依赖“卸载”（offloading）技术，即在主机内存中保存完整模型，按需将激活的专家参数加载到GPU。
- **核心痛点**：现有推理系统（如vLLM、DeepSpeed、Ollama等）在卸载场景下的专家缓存设计不佳，预测不准，导致PCIe总线I/O阻塞和GPU空闲时间过长，解码延迟（TPOT）居高不下。
- **问题定义**：如何在个人单卡、批量大小为1（单用户）的条件下，通过更智能的专家缓存与预取机制，大幅降低MoE模型的推理延迟。

### 2. 论文提出的方法论
- **核心思想**：利用单请求解码阶段专家激活的**稀疏性和请求内重用偏斜**。同一请求内少数专家被频繁重用，但跨请求后分布趋于均匀。据此，缓存应在请求级别追踪稀疏激活模式，而不是依赖全局频率或简单的依赖关系。
- **关键技术细节**：
  - **专家激活矩阵（EAM）**：将每层每个专家被路由的令牌数记录为 \( L \times E \) 矩阵。分为迭代级（iEAM）和请求级（rEAM，累积计数）。
  - **专家激活矩阵集合（EAMC）**：维护一个固定容量的历史rEAM集合，代表不同的激活模式（组）。通过余弦距离匹配当前iEAM，找到最相似的历史模式。
  - **激活预测（PredictEAM）**：根据匹配到的rEAM进行聚合（逐行求和归一化），并乘以层接近度衰减因子 \( 1 - (i-l)/L \)，得到预测激活概率（pEAM）。
  - **缓存替换算法**：当缓存满时，计算每个已缓存专家的优先级，综合考虑pEAM中的概率、层衰减（优先保留浅层专家），驱逐优先级最低的专家。
  - **预取优化**：利用pEAM提前异步加载下一层可能被激活的专家，隐藏I/O延迟。
- **流程示意**：论文以图5和图6举例，说明相比于LRU和统计计数方法，稀疏感知缓存如何避免驱逐即将被重用的专家，提高命中率。

### 3. 实验设计
- **模型**：DeepSeek-V2-Lite（31GB）、Switch-128x0.2B、NLLB-128x0.4B（220GB）、Mixtral-8x7B（120GB）、Arctic-128x4B（900GB）。
- **数据集**：覆盖290个LLM任务，来自BIGBench（166任务）、FLAN（66任务）、MMLU（58任务），包含推理、问答、翻译等。
- **对比基线**：DeepSpeed-Inference、Llama.cpp、Mixtral-Offloading、vLLM、BrainStorm（重新实现）。
- **评估指标**：每输出令牌时间（TPOT，即解码延迟）；长上下文场景下延迟增长；缓存容量与工作负载切换的鲁棒性。

### 4. 资源与算力
- 所有推理实验在**单张NVIDIA RTX A5000（24GB）**上完成，通过PCIe 4.0（32GB/s）连接主机内存。
- 主机内存配置根据模型大小不同：Switch用64GB，NLLB用256GB，DeepSeek用32GB，Mixtral用128GB，Arctic用1TB。
- 论文不涉及模型训练，仅为推理系统，未提及训练算力。

### 5. 实验数量与充分性
- **端到端性能**：5种模型 × 多种任务的平均延迟对比（图7），共记录各系统的TPOT。
- **长上下文压力测试**：DeepSeek在\(2^{12}\sim2^{17}\)令牌长上下文下的延迟表现（图8），覆盖了KV缓存增长对缓存空间的挤压。
- **微基准测试**：
  - EAMC容量从1到120的延迟影响（图9）。
  - 工作负载切换恢复实验（表3）：包括相同数据集内任务切换、跨数据集切换，记录恢复到低延迟所需请求数的分布。
- **充分性**：对比基线全面，覆盖主流卸载推理引擎；多种规模与结构的MoE模型；大量LLM任务确保了泛化性；消融实验分析了核心参数（EAMC大小）和动态适应性。整体实验设计合理且客观。

### 6. 论文的主要结论与发现
- MoE-Infinity在个人单卡上实现了**2.7–13.7倍**的解码延迟提升，尤其在专家数量多、激活稀疏的模型（如Switch、NLLB、Arctic）上优势显著。
- 长上下文下，MoE-Infinity因将KV缓存常驻GPU而更稳定，性能下降小于vLLM等需要卸载KV缓存的系统。
- 仅需很小容量的EAMC（约3%请求量）即可覆盖绝大多数激活模式，且能快速适应任务和数据集切换（平均30–50个请求即可恢复低延迟）。
- 稀疏感知缓存的关键在于请求级匹配历史模式，而非全局频率或逐层依赖，此为现有缓存方法的根本缺陷。

### 7. 优点
- **精准定位**：明确识别出个人设备、批量1场景下的激活稀疏性，以此为缓存设计基础，针对性强。
- **方法创新**：提出请求级激活模式追踪（EAM/EAMC）和基于相似度匹配的在线预测，比传统的LRU、统计计数更贴合MoE的动态稀疏特性。
- **工程全面**：结合层衰减、预取、位置感知替换等多种优化，形成完整的稀疏感知缓存方案。
- **实验扎实**：模型种类多、任务覆盖面广、基线丰富，并开源代码，具有可复现性。

### 8. 不足与局限
- **高批处理场景不适**：设计基于batch size=1，未讨论多请求批处理时的行为，可能不适用于云端多用户合并场景。
- **对极少数专家的模型提升有限**：在Mixtral（8专家/层）上提升仅1.4倍，稀疏性收益减弱。
- **额外开销**：EAMC的存储和匹配计算尽管成本低（每层查询约21–226微秒），在超低延迟要求下仍需验证。
- **依赖静态路由器**：专家激活组模式来自于预训练路由器的特性，若模型微调或路由器动态变化，历史EAMC可能失效，需重新积累，适应性未彻底验证。
- **聚类算法未落地**：文中虽给出理论容量上界，但因计算复杂度未采用聚类优化EAMC，仍使用简单替换策略，可能留有性能空间。
- **硬件实验单一**：仅在PCIe 4.0 A5000上测试，未展示更高带宽（如PCIe 5.0）或不同GPU代际的影响。

（完）
