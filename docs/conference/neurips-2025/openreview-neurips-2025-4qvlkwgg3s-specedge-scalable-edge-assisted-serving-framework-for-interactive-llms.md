---
title: "SpecEdge: Scalable Edge-Assisted Serving Framework for Interactive LLMs"
title_zh: SpecEdge：面向交互式LLM的可扩展边缘辅助服务框架
authors: "Jinwoo Park, Seunggeun Cho, Dongsu Han"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=4QVLKwgg3S"
tags: ["query:edge-llm"]
score: 10.0
evidence: 通过推测解码将LLM工作负载分割于边缘和服务器GPU之间，实现可扩展的边缘辅助服务。
tldr: 现有LLM服务系统多为服务器中心，忽视消费级边缘GPU。SpecEdge提出边缘辅助推理框架，将LLM工作负载分割于边缘与服务器GPU间，采用推测解码方案仅交换令牌输出。通过主动边缘草稿与流水线感知调度，重叠边缘令牌生成与服务器验证，提升服务器吞吐量，降低交互延迟，整体成本效率提高1.91倍。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 585, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 880, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 478, \"height\": 279, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 687, \"height\": 220, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 675, \"height\": 209, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1394, \"height\": 328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 465, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 467, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 457, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 456, \"height\": 275, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 465, \"height\": 268, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 455, \"height\": 272, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1405, \"height\": 223, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 845, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 753, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-4qvlkwgg3s/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 613, \"height\": 521, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1440, \"height\": 1047, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1439, \"height\": 782, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1160, \"height\": 786, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1442, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1136, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 998, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1178, \"height\": 574, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 489, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1441, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 556, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-4qvlkwgg3s/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1440, \"height\": 793, \"label\": \"Table\"}]"
motivation: 现有服务系统忽视边缘GPU，边缘设备算力未充分利用，服务成本高。
method: 设计边缘辅助框架SpecEdge，边缘GPU主动草稿生成，服务器验证，令牌级通信，流水线调度多请求。
result: "实验显示SpecEdge将服务器吞吐量提升2.22倍，整体成本效率提高1.91倍，降低延迟11%。"
conclusion: SpecEdge有效利用边缘GPU分担推理负载，为交互式LLM的高效可扩展服务提供了新架构。
---

## Abstract
Large language models (LLMs) power many modern applications, but serving them at scale remains costly and resource-intensive. Current server-centric systems overlook consumer-grade GPUs at the edge. We introduce SpecEdge, an edge-assisted inference framework that splits LLM workloads between edge and server GPUs using a speculative decoding scheme, exchanging only token outputs over the network. SpecEdge employs proactive edge drafting to overlap edge token creation with server verification and pipeline-aware scheduling that interleaves multiple user requests to increase server-side throughput. Experiments show SpecEdge enhances overall cost efficiency by **1.91×** through achieving **2.22×** server throughput, and reduces inter token latency by **11.24\%** compared to a server-only baseline, introducing a scalable, cost-effective paradigm for LLM serving. The code is available at https://github.com/kaist-ina/specedge

---

## 论文详细总结（自动生成）

# SpecEdge 论文详细总结

## 1. 核心问题与研究动机
- **背景**：大语言模型（LLM）在对话、代码生成等应用中普及，但规模化服务仍面临高计算成本与资源压力。
- **问题**：当前 LLM 推理系统以服务器为中心，完全忽略端侧（边缘）广泛存在的消费级 GPU（如 RTX 4090）。这些 GPU 算力高达 330 TFLOPS（FP16），成本仅为数据中心级 A100 的 1/14，却未能被现有服务架构有效利用。
- **传统方法的局限**：
  - **层分割推理（Layer-split）**：将模型层拆分到边缘与云端时，因自回归解码特性，每生成一个 token 都需要跨网络通信，在广域网高延迟下会导致 **2.35 倍**的延迟增加。
  - **I/O 瓶颈未解**：LLM 推理受内存 I/O 限制，算术强度低，层分割并不能改善 I/O 负载。
