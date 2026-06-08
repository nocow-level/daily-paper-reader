---
title: "DP-LLM: Runtime Model Adaptation with Dynamic Layer-wise Precision Assignment"
title_zh: DP-LLM：通过动态按层精度分配实现运行时模型自适应
authors: "Sangwoo Kwon, Seong Hoon Seo, Jae W. Lee, Yeonhong Park"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ppKDXf55lY"
tags: ["query:edge-llm"]
score: 10.0
evidence: 动态精度分配用于具有运行时约束的端侧LLM
tldr: 针对端侧大语言模型（LLM）的差异化运行时约束，提出DP-LLM机制，利用层敏感度随解码步骤动态变化的特性，动态分配混合精度，实现内存高效的运行时模型自适应，同时满足延迟与精度要求。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 571, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 821, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 732, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 563, \"height\": 305, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1388, \"height\": 354, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 668, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1423, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1363, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1364, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1365, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-ppkdxf55ly/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1365, \"height\": 484, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1397, \"height\": 1058, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1410, \"height\": 484, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 622, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1328, \"height\": 852, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1140, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1325, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1171, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 662, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 990, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1251, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1201, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1131, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1442, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 848, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-ppkdxf55ly/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1302, \"height\": 284, \"label\": \"Table\"}]"
motivation: 端侧LLM需应对变化延迟与精度要求的查询，静态量化难以适应。
method: 观察到各层敏感度随解码步骤变化，提出动态层精度分配机制。
result: 在不同硬件平台上实现了延迟-精度平衡，优于静态混合精度方案。
conclusion: 动态精度分配为端侧LLM部署提供了灵活高效的量化方案。
---

## Abstract
How can we effectively handle queries for on-device large language models (LLMs) with varying runtime constraints, such as latency and accuracy? Multi-scale quantization addresses this challenge by enabling memory-efficient runtime model adaptation of LLMs through the overlaying of multiple model variants quantized to different bitwidths. Meanwhile, an important question still remains open-ended: how can models be properly configured to match a target precision or latency? While mixed-precision offers a promising solution, we take this further by leveraging the key observation that the sensitivity of each layer dynamically changes across decoding steps. Building on this insight, we introduce DP-LLM, a novel mechanism that dynamically assigns precision to each layer based on input values. Experimental results across multiple models and benchmarks demonstrate that DP-LLM achieves a superior performance-latency trade-off, outperforming prior approaches.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- 核心问题：在端侧设备上进行大语言模型（LLM）推理时，如何有效处理不同运行时约束（如延迟和精度）的查询请求。
- 背景与动机：
  - 端侧资源受限，需要运行时模型自适应（runtime model adaptation），即在内存预算内提供不同精度-延迟权衡的模型变体集合（adaptation set）。
  - 现有多尺度量化（multi-scale quantization）虽能高效叠加多种位宽模型，但配置适应集（如何分配精度）仍是一个开放问题：
    - 简单统一精度分配（如整数位宽）无法支持非整数位宽（如3.5-bit），且未利用层间敏感度差异；
    - 静态按层混合精度（layer-wise mixed-precision）可改善，但忽略了**各层对量化的敏感度在解码过程中动态变化**这一关键现象。
  - 论文首次观察到层敏感度随解码步骤变化，据此提出动态按层精度分配方案，以进一步提升性能-延迟权衡。

### 2. 论文提出的方法论
#### 核心思想
- 提出 **DP-LLM（Dynamic-Precision LLM）**，运行时根据每层输入动态选择高低精度。离线阶段为每层确定候选精度集 \(\langle h, l \rangle\) 和选择阈值 \(T\)，运行时通过轻量级“精度选择器”（Precision Selector）估算“相对误差”（relative error）并决定使用 \(h\)-bit 或 \(l\)-bit 权重。

#### 关键技术组件及流程
- **阶段 1：按层最大精度选择**
  - 基于二阶泰勒展开近似量化对损失的影响，利用 Fisher 信息矩阵近似 Hessian，构建整数规划问题，在内存预算内为每层分配最大可用精度 \(B[i]\)。
- **阶段 2：按层平均精度分配**
  - 定义每层平均精度 \(p_i\)（浮点值），候选集为 \(l = \lfloor p_i \rfloor\)，\(h = \lceil p_i \rceil\)。
  - 将原线性层 \(y = W x\) 替换为 \(y = r W_l x + (1-r) W_h x\)，其中 \(r = 1 - (p_i - l)\)。
  - 对 \(p_i\) 进行微调，损失函数加入正则项：  
    \[
    L' = L + \alpha \left( \frac{\sum_i p_i M_i}{\sum_i M_i} - b_{\text{targ}} \right)^2
    \]
    确保整体平均位宽接近目标精度。
- **阶段 3：平均精度转阈值**
  - 在校准集上统计每层相对误差 \(\| \Delta W x \|\) 的分布，取 \(r_i\)-分位数作为阈值 \(T[i]\)，\(r_i = 1 - (p_i - l)\)。
