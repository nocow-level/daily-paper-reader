---
title: "HiFC: High-efficiency Flash-based KV Cache Swapping for Scaling LLM Inference"
title_zh: HiFC：面向LLM推理的高效闪存KV缓存交换
authors: "Inho Jeong, Sunghyeon Woo, Sol Namkung, Dongsuk Jeon"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=onhjdWCxZY"
tags: ["query:edge-llm"]
score: 7.0
evidence: 通过绕过DRAM实现SSD上的KV缓存交换，在有限内存下经济高效地扩展LLM推理
tldr: HiFC 针对LLM长上下文推理时KV缓存超出GPU显存、DRAM扩容成本高的问题，提出无DRAM的闪存直连交换方案，绕过CPU-to-GPU带宽瓶颈，实现高吞吐量的SSD缓存卸载，使资源受限环境下的长序列推理更加经济可行。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-onhjdwcxzy/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 826, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-onhjdwcxzy/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 603, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-onhjdwcxzy/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1407, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-onhjdwcxzy/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1449, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-onhjdwcxzy/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1447, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-onhjdwcxzy/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 723, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-onhjdwcxzy/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1451, \"height\": 441, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1070, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1296, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1356, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 663, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1186, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1356, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1456, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1462, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1460, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1463, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1283, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1199, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1449, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1277, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 610, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1008, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 916, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 871, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1057, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1185, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-onhjdwcxzy/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 800, \"height\": 473, \"label\": \"Table\"}]"
motivation: LLM 长上下文推理中 KV 缓存超出 GPU 显存，DRAM 卸载成本高。
method: 提出 HiFC，无 DRAM 的闪存直连交换方案，绕过 CPU-GPU 带宽限制直接访问 SSD。
result: 显著降低推理延迟与存储成本，在内存受限设备上实现高效长序列推理。
conclusion: HiFC 为内存受限环境下的 LLM 部署提供了低成本、高效率的存储扩展方案。
---

## Abstract
Large‑language‑model inference with long contexts often produces key–value (KV) caches whose footprint exceeds the capacity of high‑bandwidth memory on a GPU. Prior LLM inference frameworks such as vLLM mitigate this pressure by swapping KV cache pages to host DRAM. However, the high cost of large DRAM pools makes this solution economically unattractive. Although offloading to SSDs can be a cost-effective way to expand memory capacity relative to DRAM, conventional frameworks such as FlexGen experience a substantial throughput drop since the data path that routes SSD traffic through CPU to GPU is severely bandwidth-constrained. To overcome these limitations, we introduce HiFC, a novel DRAM‑free swapping scheme that enables direct access to SSD-resident memory with low latency and high effective bandwidth. HiFC stores KV pages in pseudo-SLC (pSLC) regions of commodity NVMe SSDs, sustaining high throughput under sequential I/O and improving write endurance by up to 8$\times$. Leveraging GPU Direct Storage, HiFC enables direct transfers between SSD and GPU, bypassing host DRAM and alleviating PCIe bottlenecks. HiFC employs fine-grained block mapping to confine writes to high-performance pSLC zones, stabilizing latency and throughput under load. HiFC achieves inference throughput comparable to DRAM-based swapping under diverse long-context workloads, such as NarrativeQA, while significantly lowering the memory expansion cost of a GPU server system by 4.5$\times$ over three years.

---

## 论文详细总结（自动生成）

# HiFC 论文总结

## 1. 论文的核心问题与整体含义
大语言模型（LLM）在长上下文推理时，键值（KV）缓存占用往往超出 GPU 高带宽显存（HBM）的容量。现有主流方案（如 vLLM）通过将 KV 页交换到主机 DRAM 来缓解内存压力，但大规模 DRAM 池成本高昂。另一种思路是将 KV 缓存卸载到低成本、大容量的 NVMe SSD，然而传统框架（如 FlexGen）因数据必须经过 CPU 和 DRAM，受限于 PCIe 总线和带宽瓶颈，导致吞吐量大幅下降。该论文旨在提出一种完全去除主机 DRAM 的全新交换机制，使 GPU 能够直接、高效地将 KV 缓存页写入消费级 NVMe SSD，从而在保持接近 DRAM 级推理吞吐的同时，将内存扩展成本降低 4.5 倍以上，为长上下文 LLM 推理提供经济可扩展的解决方案。

