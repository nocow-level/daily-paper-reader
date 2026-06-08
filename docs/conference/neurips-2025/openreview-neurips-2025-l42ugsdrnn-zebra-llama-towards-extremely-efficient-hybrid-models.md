---
title: "Zebra-Llama: Towards Extremely Efficient Hybrid Models"
title_zh: Zebra-Llama：迈向极致高效的混合模型
authors: "Mingyu Yang, Mehdi Rezagholizadeh, Guihong Li, Vikram Appia, Emad Barsoum"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=l42UGsdrNn"
tags: ["query:edge-llm"]
score: 8.0
evidence: 组合预训练模型构建高效混合语言模型，提升LLM推理效率以适应多样部署场景
tldr: Zebra-Llama 针对LLM推理效率低和重训成本高的问题，提出 X-EcoMLA 混合模型系列，通过组合状态空间模型和多头潜在注意力层，利用后训练知识迁移，在保持 Transformer 级精度的同时显著提升推理效率，为 LLM 的广泛部署提供高效方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 623, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1391, \"height\": 368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 646, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 660, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 660, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 656, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 648, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1345, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-l42ugsdrnn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1334, \"height\": 561, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1443, \"height\": 770, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 790, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 611, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 593, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1360, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1209, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 699, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1421, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1338, \"height\": 681, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1038, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1443, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1442, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1440, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1011, \"height\": 161, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1445, \"height\": 647, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-l42ugsdrnn/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1443, \"height\": 288, \"label\": \"Table\"}]"
motivation: LLM 部署对推理效率需求迫切，但重训成本高昂。
method: 提出 X-EcoMLA 系列，将 SSM 与 MLA 层融合，通过初始化与后训练管线实现预训练 Transformer 知识迁移。
result: 1B、3B、8B 混合模型达到 Transformer 级精度，推理效率显著提升。
conclusion: 该方案为高性能 LLM 的广泛、可持续部署提供了可行路径。
---

## Abstract
With the growing demand for deploying large language models (LLMs) across diverse applications, improving their inference efficiency is crucial for sustainable and democratized access. However, retraining LLMs to meet new user-specific requirements is prohibitively expensive and environmentally unsustainable. In this work, we propose a practical and scalable alternative: composing efficient hybrid language models from existing pre-trained models.
Our approach, X-EcoMLA, introduces a family of 1B, 3B, and 8B hybrid models by combining State Space Models (SSMs) and Multi-head Latent Attention (MLA) layers, using a refined initialization and post-training pipeline to efficiently transfer knowledge from pre-trained Transformers.
X-EcoMLA achieves Transformer-level accuracy with near-SSM efficiency using only 7–11 billion training tokens (compared to the trillions required for pre-training) and an 8B teacher. Moreover, it dramatically reduces KV cache size—down to 3.9%, 2%, and 2.73% of the original for the 1B, 3B, and 8B variants, respectively—while preserving 100%, 100%, and over 97% of average zero-shot performance on LM Harness tasks.
Compared to models like MambaInLLaMA, X-EcoMLA, Minitron, and Llamba, our approach consistently delivers competitive or superior accuracy while using significantly fewer tokens, smaller teachers, and vastly reduced KV cache memory. Notably, X-EcoMLA-8B surpasses Minitron-8B in few-shot accuracy by 7%, while using 8× fewer training tokens, over 12× smaller KV cache, and a smaller teacher (8B vs. 15B). 
It also achieves 1.4x–3.3x higher throughput (tokens/s) than MambaInLlama. The source code is
released at https://github.com/AMD-AGI/AMD-Hybrid-Models.

---

## 论文详细总结（自动生成）

## 1. 论文核心问题与整体含义
- **研究动机**：大型语言模型（LLM）在多样场景中部署时，因自注意力的二次复杂度和庞大 KV 缓存导致推理效率低下，尤其在边缘设备或延迟敏感环境中难以应用。传统重训或压缩方法存在精度下降、成本高昂和环境负担重等问题。
- **整体含义**：本文提出一种实用且可扩展的替代方案——直接从已有预训练 Transformer 组合出高效混合模型，避免完整预训练的巨大开销，同时极大降低内存占用并保持竞争性精度，推动 LLM 的可持续与民主化访问。

## 2. 方法论
- **核心思想**：将状态空间模型（Mamba2，零 KV 缓存但单独使用性能不足）与多头潜在注意力（MLA，可压缩 KV 缓存但过度压缩会掉点）交织成混合架构，实现极低缓存下的高性能。
- **关键技术细节**：
  - **结构化初始化**：使用 SVD 从预训练 Transformer 的 Q、K、V 权重映射出 MLA 的低秩压缩权重（W_DQ、W_UK 等），并从注意力表征映射出 Mamba2 的 SSM 参数。
  - **中间层蒸馏（ILD）**：在用少量数据训练纯 MLA 和纯 Mamba2 模型时，最小化各层输出与原 Transformer 对应层输出的 MSE 损失，对齐内部表征。
  - **SMART 层选择策略**：基于 KL 散度的敏感性得分（`si`），结合“首尾保留”“近均匀分布”“最大化总得分”三步法，选出最优的 MLA 层位置，其余层为 Mamba2。
  - **端到端知识蒸馏**：以原 Transformer 为教师，用 KL 散度损失对整个混合模型进行监督微调（SFT）。
  - **DPO 偏好对齐**：以蒸馏后模型自身为参考模型，使用偏好数据进一步优化。
