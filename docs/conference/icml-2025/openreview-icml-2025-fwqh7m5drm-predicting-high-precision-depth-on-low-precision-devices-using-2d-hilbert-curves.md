---
title: Predicting High-precision Depth on Low-Precision Devices Using 2D Hilbert Curves
title_zh: 使用二维希尔伯特曲线在低精度设备上预测高精度深度
authors: "Mykhail Uss, Ruslan Yermolenko, Oleksii Shashko, Olena Kolodiazhna, Ivan Safonov, Volodymyr Savin, Yoonjae Yeo, Seowon Ji, Jaeyun Jeong"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=fwQH7M5DRM"
tags: ["query:edge-llm"]
score: 6.0
evidence: 在低端设备上使用低比特精度进行深度预测
tldr: 针对深度预测网络在低端设备上部署时，低比特量化导致深度动态范围不足的问题，提出利用二维希尔伯特曲线将高动态范围深度分解为两个低动态范围分量，训练全精度网络直接预测后者以恢复高精度深度，从而在保持效率的同时提升深度估计准确度。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 837, \"height\": 759, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 841, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 492, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1759, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 874, \"height\": 225, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 873, \"height\": 281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 832, \"height\": 945, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 851, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 844, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 859, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 632, \"height\": 1081, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1615, \"height\": 893, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1615, \"height\": 1188, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1608, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1612, \"height\": 1819, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1612, \"height\": 1818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1723, \"height\": 931, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1722, \"height\": 928, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1724, \"height\": 931, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1722, \"height\": 928, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1721, \"height\": 923, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fwqh7m5drm/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1779, \"height\": 1769, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-fwqh7m5drm/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1533, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fwqh7m5drm/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fwqh7m5drm/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 600, \"height\": 207, \"label\": \"Table\"}]"
motivation: 深度预测网络计算量大，限制在低端设备上的应用；低比特量化虽提效但精度不足以表示高动态范围深度。
method: 将高动态范围深度表示为希尔伯特曲线的两个低动态范围分量，训练全精度网络预测该分量，再从预测中恢复高精度深度。
result: 方法在保持低比特量化的硬件效率的同时，显著提升了深度预测的精度。
conclusion: 希尔伯特曲线分解策略为低精度设备上的高精度深度预测提供了有效解决方案。
---

## Abstract
Dense depth prediction deep neural networks (DNN) have achieved impressive results for both monocular and binocular data but they are limited by high computational complexity, restricting their use on low-end devices. For better on-device efficiency and hardware utilization, weights and activations of the DNN should be converted to low-bit precision. However, this precision is not sufficient for representing high dynamic range depth. In this paper, we aim to overcome this limitation and restore high-precision depth from low-bit precision predictions. To achieve this, we propose to represent high dynamic range depth as two low dynamic range components of a Hilbert curve, and to train the full precision DNN to directly predict the latter. For on-device deployment, we use standard quantization methods and add a post-processing step that reconstructs depth from the Hilbert curve components predicted in low-bit precision. Extensive experiments demonstrate that our method increases bit precision of predicted depth by up to three bits with little computational overhead. We also observe a positive side effect of quantization error reduction by up to five times. Our method enables effective and accurate depth prediction with DNN weights and activations quantized to eight bit precision.

---

## 论文详细总结（自动生成）

## 1. 论文核心问题与整体含义
- **研究背景**：密集深度预测（单目/双目）在自动驾驶、AR/VR、物联网等领域至关重要，但高精度模型计算量大，难以直接部署在低端设备（如移动端DSP、TPU）上。
- **核心矛盾**：为提升效率，常将DNN的权重与激活值量化为低比特（如INT8），但深度图属于高动态范围信号，8bit精度不足以表示厘米级精度，会产生伪边缘、细节丢失等严重量化噪声。
- **整体目标**：在低精度计算设备上，从低比特预测结果中恢复出高精度深度，同时避免额外的大计算开销。

## 2. 方法论
### 2.1 核心思想：希尔伯特曲线深度表示
- 将高动态范围深度 `q ∈ [0,1]` 映射为二维 **希尔伯特曲线**（一种连续、非自交的空间填充曲线）上的点 `(x(q), y(q))`。
- 曲线长度 `L > 1`，且 `x(q), y(q)` 均被限制在 `[0,1]`，适合低比特量化。
- 深度恢复时，将预测的 `(x, y)` 映射回曲线上最近点，该过程等效于将精度提升 `log₂ L` 位，同时量化误差被压缩 `L` 倍。

### 2.2 关键技术细节
- **曲线选择**：选用希尔伯特曲线（阶数 `p`），长度 `L_p = (2^p+1)(1-2k)`，并缩放使其避开边界。实验验证 `p=2,3` 较优（可增加2~2.85位）。
- **前向/逆向变换**：通过查找表（LUT）实现快速映射，无需复杂运算。
- **网络改造**：将原有单输出头改为双头，分别预测 `x` 和 `y` 分量。在双头前可选加高斯噪声以提升量化鲁棒性。
- **损失函数**：
  ```
  Λ_full = Λ(q_GT, q_xy) + α * Λ_H(x_GT, y_GT, x, y)
  Λ_H = (x_GT - x)² + (y_GT - y)² + β * r²_xy
  ```
  其中 `r_xy` 为预测点到希尔伯特曲线的距离，迫使网络预测点落在曲线上。
