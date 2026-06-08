---
title: "Confident or Seek Stronger: Exploring Uncertainty-Based Small LM Routing From Benchmarking to Generalization"
title_zh: 自信或求助：从基准测试到泛化探索基于不确定性的小模型路由
authors: "Yu-Neng Chuang, Leisheng Yu, Guanchu Wang, Lizhe Zhang, Zirui Liu, Xuanting Cai, Yang Sui, Vladimir Braverman, Xia Hu"
date: 2025-05-10
pdf: "https://openreview.net/pdf?id=smdbra3VEi"
tags: ["query:edge-llm"]
score: 10.0
evidence: 在边缘设备上部署小型语言模型，基于不确定性路由至大模型
tldr: 该论文研究在边缘设备上部署小语言模型（SLM），当SLM置信度低时路由请求至更强大语言模型（LLM）的混合方案。通过不确定性估计实现可靠路由，在保持高效解码的同时提升复杂查询的准确率。这为资源受限设备上的大模型服务提供了一种实用的部署策略。
source: NeurIPS-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-smdbra3vei/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1451, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-smdbra3vei/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1406, \"height\": 780, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-smdbra3vei/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1393, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-smdbra3vei/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1347, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-smdbra3vei/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1452, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-smdbra3vei/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1453, \"height\": 342, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-smdbra3vei/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1457, \"height\": 384, \"label\": \"Table\"}]"
motivation: 边缘设备上小语言模型效率高但精度不足，直接调用大模型成本过高。
method: 提出基于不确定性估计的SLM路由方法，低置信度时卸载至高能力LLM。
result: 在保证边缘设备解码效率的同时，显著提升复杂查询的响应质量。
conclusion: 不确定性路由实现了边缘推理效率与精度的良好平衡，具有实际部署价值。
---

## Abstract
Small language models (SLMs) are increasingly deployed on edge devices for personalized applications, offering efficient decoding latency and reduced energy consumption. However, these SLMs often generate inaccurate responses when handling complex queries. One promising solution is uncertainty-based SLM routing, offloading high-stakes queries to stronger large language models (LLMs) when resulting in low-confidence responses on SLM. This follows the principle of If you lack confidence, seek stronger support to enhance reliability. Relying on more powerful LLMs is yet effective but increases invocation costs. Therefore, striking a routing balance between efficiency and efficacy remains a critical challenge. Additionally, efficiently generalizing the routing strategy to new datasets remains under-explored. In this paper, we conduct a comprehensive investigation into benchmarking and generalization of uncertainty-driven routing strategies from SLMs to LLMs over 5000+ settings. Our findings highlight: First, uncertainty-correctness alignment in different uncertainty quantification (UQ) methods significantly impacts routing performance. Second, uncertainty distributions depend more on both the specific SLM and the chosen UQ method, rather than on downstream data. Building on the insight, we propose a proxy routing data construction pipeline and open-source a hold-out set to enhance the generalization on predicting the routing curve for new downstream data. Experimental results indicate that proxy routing data effectively bootstraps routing performance without any new data.

---

## 论文详细总结（自动生成）

## 一、论文的核心问题与整体含义

- 边缘设备上部署小型语言模型（SLM）具有低延迟、低功耗等优势，但处理复杂查询时准确性不足。
- 一种有前景的解决方案是**基于不确定性的 SLM 路由**：当 SLM 对自身回答置信度较低时，将查询转发给更强的 LLM 处理（“缺乏信心就寻求更强支持”）。
- 这种混合模式虽然可靠，但 LLM 的调用成本高昂，且如何将路由策略高效泛化到新的下游数据和场景仍未被充分探索。
- 本文围绕两个核心问题展开：
  1. 在 SLM→LLM 路由中，**不同不确定性量化（UQ）方法的最佳实践**是什么？
  2. 面对全新数据集时，**如何不依赖该数据就快速建立有效的路由策略**？
- 整体目标是在**效率（成本）与效果（正确性）之间取得实用化的路由平衡**。

## 二、论文提出的方法论

### 1. 不确定性量化（UQ）方法汇总
- 论文评估了 8 种 UQ 方法，分为四个流派：
  - **基于 token/序列概率**：Average Token Prob、Perplexity、p(True)。
  - **基于输出一致性**：Jaccard Degree（多采样计算相似度）。
  - **基于言语化不确定性**：Verbalization‑1s、Verbalization‑2s（模型主动输出置信度）。
  - **基于训练不确定性探针**：Trained Probe（域内训练）、OOD Probe（跨域训练）。

### 2. 路由策略的核心工作方式
- 对每个查询，SLM 先给出回答并提取**置信度分数**。
- 设置一个置信度阈值：  
  - 若 SLM 置信度高于阈值 → 由 SLM 直接回答。  
  - 若低于阈值 → 将查询路由至更强大的 LLM 处理。
- 通过调整阈值，可以得到**路由比例‑整体准确率**曲线，用于选择最佳的工作点。

### 3. 泛化方法：代理路由数据构造流水线（Proxy Routing Data）
- **核心洞察**：不确定性分布主要取决于**SLM 和 UQ 方法**，而与下游具体数据集关系很小。  
- 基于这一发现，提出如下构造流程（见 Algorithm 1）：
  1. 收集多个领域多样的数据集集合 \(D\)。
  2. 对 \(D\) 中所有样本，用选定的 UQ 方法获得不确定性分布，并将该分布划分为 \(M\) 个分箱（bin）。
  3. 从每个分箱中按比例**加权随机采样**一部分实例，形成“代理路由数据集”\(X\)，该数据集在不确定性各水平上与原分布相似。