- **整体含义**：SpecEdge 旨在利用边缘消费级 GPU 分担 LLM 工作负载，通过 **推测解码**范式分割边缘草稿与服务器验证，从而在保持服务质量的前提下大幅提升成本效率。

## 2. 方法论核心思想与关键技术
### 2.1 分离式推测解码（Disaggregated Speculative Decoding）
- 将传统推测解码的 **草稿生成（drafting）** 和 **验证（verification）** 分配到不同硬件：
  - **边缘 GPU**：运行小型草稿模型，生成若干候选 token 并发送至服务器。
  - **服务器 GPU**：运行大型目标模型，一次性验证多 token，并额外生成一个 bonus token 返回边缘。
- 仅交换 token 输出而非中间状态，极大降低网络带宽需求与通信轮次。

### 2.2 主动边缘草稿（Proactive Edge Drafting）
- **动机**：分离架构中，若边缘等待服务器验证结果，会引入网络空闲时间。
- **机制**：在初始草稿树提交后，边缘立即选择 **累积对数概率最高的一条路径** 作为“扩展头”（expansion head），继续生成更多候选 token 而不等待验证结果。
- **增益公式**（文本描述）：
  ```
  E(Gain) = P_align * P_match|align * (T_draft / H_expand - 1)
  ```
  - `P_align`：验证序列与草稿树对齐的概率。
  - `P_match|align`：对齐时 bonus token 匹配扩展头的概率。
  - `T_draft`：主动生成的 token 总数，`H_expand` 为扩展头数量。
- **策略**：聚焦单一路径扩展（而非所有叶子节点），以牺牲对齐概率换取更高保留收益。
- **效果**：对齐成功时可无缝衔接主动草稿，隐藏网络和验证延迟，并生成更深草稿树。

### 2.3 服务器端流水线感知调度（Pipeline-Aware Scheduling）
- **挑战**：分离后，服务器若仅等待同一请求的验证任务，会产生“气泡”空闲期。
- **解决方案**：交错处理多个独立边缘端的请求：
  - 当一批请求的草稿正在边缘生成时，服务器验证另一批已完成的草稿。
  - 动态调整每个请求的 **草稿深度**，使得 `server_verify_time ≈ edge_draft_time + network_RTT`，从而确保验证批次到达时服务器刚好完成上一批工作。
- **处理异构请求**：通过自定义注意掩码和 KV 缓存填充，支持不同序列长度的请求合并成统一批次，最大化 GPU 并行效率。

## 3. 实验设计
### 3.1 实验设置
- **硬件配置**：
  - 服务器：NVIDIA A100（40GB 或 80GB）。
  - 边缘：NVIDIA RTX 4090（多卡），与服务器通过广域网连接，平均 RTT 为 14.07 ms。
- **基本模型对**：
  - 目标模型：Qwen3-32B, Qwen3-14B, Vicuna-33B, Llama2-13B-chat。
  - 草稿模型：Qwen3-1.7B, Qwen3-0.6B, Sheared Llama-1.3B, Tiny Llama-1.1B, JackFram-160M。
- **数据集**：SpecBench（6 种任务：多轮对话、翻译、摘要、问答、数学、RAG），以及 C4、OAsst、WikiText-2、MTBench。
- **对比基准**：
  - 服务器端推测解码（server-only speculative decoding，同样使用树状推测）。
  - 自回归解码（autoregressive）。
  - 层分割方案（将部分模型层卸载至边缘）。

### 3.2 评价指标
- **成本效率**：每美元生成的 token 数（1k tokens/$）。
- **服务器吞吐量**：每秒生成的 token 数（tok/s）。
- **令牌间延迟（inter token latency）**：用户感知的每个输出 token 时间。

## 4. 资源与算力
- 论文主要涉及推理服务，不涉及模型**训练**，因此无训练时长和训练算力需求。
- 推理计算资源：服务器 A100 单卡，边缘 RTX 4090 多卡（并发请求数 ×2）。此外还测试了 RTX 4070 Ti Super、RTX 3090、RTX 2080 Ti、RTX 3060 Ti 等轻量级 GPU。
- 成本估算基于云商实时价格（Google Cloud、AWS、Azure、Vast.ai 等）。