## 2. 论文提出的方法论
HiFC（High-efficiency Flash Cache）的核心思想是利用 GPU Direct Storage（GDS）实现 GPU 到 SSD 的直接数据传输，绕过主机内存与 CPU，并通过精细化的闪存块管理避免传统 SSD 卸载中的性能与耐久性问题。具体技术包含三个紧密集成的部分：

- **Flash Cache（FC）块分配器**：在 vLLM 原有 Block Manager 中新增 FC 块管理，为 KV 缓存块在 SSD 上分配固定大小的物理块（如 32–128 token）。采用**追加式块分配策略**，保证所有被换出的 KV 块在 SSD 上顺序写入和存储，避免随机 I/O。
- **闪存感知块管理**：利用消费级 NVMe SSD 的**伪SLC（pSLC）区域**（占总容量的约20%）专门存放 KV 缓存，该区域提供更高的顺序读写带宽和**高达 8× 的写入耐久度**。通过严格保持顺序写入，写放大因子（WAF）仅 1.02，远低于常规 SSD 的 1.4，极大延长设备寿命。
- **GDS 加速的缓存交换引擎**：在 vLLM 的调度器和 worker 中集成 CUDA 内核，使用 GDS 以 4KB 对齐方式直接传输 GPU 张量到 SSD，实现多线程 I/O（最多 16 线程），吞吐量超过 4.7 GiB/s。调度器在解码阶段当 GPU HBM 不足时，选择受害者序列，发起异步 swap-out，回收显存后立刻分配给活跃序列，swap-in 延迟被流水线隐藏。

**工作流程**：解码过程中，GPU 显存压力出现时，调度器选定受害序列组并通知 worker 执行 swap-out → worker 调用 CUDA 内核通过 GDS 将 KV 数据直接写入 SSD 的 pSLC 区域 → 释放的 GPU 块立即重分配给其他活跃序列 → 后续需要时，再将该序列的 KV 块 swap-in 回 GPU。整个过程无需 DRAM 中转。

## 3. 实验设计
- **模型与数据集**：主实验采用 DeepSeek-R1-Distill-Qwen-32B；稳健性验证覆盖 DeepSeek-Llama-8B、DeepSeek-Qwen-14B、Mistral-7B。评测数据集取自 LongBench，包括 Qasper（平均 3.6k token）、GovReport（平均 8.7k token）、NarrativeQA（平均 18.4k token），覆盖短到极长上下文场景。
- **对比方法**：主要对比**基于 DRAM 的交换**（vLLM 内置的 CPU offload），也对比了 GPU-only（触发 OOM）和 FlexGen 等传统 SSD 离线方法（文中提及原理但未列入直接对比表）。成本分析对比了 DDR4 DRAM、企业级 TLC SSD 和 HiFC（pSLC SSD）。
- **评测指标**：推理吞吐（tokens/s）、交换事件计数、延迟、I/O 带宽、写放大因子（WAF）、初始化时间、3 年内存扩展成本（CapEx + OpEx）等。
- **硬件拓扑测试**：1 GPU:1 SSD、2 GPU:1 SSD、2 GPU:2 SSD 三种多 GPU 配置下进行扩展性测试。

## 4. 资源与算力
- 硬件平台：Dell PowerEdge R750xa 服务器，双路 Intel Xeon Silver 4310 CPU，2×NVIDIA A100 80 GB GPU，256 GiB DDR4 内存。
- 存储：1 TB NVMe Gen4 消费级 SSD（pSLC 缓存约 200 GiB）作为 HiFC 闪存缓存；系统盘为 Samsung PM893 7.68 TB SATA SSD。
- 软件栈：Ubuntu 22.04，vLLM v0.6.6，CUDA 12.3，PyTorch 2.5.1，GDS 1.8.1.2。
- 论文未涉及模型训练，仅部署推理，无训练时长或大规模集群算力报告。