- **公式要点**：注意力线性化映射为 `ht = Atht-1 + Btxt, yt = Ctht`；ILD 损失为 `Σ||h_attn_l – h_M2_l||²` 等；敏感性得分 `si` 定义为替换第 i 层为 MLA 后 KL 散度的降低量。

## 3. 实验设计
- **基座与教师**：选用 Llama3.2-1B-Instruct、3B-Instruct 和 Llama3.1-8B-Instruct 作为基座，部分实验使用 8B/70B 作为教师。
- **训练数据**：ILD 和 SFT 共用 OpenHermes-2.5、GenQA、Infinity-Instruct 共 6.8B tokens（分割为 20%/80%），DPO 使用 Llama3-ultrafeedback、orca_dpo_pairs 等。
- **评估基准**：LM Harness Eval 零样本和少样本（ARC-C/E、HellaSwag、MMLU、OpenBookQA、PIQA、RACE、Winogrande），以及 GSM8K 数学推理、GPQA、RULER 长文本评估、推理吞吐与峰值内存测试。
- **对比方法**：同尺寸 Llama、MambaInLLaMA（混合 Mamba2-GQA）、X-EcoMLA（纯 MLA）、Llamba（纯 Mamba2）、Minitron（剪枝+蒸馏）、以及预训练混合模型（Samba、Hymba、Mamba-2-Hybrid 等）。

## 4. 资源与算力
- **硬件**：单个节点配备 8 块 AMD MI300 GPU（每卡 192GB 显存）。推理测试使用单卡 AMD MI300X。
- **训练时长**：例如 Zebra-Llama-1B 系列 ILD 约 1.7~1.8 小时/模块，SFT 约 13.7 小时，DPO 约 0.5 小时；3B 模型 SFT 约 31.2 小时；8B 模型 ILD 约 9~10 小时，SFT 约 78 小时，DPO 2.3 小时。整体训练代价远低于预训练。

## 5. 实验数量与充分性
- **多尺寸模型**：构建了 1B、3B、8B 三个规模，每个规模测试多种 MLA/Mamba2 配比（如 8MLA-8M2、4MLA-12M2 等），覆盖不同 KV 压缩率（3.9% 到 7.8% 等）。
- **消融实验丰富**：对初始化策略（随机/结构化/有无 ILD）、SMART 层选择（对比均匀、贪婪等）、MLA 层数 vs. 压缩率 trade-off、教师模型缩放（1B/3B/8B/70B）、以及扩展到 Qwen 架构等进行了充分检验。
- **评估维度全面**：包含零样本/少样本语言理解、数学推理、长上下文、吞吐/内存效率，并与蒸馏、剪枝、纯 SSM、纯 MLA 及预训练混合模型多组 baseline 对比。实验结果公平、客观，配置信息详尽。

## 6. 主要结论与发现
- **极致 KV 压缩**：1B/3B/8B 模型分别实现 25×、50×、36× KV 缓存压缩（压缩至 3.9%、2.0%、2.7%），同时保持基座 100%/100%/>97% 的零样本平均性能。
- **训练高效**：仅需 7–11B 训练 tokens 和 8B 教师，远少于 MambaInLLaMA 等 baseline（需 20B tokens 或 70B 教师），也远少于预训练混合模型的数万亿 tokens。
- **推理加速**：相比 Llama-8B 吞吐提升 3.9×（16k 输入），比 MambaInLlama 高 1.4–3.3×，且支持长上下文（如 131k tokens）而基线出现 OOM。
- **少样本与数学推理**：Zebra-Llama-8B 平均少样本准确率优于 Minitron-8B 7%，且 1B/3B 模型在 GSM8K 上超越部分基线，内存占用极低。
- **策略有效性**：结构化初始化+ILD 显著提升后训练效果，SMART 层选择优于简单启发式，MLA 层数与压缩率间存在最优平衡。

## 7. 优点
- **无需预训练**，利用已有 Transformer 权重的映射与蒸馏，极大降低了构建高效模型的成本。
- **压缩倍率高**，同时精度损失极小，平衡性业界领先。
- **训练和推理资源需求低**，支持在边缘设备或长上下文场景部署。
- **方法普适**，成功扩展至 Qwen 架构，并开源代码以促进复现。
- **实验设计系统**，多维度的消融与对比验证了各组件贡献。

## 8. 不足与局限
- **长上下文训练受限**：当前模型仅在最大序列长度 2048 下训练，导致 RULER 基准表现尚有不足，未来需进一步扩展上下文训练。
- **知识密集型任务仍有差距**：MMLU 性能约为基座的 83%–86%，受限于训练数据质量（如未使用 FineWeb-Edu）和 SSM 在多选题格式上的固有劣势。
- **依赖强教师模型**：蒸馏仍需要能力较强的教师，在无强力教师时性能可能受限。
- **模型规模未探索更大参数**：目前最高 8B，更大规模模型的蒸馏效果及扩展性有待验证。
- **DPO 阶段相对简单**，可能未充分挖掘偏好优化的潜力。

（完）
