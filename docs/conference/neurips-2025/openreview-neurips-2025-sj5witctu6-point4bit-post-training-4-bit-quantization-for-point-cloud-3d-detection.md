---
title: "Point4Bit: Post Training 4-bit Quantization for Point Cloud 3D Detection"
title_zh: Point4Bit：面向点云3D检测的训后4位量化
authors: "Jianyu Wang, Yu Wang, Shengjie Zhao, Sifan Zhou"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=sj5wiTCtu6"
tags: ["query:edge-llm"]
score: 10.0
evidence: 4位训后量化为边缘设备上的点云3D检测，实现低精度神经网络推理
tldr: 提出首个通用4位训后量化框架Point4Bit，通过前景感知分段激活量化和自适应缩放技术，使基于体素的3D检测器能在边缘设备上以INT4精度高效运行，显著降低计算和内存需求。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-sj5witctu6/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1180, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-sj5witctu6/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1029, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-sj5witctu6/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1171, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-sj5witctu6/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1437, \"height\": 2077, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-sj5witctu6/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1433, \"height\": 1580, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1439, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1445, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1448, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1456, \"height\": 556, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1448, \"height\": 462, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 734, \"height\": 91, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 742, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 537, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 540, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 534, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 747, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 730, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 748, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-sj5witctu6/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 982, \"height\": 325, \"label\": \"Table\"}]"
motivation: 点云检测模型计算量大，现有量化方法不支持INT4，限制边缘部署。
method: 设计前景感知分段激活量化和自适应缩放，实现4位PTQ。
result: 在多个数据集上，以4位精度保持检测性能，大幅减少资源消耗。
conclusion: 4位量化为点云检测在资源受限边缘设备上的部署开辟了新途径。
---

## Abstract
Voxel-based 3D object detectors have achieved remarkable performance in point cloud perception, yet their high computational and memory demands pose significant challenges for deployment on resource-constrained edge devices. Post-training quantization (PTQ) provides a practical means to compress models and accelerate inference; however, existing PTQ methods for point cloud detection are typically limited to INT8 and lack support for lower-bit formats such as INT4, which restricts their deployment potential. In this paper, we present Point4bit, the first general 4-bit PTQ framework tailored for voxel-based 3D object detectors. To tackle challenges in low-bit quantization, we propose two key techniques: (1) Foreground-aware Piecewise Activation Quantization (FA-PAQ), which leverages foreground structural cues to improve the quantization of sparse activations; and (2) Gradient-guided Key Weight Quantization (G-KWQ), which preserves task-critical weights through gradient-based analysis to reduce quantization-induced degradation. Extensive experiments demonstrate that Point4bit achieves INT4 quantization with minimal accuracy loss with less than 1.5\% accuracy drop. Moreover, we validate its generalization ability on point cloud classification and segmentation tasks, demonstrating broad applicability. Our method further advances the bit-width limitation of point cloud quantization to 4 bits, demonstrating strong potential for efficient deployment on resource-constrained edge devices.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义
- **研究背景**：基于体素的3D目标检测器在点云感知中性能优异，但其高昂的计算与内存需求严重阻碍了在资源受限的边缘设备（如车载平台）上的部署。
- **核心问题**：现有针对点云检测的训练后量化方法通常局限于INT8精度，一旦强行降至INT4精度，性能会急剧恶化，无法兼顾极低比特带来的计算加速与模型精度保持。
- **整体含义**：论文提出了**Point4bit**，这是首个面向体素3D检测器的通用4-bit PTQ框架，成功将点云量化推进至4比特，为在边缘设备上高效、高精度地部署点云感知模型提供了可行路径。

### 论文提出的方法论
Point4bit框架的核心在于两个互补技术，分别针对激活和权重的极低比特量化难点。

- **核心思想**：不再将所有激活或权重视为同一分布进行统一量化，而是自动识别对任务至关重要的“前景”区域和“关键”权重，对其施加更精细、更高保真度的量化策略，从而在极低比特下最大限度保留任务相关特征。

- **关键技术一：前景感知分段激活量化**
  - **问题**：点云激活图高度稀疏，且前景物体（如车辆）对应的激活值强度远高于背景，均匀量化的舍入误差会严重破坏这些稀疏但关键的语义信息。
  - **自适应前景识别**：通过对每层BEV特征图逐通道计算平均激活值，选出强度最高的前 $K$ 个非空体素位置。论文通过可视化验证，这些位置与真实边界框高度重合，因此能够以无监督方式自动定位前景。
  - **分段量化**：对筛选出的前景激活值，基于累积分布函数划分若干区间，确保每个区间包含相同概率质量，并独立计算量化尺度；对背景区域则采用常规策略。这相当于对数据密集区分配更多量化等级，减少了整体量化误差。

- **关键技术二：梯度引导的关键权重量化**
  - **问题**：在4比特量化下，权重可表示值极度稀疏，舍入误差对任务敏感权重造成的破坏尤甚。
  - **权重敏感度评估**：对校准数据执行一次前向-后向传播，根据任务总损失对权重的平均梯度幅值，评估每个输出通道的敏感度。
  - **差异化量化**：按敏感度对通道排序，保留顶部一定比例（$m_2$）作为“关键”通道，并在量化损失函数中对这些通道的舍入误差施加更大惩罚权重，从而促使优化过程对其保留更高保真度。

