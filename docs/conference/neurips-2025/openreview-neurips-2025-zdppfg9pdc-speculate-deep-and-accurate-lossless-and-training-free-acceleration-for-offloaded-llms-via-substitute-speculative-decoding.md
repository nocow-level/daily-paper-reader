---
title: "Speculate Deep and Accurate: Lossless and Training-Free Acceleration for Offloaded LLMs via Substitute Speculative Decoding"
title_zh: 推测既深又准：通过替代推测解码实现卸载LLM的无损且无需训练的加速
authors: "Pei-Shuo Wang, Jian-Jia Chen, Chun-Che Yang, Chi-Chih Chang, Ning-Chi Huang, Mohamed S. Abdelfattah, Kai-Chiang Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ZDpPfg9pDc"
tags: ["query:edge-llm"]
score: 10.0
evidence: 面向内存受限的消费级GPU，结合参数卸载与推测解码技术实现LLM部署加速。
tldr: 针对大模型在内存有限的消费级GPU上部署的难题，现有方法如压缩会损失质量，参数卸载虽保质量但慢。本文提出替代推测解码，无需训练且无损，通过快速近端草稿模型生成假设令牌，由卸载的大模型并行验证，显著减少了前向传播中耗时的权重传输，实现了数倍加速。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-zdppfg9pdc/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1363, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zdppfg9pdc/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1439, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zdppfg9pdc/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1443, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zdppfg9pdc/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1432, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zdppfg9pdc/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1244, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zdppfg9pdc/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1243, \"height\": 679, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-zdppfg9pdc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 1056, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zdppfg9pdc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 732, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zdppfg9pdc/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 503, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zdppfg9pdc/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 630, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zdppfg9pdc/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 772, \"height\": 197, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zdppfg9pdc/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1449, \"height\": 470, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zdppfg9pdc/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 569, \"height\": 155, \"label\": \"Table\"}]"
motivation: 内存受限的消费级GPU难以直接加载大模型，参数卸载虽可行但推理速度极慢。
method: 提出替代推测解码，利用快速草稿模型生成令牌序列，大模型并行验证，隐藏权重传输延迟。
result: 实验表明该方法在内存受限GPU上实现无损、免训练的LLM推理加速高达数十倍。
conclusion: 替代推测解码为内存受限设备上的LLM高效部署提供了实用化路径。
---

## Abstract
The immense model sizes of large language models (LLMs) challenge deployment on memory-limited consumer GPUs.
    Although model compression and parameter offloading are common strategies to address memory limitations, compression can degrade quality, and offloading maintains quality but suffers from slow inference.
    Speculative decoding presents a promising avenue to accelerate parameter offloading, utilizing a fast draft model to propose multiple draft tokens, which are then verified by the target LLM in parallel with a single forward pass. This method reduces the time-consuming data transfers in forward passes that involve offloaded weight transfers.
    Existing methods often rely on pretrained weights of the same family, but require additional training to align with custom-trained models. Moreover, approaches that involve draft model training usually yield only modest speedups. This limitation arises from insufficient alignment with the target model, preventing higher token acceptance lengths.
    To address these challenges and achieve greater speedups, we propose SubSpec, a plug-and-play method to accelerate parameter offloading that is lossless and training-free. SubSpec constructs a highly aligned draft model by generating low-bit quantized substitute layers from offloaded target LLM portions. Additionally, our method shares the remaining GPU-resident layers and the KV-Cache, further reducing memory overhead and enhance alignment.
    SubSpec achieves a high average acceptance length, delivering 9.1$\times$ speedup for Qwen2.5 7B on MT-Bench (8GB VRAM limit) and an average of 12.5$\times$ speedup for Qwen2.5 32B on popular generation benchmarks (24GB VRAM limit).

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机：** 大语言模型（LLM）庞大的参数规模导致在内存受限的消费级GPU（如8~24 GB显存）上部署困难。模型压缩（量化）虽减少内存却会损失生成质量；参数卸载（offloading）虽能保持质量，但频繁的CPU↔GPU数据传输导致推理延迟极高（例如仅2~3 tokens/s），无法满足实时交互需求。
- **问题定义：** 如何在保持LLM推理质量无损、且无需额外训练的前提下，大幅提升参数卸载场景下的推理速度。
- **核心思路：** 利用推测解码（Speculative Decoding）加速卸载推理，通过构建一个与目标LLM高度对齐、完全GPU驻留的“草稿模型”来生成大量候选token，目标模型只需一次前向即可并行验证，从而极大减少耗时的目标模型参数传输次数。论文提出 **SubSpec**，实现无损、免训练的即插即用加速。

### 2. 方法论
- **核心思想：** 构建一个与目标模型分布高度一致的GPU驻留草稿模型，并采用深度树形推测解码来最大化平均接受长度 \\(\tau\\)，从而最小化目标模型的调用次数。
- **草稿模型构建（三项策略）：**
  - **低比特替代层：** 对目标模型中需卸载到CPU的层，生成对应的4-bit量化版本，完全留在GPU上充当“替代层”。量化采用数据无关的HQQ方法，处理时间短（分钟级）。
  - **GPU驻留层共享：** 目标模型中本就在GPU上的层，草稿模型直接重用其权重，进一步提高对齐并节省显存。
  - **共享KV-Cache：** 草稿模型与目标模型共用一套KV-Cache，减少内存占用并增强上下文一致性，且免去草稿模型的预填阶段。
