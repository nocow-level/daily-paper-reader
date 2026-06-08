---
title: "Oracle-MoE: Locality-preserving Routing in the Oracle Space for Memory-constrained Large Language Model Inference"
title_zh: Oracle-MoE：在Oracle空间中保持局部性的路由用于内存受限大语言模型推理
authors: "Jixian Zhou, Fang Dong, Ruijun Huang, Hengjie Cao, Mengyi Chen, Yifeng Yang, Anrui Chen, Mingzhi Dong, Yujiang Wang, Dongsheng Li, David A. Clifton, Qin Lv, Rui Zhu, Chun Zhang, Fan Yang, Tun Lu, Ning Gu, Li Shang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=wn6WHREK9k"
tags: ["query:edge-llm"]
score: 10.0
evidence: 利用MoE架构在内存有限的边缘设备上部署大语言模型
tldr: 针对现有MoE架构在内存受限边缘设备上因专家切换频繁导致高延迟的问题，通过分析令牌间专家激活的时间不一致性，提出Oracle-MoE架构，利用局部性保持路由减少专家交换，显著降低推理延迟，实现在有限内存下的高效大语言模型推理。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 822, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 821, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 839, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1649, \"height\": 268, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1744, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 862, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 434, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 870, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 871, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1320, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1377, \"height\": 272, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1320, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1381, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1337, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1388, \"height\": 275, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1329, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wn6whrek9k/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1383, \"height\": 289, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-wn6whrek9k/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1663, \"height\": 510, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wn6whrek9k/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 690, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wn6whrek9k/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1283, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-wn6whrek9k/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1060, \"height\": 274, \"label\": \"Table\"}]"
motivation: MoE理论上适合边缘设备，但现有架构因专家激活时间不一致导致过多专家交换，推理延迟不可接受。
method: 提出Oracle-MoE架构，通过保持局部性的路由策略在Oracle空间中进行专家选择，减少专家交换需求。
result: 在内存受限设备上显著降低了大语言模型推理的延迟，实现了高效部署。
conclusion: Oracle-MoE通过优化路由解决了MoE在边缘设备上的关键效率瓶颈。
---

## Abstract
Mixture-of-Experts (MoE) is widely adopted to deploy Large Language Models (LLMs) on edge devices with limited memory budgets.
Although MoE is, in theory, an inborn memory-friendly architecture requiring only a few activated experts to reside in the memory for inference, current MoE architectures cannot effectively fulfill this advantage and will yield intolerable inference latencies of LLMs on memory-constrained devices. 
Our investigation pinpoints the essential cause as the remarkable temporal inconsistencies of inter-token expert activations, which generate overly frequent expert swapping demands dominating the latencies. 
To this end, we propose a novel MoE architecture, Oracle-MoE, to 
fulfill the real on-device potential of MoE-based LLMs. 
Oracle-MoE route tokens in a highly compact space suggested by attention scores, termed the *oracle space*, to effectively maintain the semantic locality across consecutive tokens to reduce expert activation variations, eliminating massive swapping demands. 
Theoretical analysis proves that Oracle-MoE is bound to provide routing decisions with better semantic locality and, therefore, better expert activation consistencies. 
Experiments on the pretrained GPT-2 architectures of different sizes (200M, 350M, 790M, and 2B) and downstream tasks demonstrate that without compromising task performance, our Oracle-MoE has achieved state-of-the-art inference speeds across varying memory budgets, revealing its substantial potential for LLM deployments in industry.

---

## 论文详细总结（自动生成）

# 论文总结：《Oracle-MoE: 在 Oracle 空间中保持局部性的路由用于内存受限大语言模型推理》