- **运行时精度选择**
  - 采用**混合相对误差估计**（Hybrid Relative Error Estimation）：
    - 对于输入范数与相对误差呈强线性关系的层（\(R^2 > 0.9\)），使用线性回归估计：\(\| \Delta W x \| \approx \| x \| \cdot \alpha + \beta\)（零开销）。
    - 对于其他层，使用随机投影（基于 Johnson-Lindenstrauss 引理）：预计算 \(G = A \Delta W\)，运行时计算 \(\| G x \|\) 近似真实误差。
  - 利用残差连接性质进行**异步估计**：使用上一步残差输出作为当前层输入进行估计，隐藏延迟。

#### 算法流程概览
- 离线：确定每层最大精度 → 微调平均精度 → 统计校准集确定阈值。
- 在线：对每个解码步骤，精度选择器计算相对误差并与阈值比较，动态决定使用 \(h\)-bit 或 \(l\)-bit 权重。

### 3. 实验设计
#### 数据集与基准
- 困惑度评估：WikiText2 和 C4。
- 下游任务评估：GSM8K（数学推理），MBPP（代码生成），BBH（多任务推理），MATH（数学），均采用生成解码方式。
- 延迟评估：使用 gpt-fast 框架（torch.compile），在 NVIDIA Jetson Orin AGX 64GB 和 RTX 4060 Ti 16GB 上测量 TPOT。

#### 对比方法
- **静态层混合精度方案**：LLM-MQ（基于梯度）和 HAWQ-V2（基于 Hessian／Fisher），均建立在 Any-Precision LLM 多尺度量化框架之上。
- 统一精度分配方案（用于说明动机）。
- 为公平比较，所有方法使用相同的内存预算和 Any-Precision 后端，从 3-bit 到 6-bit 支持。

#### 实验设置
- 模型：Llama-3-8B，Phi-3-Medium (14B)。
- 配置：在 5-bit 内存预算下，目标精度从 3.25 到 4.75，步长 0.25；同时评估了 4-bit 和 6-bit 内存预算。
- 校准与微调：使用 C4 训练集 1000 样本，每样本 512 token，微调仅更新 \(p_i\)，学习率 0.01，5 轮。

### 4. 资源与算力
- 微调成本：
  - Llama-3-8B：单张 RTX 3090 (24GB VRAM) 约 1 小时（占用 14GB VRAM）；A100 80GB 约 30 分钟。
  - Phi-3-Medium：单张 RTX 3090 约 2 小时（占用 21GB VRAM）；A100 80GB 约 1 小时。
- 推理延迟测量在两款边缘 GPU 上完成。
- 总体算力要求相对较低，微调可在消费级 GPU 上完成。

### 5. 实验数量与充分性
- 实验覆盖：
  - 两类模型 × 多个目标精度（7 个精度点）× 2 个困惑度数据集 + 4 个下游任务；
  - 不同内存预算（4-bit, 5-bit, 6-bit）；
  - 额外模型尺寸评估（Qwen2.5-3B, Qwen2.5-32B）；
  - 消融实验：近似方法有效性（精确误差 vs 近似误差）、异步估计的效果、候选精度对 \((l, h)\) 选择、校准集敏感性等；
  - 延迟开销详细比较和逐查询 QoS 分布分析。
- 实验设计合理，对比公平（统一框架），且提供了充足的支撑数据来证明动态分配相较于静态方案的性能优势，并且分析了近似引入的开销和误差。

### 6. 论文的主要结论与发现
- 层敏感度在解码过程中动态变化，静态混合精度分配错过了这一动态机会。
- DP-LLM 通过动态层精度分配，在多种模型和数据集上实现了优于静态混合精度方案（LLM-MQ, HAWQ-V2）的性能-延迟权衡。
- 相对误差近似方法（混合估计 + 异步执行）仅引入约 1.45%（Llama-3-8B）和 0.81%（Phi-3-Medium）的延迟开销，且内存开销极小。
- 动态选择能有效匹配目标精度，且对单查询的精度偏离影响很小（99分位有效位宽偏离 <3.3%）。

### 7. 优点
- **新洞察**：首次将层敏感度的解码时动态性用于 LLM 运行时混合精度，概念新颖且有实际潜力。
- **方法系统完整**：从模型最大精度选择、平均精度微调、阈值确定到运行时估算与异步执行，形成完整方案。
- **开销极低**：混合估计和异步策略使动态精度选择的额外延迟和内存占用几乎可忽略。
- **实验翔实**：对比两个强静态基线，多模型、多任务、多精度点，多硬件平台，并包含丰富消融研究。
- **易于部署**：建立在已有 Any-Precision LLM 框架之上，与权重仅量化方案兼容。

### 8. 不足与局限
- **仅针对解码阶段**：预填充阶段未受益，且不适用于仅需对数概率的下游任务。
- **QoS 保证为尽力型**：文中明确指出，动态选择是基于最佳努力的，没有提供严格的 QoS 保证，仅显示实际偏差较小。
- **微调需额外校准数据**：平均精度微调需要小规模校准集，且超参数 α 需针对极低位（3.25）调整。
- **随机投影近似误差**：尽管可控，但非无损，需离线校准 G 矩阵，且其投影维度和精度保证依赖经验选择。
- **权重仅量化的局限**：方案基于权重仅量化，对于内存带宽不是绝对瓶颈的场景（例如大 batch）优势可能减弱。

（完）
