---
title: "RWKVQuant: Quantizing the RWKV Family with Proxy Guided Hybrid of Scalar and Vector Quantization"
title_zh: RWKVQuant：对RWKV家族采用代理引导的混合标量与向量量化
authors: "XUCHEN, Yuxuan Yue, Zukang Xu, Xing Hu, JiangyongYu, Zhixuan Chen, Sifan Zhou, Zhihang Yuan, Dawei Yang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=UOw6Qt0qYU"
tags: ["query:edge-llm"]
score: 9.0
evidence: 对RWKV系列进行量化，以实现在资源受限设备上的部署
tldr: 针对RWKV模型部署到资源受限设备面临的量化挑战，发现非线性算子与均匀分布权重的限制，提出代理引导的混合标量和向量量化方法，有效降低模型大小和推理延迟，实现高效部署。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 707, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 968, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1603, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 849, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 715, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1742, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1739, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1740, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uow6qt0qyu/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1669, \"height\": 824, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 720, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1774, \"height\": 805, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 859, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 861, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 870, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 870, \"height\": 477, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 781, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1782, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1775, \"height\": 1784, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1770, \"height\": 2322, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1771, \"height\": 858, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1475, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1053, \"height\": 683, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1249, \"height\": 855, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uow6qt0qyu/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1676, \"height\": 1278, \"label\": \"Table\"}]"
motivation: RWKV在部署时仍面临挑战，现有后训练量化方法导致性能显著下降。
method: 分析RWKV量化约束，提出代理引导的混合量化策略克服非线性和权重分布问题。
result: 在保持性能的同时实现模型压缩和加速。
conclusion: RWKVQuant为RWKV模型的高效部署提供了有效的量化方案。
---

## Abstract
RWKV is a modern RNN architecture with comparable performance to Transformer, but still faces challenges when deployed to resource-constrained devices. 
Post Training Quantization (PTQ), which is a an essential technique to reduce model size and inference latency, has been widely used in Transformer models.
However, it suffers significant degradation of performance when applied to RWKV.
This paper investigates and identifies two key constraints inherent in the properties of RWKV:  (1) Non-linear operators hinder the parameter-fusion of both smooth- and rotation-based quantization, introducing extra computation overhead. (2) The larger amount of uniformly distributed weights poses challenges for cluster-based quantization, leading to reduced accuracy.
To this end, we propose RWKVQuant, a PTQ framework tailored for RWKV models, consisting of two novel techniques: (1) a coarse-to-fine proxy capable of adaptively selecting different quantization approaches by assessing the uniformity and identifying outliers in the weights, and (2) a codebook optimization algorithm that enhances the performance of cluster-based quantization methods for element-wise multiplication in RWKV.
Experiments show that RWKVQuant can quantize RWKV-6-14B into about 3-bit with less than 1\% accuracy loss and 2.14$\times$ speed up.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究动机**：RWKV 作为融合 RNN 与 Transformer 优势的现代序列模型，性能可比肩 Transformer，但庞大的参数量严重阻碍其在资源受限设备上的部署（如 RWKV-6-14B 需约 30GB 内存）。
- **核心问题**：后训练量化（PTQ）是压缩模型、降低推理延迟的关键技术，在 Transformer 模型上已广泛应用。然而，直接将主流 PTQ 方法（标量量化 SQ、向量量化 VQ）迁移至 RWKV 会导致严重的性能退化（精度损失 >16%）。
- **问题根源**：论文识别出 RWKV 的两个固有特性对量化带来的关键约束：
  1. **非线性算子阻碍参数融合**：RWKV 中的 token-shift、Sigmoid、指数函数等非线性模块，阻断了平滑量化和旋转量化中参数的线性融合路径，导致运行时额外开销。
  2. **大量均匀分布权重挑战聚类量化**：与 Transformer 权重相比，RWKV 权重分布更加均匀，使得基于聚类的 VQ 方法聚类损失更大，精度下降更为显著。

## 2. 论文提出的方法论
核心思想是**自适应混合使用标量量化（SQ）和向量量化（VQ）**，利用补偿型 SQ（如 GPTQ）处理均匀分布权重，用 VQ 处理非均匀或有局部异常值的权重。

