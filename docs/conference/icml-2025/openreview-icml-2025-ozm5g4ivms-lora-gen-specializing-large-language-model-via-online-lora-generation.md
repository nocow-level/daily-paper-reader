---
title: "LoRA-Gen: Specializing Large Language Model via Online LoRA Generation"
title_zh: LoRA-Gen：通过在线LoRA生成专业化大型语言模型
authors: "Yicheng Xiao, Lin Song, Rui Yang, Cheng Cheng, Yixiao Ge, Xiu Li, Ying Shan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=oZM5g4IvmS"
tags: ["query:edge-llm"]
score: 10.0
evidence: 云端模型为边缘模型生成LoRA参数实现专业化
tldr: 针对边缘侧小模型在特定任务上效果和效率不足的问题，LoRA-Gen框架利用云端大模型根据任务描述生成LoRA参数，并合并到边缘模型中实现专业化。这一知识迁移方法减少了输入上下文长度，显著提升了边缘模型的推理效率。实验表明该方法有效促进了模型间的知识传递，为云边协同的端侧LLM部署开辟了新途径。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ozm5g4ivms/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 724, \"height\": 610, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozm5g4ivms/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1593, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozm5g4ivms/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1756, \"height\": 1002, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozm5g4ivms/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1705, \"height\": 946, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1732, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1458, \"height\": 709, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1441, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 844, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 385, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 345, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 724, \"height\": 170, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 435, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 364, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 803, \"height\": 683, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1336, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1255, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozm5g4ivms/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1181, \"height\": 283, \"label\": \"Table\"}]"
motivation: 大型语言模型在特定领域任务上效率和效果不足，尤其对边缘小模型。
method: 云端大模型根据任务描述在线生成LoRA参数，重参数化到边缘小模型实现专业化。
result: 通过知识迁移提升了边缘模型的推理效率和效果。
conclusion: LoRA-Gen为边缘模型提供了一种灵活高效的云边协同专业化方法。
---

## Abstract
Recent advances have highlighted the benefits of scaling language models to enhance performance across a wide range of NLP tasks. However, these approaches still face limitations in effectiveness and efficiency when applied to domain-specific tasks, particularly for small edge-side models. We propose the LoRA-Gen framework, which utilizes a large cloud-side model to generate LoRA parameters for edge-side models based on task descriptions. By employing the reparameterization technique, we merge the LoRA parameters into the edge-side model to achieve flexible specialization. Our method facilitates knowledge transfer between models while significantly improving the inference efficiency of the specialized model by reducing the input context length. Without specialized training, LoRA-Gen outperforms conventional LoRA fine-tuning, which achieves competitive accuracy and a 2.1x speedup with TinyLLaMA-1.1B in reasoning tasks.
Besides, our method delivers a compress ratio of 10.1x with Gemma-2B on intelligent agent tasks.

---

## 论文详细总结（自动生成）

# LoRA-Gen：通过在线LoRA生成实现大型语言模型的专业化

## 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型遵循规模法则，但部署到特定领域任务时，存在效果与效率的平衡难题，尤其是面向资源受限的“边缘侧”小模型。
- **核心问题**：传统LoRA微调存在灾难性遗忘，且多任务/未见任务泛化受限；LoRA混合专家（LoRA-MoE）虽可缓解，但引入了额外的推理开销，而现有的上下文压缩方法无法兼顾训练自由与知识迁移。
- **整体含义**：该文提出**云边协同**的新范式——利用云端大模型为边缘小模型**在线生成任务特定的LoRA权重**，实现灵活的模型专业化，兼具上下文压缩、无训练部署与知识注入等优势。

## 2. 论文提出的方法论
### 核心思想
- **LoRA-Gen** 分为两部分：**云端LoRA生成器** 和 **边缘侧专业化语言模型**。
- 系统提示（任务描述、few-shot样本等）输入云端LLaMA3-8B，生成**元令牌（meta-tokens）**，每个元令牌对应边缘模型的一层，通过路由模块从LoRA专家池中选择并组合专家权重，生成最终的任务LoRA；然后通过重参数化合并到边缘模型，得到专用模型。

### 关键技术细节
1. **元令牌生成**  
   云端LLM在系统提示末尾追加`L`个特殊的 `<meta>` 令牌（`L`等于边缘模型层数），单次前向传播即把任务知识压缩到这些令牌中。

2. **LoRA专家池与路由**  
   - 构建包含`n`个专家的池，每个专家含三个LoRA块（对应FFN的门、升维、降维线性层）。
   - 路由模块由两层线性变换+BN+SiLU组成，输入为第`i`层对应的元令牌，输出第`i`层的专家门控分数。
   - 采用**KeepTOP-K**策略：对softmax概率取前K个值并重新归一化，其余置0，以确定性方式组合专家。

3. **任务LoRA的生成**  
   第`i`层的生成权重：θ_i = Σⱼ G_iⱼ E_j   
   其中`G_i`是第`i`层的门控分数，`E_j`是专家`j`的LoRA参数。

4. **重参数化**  
   训练完成后，将生成的LoRA权重合并到边缘模型的原FFN权重中：Ŵ = W + AB，推理时无额外专家或路由模块。

