---
title: "BlockDialect: Block-wise Fine-grained Mixed Format Quantization for Energy-Efficient LLM Inference"
title_zh: BlockDialect：面向能效LLM推理的逐块细粒度混合格式量化
authors: "Wonsuk Jang, Thierry Tambe"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Y0yXuQtPn8"
tags: ["query:edge-llm"]
score: 10.0
evidence: 采用FP4变体的逐块细粒度混合格式量化，实现LLM节能推理
tldr: BlockDialect提出逐块细粒度混合格式量化方法，为每个块分配最优数字格式，并引入DialectFP4格式库以适应多样数据分布，从而实现LLM的节能推理。该方法在保持模型准确性的同时大幅降低能耗，为边缘硬件上的LLM部署提供了高效的量化方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 773, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 670, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 700, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1786, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 862, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1784, \"height\": 1231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1776, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-y0yxuqtpn8/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1357, \"height\": 454, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1576, \"height\": 688, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 843, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 720, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 843, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 756, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 758, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1756, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1756, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 872, \"height\": 668, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 714, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1756, \"height\": 1498, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1756, \"height\": 1498, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-y0yxuqtpn8/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1756, \"height\": 1498, \"label\": \"Table\"}]"
motivation: 现有量化方法难以捕捉细粒度块数据分布，导致精度损失。
method: 提出BlockDialect和DialectFP4，为每个块动态选择最优FP4变体格式。
result: 在多种LLM上实现能效提升，精度损失极小。
conclusion: BlockDialect通过细粒度混合格式量化显著降低LLM推理能耗。
---

## Abstract
The rapidly increasing size of large language models (LLMs) presents significant challenges in memory usage and computational costs. Quantizing both weights and activations can address these issues, with hardware-supported fine-grained scaling emerging as a promising solution to mitigate outliers. However, existing methods struggle to capture nuanced block data distributions. We propose BlockDialect, a block-wise fine-grained mixed format technique that assigns a per-block optimal number format from a formatbook for better data representation. Additionally, we introduce DialectFP4, a formatbook of FP4 variants (akin to dialects) that adapt to diverse data distributions. To leverage this efficiently, we propose a two-stage approach for online DialectFP4 activation quantization. Importantly, DialectFP4 ensures energy efficiency by selecting representable values as scaled integers compatible with low-precision integer arithmetic. BlockDialect achieves 10.78% (7.48%) accuracy gain on the LLaMA3-8B (LLaMA2-7B) model compared to MXFP4 format with lower bit usage per data, while being only 5.45% (2.69%) below full precision even when quantizing full-path matrix multiplication. Focusing on how to represent over how to scale, our work presents a promising path for energy-efficient LLM inference.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义
- **研究动机：** 大型语言模型（LLM）的规模快速增长带来严重的内存与计算开销。权值和激活值的量化是缓解该问题的关键技术。
- **现存挑战：** 硬件支持的细粒度块级量化（如Microscaling MX格式）虽能处理异常值，但难以捕捉不同块内细致的数据分布差异，导致量化精度下降。
- **核心思想：** 论文提出 **“如何表示”优于“如何缩放”** 的理念，将每个细粒度块分配最优的数字格式（而不仅仅是统一的缩放因子），从而更精准地适配块内的数据分布，实现高能效LLM推理。

## 方法论
### 1. DialectFP4 格式库
- 基于FP4（E2M1）的16种变体，称为“方言”（dialects），满足三个原则：
  - **覆盖全部最大幅值**：每种方言的最大表示值不同。
  - **优先表示大幅度值**：不同方言在较大幅值区域有不同的取值分布。
  - **硬件高效**：表示值均以0.5为粒度，可与低精度整数算术兼容。
- 每个数据点存储为 4 位（1位符号，3位索引），每块额外用 4 位标识方言索引。

### 2. 逐块最优方言选择（两阶段在线选择）
- **预处理**：基于块内最大值计算5位共享指数，将元素左移对齐至[0,8)范围，得到5位中间表示（3位整数、2位小数）。
- **第一阶段**：根据块的截断最大值选择对应最大幅值的一对方言，避免范围浪费或低估。
- **第二阶段**：通过预定义的“有益范围”进行逻辑比较，高效计数落入每个特征区间的元素，选出更优的方言。
  - 将范围判断转换为简单的位运算，可并行处理，适合小尺寸块的实时选择。

