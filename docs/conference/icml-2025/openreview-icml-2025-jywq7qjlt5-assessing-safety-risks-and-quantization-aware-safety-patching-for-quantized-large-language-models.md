---
title: Assessing Safety Risks and Quantization-aware Safety Patching for Quantized Large Language Models
title_zh: 量化大语言模型的安全风险评估与量化感知安全修补
authors: "Kejia Chen, Jiawen Zhang, Jiacong Hu, Yu Wang, Jian Lou, Zunlei Feng, Mingli Song"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=jywq7qJLt5"
tags: ["query:edge-llm"]
score: 6.0
evidence: 解决资源受限环境下量化大模型的安全风险，提出Q-resafe安全补丁框架
tldr: 随着量化大模型在资源受限设备上的部署日益广泛，其安全能力可能受损。本文系统评估了多种量化方法下的安全风险，并提出量化感知安全补丁框架Q-resafe，有效恢复模型安全性，为量化模型的安全部署提供了保障。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-jywq7qjlt5/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1538, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jywq7qjlt5/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1592, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-jywq7qjlt5/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1594, \"height\": 529, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 824, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1568, \"height\": 887, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 863, \"height\": 866, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1608, \"height\": 801, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 672, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 749, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 690, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1708, \"height\": 637, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1118, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 788, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1416, \"height\": 998, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1476, \"height\": 997, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-jywq7qjlt5/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1245, \"height\": 1013, \"label\": \"Table\"}]"
motivation: 量化虽使模型能部署于边缘，但可能损害安全性，急需评估与修复。
method: 提出量化感知安全补丁框架Q-resafe，不依赖校准数据修复安全缺陷。
result: 广泛安全基准测试表明，Q-resafe有效恢复量化模型的安全性。
conclusion: 本工作为量化大模型的安全部署提供了系统评估和实用修复方案。
---

## Abstract
Quantized large language models (LLMs) have gained increasing attention and significance for enabling deployment in resource-constrained environments. However, emerging studies on a few calibration dataset-free quantization methods suggest that quantization may compromise the safety capabilities of LLMs, underscoring the urgent need for systematic safety evaluations and effective mitigation strategies. In this paper, we present comprehensive safety evaluations across various mainstream quantization techniques and diverse calibration datasets, utilizing widely accepted safety benchmarks. To address the identified safety vulnerabilities, we propose a quantization-aware safety patching framework, Q-resafe, to efficiently restore the safety capabilities of quantized LLMs while minimizing any adverse impact on utility.  Extensive experiment results demonstrate that Q-resafe successfully re-aligns the safety of quantized LLMs with their pre-quantization counterparts, even under challenging evaluation scenarios. Project page: https://github.com/Thecommonirin/Qresafe.

---

## 论文详细总结（自动生成）

### 1. 研究动机与核心问题
- **量化部署需求与安全风险矛盾**：大语言模型（LLM）在资源受限环境（如边缘设备）部署时，常采用量化技术（如 INT8/INT4）压缩模型，但现有研究（主要针对无校准数据集的量化方法）表明，量化过程会显著损害模型的安全能力（如生成有害内容、易被 jailbreak 攻击）。
- **系统评估缺失**：缺乏对主流量化方法（包含有/无校准数据集、PTQ 和 QAT 等类别）及不同校准数据集风险水平下的统一安全评估。
- **安全修复需求**：如何在保持量化模型高效性的同时，恢复其安全能力，是一个待解决的关键挑战。

### 2. 方法论：量化感知安全修补框架 Q-resafe
- **核心思想**：仅更新量化模型中极少量的“安全关键权重”，通过预量化模型引导的偏好对齐（DPO），恢复量化模型的安全能力，同时最大程度保留原有量化权重以维持效用。
- **实现步骤**：
  1.  **安全修补数据集构建**：使用辅助校准数据集中的提示词 `x`，分别输入预量化 LLM（生成优胜响应 `yw`）和量化 LLM（生成劣响应 `yl`），形成偏好三元组 `(x, yw, yl)`，无需人工标注。
  2.  **周期性安全关键权重识别**：基于 SNIP 重要性分数 `I(W_ij, x) = |W_ij · ∇_{W_ij} L(x)|`（在安全修补数据集上平均），取前 τ% 高重要性的权重作为安全关键权重，生成二值掩码矩阵 `M_Q`。为适应训练中权重变化，每 K 步重新识别。
  3.  **约束更新**：在 LoRA 框架下，仅更新掩码选中的低秩矩阵 `(A, B)` 部分，更新后重新量化为低精度格式：`A_{t+1} = M_A ⊙ (A_t - η∇_A L) + (1-M_A) ⊙ A_t`，`Q_{t+1} = Q_0 + Quant(A_{t+1}B_{t+1})`。优化目标采用 DPO 损失，使量化模型向预量化模型的响应偏好对齐。
- **算法简化流程**：
  - 输入：量化模型 π_Q0，预量化模型 π_W，校准集 D_calib
  - 用预量化与量化模型对 D_calib 中的提示生成响应，构建 D_patch
  - 循环：定期根据 SafeScore 更新掩码 M_Q；仅更新掩码选中的 LoRA 参数；重新量化为 Q_t+1

