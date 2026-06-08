---
title: "EUGens: Efficient, Unified and General Dense Layers"
title_zh: "EUGens: 高效、统一且通用的稠密层"
authors: "Sang Min Kim, Byeongchan Kim, Arijit Sehanobish, Somnath Basu Roy Chowdhury, Rahul Kidambi, Dongseok Shim, Kumar Avinava Dubey, Snigdha Chaturvedi, Min-hwan Oh, Krzysztof Marcin Choromanski"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=tIR9Naukr3"
tags: ["query:edge-llm"]
score: 10.0
evidence: 提出高效稠密层替代标准全连接层，用于资源受限的实时应用
tldr: 针对全连接层造成的神经网络计算与参数瓶颈，本文提出一种高效、统一且通用的稠密层EUGens，利用随机特征近似标准全连接层并融入输入范数依赖，从而大幅降低推理复杂度。实验表明，EUGens在保持性能的同时显著提升效率，特别适用于资源受限的实时应用，为边缘设备上的神经网络部署提供了新的基础模块。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1290, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1332, \"height\": 401, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1413, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1400, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1414, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1426, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1409, \"height\": 313, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1409, \"height\": 328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1392, \"height\": 303, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 758, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1449, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 796, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1394, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1342, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1369, \"height\": 2166, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 591, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1361, \"height\": 1716, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1419, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1293, \"height\": 1940, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1427, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1437, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1326, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1357, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1409, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1384, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1426, \"height\": 1194, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1423, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1384, \"height\": 328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 1434, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 1420, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 849, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tir9naukr3/fig-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 1419, \"height\": 295, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1433, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1445, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1504, \"height\": 500, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 950, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1120, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1132, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1451, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1317, \"height\": 398, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 900, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1300, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 955, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1133, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-tir9naukr3/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 837, \"height\": 415, \"label\": \"Table\"}]"
motivation: 全连接层是神经网络计算和参数的瓶颈，限制模型在资源受限环境中部署。
method: 利用随机特征近似标准全连接层，并引入对输入范数的依赖，提出统一的高效稠密层EUGens。
result: EUGens在降低推理复杂度的同时保持模型性能，优于现有高效层扩展方法。
conclusion: 为资源受限的实时推理提供了有效的基础组件，推动神经网络在边缘设备的应用。
---

## Abstract
Efficient neural networks are essential for scaling machine learning models to real-time applications and resource-constrained environments. Fully-connected feedforward layers (FFLs) introduce computation and parameter count bottlenecks within neural network architectures.  To address this challenge, in this work, we propose a new class of dense layers that generalize standard fully-connected feedforward layers, $\textbf{E}$fficient, $\textbf{U}$nified and $\textbf{Gen}$eral dense layers (EUGens).  EUGens leverage random features to approximate standard FFLs and go beyond them by incorporating a direct dependence on the input norms in their computations. The proposed layers unify existing efficient FFL extensions and improve efficiency by reducing inference complexity from quadratic to linear time. They also lead to $\textbf{the first}$ unbiased algorithms approximating FFLs with arbitrary polynomial activation functions. Furthermore, EuGens reduce the parameter count and computational overhead while preserving the expressive power and adaptability of FFLs. We also present a layer-wise knowledge transfer technique that bypasses backpropagation, enabling efficient adaptation of EUGens to pre-trained models. Empirically, we observe that integrating EUGens into Transformers and MLPs yields substantial improvements in inference speed (up to $\textbf{27}$\%) and memory efficiency (up to $\textbf{30}$\%) across a range of tasks, including image classification, language model pre-training, and 3D scene reconstruction. Overall, our results highlight the potential of EUGens for the scalable deployment of large-scale neural networks in real-world scenarios.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将基于所提供的论文内容，以 Markdown 格式对该论文进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义

*   **研究问题**：全连接前馈层是 Transformer、隐式神经表示等现代神经网络架构的核心组件，但也是计算和参数量的主要瓶颈。其推理复杂度为二次方，严重阻碍了模型在实时应用和资源受限环境中的规模化部署。
*   **研究动机**：为提高神经网络的效率，现有方法（如剪枝、量化、低秩近似等）存在局限，无法在保持全连接层表达力的同时，将其推理复杂度从二次方降低到线性。因此，需要一种在计算效率和表达能力之间取得更好平衡的新机制。
*   **整体含义**：论文旨在提出一种名为 EUGens 的新型高效稠密层，它不仅能作为标准全连接层的通用近似，还能统一现有高效层的扩展，为在现实世界场景中部署大规模网络提供关键的效率提升，是向更高效神经网络基础模块迈出的重要一步。