## 1. 核心问题与整体含义（研究动机与背景）
- **背景**：大语言模型（LLM）在边缘设备（如手机、嵌入式平台）上部署面临严格的内存限制。Mixture-of-Experts（MoE）架构理论上是一种内存友好的选择，因为每次推理只需激活少数几个专家，其余专家可以在需要时动态加载。
- **痛点**：当前 MoE 模型在内存受限设备上会产生极高的推理延迟，主要是由于连续 token 之间的专家激活模式极度稀疏且时间不一致（temporal inconsistencies），导致频繁的专家加载/卸载（expert swapping），其 I/O 开销占了总延迟的 50%–85%（图 1）。
- **根本原因**：现有 MoE 的路由（routing）基于 token embedding，而 token embedding 包含大量 token 身份（token-identity）信息，相邻 token 之间变化剧烈，导致专家选择频繁变动。
- **目标**：在不牺牲下游任务性能的前提下，大幅降低因专家交换引起的推理延迟，使 MoE 真正适用于内存受限的边缘场景。

## 2. 方法论
### 2.1 核心思想
- **语义局部性（Semantic Locality）**：边缘场景下连续 token 通常具有相近的高层语义（如同一用户输入的连续语句）。论文提出不在原始的 token 嵌入空间进行路由，而是在一个能更好保持语义局部性的紧凑空间——**Oracle Space**——中进行路由。
- **语义分组（Semantic Groups）**：利用注意力矩阵中高的注意力得分（attention scores）来识别共享高级语义的 token 群组。同一群组内的 token 被认为具有相似的高层语义，其 token 嵌入可分解为共享的高层语义部分 + 独立的 token 身份部分。

### 2.2 关键技术细节与流程
1. **构建 Oracle Space**:
   - 在预训练 warm-up 后，对一批数据进行前向传播，提取注意力分数矩阵。
   - 根据注意力分数阈值 ε 构建有向图：若 token i 对 token j (i > j) 的注意力分数 > ε，则在图中添加边 i ← j。语义群组被定义为该图的极大连通子集（Def. 2）。
   - 对每个语义群组，计算其所有 token 嵌入的平均值，作为该群组的语义群组嵌入（Def. 3）；所有群组嵌入的集合构成 Oracle Space。
   - 用 SVD 降维以提高计算效率。

2. **Oracle-MoE 路由**:
   - **训练阶段**：在 Oracle Space 上用 K-means 聚类得到 K 个簇（K 等于原 MoE 专家数）。对于每个输入 token，根据其所属的语义群组，将整个群组的 token 分配给相同簇对应的专家，而非基于单个 token 的嵌入。
   - **推理阶段**：prefill 阶段与训练一致；decode 阶段基于 KV cache 持续更新语义群组归属，将新 token 分配到相应簇的专家，从而最大程度减少相邻 token 间的专家变化。

3. **理论保证**：
   - 定义连续语义差异（Consecutive Semantic Difference, CSD）来衡量专家选择在连续 token 上的变化量。
   - 定理 1 证明：在高概率下，基于 token 嵌入的路由产生的 CSD 严格大于基于 Oracle Space 的路由产生的 CSD。即 Oracle Space 路由天然具有更低的专家激活不一致性，从而减少专家交换开销。

### 2.3 额外优化：专家预测
- 利用浅层（第一层）的嵌入预测深层各层的专家激活，实现预加载，进一步提升速度（预测准确率 85%–95% vs. 传统方法的 40%–60%），可将专家加载延迟再降低 10%–15%。

## 3. 实验设计
- **硬件平台**：NVIDIA Jetson Xavier NX（384-core GPU，8 GiB GPU memory）。
- **模型规模**：基于 GPT-2 架构，构建不同规模的 MoE 模型：195M（2 MoE 层×4 专家）、295M（4×8）、729M（8×16）、2.06B（9×24）。每层激活 1 个专家。
- **对比方法**：主要对比 Switch Transformer（token-level MoE）结合三种专家交换策略：FIFO、LRU、SwapMoE。
- **任务与数据集**：
  - 预训练：OpenWebText。
  - 下游任务：QA（TriviaQA）、分类（GLUE, MAG, SciCite）、摘要（XSum）。
- **评估指标**：
  - 专家激活变化图（Expert Activation）。
  - 内存-延迟曲线（Memory-latency curve）：不同可用内存下处理单条数据的平均时间。
  - 首 token 延迟（First token latency）。
  - 下游任务性能（零样本/微调后指标）。