- **粗-细粒度代理引导的混合量化**
  - 目标：为每一组权重在 SQ 和 VQ 之间做出选择，以最小化模型输出均方误差。为避免指数级搜索，设计高效代理。
  - **粗粒度代理（\(P_c\)）**：基于信息熵评估权重整体均匀性。
    1. 对权重矩阵排序后计算相邻位置间隔，将其归一化为概率分布 \(G'\)。
    2. 计算该分布与完全均匀分布的信息熵差值 \(P_c(G') = H(\hat{G'}) - H(G')\)。
    3. \(P_c\) 越大表示分布越不均匀。若 \(P_c < \tau_c\)，则权重整体均匀，进入细粒度判定；否则直接使用 VQ。
  - **细粒度代理（\(P_f\)）**：检测整体均匀权重中存在的局部异常值。
    1. 对信息熵差值进行泰勒展开，发现其可表示为各阶中心矩（方差、偏度、峰度等）的加权和。
    2. 取加权和的绝对值作为细粒度代理 \(P_f(G') = \sum_{k=2}^{K} v_k |M_k|\)。
    3. 当 \(P_c < \tau_c\) 且 \(P_f < \tau_f\) 时选用 SQ，其他情况选用 VQ。

- **面向元素乘法的码本优化**
  - 针对 RWKV 中独特的元素乘法算子（\(x \odot \mu\)），优化 VQ 码本。
  - 量化损失与激活值平方和误差相关。提出用校准激活值的平方作为重要性权重，指导加权 KMeans 聚类生成码本。
  - 为聚合多批次激活，先对单样本激活值进行百分位截断（剔除长尾异常值）后再求平均，得到更具代表性的期望激活。

## 3. 实验设计
- **数据集与场景**
  - **语言任务**：RWKV-6 和 RWKV-7 系列模型（0.1B ~ 14B），使用 LAMBADA 数据集评估困惑度（PPL），以及 9 个零样本常识推理任务（如 LAMBADA-OpenAI、HellaSwag、PIQA 等）的准确率。
  - **视觉任务**：VRWKV 系列模型，使用 ImageNet（分类，Top-1 Acc）、COCO（检测，Box AP）、ADE20K（分割，mIoU）。
- **对比基准**
  - SQ 类：RTN、GPTQ、AWQ、QuaRot。
  - VQ 类：KMeans、GPTVQ、VPTQ。
- **设置细节**
  - 量化位宽：报告 3.5 bpw 和 3.25 bpw 两种配置；RWKVQuant 最终实现约 3.275 bpw。
  - 所有方法均采用权重仅量化，校准样本数为 128。RWKVQuant 中各模型动态设定阈值，使 SQ (3.25 bpw) ：VQ (3.5 bpw) 层数比约为 9:1。

## 4. 资源与算力
- 论文中**未提供**量化过程（如码本优化、代理计算）所消耗的具体算力，例如 GPU 型号、数量、训练/校准时间。
- 仅提及在 NVIDIA A6000 GPU 上测试最终模型的推理速度与内存占用，未涉及量化阶段算力开销。

## 5. 实验数量与充分性
- **丰富的模型覆盖**：7 种不同规模的语言模型（0.1B~14B）和 2 种视觉模型。
- **多维度评测**：语言、视觉两大跨模态任务，语言任务下包含困惑度与 9 项零样本评测。
- **充分对比**：与 7 种主流 SQ/VQ 方法在两种位宽下对比，并给出与浮点模型的对比。
- **翔实的消融实验**：
  - 验证混合策略 vs 单独使用 GPTQ/GPTVQ。
  - 对比不同代理指标（方差、变异系数、范围、MAD、MSE、仅信息熵）的效果。
  - 消融码本优化对最终精度的影响。
  - 考察超参数 K（泰勒展开阶数）的作用。
  - 附录给出详细的表格对比，实验设计客观、公平且充分。

## 6. 论文的主要结论与发现
- RWKVQuant 能够将 RWKV-6-14B 成功量化至约 3 比特，精度损失小于 1%，同时实现 2.83 倍内存节省和 2.14 倍推理加速。
- 相比单独使用 SQ 或 VQ 方法，混合策略在所有评测模型上均实现更优或可比性能。
- 提出的粗-细粒度代理能有效区分适用 SQ 和 VQ 的权重层，优于单一均匀性指标。
- 针对元素乘法的码本优化进一步提升了量化模型的精度。
- 此项工作首次为 RWKV 家族提供了全面的 PTQ 框架。

## 7. 优点
- **问题洞见深刻**：首次系统分析 RWKV 量化中非线性融合与均匀权重的双重挑战。
- **方法创新合理**：利用信息熵和中心矩构造轻量化代理，避免了搜索的指数复杂度，计算开销仅 \(O(M)\)。
- **针对性强**：为 RWKV 特有的元素乘法设计码本优化，并引入截断均值处理激活分布异常值。
- **实验扎实全面**：覆盖多个规模、多种任务，对比主流方法，消融实验充分验证各模块有效性，公平可信。

## 8. 不足与局限
- **阈值设定依赖经验**： \( \tau_c \) 和 \( \tau_f \) 虽给出基于百分位数的自动化方法，但其比例（如 50%、20%）对所有模型固定，可能不是最优配置，需要进一步自适应该比例。
- **量化比例固定**：文中 SQ 与 VQ 的比例固定在大约 9:1，未探讨不同比例对压缩率和精度的动态权衡。
- **未探索更低位宽与激活量化**：实验限于 3.25~3.5 bpw 权重仅量化，没有讨论 2 比特量化或同时量化激活的效果。
- **校准数据依赖性**：量化过程依赖少量校准样本（128），可能对不同分布的下游任务存在一定的泛化风险。
- **算力细节缺失**：未报告量化过程自身的资源消耗（如码本优化耗时），不利于评估实际部署成本。

（完）