### 2. 论文提出的方法论

*   **核心思想**：
    *   EUGens 层的核心创新在于解耦了对权重（W）和输入（x）的处理。它使用非线性映射函数 `f(x)` 和 `g(W)` 分别将输入和权重变换到低维空间，然后通过点积等线性操作将它们连接起来。
    *   这种方法受到随机特征核心思想的启发，将全连接层的计算视为一个核方法，从而将推理复杂度从关于维度 `d` 的 `O(d²)` 优化为线性时间 `O(mdk²)`，当 `m ≪ d` 时，可获得显著增益。

*   **关键技术细节与公式**：
    *   **通用公式**：一个 `k` 阶 EUGen 层定义为： `EUGen_k(w, x) = g(w)⊤ f(x)`。
    *   **输入/权重变换**： `f(x)` 和 `g(w)` 基于输入 `x` 和权重 `w` 的 Kronecker 积（Hadamard 积）与随机投影矩阵 `G_ij` 的乘积构建。具体而言，它们是对从 0 到 `k` 阶的乘积项的拼接结果，再进行元素级非线性映射 `Φ` 和 `Ψ`。
    *   **无偏估计**：**定理 3.1** 首次证明了对于具有任意多项式激活函数 `f(x) = Σ a_i x^i` 的全连接层，通过选择特定分布的零均值随机投影矩阵 `G_ij` 并将 `Φ` 和 `Ψ` 设为单位函数，EUGens 可以提供无偏估计，即 `E[EUGen(W, x)] = f(Wx)`。
    *   **浓度界**：**定理 3.2** 和 **3.3** 提供了该无偏估计的方差和指数级浓度界，证明了近似误差随着随机特征数量 `m` 的增加而指数级收敛。
    *   **扩展与改进**：EUGens 还能直接依赖输入范数 `||x||²`，使其能超越标准全连接层。此外，通过引入准蒙特卡洛技术（如使用高斯正交矩阵）可以进一步减少估计方差。

### 3. 实验设计

*   **数据集/场景**：
    *   **合成实验**：用于评估近似质量。
    *   **语言模型预训练**：在 OpenWebText 数据集上预训练 GPT-2 架构。
    *   **图像分类**：使用 ViT-Base 和 ViT-L 架构在 ImageNet 和 Places365 数据集上进行评估。
    *   **3D场景重建**：
        *   **NeRF 系列**：在 Synthetic NeRF 数据集上评估 NeRF；在 `360_v2` 数据集上评估 Mip-NeRF 360 和 Zip-NeRF；在 D-NeRF 数据集上评估动态场景重建。
        *   **iSDF**：在 ReplicaCAD 场景数据集上评估隐式符号距离场重建。
*   **对比方法（Benchmark）**：
    *   **合成实验**：低秩近似（Low Rank）和 SNNK 。
    *   **GPT-2/T5**：标准 GPT-2/T5 以及用低秩矩阵替换全连接层的版本。
    *   **ViT**：标准 ViT 和使用低秩近似替换的 ViT。
    *   **3D重建**：各场景的原始模型，如 NeRF、Mip-NeRF 360、Zip-NeRF、D-NeRF、iSDF。
*   **评估场景**：不仅包括从头训练，还包含一种无需反向传播的逐层知识蒸馏框架，用于将预训练模型中的全连接层直接替换为 EUGens。

### 4. 资源与算力

*   **GPU 型号与数量**：
    *   GPT-2 预训练：4 块 NVIDIA A6000 GPU。
    *   其余大部分实验（如 NeRF、iSDF、合成实验）：单块 NVIDIA RTX 4090。
*   **训练时长**：
    *   GPT-2 预训练：共 5 万次迭代，处理约 368 亿个 Token。
    *   图像分类（ViT）：在 ImageNet 上训练 300 个 epoch；在 Places365 上训练 80,000 步。
    *   **明确说明**：文中仅提及部分实验的 GPU 配置和训练轮次，未对所有实验的完整训练总时长（墙钟时间）进行系统性报告。