- **算法流程**
  1. 在小型无标签校准数据集上，先通一遍前向-后向传播，用公式计算各层权重通道的梯度敏感度 $\alpha_{\ell j}$。
  2. 基于 $\alpha_{\ell j}$ 与舍入误差项，构建联合损失，用网格搜索为所有权重通道优化量化参数。
  3. 再次前向传播校准数据，收集中间层激活特征图。
  4. 根据公式自适应分离出 $X_{fg}$ 和 $X_{bg}$。
  5. 对 $X_{fg}$ 用基于CDF的分段量化计算各区间尺度 $s_k^{fg}$；对 $X_{bg}$ 用网格搜索优化尺度 $s_{bg}$。

### 实验设计
- **数据集与场景**：
  - **3D目标检测（主任务）**：在大规模自动驾驶数据集 **nuScenes** 上进行，评测指标为mAP（平均精度均值）和NDS（nuScenes检测分数）。
  - **泛化性验证**：在 **ModelNet40** 和 **ScanObjectNN** 上进行点云分类（评测OA、mAcc）；在 **SemanticKITTI** 上进行点云语义分割（评测mIoU）。
- **基准模型**：体素检测器（CP-Voxel, VoxelNeXt, PillarNeXt）、分类模型（PointNet++, PointNeXt）、分割模型（LargeKernel3D）。
- **对比方法**：与主流的PTQ基线方法进行全面对比，包括 **RTN（朴素量化）**、**RTN+GS（网格搜索）**、**PD-Quant**、**QDrop** 以及专门的3D检测量化方法 **LiDAR-PTQ**。
- **量化位宽**：系统评估了W8A8、W4A8、W4A4以及极限的W3A3精度设定。

### 资源与算力
- **硬件**：所有实验均在**单张NVIDIA Tesla V100 GPU**上完成。
- **校准开销**：校准数据集极小（nuScenes上仅用256帧，占训练集0.91%），量化时间极短。例如，在CP-Voxel模型上，Point4bit仅需约**39.1分钟**，相比LiDAR-PTQ（224.4分钟）快了近6倍，且远快于PD-Quant和QDrop等其他方法。

### 实验数量与充分性
- **实验组数丰富**：论文包含大量实验，充分验证了方法的有效性和鲁棒性。
  - **主结果表**：在3种检测模型（CP-Voxel, VoxelNeXt, PillarNeXt）、4种位宽设定下，与6种基线方法对比。
  - **任务泛化表**：在分类（2个数据集×2种模型）和分割（1个数据集×1种模型）任务上，多种位宽设定下与基线对比。
  - **消融实验**：对两个核心模块分别进行消融，验证了其互补性；并对关键超参数（前景选择比例 $m_1$、分段数 $m$、关键权重比例 $m_2$、分区策略、校准集大小）进行了细致的单变量控制分析。
  - **效率与可视化**：报告了推理速度（FPS）和量化前后检测、分割效果的可视化对比。
- **客观公平性**：所有实验均与公开的基线方法在相同数据、相同评价指标下进行对比，校准数据规模和实验设置均有明确说明，对比客观可信。

### 论文的主要结论与发现
1.  **突破位宽限制**：Point4bit是首个能将通用点云3D检测、分类、分割模型成功量化至**W4A4**精度且保持几乎无损性能的PTQ框架。
2.  **优越的性能**：在W4A4设定下，Point4bit在nuScenes检测任务上仅以不到**1.5%** 的mAP损失大幅领先所有基线方法，而多数基线方法在此设定下会彻底崩溃。
3.  **极强泛化能力**：该方法不仅在3D检测上有效，在没有额外修改的情况下，直接迁移到点云分类和语义分割任务上同样取得优异结果，显示出框架的通用性。
4.  **实际部署潜力**：在Jetson AGX Orin上，W8A8量化模型实现了近**3倍**的真实加速，证明了量化技术对点云模型部署的现实价值。

### 优点
- **创新性强**：首次将PTQ带到点云感知的4比特领域，并针对点云数据的稀疏性与结构性，提出前景感知和梯度引导两大巧妙的非对称保护机制。
- **方法优雅高效**：整个过程无需标签数据和反向传播训练，仅基于分布统计和少量校准数据的梯度，量化耗时短，部署成本极低，实用价值高。
- **论证扎实全面**：实验设计极为详尽，覆盖多个主流模型、多个感知任务、多种位宽，并通过大量消融实验深刻揭示了各组件与参数的作用机理，结论非常可信。
- **理论与工程结合**：既有从数据分布（CDF）出发的理论优化，又验证了在真实硬件上的实际加速效果，做到了“研以致用”。

### 不足与局限
- **硬件支持滞后**：论文明确指出，当前边缘设备（如NVIDIA Orin）的推理库（如TensorRT）对稀疏卷积（spconv）的4-bit推理支持尚不成熟，因此W4A4的实际加速效果目前仍无法在边缘设备上实现，仅停留在学术论证阶段。
- **极端低位宽探索有限**：即使论文展示了W3A3的结果（32.98% mAP），但与全精度性能差距巨大，离实用还有距离。
- **单数据源验证**：尽管任务泛化性好，但3D检测的核心结论主要基于nuScenes数据集，缺少在更多样化（如不同天气、不同传感器）的自动驾驶数据集上的验证，这在一定程度上限制了其鲁棒性的普遍说服力。

（完）