## 4. 资源与算力
- 文中未明确列出全部训练所用 GPU 型号、数量、总训练时长。只提到实验平台是 NVIDIA Jetson Xavier NX（用于推理测试）。训练阶段的算力开销（如“训练阶段开销”一节）仅给出与 baseline 的相对比较：cluster analysis 约 4 分钟/层，且认为可以忽略不计。因此具体训练算力需求并不透明。

## 5. 实验数量与充分性
- **规模覆盖**：4 种不同大小的模型（195M 到 2.06B），涵盖多种下游任务类型，提供了较全面的不同规模场景。
- **对比 Baselines**：与 Switch Transformer 结合三种经典/先进的加载策略对比，还包含与 full model 住留在内存的对比。
- **消融与深入分析**：包含延迟构成拆解、不同内存预算下的曲线、首 token 延迟对比、下游任务性能表、激活一致性统计、语义组可视化、专家预测实验等。
- **扩展实验**：还在 DeepSeekMoE-16B 和 Qwen1.5-MoE-A2.7B 等大型公开 MoE 模型上验证了语义局部性和语义分组方法的普适性（附录 B.2）。亦测试了细粒度专家模型（类似 DeepSeek-MoE 设定）。
- **公平性**：对比时使用同等架构和专家数量，Oracle-MoE 与 Switch Transformer 共享训练数据，且交换策略在两类模型上均采用相同机制。结果展示了 Oracle-MoE 在各种策略下均大幅领先。
- **局限**：未在数十亿参数以上的更大规模最新 MoE 模型（如 Mixtral 8×7B）上进行直接对比，仅在 GPT-2 自家的 MoE 扩展上验证。因此，对更大规模的泛化性尚未完全确定。

## 6. 主要结论与发现
- Oracle-MoE 通过维持语义局部性显著减少了相邻 token 间的专家激活变化，从而大幅降低专家交换引发的 I/O 延迟。
- 在内存紧张时，传统 MoE 延迟可能上升 15–30 倍，而 Oracle-MoE 在仅 25% 完整内存下仅增加约 3 秒延迟；在内存提升至 50% 全量时几乎无额外延迟。
- 下游任务性能未受损，甚至部分任务略有提升，推测得益于专家专注于高级语义子集，减少了冗余。
- 专家预测模块进一步压缩了加载延迟，且 Oracle Space 下的预测准确率远高于 token-level 路由。

## 7. 优点
- **问题定位精准**：通过定量分析揭示专家交换是边缘推理延迟的主要瓶颈，并将其归因于 token 级别路由的语义不连续性。
- **方案新颖且理论扎实**：创新性地利用注意力分数构建 Oracle Space 并在此空间进行路由，从理论上证明其 CSD 更低，设计有完整的定理支撑。
- **实用性强**：方法无需对硬件或交换策略进行侵入性修改，且与现有 KV cache 机制兼容；额外计算开销极小。
- **实验充分且工业场景贴近**：在真实边缘硬件上评估，覆盖多种预算、多种任务，展示了实质性的延迟降低。
- 方法具有通用潜力，在多种大模型上验证了语义分组的可提取性。

## 8. 不足与局限
- **模型规模受限**：实验基于 GPT-2 扩展的 MoE，最大 2B 参数，未在百亿、千亿参数级别的现代 MoE LLM 上（如 Mixtral、DeepSeek-V2）验证，对大规模部署的有效性有待进一步证实。
- **训练成本信息缺失**：缺少具体的训练 GPU 资源、时间、能耗数据，难以评估预训练阶段的投入产出比。
- **依赖注意力得分质量**：Oracle Space 的构建依赖于注意力矩阵反映高级语义的假设；当模型注意力机制不成熟或任务特殊性较强时，方法可能失效。
- **阈值和聚类数等超参数**：文中对阈值 ε 的选择、聚类算法对性能的敏感性缺乏详细消融（虽提到 K 从 4 到 32 表现稳定，但未给出全面分析）。
- **边缘设备单一**：推理仅在 Jetson Xavier NX 上测试，未在更广泛边缘设备（手机、树莓派等）验证，结论的泛化性有限。
- **负载变化场景**：虽然测试了拼接不同来源句子的“高话题变化”场景，但更多极端或非自然语言文本（代码、公式）的适用性未探。

（完）