### 5. 实验数量与充分性

*   **实验数量与覆盖度**：实验设计非常充分且全面，覆盖了从**合成数据**到**真实世界应用**的多种模态和任务，包括：
    *   1 组合成近似质量实验（与 SNNK、低秩对比）。
    *   2 种 Transformer 架构的预训练/微调（GPT-2、BERT），覆盖语言和图像任务。
    *   5 种 3D 场景重建算法（NeRF, Mip-NeRF 360, Zip-NeRF, D-NeRF, iSDF）。
*   **消融研究**：进行了丰富的消融实验，分析了以下关键因素的影响：
    *   可训练 vs. 固定的随机投影矩阵（Gij）。
    *   随机特征的数量（m）。
    *   正交随机特征 vs. 普通随机特征。
    *   使用 ReLU vs. Softplus 激活函数（在 iSDF 中）。
    *   非线性 (`k≥1`) vs. 低秩近似 (`k=1`，`Φ=Ψ=Id`) 的影响。
    *   多项式阶数 `k` 对性能的影响。
*   **客观性与公平性**：实验设置合理，对比了参数匹配的基线模型（如低秩近似、减少隐藏维度的模型），确保了比较的公平性。多个实验在多个随机种子下重复并报告平均值，增加了结果的可靠性。

### 6. 论文的主要结论与发现

*   EUGens 层能够以极高精度近似具有常用激活函数（ReLU, GeLU, Softplus）的全连接层，显著优于低秩近似和 SNNK 方法。
*   在 LLM 预训练（GPT-2）和图像分类（ViT）中，用 EUGens 替换部分全连接层，可以在几乎不影响性能（验证损失/准确率）的情况下，将推理参数量减少最多 **30%**。
*   在 3D 场景重建任务中，集成 EUGens 可在保持相近重建质量（PSNR, L1距离）的同时，将推理速度提升 **6.2% 至 27.3%**。
*   提出一种无需反向传播的分析性知识蒸馏方法，能够快速将预训练模型中的全连接层替换为 EUGen 层，实现零样本或少样本加速，大大降低了部署成本。

### 7. 优点

*   **坚实的理论基础**：提供了关于无偏估计、方差和浓度界的严格数学证明，特别是首次实现了对任意多项式激活的无偏近似，理论贡献显著。
*   **性能与效率的优异权衡**：在多种架构和任务中一致地展示了 EUGens 能以极小的性能代价换取了显著的推理速度和内存效率提升，优于现有基线。
*   **广泛的适用性与统一性**：作为一个通用模块，EUGens 可以无缝集成到 Transformer、NeRF、iSDF 等多种主流架构中，展示了其强大的通用性。
*   **实用的蒸馏框架**：提出的闭环知识蒸馏方法极具实用价值，允许用户对已有的大模型进行快速后训练压缩，而无需从头开始的昂贵重训。

### 8. 不足与局限

*   **实验覆盖**：虽然应用场景广泛，但所选的 Transformer 模型规模相对较小（如 86M/124M 参数的 ViT/GPT-2），其在千亿/万亿参数级别超大模型上的扩展性尚待验证。
*   **理论局限性**：无偏估计算法的证明目前仅对**多项式激活函数**严格成立。对于更广泛或常用的连续激活函数，论文提供的是间接的近似理论（定理 3.4），而非直接的无偏估计设计。
*   **速度-质量权衡**：性能增益高度依赖于随机特征数量 `m` 的选取，增加 `m` 会提升质量但降低速度，需要针对具体应用进行权衡调优。对于某些高精度任务，这可能需要较复杂的调参过程。
*   **算力细节披露**：论文未系统报告所有实验的完整 GPU 训练时长（墙钟时间），仅部分提及。这对于全面评估其训练效率增益（相对于推理效率）构成了信息缺失。
*   **对边缘设备的针对性**：论文主要关注推理加速和模型压缩，但未深入探讨 EUGens 在特定边缘硬件（如 NPU、移动端 GPU）上的针对性优化或部署效果，当前的“速度提升”仍是基于通用 GPU 的测量。

（完）
