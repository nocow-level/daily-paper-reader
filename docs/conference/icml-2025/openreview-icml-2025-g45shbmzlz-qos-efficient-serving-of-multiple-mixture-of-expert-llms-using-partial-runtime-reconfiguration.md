---
title: QoS-Efficient Serving of Multiple Mixture-of-Expert LLMs Using Partial Runtime Reconfiguration
title_zh: 使用运行时部分重配置的多专家混合大模型服务质量高效服务
authors: "HamidReza Imani, Jiaxin Peng, Peiman Mohseni, Abdolah Amirany, Tarek El-Ghazawi"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=g45SHBmZLz"
tags: ["query:edge-llm"]
score: 9.0
evidence: 通过专家合并和运行时部分重配置在单个GPU上高效服务多个MoE大模型，降低内存占用
tldr: 针对多租户场景下多个微调MoE大模型服务的高内存需求问题，提出基于相似度的专家合并策略，跨模型共享相似专家以降低整体内存占用，并引入运行时部分重配置机制动态替换非专家层以保证输出质量。该方法有效压缩了模型内存足迹，实现了在单GPU上高效服务多个MoE-LLM的目标。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-g45shbmzlz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 697, \"height\": 856, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g45shbmzlz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1548, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g45shbmzlz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1548, \"height\": 698, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g45shbmzlz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1614, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-g45shbmzlz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1680, \"height\": 672, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-g45shbmzlz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 878, \"height\": 1032, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g45shbmzlz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 1494, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g45shbmzlz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g45shbmzlz/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 731, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g45shbmzlz/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1676, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-g45shbmzlz/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1239, \"height\": 729, \"label\": \"Table\"}]"
motivation: 多租户环境中多个微调MoE-LLM的高内存需求限制了传统虚拟化技术的有效性。
method: 提出相似度驱动的专家合并减少内存，并通过运行时部分重配置保证输出质量。
result: 实现单GPU上多个MoE-LLM的高效服务，显著降低内存占用。
conclusion: 所提系统通过专家合并与动态重配置，解决了多模型部署的内存瓶颈，提升了服务效率。
---

## Abstract
The deployment of mixture-of-experts (MoE) large language models (LLMs) presents significant challenges due to their high memory demands. These challenges become even more pronounced in multi-tenant environments, where shared resources must accommodate multiple models, limiting the effectiveness of conventional virtualization techniques. This paper addresses the problem of efficiently serving multiple fine-tuned MoE-LLMs on a single GPU. We propose a serving system that employs \textit{similarity-based expert consolidation} to reduce the overall memory footprint by sharing similar experts across models. To ensure output quality, we introduce \textit{runtime partial reconfiguration}, dynamically replacing non-expert layers when processing requests from different models. As a result, our approach achieves competitive output quality while maintaining throughput comparable to serving a single model, and incurs only a negligible increase in time-to-first-token (TTFT). Experiments on a server with a single NVIDIA A100 GPU (80GB) using Mixtral-8x7B models demonstrate an 85\% average reduction in turnaround time compared to NVIDIA's multi-instance GPU (MIG). Furthermore, experiments on Google's Switch Transformer Base-8 model with up to four variants demonstrate the scalability and resilience of our approach in maintaining output quality compared to other model merging baselines, highlighting its effectiveness.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题背景**：混合专家模型（MoE）大语言模型（LLM）参数量巨大（如Switch Transformer有1.6万亿参数，占3.1TB显存），部署时需要将参数分割在CPU内存与GPU显存之间，导致频繁的主机到设备拷贝，严重拖慢推理管线。在**多租户环境**（multi-tenant）下，多用户需同时使用各自微调的MoE-LLM，而单一GPU显存有限，传统虚拟化技术效率低下。
- **现有方案局限**：
  - **时间共享**：请求不同模型时需完整卸载当前模型并加载另一模型，耗时可达2分钟，延迟不可接受。
  - **空间共享（如NVIDIA MIG）**：将GPU切分为独立实例，限制了每个实例的可用带宽和计算单元，导致通信开销加倍、吞吐量下降。