- **推测解码算法设计：**
  - **深度上下文感知动态草稿树：** 采用树形推测解码，每一时间步对叶子节点进行得分累积，选取 top-k 条路径继续扩展，生成深度为 \\(D\\) 的草稿树。文中探索了极深的 \\(D \\)（如48），远大于常规方法（\\(D \le 7\\)）。
  - **草稿概率锐化（Probability Sharpening）：** 针对贪婪解码（temperature=0）下深层树出现的“假正路径”累积概率发散问题，在草稿模型输出分布上应用低温度（0.2），使分布更尖峰，抑制低概率路径干扰，提升平均接受长度。
  - **异步数据传输：** 在当前层计算的同时，预取下一卸载层的参数，将传输与计算重叠，隐藏目标模型验证阶段的数据传输开销。
  - **分块预填（Chunked Prefill）：** 对长输入提示分段预填KV-Cache，降低峰值显存，使更多目标模型层可驻留GPU。
- **理论加速比分析：**
  \[
  \frac{T^N_{AR}}{T^N_{SD}} = \frac{\tau}{\frac{D \cdot t_{Draft}}{t_{Target}} + \gamma}, \quad 1 \le \tau \le D+1
  \]
  分析指出，在卸载场景下 \\(t_{Target}\\) 极大，推理时间主要受目标模型调用次数支配，因此最大化 \\(\tau\\) 比降低草稿模型延迟更为关键，这解释了为何高度对齐的草稿模型（即使速度稍慢）更优。

### 3. 实验设计
- **评价基准：** 五个代表性生成任务：多轮对话（MT-Bench）、代码生成（HumanEval）、数学推理（GSM8K）、指令跟随（Alpaca）、文本摘要（CNN/Daily Mail）。此外在推理模型上测试了AIME 2024、MATH 500、GPQA Diamond、LiveCodeBench。
- **对比方法：**
  - **基线：** 无推测解码的纯卸载推理。
  - **EAGLE-2：** 训练式草稿模型（用于标准场景设计）。
  - **同家族小模型作为草稿模型：** 如Qwen2.5‑1.5B、Llama-3.2‑1B 等。
  - **SubSpec（本文方法）。**
- **实验配置：** 单张 RTX 4090 (24 GB)，通过限制显存模拟8/12/24 GB环境；贪婪解码（temp=0）和随机解码（temp=0.6）；所有方法统一使用上下文感知动态草稿树、torch.compile 最大优化、静态KV-Cache 2048 tokens。SubSpec草稿深度48，k=6，替代层4-bit量化；EAGLE-2用默认参数。

### 4. 资源与算力
- **硬件：** 一张 NVIDIA RTX 4090 (24 GB)，Intel i7‑13700K CPU，128 GB DDR5 RAM，PCIe 4.0 x16 总线。
- **训练开销：** 本文方法完全免训练，无需任何额外训练算力。替代层量化耗时极短（分钟级，可在同一消费GPU上完成）。
- **推理效率：** 所有实验均在上述单卡上运行，显存以编程方式限制；文中未提及训练型对比方法的训练成本细节。

### 5. 实验数量与充分性
- 进行了多维度实验，覆盖**不同模型规模**（7B/8B/14B/32B）、**多个基准数据集**（5个常规+4个推理）、**两个采样温度**（贪心/随机）、**多组对比方法**，总计数十组端到端性能对比。
- 包含**消融研究**（逐步叠加组件，验证各优化贡献）、**草稿深度与温度影响分析**、与 SpecExec 的配套实验、以及不同量化位宽配置的影响分析。
- 实验设计**公平客观**：所有SD方法使用同一套树构建算法，并对硬件环境进行统一限制；结果汇报吞吐量（tokens/s）与平均接受长度，并申明标准方差极低。
- 总体实验**全面且充分**，能够有力支撑论文结论。

### 6. 主要结论与发现
- SubSpec 在无损、免训练条件下，为参数卸载的LLM推理带来了显著加速：
  - Qwen2.5‑7B @ 8 GB VRAM：MT-Bench 上 9.1× 加速（25.35 tokens/s）。
  - Qwen2.5‑32B @ 24 GB VRAM：平均 12.5× 加速。
  - 推理模型（DeepSeek-R1蒸馏版、QWQ）也获得 >10× 加速。
- 高度对齐的草稿模型使平均接受长度 \\(\tau \\) 稳定在约 30，是传统方法（<10）的数倍。
- 各组件（共享KV-Cache、概率锐化、异步传输）均带来5~13%的额外加速，消融证明了各自有效性。
- 在卸载场景下，草稿模型的对齐质量比对推演速度更为重要，与理论分析一致。

### 7. 优点
- **无损且免训练：** 无需任何微调或蒸馏，不牺牲模型原始输出质量，降低使用门槛。
- **高度对齐：** 通过量化替代层与共享机制，草稿模型与目标模型分布极为接近，实现超大接受长度。
- **系统性加速设计：** 将深度树推测、概率锐化、异步传输、共享KV-Cache等有机结合，从算法到系统栈全面优化。
- **理论与实证结合：** 提供了清晰的理论加速比分析，并通过实验验证了“对齐优先”的设计哲学。
- **可复现性与开源：** 提供代码，环境细节清晰，实验对比公平。

### 8. 不足与局限
- **最低显存门槛较高：** 草稿模型需完全GPU驻留，以Qwen2.5‑7B为例需约7.1 GB显存，限制了更小显存设备（<8 GB）的部署。
- **量化位宽探索有限：** 仅评估了4-bit替代层，未探索2-bit或3-bit等更激进的量化如何影响对齐与速度的权衡。
- **架构适用范围：** 方法针对稠密LLM（如Llama、Qwen）设计，直接应用于Mixture-of-Experts（MoE）等架构可能需要额外适配。
- **随机解码加速比下降：** 在温度=0.6的随机生成场景下，加速比从~10×降至约6~7×，推测解码的性能优势有所收缩。
- **依赖PCIe带宽：** 性能提升程度受限于CPU-GPU互连带宽，未来带宽提升后相对加速比可能改变，但当前代际收益显著。

（完）