## 5. 实验数量与充分性
论文进行了极为丰富的实验，主要包括：
- **主体性能对比**：6 种任务 × 3 种模型对（18 组）的吞吐量与成本效率表格（Table 1）。
- **多种模型与数据集扩展**：又增加 Vicuna/Llama 目标模型 + 不同草稿模型，跨 4 个数据集（Table 2-3），共 12 组。
- **消融实验**（Figure 8）：逐一剥离“主动草稿”与“流水线调度”，验证各模块贡献。
- **网络敏感性分析**（Figure 11）：不同 RTT 下对比层分割和服务器基准的延迟变化。
- **硬件泛化测试**（Figure 12）：4 种边缘显卡的速度提升对比。
- **更轻 GPU 验证**（Table 4）：RTX 3060 Ti/2080 Ti 的性能。
- **非树状推测解码兼容性**（Table 5-6）：使用单序列推测方法的全面测试。
- **批处理草稿部署**（Table 7）：探讨减少边缘 GPU 数量的权衡。
- **推理模式**（Table 8）：开启/关闭推理 token 的对比。
- **多供应商成本对比**（Table 11）：验证成本优势的鲁棒性。
- **案例研究**：完整展示草稿生命周期。

总计超过 40 组表格或图表数据，覆盖方法论、任务、模型、硬件、部署策略等多维度，消融充分，对比客观公平。

## 6. 主要结论与发现
- **成本与吞吐**：SpecEdge 在多种任务上平均将服务器吞吐量提升 **2.22 倍**，整体成本效率提高 **1.91 倍**，同时仅增加少量边缘 GPU 成本。
- **延迟**：即使存在 14 ms 网络 RTT，SpecEdge 的令牌间延迟仍比零网络延迟的服务器端推测解码平均低 **11.24%**。
- **各组件价值**：仅分离架构吞吐量低且延迟高；加入主动草稿可降低延迟；完整系统（含流水线调度）吞吐量再提升 2.07 倍，实现延迟与吞吐兼得。
- **网络鲁棒性**：RTT 50 ms 以下时 SpecEdge 延迟优于服务器基准；RTT 65 ms 时延迟仅上升 22%，远超层分割方案。
- **架构通用性**：支持不同推测解码方法（树状/非树状）、不同边缘硬件（包括较旧显卡），且推理模式下的冗余 token 可进一步提升效率。

## 7. 优点
- **创新的边缘–云协同范式**：首次通过推测解码解耦草稿与验证，突破传统层分割在广域网下的极限。
- **系统设计精巧**：主动草稿利用单一路径扩展，以较低的实现复杂度获取显著收益；流水线调度动态平衡时间线，避免资源空洞。
- **实验极其全面**：覆盖多种模型、任务、数据集、硬件、网络条件、定价模型，消融实验严谨，结论可靠。
- **实际应用价值高**：显著降低成本且可即插即用，不改变输出质量（严格保持目标模型分布），代码开源。
- **扩展性好**：兼容未来新的推测解码技术，可融入不同边缘设备，甚至支持用户自有 GPU 参与。

## 8. 不足与局限
- **模型规模有限**：实验最大仅 33B 参数，未在百亿级更大模型（如 70B、405B）上验证，尽管论文认为设计可扩展，但更大模型的内存和通信开销可能带来新挑战。
- **安全与容错未深入**：当边缘端由用户或不可信设备提供时，计算完整性、隐私保护和故障恢复等尚待研究。
- **批处理草稿的权衡**：为节省边缘 GPU 数量而采用单 GPU 批处理多个请求时，延迟明显上升（最高 19%），可能需要用户忍受更长等待。
- **网络延迟上限**：当 RTT 超过 50 ms 后，相对于零延迟的服务器基准，延迟优势消失（但仍优于层分割）。
- **依赖边缘硬件更新**：性能提升依赖于边缘 GPU 的算力，老旧设备加速有限。

（完）