- **部署流程**：全精度训练 → 标准量化（QAT/PTQ）→ 片上低比特推理得到 `x, y` → CPU后处理（LUT查表）重建高精度深度。

## 3. 实验设计
### 3.1 数据集
- **主实验**：基于 **ScanNet v2** 渲染双目立体匹配数据，使用PyRender生成左右视图（基线60mm），按官方划分训练/测试。
- **额外实验**：**KITTI 2012**（稀疏真实视差）和 **MS COCO**（人体姿态估计，验证方法泛化性）。

### 3.2 对比基准与平台
- **模型**：**DispNet**（经典卷积架构）和 **DPT**（结合MobileViTv3‑S的Transformer架构）。
- **量化与部署**：使用Qualcomm SNPE SDK v2.24，在 **Samsung S24+（骁龙8 Gen3，Hexagon DSP）** 上测试。
- **对比方案**：
  - 原始模型 vs 希尔伯特版本（不同阶数 `p=1,2,3,4`）
  - 精度格式：FP32（CPU）、FP16（DSP）、W8A16（DSP）、**W8A8（DSP & CPU）**
  - W8A8 CPU模式用于单独分析量化误差（无实际硬件精度损失）
- **评价指标**：常规深度误差（Abs Rel、RMSE、EPE、D1），新增基于离散余弦变换（DCT）的余弦相似度 **SC** 以捕捉轮廓和均匀区域的量化伪影，以及量化误差标准差（Robust SD）。

### 3.3 实验覆盖
- 不同曲线阶数消融
- 原始vs改进模型在不同量化格式下的精度、延迟、功耗
- 量化误差分布分析（沿曲线vs跨曲线）
- 3D网格重建质量对比（TSDF融合）
- 人体姿态估计（热力图回归与直接坐标回归）的通用性验证

## 4. 资源与算力
- 论文**未明确说明**训练所用GPU型号、数量及训练时长。
- 推理端的硬件平台为商用手机Samsung S24+，量化工具为SNPE SDK。
- 功耗测量通过Monsoon Power Monitor进行。

## 5. 实验数量与充分性
- 实验组数较丰富：2种模型 × 5种精度变体 × 多阶曲线，附加KITTI、HPE、网格重建等扩展实验。
- 主表（Table 1）系统比较了FP32、W8A8（DSP/CPU），覆盖多种误差指标，并提供视觉效果图（Fig. 7~9）。
- 量化误差分析（Fig. 10）从统计角度解释了误差压缩机理，并验证了误差独立性的假设。
- 实验整体设计**客观、公平**，同框架下比较原始与改进模型，控制了量化工具、硬件、数据集等变量。

## 6. 主要结论与发现
- **位宽提升**：在W8A8约束下，希尔伯特方法可将深度有效位数提升约2~3位（达到INT10~INT11），大幅减少平面区域伪影。
- **精度恢复**：改进的W8A8模型在DSP上的误差指标接近甚至优于原始W8A16模型，且显著优于原始W8A8。
- **效率增益**：推理延迟降低约1.3~2倍，功耗降至原始W8A16模型的65%左右。
- **量化误差压缩**：旁效应使量化误差降低最高达4.6倍（DispNet p=3, DSP上），原因在于两个分量误差部分去相关，且沿曲线方向误差被压缩。
- **3D重建质量**：改进模型生成的深度图可重建出更平整、少噪声的网格。

## 7. 优点
- **创新性强**：首次将希尔伯特曲线用于量化网络的深度表示，从信号结构层面解决精度瓶颈，而非仅改进量化算法。
- **硬件友好**：后处理仅需一个小LUT，不增加乘加运算；增加的模型参数量与数据搬移极小。
- **即插即用**：可叠加于现有量化方法（PTQ/QAT），对网络架构改动小。
- **额外收益**：意外获得量化误差大幅下降的正向“副作用”，部分任务中无需更高位宽即可提升质量。

## 8. 不足与局限
- **依赖重训练**：需要修改模型并重新训练全精度网络，不能直接用于已部署模型。
- **误差有界要求**：当量化噪声过大时，可能导致映射错误，破坏深度与曲线点的一一对应。
- **任务敏感**：在人体姿态直接回归任务中，两个分量的量化误差呈现强相关性，几乎无误差压缩效果（仅位宽提升），说明收益依赖于任务内部表征的独立性。
- **架构限制**：当前方法仅适用于单次预测深度的一阶段模型，未探讨迭代式优化网络（如GRU细化）的适配。
- **训练细节缺失**：未明确给出训练算力与超参搜索空间，复现成本未知。
- **KITTI实验为稀疏真值**，SC指标无法适用，评价维度略窄。

（完）
