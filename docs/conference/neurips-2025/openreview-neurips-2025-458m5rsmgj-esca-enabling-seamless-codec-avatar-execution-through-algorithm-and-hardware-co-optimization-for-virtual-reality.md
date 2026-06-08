---
title: "ESCA: Enabling Seamless Codec Avatar Execution through Algorithm and Hardware Co-Optimization for Virtual Reality"
title_zh: ESCA：通过算法与硬件协同优化实现虚拟现实中无缝的Codec Avatar执行
authors: "Mingzhi Zhu, Ding Shang, Sai Qian Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=458m5RSMgJ"
tags: ["query:edge-llm"]
score: 9.0
evidence: 训后量化和定制硬件用于资源受限VR设备上的实时推理
tldr: 针对VR头显等资源受限设备上的Codec Avatar模型，提出高效的训后量化方法和定制硬件加速器，在低精度下实现实时推理且保持输出质量，解决了延迟和功耗关键问题。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-458m5rsmgj/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 645, \"height\": 224, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-458m5rsmgj/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1429, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-458m5rsmgj/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1449, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-458m5rsmgj/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1424, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-458m5rsmgj/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1446, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-458m5rsmgj/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1436, \"height\": 574, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-458m5rsmgj/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1376, \"height\": 822, \"label\": \"Table\"}]"
motivation: VR设备上的Codec Avatar模型计算量大，难以实现实时推理。
method: 提出适配Codec Avatar的训后量化方法，并设计定制硬件加速器。
result: 在VR头显上以低精度执行，推理速度满足实时要求且质量不降低。
conclusion: 算法与硬件协同优化是实现VR应用中实时Avatar执行的有效途径。
---

## Abstract
Photorealistic Codec Avatars (PCA), which generate high-fidelity human face renderings, are increasingly being used in Virtual Reality (VR) environments to enable immersive communication and interaction through deep learning–based generative models. However, these models impose significant computational demands, making real-time inference challenging on resource-constrained VR devices such as head-mounted displays (HMDs), where latency and power efficiency are critical.
To address this challenge, we propose an efficient post-training quantization (PTQ) method tailored for Codec Avatar models, enabling low-precision execution without compromising output quality. In addition, we design a custom hardware accelerator that can be integrated into the system-on-chip (SoC) of VR devices to further enhance processing efficiency.
Building on these components, we introduce ESCA, a full-stack optimization framework that accelerates PCA inference on edge VR platforms. Experimental results demonstrate that ESCA boosts FovVideoVDP quality scores by up to +0.39 over the best 4-bit baseline, delivers up to 3.36× latency reduction, and sustains a rendering rate of 100 frames per second in end-to-end tests, satisfying real-time VR requirements. These results demonstrate the feasibility of deploying high-fidelity codec avatars on resource-constrained devices, opening the door to more immersive and portable VR experiences.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：VR 头显（HMD）上的真实感 Codec Avatar（PCA）需实时渲染高保真人脸，但其解码器依赖大量转置卷积，计算开销极大，导致延迟和功耗过高，难以在资源受限的边缘设备上满足 90 FPS 的实时要求。
- **核心挑战**：
  - 训后量化（PTQ）难以直接应用：激活异常值（长尾分布）严重，尤其在转置卷积层；且现有平滑/旋转方法（如 SmoothQuant、QuaRot）因转置卷积的特殊结构和非线性激活（LeakyReLU）而失效。
  - 硬件利用率低：转置卷积的 im2col 变换导致激活矩阵极度稀疏（>85% 零值），传统脉动阵列的 MAC 利用率低下。
- **整体含义**：提出一种“算法-硬件”全栈协同优化框架 **ESCA**，通过定制量化策略和专用加速器，在 4-bit 低精度下实现 100 FPS 的实时 PCA 推理，且不牺牲视觉质量。

## 2. 方法论
ESCA 由四个紧密耦合的技术组件构成：

### 2.1 输入通道激活平滑（ICAS）
- **核心思想**：为转置卷积的每个输入通道引入缩放因子 \(s_c\)，激活乘 \(s_c\)，对应权重通道除以 \(s_c\)，保持输出数学等价，从而均衡通道间激活幅度，抑制异常值对量化的干扰。
- **关键公式**：
  - 缩放因子：\(s_c = \frac{(\max_{m,n} X[c,m,n])^\alpha}{(\max_{c_o,k,h} W[c,c_o,k,h])^{1-\alpha}}\)，\(\alpha\) 控制平滑强度（取 0.8）。
  - 可融合性证明：缩放可被吸收到前一层的权重和偏置中，无需运行时额外操作（附录 A/B 给出严格证明）。

### 2.2 面部特征感知平滑（FFAS）
- **核心思想**：利用预定义的面部区域掩码（眼、嘴等），计算各通道在关键区域的激活方差。对方差最大的 top-k% 通道跳过 ICAS 平滑（\(s_c=1\)），以保护高频细节（如皱纹、唇形）。
- **公式**：\(\sigma^2_c(R_l^c) = \frac{1}{|R_l^c|} \sum_{(m,n)\in R_l^c} (X_l[c,m,n] - \mu_c)^2\)，取前 k=75% 通道豁免平滑。