### 3. 在线量化与MAC运算
- 激活值量化通过逻辑匹配最近的可表示值，无需浮点MSE计算。
- 权值离线预量化，推理时通过查表将3位索引转为4位无符号整数。
- 乘法使用4位无符号整数运算，块内共享同一个指数和，累加结束后再偏移2位以补偿0.5因子，最后转换为FP16并进入下一层。
- 整个过程可流水化，方言选择、量化和MAC操作均可重叠。

## 实验设计
- **模型与数据集：**  
  LLaMA-2-7B、LLaMA-3-8B、Mistral-7B、OPT-6.7B；零样本常识推理（LAMBADA、HellaSwag、BoolQ、PIQA、WinoGrande、ARC-easy、ARC-challenge）和WikiText2困惑度。
- **对比方法：**  
  MXFP4（硬件支持缩放）、LLM-FP4（矩阵级混合格式）、QuaRot（旋转矩阵去除异常值）、NVFP4（NVIDIA块缩放格式）。
- **量化范围：**  
  - `linear`：仅线性层权重和激活。  
  - `all`：全路径，包括注意力中的QK、Score×V乘法（KV缓存也量化）。
- **块大小与格式库大小消融：** 块大小16/32/64，方言数8/16/24动态对比。

## 资源与算力
- **软件环境：** 基于PyTorch、HuggingFace Transformers，在单个NVIDIA H100 GPU上执行模拟。
- **硬件评估：** 使用SystemVerilog建模MAC单元，在Nangate 45nm库、0.5GHz下用Synopsys DC综合面积与功耗；另用SkyWater 130nm库、100MHz综合量化/反量化模块。
- **训练/校准：** 论文方法为训练后量化（PTQ），无需额外训练，仅需少量校准数据（WikiText2）进行方言选择。

## 实验数量与充分性
- **实验规模：** 包含多个模型、多个比特宽度、多种块大小、不同范围（linear/all）、多种方言数量、动态块大小分配、方言选择方法（MSE vs 两阶段）、块形状（1D/2D）、与SmoothQuant组合等。
- **消融实验：**  
  - 块大小影响（Table 3）  
  - 方言数量（Table 4）  
  - 选择策略对比（Table 2）  
  - 量化子层敏感度分析  
  - 与NVFP4、SmoothQuant的联合效果  
  - 硬件开销对比（MAC单元、量化/反量化逻辑面积、功耗、周期）
- **公平性：** 采用统一评估框架（lm-eval-harness），对比方法使用开源代码，有效比特宽明确计算，较客观。部分对比（如QuaRot）保留了FP16组件，作者已做说明。

## 主要结论与发现
- BlockDialect 在所有模型上均大幅超越 MXFP4，有效比特宽更低。
- 在 LLaMA3-8B 上，仅线性层量化时准确率下降仅1.76%（块大小32混合），全路径量化仅比全精度低5.45%。
- 两阶段选择方法与MSE方法精度仅差约0.6%，但硬件成本降低约10倍。
- 16方言 DialectFP4 实现了范围覆盖与分布代表的最佳平衡。
- 硬件综合显示，BlockDialect的MAC单元功耗、面积接近FP4，远超FP6/INT8，量化/反量化逻辑开销可控。

## 优点
- **创新视角**：将块量化的焦点从“缩放”转向“表示”，提出块级混合格式概念。
- **硬件友好**：DialectFP4值均为0.5的倍数，可直接映射到整数运算，无需浮点乘法。
- **在线高效选择**：两阶段逻辑避免了实时MSE计算，资源开销小，支持流水线。
- **全路径低精度**：即实现对激活-权重和激活-激活乘法的完整4bit量化，包括KV缓存。
- **实验扎实**：多模型、多任务、丰富消融、硬件成本实测，论证全面。

## 不足与局限
- **未与最新旋转量化方法深度集成**：虽尝试与SmoothQuant结合，但未探索与Hadamard旋转等方法的更优组合。
- **KV缓存更新策略存在复杂度**：子通道量化需维护高精度分块，可能增加实现难度和少量存储开销。
- **预定义方言库依赖数据分布分析**：方言设计基于WikiText2校准集的块级分布，若目标领域分布差异较大，效果可能下降。
- **硬件评估尚在原型级别**：综合采用45nm/130nm库，未在先进工艺下验证，缺乏完整加速器系统级评估。
- **生成任务未覆盖**：评估仅包括困惑度和判别类任务，未测试长文本生成等更实际的LLM应用场景。

（完）