- **动机与目标**：设计一种能在一张GPU上高效服务**多个微调MoE-LLM**的推理系统，期望维持接近单模型服务的吞吐量，仅轻微影响首token延迟（TTFT）和输出质量。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **整体思路**：利用不同微调模型的**专家相似性**进行合并减少显存占用，并借助**运行时部分重配置**动态切换非专家层以保证特定模型的输出质量。
- **相似度驱动的专家合并（Similarity-Based Expert Consolidation）**：
  - **距离度量**：将每个专家的权重展开为一维张量，计算**L2距离**作为专家间相似度。对于>2个模型，每个专家位置的相似度为所有模型两两组合距离之和。
  - **统一布局生成**：按相似度对专家位置排序（最相似者优先），采用**轮询（round-robin）方式**从各模型中选取专家加载到GPU。例如，两个模型时，奇数排名位置加载模型A的专家，偶数加载模型B的专家。
  - **初始加载（Algorithm 1）**：先加载非专家层（随机选择某模型），然后按上述布局加载专家，直至GPU显存填满。生成一个专家映射表（`map`），记录每个位置专家来源于哪个模型。
- **运行时部分重配置（Runtime Partial Reconfiguration）**：
  - **非专家层动态替换**：非专家层参数量约3GB，通过PCIe传输仅需约1.2秒。当新请求的目标模型与当前加载的非专家层模型不一致时，仅替换非专家层参数，而不动专家部分。
  - **推理编排（Algorithm 2）**：处理每个token时，若门控网络选中的专家已存在于GPU，直接使用（可能来自其他模型）；若缺席，则从CPU内存加载目标模型的对应专家，保护输出质量。
- **整体效果**：合并减少显存占用，动态替换非专家层在保持本模型特定能力的同时，将通信开销限制在极小的一次性交换上。

### 3. 实验设计：数据集/场景、benchmark、对比方法

- **模型与平台**：
  - **主要模型**：Mixtral-8x7B-v0.1（两变体：base和Instruct），Switch Transformer Base-8（1个base和3个社区微调变体）。
  - **硬件**：单颗NVIDIA A100 80GB GPU，AMD 16核MILAN CPU，PCIe Gen4互联。
- **服务质量（QoS）评估**：
  - **工作负载模拟**：请求到达服从两个独立的**泊松过程**（每个模型一个），请求提示20个token，生成25个token。
  - **指标**：平均TTFT、平均周转时间、吞吐量（处理请求数/分钟）。
  - **对比基线**：
    - 单模型服务（将两个模型的请求混合，总到达率是单模型的两倍）。
    - NVIDIA MIG（将A100分为两个等大实例，各自服务一个模型）。
- **输出质量评估**：
  - **数据集**：WikiText2、PTB、C4（perplexity）；MT-Bench（指令跟随）；MMLU、HellaSwag、TruthfulQA（通用理解）。
  - **对比基线**：
    - Mixtral-base、Mixtral-Instruct独立模型。
    - **模型平均合并（Avg）**：对base和Instruct模型参数直接平均。
    - 对于Switch Transformer，对比了类似平均的静态权重合并。
- **可扩展性实验**：Switch Transformer下依次合并2、3、4个变体，使用ROUGE指标在SAMSum数据集上评估摘要质量。

### 4. 资源与算力

- **推理硬件**：1块NVIDIA A100 80GB GPU，通过PCIe Gen4与主机连接，主机为AMD 16核MILAN CPU。
- **训练/微调消耗**：论文未提及模型重训练或微调。专家距离计算和布局生成属一次性离线操作，文中未给出具体耗时，但强调只需执行一次。
- 未报告任何训练阶段的GPU数量或训练时长，全篇聚焦推理服务。