### 2.3 UV 加权 Hessian 指导的权重量化（UV-Weighted PTQ）
- **核心思想**：基于解码器输出的 UV 纹理坐标，生成像素级面部重要性权重 \(W_{uv}\)（关键区域如眼、嘴权重高，不可见区域为 0）。
- **步骤**：
  1. 将各层输入激活与下采样的 UV 重要性权重相乘以获得加权激活。
  2. 计算加权 Hessian 矩阵：\(H_{uv}^l = \frac{1}{S} \sum_{s=1}^S (2(W_{uv}^l \cdot X_{l s}) * (W_{uv}^l \cdot X_{l s})^T) + \lambda I\)。
  3. 采用 GPTQ 式贪心量化，利用该加权的 Hessian 的逆来补偿列量化误差，使面部关键区域误差惩罚更大。

### 2.4 定制硬件加速器与优化管线
- **输入合并机制**：针对 im2col 后的激活矩阵，将 4×4 tile 分为全零 tile 和有 checkerboard 稀疏的 tile，丢弃全零 tile，垂直堆叠剩余 tile，压缩输入。
- **PE 微架构**：每个 PE 预载两个权重，接收两个激活（其中一个是零），通过多路选择器选出非零激活及其对应权重，每周期只做一次 MAC，从而绕过约 75% 的冗余计算。
- **优化管线**：编码与传输、解码与传输并行，多帧重叠，最终将有效帧率提升至 100 FPS。

## 3. 实验设计
- **数据集与场景**：使用 MultiFace 数据集，包含 65 种脚本表情，分别渲染为正面、左 45°、右 45° 三个视角。另选三种自发表情（噤声、惊讶、皱眉）测试泛化性。
- **评价指标**：以 FovVideoVDP（VDP，专为宽视场 VR 设计的感知视频质量指标）为主要指标，LPIPS 等作为辅助。
- **对比基线**：
  - 全精度浮点模型（Full Model）。
  - 经典 PTQ：AdaRound + LSQ， GPTQ。
  - 针对超分的 2DQuant。
  - 专为 Codec Avatar 设计的 POCA。
  - 消融版本：仅 UV-W（无平滑）、仅 ICAS、ICAS-UV（无 FFAS）、FFAS-UV（完整 ESCA）。
- **精度设置**：W4A4 和 W8A8。
- **硬件基线**：SoC 为 Snapdragon XR2 Gen 2（Quest 3），GPU 渲染模拟为 NVIDIA Tesla T4（匹配 Jetson Orin NX）。

## 4. 资源与算力
- 量化部分的校准在 **NVIDIA A100 GPU** 上进行，使用 512 帧样本完成离线校准（PTQ 无需重训练）。
- 硬件加速器的延迟通过架构模拟器评估，并未在真实的硅片或 FPGA 上实现。论文未明确给出 A100 的算力占用或校准耗时，仅说明校准数据规模（512 帧），无需大规模训练。
- 推理延迟比较基于模拟加速器与骁龙平台，渲染部分在 T4 GPU 上实测。

## 5. 实验数量与充分性
- **主要量化实验**：4 种精度组合 ×（3 个视角）× 约 10 个方法，总计 120+ 项测试，覆盖全面。
- **消融实验**：通过组件拆分（ICAS、UV-W、ICAS-UV、FFAS-UV）清晰展示了各模块的贡献。
- **泛化实验**：额外对 3 种自发表情在 3 个视角下进行 4-bit 量化测试。
- **系统实验**：量化加速器的延迟对比（编码/解码/端到端管线），以及帧率分析。
- **公平性**：所有方法均基于相同的预训练 float32 解码器，使用相同校准集，对比公平。

## 6. 主要结论与发现
- **质量**：在 4-bit 下，完整 ESCA（FFAS-UV）的 VDP 较最佳基线 GPTQ 提升 +0.39，且视角间一致性更好（正面-侧面差距缩小）。在 8-bit 下亦保持优势。
- **延迟**：输入合并机制使解码器延迟从 42ms 降至 12.5ms（8-bit），在 4-bit 下进一步降至 3.13ms，实现 3.36× 加速。
- **吞吐**：优化后的端到端管线达到 100 FPS，满足 VR 实时性要求。
- **泛化**：在未见过的自发表情上，ESCA 仍显著优于 GPTQ。

## 7. 优点
- **算法-硬件协同**：针对 PCA 解码器的特有结构（转置卷积、面部纹理）进行全栈定制，而非通用方案。
- **理论完备**：给出了通道平滑在转置卷积及融合至前层的数学证明，保证了等价性。
- **细粒度保护**：FFAS 根据面部区域动态保留关键通道，避免细节丢失；UV 加权 Hessian 将纹理重要性与量化误差直接挂钩。
- **硬件效率**：输入合并机制巧妙利用了转置卷积的棋盘稀疏性，极大提升脉动阵列利用率，且仅需微小 PE 修改（增加多路选择器）。

## 8. 不足与局限
- **强依赖 UV 先验**：FFAS 和 UV 加权量化均假定存在精确的面部 UV 映射，对于泛化到无 UV 映射的任务存在局限。
- **加速范围有限**：硬件加速器仅针对解码器部分设计，编码、传输、渲染等环节未一并优化，亦未考虑传感器等其他延迟。
- **模拟环境**：加速器性能基于模拟，未在真实芯片或 FPGA 上验证，实际硅开销和功耗未知。
- **数据集与视角单一**：仅在 MultiFace 的 65 种表情和固定视角下测试，不同光照、遮挡或更大幅度的姿态变化下的鲁棒性有待验证。

（完）
