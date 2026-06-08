---
title: "SpeCache: Speculative Key-Value Caching for Efficient Generation of LLMs"
title_zh: SpeCache：面向大模型高效生成的投机键值缓存
authors: "Shibo Jie, Yehui Tang, Kai Han, Zhi-Hong Deng, Jing Han"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=PQIrsaIQdn"
tags: ["query:edge-llm"]
score: 9.0
evidence: 将完整KV缓存卸载至CPU内存并投机预取，克服GPU内存限制
tldr: 针对GPU内存限制导致长上下文推理中KV缓存不足的问题，提出SpeCache，利用CPU内存卸载完整缓存并投机获取所需KV对，避免压缩带来的信息遗忘，在保持精度的同时提升推理效率，为资源受限环境下的Transformer模型运行提供了新思路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-pqirsaiqdn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqirsaiqdn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1668, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqirsaiqdn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1672, \"height\": 773, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqirsaiqdn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 961, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pqirsaiqdn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 838, \"height\": 392, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-pqirsaiqdn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1622, \"height\": 1330, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqirsaiqdn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1618, \"height\": 937, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqirsaiqdn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1551, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqirsaiqdn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1671, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqirsaiqdn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 820, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pqirsaiqdn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1718, \"height\": 900, \"label\": \"Table\"}]"
motivation: 有限GPU显存无法容纳随序列长度线性增长的KV缓存，成为长上下文推理瓶颈。
method: 利用CPU内存保存完整KV缓存，基于投机机制动态预取所需KV对。
result: 避免了压缩导致的信息遗忘，在保持准确性的同时有效利用了CPU内存，提升推理效率。
conclusion: SpeCache通过层次化内存利用方案，缓解了内存压力，有助于长序列大模型部署。
---

## Abstract
Transformer-based large language models (LLMs) have already achieved remarkable results on long-text tasks, but the limited GPU memory (VRAM) resources struggle to accommodate the linearly growing demand for key-value (KV) cache as the sequence length increases, which has become a bottleneck for the application of LLMs on long sequences. Existing KV cache compression methods include eviction, merging, or quantization of the KV cache to reduce its size. However, compression results in irreversible information forgetting, potentially affecting the accuracy of subsequent decoding. In this paper, we propose SpeCache, which takes full advantage of the large and easily expandable CPU memory to offload the complete KV cache, and dynamically fetches KV pairs back in each decoding step based on their importance measured by low-precision KV cache copy in VRAM. To avoid inference latency caused by CPU-GPU communication, SpeCache speculatively predicts the KV pairs that the next token might attend to, allowing us to prefetch them before the next decoding step which enables parallelization of prefetching and computation. Experiments on LongBench and Needle-in-a-Haystack benchmarks verify that SpeCache effectively reduces VRAM usage while avoiding information forgetting for long sequences without re-training, even with a 10x high KV cache compression ratio.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- 大型语言模型（LLM）处理长序列时，键值（KV）缓存的大小随序列长度线性增长，有限的 GPU 显存（VRAM）成为严重瓶颈。
- 现有的 KV 缓存压缩方法（如驱逐、合并、量化）虽然能减小显存占用，但会造成不可逆的信息遗忘，影响后续解码质量。
- 将完整 KV 缓存卸载到 CPU 内存可以避免信息丢失，但频繁的 CPU‑GPU 通信会大幅增加推理延迟。
- 因此，本文的核心动机是：如何在几乎不增加延迟的前提下，利用 CPU 内存保存完整 KV 缓存，同时仅将少量最重要的 KV 对动态预取到 GPU，实现高效且无信息遗忘的长序列推理。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **整体框架（SpeCache）核心思想**  
  - 在 CPU 内存中永远保存完整的 16‑bit KV 缓存。  
  - 在 GPU 显存中仅保留一个低比特量化副本（如 2‑bit、1‑bit），用以近似估计注意力重要性。  
  - 每个解码步骤中，同时解码两个 token：正常输出 token 与“投机 token”。利用投机 token 的注意力分数预测下一解码步骤可能需要的 top‑k 个 KV 对，并提前从 CPU 预取到 GPU，从而实现预取与计算的并行，隐藏通信延迟。

- **关键算法阶段**（见图 3）  
  1. **预填充阶段**：逐层计算注意力后，将本层 KV 缓存量化为低比特，卸载原始 16‑bit 缓存到 CPU，仅在 GPU 保留量化副本。  
  2. **预解码阶段**：用第一个输出 token 进行一次前置解码，生成一个投机 token，同时将其 top‑k 索引对应的 16‑bit KV 对从 CPU 预取到 GPU。  
  3. **解码阶段**（每一步）：
     - 输入：上一步输出 token 与投机 token（两个 token 并行）。
     - 注意力计算使用 GPU 中的低比特副本 + 已预取的 top‑k 16‑bit KV 对。
     - 根据投机 token 的注意力分数得到新的 top‑k 索引。
     - 并行启动预取下一批 top‑k 16‑bit KV 对，同时将不再需要的 16‑bit 对释放，并把新生成的 KV 对量化后卸载到 CPU。
     - 输出 token 作为准确结果，投机 token 作为下一轮的近似输入。

- **量化方法改进（针对 1‑bit）**  
  原有 KIVI 量化在 1‑bit 时会导致数值幅度过大。SpeCache 修改零点和缩放因子，使量化值落到区间中点的平均值，例如：
  - \( z_X = \frac{3\cdot\min X + \max X}{4} \)
  - \( s_X = \frac{\max X - \min X}{2} \)  
  从而在 1‑bit 时也能稳定进行文本生成。