- 当面对**全新下游数据集**时，可直接使用代理路由数据集来**预测路由曲线**，确定合适的阈值，无需访问任何真实新数据。

## 三、实验设计

### 1. 模型 与 数据集
- **SLM**：12 个开源模型，涵盖非推理型（如 Llama‑3.2‑1B/3B、Phi‑3.5‑mini、Mistral‑7B 等）、推理型（如 Qwen3‑0.6B/1.7B/4B、Phi‑4‑mini‑reasoning）以及 RNN 模型（RWKV‑7‑2.9B）。
- **LLM**：4 个强模型，包括 Llama‑3.1‑70B、Qwen3‑32B、DeepSeek‑R1 以及 GPT‑4.1 mini（API）。
- **数据集**：15 个，覆盖数学推理、常识推理、对话与上下文理解、问题求解四类（如 GSM8K、CommonsenseQA、OpenBookQA、MMLU 等）。

### 2. 基准测试与评估指标
- **基准测试**：5000+ 种组合设定下，比较 8 种 UQ 方法的路由性能。
- **主要评估方式**：
  - ROC AUC：衡量不确定性‑正确性对齐程度。
  - 路由曲线：总体准确率 vs 被路由到 LLM 的查询比例。
  - 相对准确率：在逐步排除低置信度查询后，SLM 准确率与 LLM 准确率的比值。

### 3. 代理路由数据泛化评估
- **全领域外**：目标数据集的领域完全不在源数据集中出现。
- **部分领域内**：用其余 14 个数据集构造代理数据，评估第 15 个目标任务。
- 对比目标：代理数据预测的路由曲线 vs 在全量新数据上得到的真实路由曲线。

## 四、资源与算力

- 所有实验在 **4 张 80 GB NVIDIA A100 GPU** 上完成。
- 文中未明确给出训练总时长或推理时间，但指出部分 UQ 方法（如 Trained Probe、OOD Probe）需要训练多层感知机，代理数据构造也需要批量不确定性计算。
- 开源代码地址已提供（https://anonymous.4open.science/r/quodlibeta），有助于复现和资源估计。

## 五、实验数量与充分性

- **组合覆盖面极广**：12 SLM × 4 LLM × 15 数据集 × 8 UQ 方法，累计超过 5000 种配置。
- **消融与对比维度**：
  - 不同 UQ 方法的对齐性和路由效果对比。
  - 不同模型（非推理、推理、RNN）的置信度特性。
  - 代理路由数据在两种泛化设定（全领域外、部分领域内）下的性能。
- 实验**客观性**：所有方法统一超参数、温度，推理使用固定随机种子；对于自由形式回答，使用 GPT‑4.1 mini 作为评判器；对言述类方法，剔除了未产生置信度的样本。
- 部分结果**平均值基于三次实验运行**，但论文中未展示误差条（在 checklist 中声明为 NA），这在一定程度上影响了显著性判断，但整体实验规模仍很充分。

## 六、论文的主要结论与发现

1. **不确定性与正确性的对齐程度显著影响路由性能**。  
   - Perplexity、Trained Probe、OOD Probe 在多数模型和数据集上对齐更好；  
   - 言语化方法（Verbalization‑1s/2s）在 SLM 中普遍对齐较弱，导致大量正确查询被错误路由。

2. **SLM 在高置信度查询上可达到与 LLM 接近的准确率**。  
   - 通过逐步排除低置信度查询，SLM 在剩余 top‑k% 样本上的相对准确率可显著提升。

3. **置信度分布主要取决于 SLM 和 UQ 方法，与下游数据集关系很小**。  
   - 聚合多个数据集的置信度分布形状高度一致。

4. **代理路由数据可以在无任何新数据的情况下准确预测路由曲线**。  
   - 无论全领域外还是部分领域内设定，代理数据给出的路由曲线都与全量真实数据曲线高度匹配。

## 七、优点

- **大规模系统性基准研究**：覆盖模型、数据集、UQ 方法的组合前所未有，为社区提供了坚实参考。
- **数据‑效率泛化方案**：提出的代理路由数据构造方法无需新的下游数据，在部署初期即可初始化路由策略，实用性强。
- **开源可复现**：提供了匿名代码仓库，实验细节透明。
- **洞察深刻**：揭示了不确定性分布的数据无关性，为路由泛化提供了理论基础；得到了 UQ 方法选择的明确建议。
- **兼顾效率与效果**：通过路由比例‑准确率曲线的分析，指导实际系统在成本和质量间找到“甜点”。

## 八、不足与局限

- **统计显著性报告不完整**：虽然部分结果报告了三次运行的平均值，但未展示误差区间，对算法稳定性无法完全量化。
- **仅限文本场景**：实验未涉及多模态语言模型或视觉‑语言模型的路由，而实际边缘设备可能处理多模态输入。
- **模型和数据集偏差**：使用的 SLM 和 LLM 主要为开源或部分 API 模型，可能不能完全代表工业级极高参数模型的行为；数据集以英文为主，其他语言未覆盖。
- **边缘设备建模不充分**：未深入讨论不同硬件平台（如 iOS vs Android）对路由阈值和推理性能的影响。
- **长期自适应能力未验证**：代理数据在初始部署阶段效果好，但如何持续融合私有数据、在保护隐私下逐步优化路由策略，仍是开放挑战。
- **UQ 方法限制**：代理路由数据效果依赖于所选 UQ 方法的对齐性；若 UQ 本身不可靠，代理数据可能引入偏差。

（完）