## 5. 实验数量与充分性
- **性能比较实验**：在不同输入序列长度（1k–5k）和输出长度（1k–10k）下，系统比较 HiFC 与 DRAM 交换的吞吐和交换次数（Fig. 3、Fig. 6）。
- **块大小消融**：测试 16、32、64、128、256 token 的块大小对交换吞吐、交换次数和端到端吞吐的影响。
- **多模型多数据集验证**：3 种不同大小的开源模型 × 3 个长上下文数据集，共计 9 组独立实验，结果均显示 HiFC 与 DRAM 性能差距在 1–2% 以内。
- **扩展性测试**：不同 GPU-SSD 拓扑（1:1, 2:1, 2:2），利用数据并行验证线性扩展能力。
- **写放大与 I/O 基准**：量化分析顺序 vs 随机写入下的写放大因子，并用 gdsio 工具测试 SSD 在不同 I/O 模式和 LBA 范围的带宽。
- **延迟与初始化**：对比 HiFC 和 DRAM 的请求平均延迟，测量 KV 缓存初始化时间随缓存容量增加的变化。
- **成本模型**：基于 3 年 TCO 估算，比较 DRAM、企业级 TLC SSD、HiFC 的 CapEx 与 OpEx。
- 实验设计充分、公平，严格遵守对照原则（相同块大小、相同调度器、相同 swap 空间大小），且涵盖长时间耐久性和成本分析，整体覆盖全面。

## 6. 主要结论与发现
- HiFC 在不依赖主机 DRAM 的前提下，实现了与 DRAM 交换**同等水平的推理吞吐量**（差距 <2%），同时在长上下文、大 batch 场景下性能稳定。
- 3 年内存扩展成本仅为 DRAM 方案的约 1/4.5（H2 2025 更新后为 1/6.1），主要由极低的 SSD 功耗和更低的资本支出驱动。
- 通过使用 pSLC 区域并强制顺序写入，**写放大因子低至 1.02**，SSD 寿命提升约 **8 倍**，可在持续工作负载下支持超过 8 年的使用。
- vLLM 的流水线调度有效地**掩盖了 SSD 交换延迟**，在深度序列流水线下，即使交换操作增加，端到端吞吐也不会下降。
- 多 GPU 场景下，HiFC 随 GPU 数量线性扩展，I/O 未成为瓶颈。

## 7. 优点
- **完全去 DRAM 的设计**：简化系统架构，大幅降低硬件成本和功耗。
- **直接利用消费级 SSD**：无需特殊硬件（如计算型存储 CSD），易于部署和推广。
- **深入融合 vLLM 框架**：几乎无侵入性改动，保留了 vLLM 的 PagedAttention 和流水线优势。
- **同时提升耐久性与性能**：通过闪存物理特性感知的块管理，兼顾高吞吐和长寿命。
- **全面的实验验证**：覆盖吞吐、延迟、成本、耐久性、扩展性，实验设计严谨。

## 8. 不足与局限
- **短上下文与低延迟场景适应性问题**：对于延迟极度敏感的任务，SSD 访问延迟可能成为瓶颈，尚未给出优化方案。
- **多 GPU 共享 SSD 的带宽调度**：文中仅做静态划分，如何在深度数据并行下避免 I/O 竞争未详细探讨。
- **部署需要一定专业调优**：如 pSLC 区域大小设置、文件系统和 DMA 缓冲对齐等需要领域知识，普适性受限。
- **模型规模覆盖有限**：实验仅使用 7B–32B 参数模型，未在 100B+ 级别验证，虽然设计原则适用，但实际带宽压力可能不同。
- **无真实生产环境长期稳定性测试**：虽然通过预测模型给出了 8 年寿命，但缺少真实跑满寿命的实验数据。

（完）