### 3. 实验设计
- **模型与量化方法**：
  - 基座模型：Llama-2-7B-Chat 和 Gemma-7B-Instruct。
  - 量化方法：AWQ（无微调 PTQ）、AQLM（有微调 PTQ）、LLM-QAT（QAT 全量微调）、QLoRA（QAT 参数高效微调）。
  - 位宽：INT8、INT4（部分实验扩展至 3‑bit、2‑bit）。
- **数据集与安全风险等级**（校准/修补数据集）：
  - **Risk‑III（直接有害）**：从 AdvBench 抽取 10 条有害指令及对应有害响应。
  - **Risk‑II（间接有害）**：使用无害指令但植入诱导服从性/不安全行为的响应（基于 AdvBench 构建）。
  - **Risk‑I（良性）**：从 UltraChat 抽取 10 条无害效用导向样本。
- **安全与效用指标**：
  - 安全：攻击成功率（ASR，基于 AdvBench 有害指令），部分场景使用解码攻击下的 ASR 或 HarmBench 分类器。
  - 效用：MT-Bench 和 AlpacaEval。
- **对比方法**：四种量化方法自身；Q-resafe 应用在这些量化方法上的效果；以及 SFT、DPO 等安全微调方案（消融实验）。

### 4. 资源与算力
- 文中提及实验使用 4 块 NVIDIA A100 40GB GPU。
- 训练时长未给出总卡时，但在消融实验（表 5、6）中给出了不同方法的 GPU 小时数，例如：
  - 在 UltraChat 200k 上 1 epoch，当 τ=0.6 时 Q-resafe 耗时约 1.2 小时，全参数更新（τ=1.0）约 2.1 小时。
  - QLoRA+SFT 需 3.4 小时，DPO 需 3.8 小时，而 QLoRA+Q-resafe 仅需 1.2 小时。
- 其他实验的具体训练时长未完全列出，但可推断整体算力消耗适中。

### 5. 实验数量与充分性
- **主要安全评估实验**：
  - 两种基座模型 × 两种位宽 × 四种量化方法 × 三种校准数据集（对 AWQ 采用解码攻击评估），共计约 52 组主要安全结果（表 3 及附录）。
  - 多次迭代训练（不同 epochs、不同数量的 harmful 样本）评估安全与效用变化（表 11-13）。
- **消融与附加实验**：
  - 安全关键权重比例 τ 从 1.0 到 0.0 变化（表 5）。
  - 对比不同安全微调方法（SFT、DPO、Q-resafe）（表 6）。
  - 多种量化 bit‑width（8/4/3/2）的安全性变化（表 7）。
  - 额外量化方法（LLM.int8()、NF4、FP4）的修补效果（表 10）。
  - 不同解码策略的影响（图 3）。
  - 使用 HarmBench 和 GPT‑4 评分作为补充安全度量（表 9）。
- **充分性与公平性**：实验覆盖全面，包括多种量化范式、风险级别、模型类型、位宽，并设置了消融实验和控制变量，比较了多种基线方法，总体设计客观、公平，能够支撑论文结论。

### 6. 主要结论与发现
- **量化普遍损害安全**：所有评估的量化方法（无论 PTQ 还是 QAT）均导致安全能力下降，INT4 比 INT8 退化更严重；使用有害或间接有害校准数据集会使安全风险剧增。
- **Q-resafe 有效恢复安全**：在各种校准数据集和量化方法上，Q-resafe 都能将量化模型的 ASR 降低至接近或等于预量化模型的水平，且对效用（MT-Bench、AlpacaEval）影响极小。
- **选择性更新权重节约成本**：仅更新 top 20‑60% 的安全关键权重即可实现良好安全修复，全量更新效果略好但成本更高；完全不做安全权重识别则无法恢复安全性。
- **优于直接 SFT/DPO**：相比常规 SFT 或 DPO 安全微调，Q-resafe 在更短训练时间内实现相当或更优的安全恢复，并保持效率优势。

### 7. 论文优点
- **系统性安全评估**：首次覆盖 PTQ/QAT、不同校准数据集风险等级、多种位宽的全面安全评估，为社区提供了基准。
- **新颖的修补方法**：提出选择性更新安全关键权重的量化感知修补框架，兼顾安全恢复与效用保持，且无需额外人工标注。
- **高效性**：通过 LoRA 微调和定期重要性剪枝显著降低计算开销，实验证明 GPU 小时数远低于全量微调。
- **通用性**：方法不依赖特定量化技术，可适配 AWQ、AQLM、LLM‑QAT、QLoRA、LLM.int8() 等多种量化方案。

### 8. 不足与局限
- **预量化模型依赖**：安全修补数据集构建依赖预量化 LLM 作为偏好来源，若预量化模型不可用（如闭源或无法获取），需寻求替代对齐模型，泛化性可能受限。
- **校准数据集影响未完全消除**：修补虽有效，但若原始量化中使用了高危害数据集，安全恢复仍可能留有残余风险（ASR 未完全降至 0）。
- **实验模型规模有限**：仅在 7B 级别模型上验证，未在更大规模（13B、70B 等）模型上测试，对更高参数量的扩展性未知。
- **安全评估范围**：ASR 为主要安全指标，虽结合 HarmBench 和 GPT‑4 评分，但对更复杂的安全威胁（如多轮对话安全、隐私泄漏等）未细致探讨。
- **LoRA 秩与阈值选择**：rank r、τ 等超参数需手动设定，未给出自动化选择策略。

（完）