## 3. 实验设计：数据集 / 场景、基准、对比方法
- **评估任务与数据集**  
  - **LongBench**：包含 10 个长文本理解任务（Qasper、MultiFieldQA、HotpotQA、2WikiMQA、MuSiQue、GovReport、MultiNews、PassageRetrieval、LCC、RepoBench‑P）。  
  - **Needle‑in‑a‑Haystack (NIAH)**：合成长文本检索任务（最高 32k 令牌）。  
  - 最大序列长度按模型设定：LLaMA‑2 为 4k，Mistral 为 32k，LLaMA‑3 为 8k。

- **对比方法**  
  - 全精度 16‑bit KV 缓存（无压缩）。  
  - KIVI 量化（2‑bit、1‑bit，组大小 32 和 64），含少量残差 KV 对。  
  - 其他训练无关压缩方法：InfLLM、StreamLLM、H2O（在相同 KV 缓存压缩比下比较）。  
  - 为公平对比，SpeCache 减少残差长度以保证总 GPU 缓存大小与 KIVI 基线一致。

## 4. 资源与算力
- 吞吐量测试明确使用 **单卡 NVIDIA A6000（48 GB VRAM）**，测试不同上下文长度下的最大批处理量和吞吐量。
- 方法本身是训练无关的（training‑free），**无需任何训练或微调**，因此没有训练时间或大规模算力的消耗报告。
- 数据的 CPU‑GPU 交互基于 PyTorch 的多流机制实现，但作者指出通过更底层定制算子可进一步提升效率。

## 5. 实验数量与充分性
- **模型多样性**：在 4 个不同 LLM 上测试（LLaMA‑2‑7B‑Chat、LLaMA‑2‑13B‑Chat、Mistral‑7B‑Instruct‑v0.2、LLaMA‑3‑8B‑Instruct），涵盖多个架构和规模。
- **压缩配置**：测试了 2‑bit 和 1‑bit 量化，组大小 32/64，对应不同的 GPU KV 缓存比例（约 0.10×~0.22×）。
- **任务覆盖**：LongBench 上 10 个任务全面评估，NIAH 上测试检索能力。
- **消融实验**：
  - 预取 top‑k 数量 k 的影响（0~256）。
  - 1‑bit 量化改进的单独效果。
  - 投机预取 vs 非投机精确取回（延迟与性能对比）。
- **效率实验**：不同上下文长度下最大吞吐量、批处理量、延迟对比。
- 整体实验设计较为系统，对比基线丰富，消融充分。由于采用了与 KIVI 等基线相同的总 GPU 缓存大小，保证了**公平性**。但对更大模型（如 70B+）和更极端的上下文长度（如 128k+）尚缺乏验证。

## 6. 论文的主要结论与发现
- SpeCache 能在 GPU 中仅保留约 **10%** 的原始 KV 缓存（1‑bit 量化 + 少量 top‑k 预取）时，将长文本理解性能恢复到接近全精度基线，平均差距仅约 1‑2%。
- 相比同等压缩比下的其他方法（H2O、InfLLM、StreamLLM），SpeCache 取得最优平均性能，且在 1‑bit 极端压缩下优势尤为突出（部分任务性能提升超过 10 分）。
- 在 NIAH 长文档检索任务中，1‑bit 量化后的 SpeCache 几乎完全恢复了 16‑bit 缓存的检索精度。
- 由于显著降低 GPU 缓存占用，单卡最大批处理量可提升 **12 倍**，解码吞吐量提升最高 **4.6 倍**。
- 投机预测机制使预取与计算并行，在大批处理时可将延迟增幅压到最低，优于非投机精确取回方案。

## 7. 优点：方法或实验设计上的亮点
- **训练无关**：无需任何重新训练或校准（除了结合已有的无校准 KIVI），即插即用。
- **彻底避免信息遗忘**：完整 KV 缓存始终存在于 CPU，所有注意力所需的 KV 对理论上都可被取回，击中了压缩方法的痛点。
- **通信与计算并行化**：利用解码阶段的内存‑IO 瓶颈特性，将额外投机 token 的计算和预取通信隐藏在并行中，实际延迟增加很小。
- **方法兼容性**：底层量化方法可替换，文中展示了与 KIVI 的结合，并改造出更优的 1‑bit 量化。
- **全面的实验验证**：覆盖多个模型、多个任务类型和压缩强度，消融实验清晰揭示了各组件的作用（预取 k、1‑bit 改进、投机机制）。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **模型规模有限**：主要实验在 7B/8B/13B 模型上进行，未扩展到 70B 或更大模型，是否仍能保持稀疏性优势未知。
- **上下文长度限制**：LongBench 中最长仅 32k（Mistral），未验证在 100k+ 超长序列下 CPU 传输和预取命中率是否依然有效。
- **对稀疏性的依赖**：方法建立在注意力高度稀疏的假设上，若未来模型或任务导致注意力更分散，预取命中率可能下降，恢复效果可能减弱。
- **CPU‑GPU 带宽敏感**：预取仍需要足够的 PCIe 带宽，在带宽较低的系统（如部分边缘设备）上可能无法完全隐藏延迟。
- **对比基线维度**：与更先进的训练后压缩方法（如 ZipCache、ShadowKV）未进行直接对比，仅与 KIVI、InfLLM、H2O、StreamLLM 比较。
- **无实际部署多样性测试**：未在真实长文本对话、多轮交互等场景下评估端到端延迟和首 token 延迟的影响。
- **1‑bit 量化改造的局限性**：改进后的 1‑bit KIVI 虽然有效，但可能对某些分布偏差的数据依然不够鲁棒，文中仅在少数模型上验证。

（完）