5. **训练目标**  
   - 主损失：标准语言建模交叉熵 `L_LM`  
   - 辅助损失：批次内专家门控分数的变异系数平方 `L_cv = α(σ(G)/μ(G))²`，鼓励负载均衡。总损失 `L_total = L_cv + L_LM`。

### 与已有方法的区别
- 对比LoRA-MoE：推理时无需额外参数，无多余计算。
- 对比AutoCompressors等软提示方法：将上下文压缩为LoRA权重（而非固定长度的软令牌），对未见任务泛化更优。

## 3. 实验设计
### 数据集与场景
- **常识推理任务**（8个基准）：BoolQ、ARC-c、ARC-e、OpenBookQA、PIQA、SocialQA、HellaSWAG、Winogrande。前5个作为多任务训练集，后3个作为**未见任务**测试集。
- **智能体任务**：GPT4Tools（工具使用），包含71k训练样本，测试集含8个未见工具（652条），评估工具使用的思维成功率(SR_t)、动作成功率(SR_act)、参数成功率(SR_args)、成功率(SR)以及IoU。特别测试了**不提供工具定义**下的压缩能力。

### 评估指标
- 推理：准确率、平均准确率(AVE)、调和平均(HAR)、推理延迟。
- 智能体：SR、IoU、平均得分、压缩比（速度提升倍数）。

### 对比方法
- 基线：直接使用小模型（TinyLLaMA-1.1B、Qwen-1.5B、Gemma-2B）
- **LoRA**：传统LoRA微调
- **LoRAMoE**：LoRA混合专家
- **MixLoRA**：另一种LoRA-MoE
- **AutoCompressors**：上下文压缩方法（仅部分实验）
- LoRA-Gen自身不同变体（消融）

## 4. 资源与算力
- **训练硬件**：8块NPU（每块64GB显存），未提及GPU型号，但推理延迟在Nvidia A100（40GB）上测量。
- **训练配置**：优化器AdamW，学习率2e-5，warmup 50步，weight decay 0.1，批大小64，训练4 epoch，最大长度2048，LoRA秩16。
- 云端模型LLaMA3-8B本身大小中等，整体训练成本可控，但未给出具体训练时间。

## 5. 实验数量与充分性
- **主干实验**：在3种规模的边缘模型（1.1B、1.5B、2B）上评测，覆盖8个推理任务，与4种基线对比，表格详实。
- **智能体实验**：在Gemma-2B上与LoRA基线比较，检验训练/未见工具、有无工具定义的不同配置，展示压缩比优势。
- **消融实验**（至少6组）：
  - 专家数量（4/8/12）
  - 辅助损失系数（0.1/0.01/0.005）
  - 路由策略（Gumbel-softmax vs KeepTOP-K）
  - LoRA生成方式（元令牌 vs 直接投影）
  - 知识迁移效果（few-shot数量 vs 基线）
  - 与AutoCompressors在未见任务上的比较
- 实验覆盖了多任务学习、泛化性、效率、压缩比等多维度，对比方法涵盖主流，消融充足，总体客观公平。

## 6. 主要结论与发现
- LoRA-Gen在常识推理上在**未见任务**上表现优于LoRA微调和LoRA-MoE，且推理延迟显著降低（如TinyLLaMA-1.1B上延迟21.2ms vs LoRA 44.5ms，同时准确率提升1.3% Harmony Mean）。
- 在智能体任务上，**不提供工具定义**即可获得91.5%平均得分，输入压缩比高达**10.1倍**；即使未经GPT4Tools训练，也能提升基线4.9%平均分，展现强大的零样本泛化能力。
- 云边知识迁移效果明显：仅1-shot的LoRA-Gen便超越5-shot的基线模型。
- 消融显示：8个专家、KeepTOP-K路由、辅助损失系数0.01、元令牌方式为最佳配置；直接生成LoRA权重易过拟合。

## 7. 优点
- **新范式**：首次利用云端大模型为边缘模型生成LoRA，将任务描述压缩到模型参数中，兼具上下文压缩、免训练部署、跨模型知识注入。
- **效率很高**：重参数化后推理时零额外开销，显著减短上下文，带来实际加速（2.1x推理、10.1x压缩）。
- **泛化性强**：在未见任务和未见工具上均保持高性能，不易过拟合。
- **实验扎实**：多模型、多任务、多维度对比，消融分析详尽，论证充分。
- **可解释性强**：通过定性案例和图表演示了压缩效果和生成质量。

## 8. 不足与局限
- **云边模型耦合**：要求云端模型够大，且需在线生成，增加了云侧推理成本（单次生成元令牌），对于高并发场景仍有压力。
- **未见任务范围有限**：仅评估了常识推理和工具使用，其他领域（如数学、代码、多模态）有待验证。
- **专家池规模固定**：训练时专家数量预定义，可能无法动态扩充。
- **潜在公平性问题**：未见任务虽无训练，但生成元令牌仍依赖云模型的能力，可能在不同云模型间性能波动。
- **训练成本未详细报告**：未给出完整训练时长或能源消耗数据。
- **压缩极限未探索**：10.1x压缩虽高，但在超长提示（如长文档）下的泛化未涉及。

（完）