### 5. 实验数量与充分性：大概做了多少组实验，是否充分、客观、公平

- **实验维度较全面**：
  - **QoS**：不同到达率（λ=0.01~0.07）下的吞吐量曲线，并报告TTFT和周转时间均值（Table 2），重复5次取平均。
  - **输出质量**：7项基准（3个perplexity，1个指令跟随，3个多选问答）对比4种配置（base/Instruct/avg/Proposed），覆盖语言模型核心能力。
  - **可扩展性**：在Switch Transformer上，针对2/3/4个模型合并分别评估ROUGE-1/2/L/Lsum，与平均合并对比。
  - **消融分析**：通过Table 1给出不同专家命中率下的层延迟，间接解释方法性能来源。
- **公平性分析**：对比基线包括独立模型、NVIDIA官方MIG、经典模型平均法，基准选择合理。单模型服务通过总到达率加倍来匹配工作负载总量，使吞吐量对比公平。
- **局限性**：主要评估两个模型的场景，4模型仅在较小Switch Transformer上进行；未测试不同专家容量或混合不同种类请求的极端压力场景。

### 6. 论文的主要结论与发现

- **吞吐量优势**：所提系统与单模型服务接近，均可在较高λ（0.06）达到饱和，而NVIDIA MIG提早饱和（λ=0.04），且最大吞吐量远低于前两者。
- **延迟改善显著**：相比NVIDIA MIG，平均周转时间减少85%（8.78s vs 49.67s），TTFT增加可忽略（1.41s vs 5.86s）。该延迟增量来自非专家层交换，连续请求同一模型时不会发生。
- **输出质量竞争力**：在perplexity（WikiText,C4）上优于直接平均的模型；MT-Bench得分8.16，接近Instruct模型（8.13），且表现稳定；MMLU、HellaSwag等指标基本持平或小幅下降。
- **可扩展性鲁棒**：随着合并模型数增加，平均合并方法ROUGE-1从0.49降至0.25，而提出的方法从0.49降至0.46，显著更抗质量退化。

### 7. 优点：方法或实验设计上的亮点

- **新颖的组合策略**：将静态专家合并与动态非专家层替换结合，兼顾内存节约与模型特异性，这种“动静结合”思路在MoE多租户场景下具有原创性。
- **低侵入性设计**：只需离线计算一次专家布局，运行时仅替换量级远小于专家层（3GB vs 数十GB）的非专家部分，附加开销小。
- **实验验证扎实**：在真实硬件（A100）上测试，横向对比MIG和权重平均，指标涵盖延迟、吞吐、输出质量、可扩展性，说服力较强。
- **横向可推广性**：方法对MoE架构和微调模型数量无硬性限制，实验中展示了在两个模型家族上的有效迁移。

### 8. 不足与局限

- **输出质量下限依赖专家覆盖**：该方法高质量的前提是“相似位置专家可互换”，对于差异过大的微调方向（如不同语言、完全不同的任务领域），专家相似度可能降低，此时输出质量可能明显下降，而论文未探讨极端差异模型。
- **离线预处理复杂度**：需计算所有模型对的专家距离，当模型数量或专家数很大时（如GLaM的64专家/层），距离计算开销较大，文中未给出复杂度评估。
- **非专家层容量假设**：假定非专家层快速切换且无内存冲突，但若非专家层也很大（如某些深层模型自注意力参数庞大），传输开销可能不可忽略，论文未深入分析此边界条件。
- **请求调度策略简化**：默认按到达顺序服务，未研究请求重排、批处理或专家缓存策略以进一步优化命中率，可能影响实际吞吐。
- **实验覆盖度有限**：仅用Mixtral和Switch Transformer，未涉及其他主流MoE（如DeepSpeed-MoE、GLaM），且多模型场景上限为4个，真实多租户（数十个模型）下的表现未知。

（完）
