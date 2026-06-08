---
title: Analog Foundation Models
title_zh: 模拟基础模型
authors: "Julian Büchel, Iason Chalas, Giovanni Acampa, An Chen, Omobayode Fagbohungbe, Hsinyu Tsai, Kaoutar El Maghraoui, Manuel Le Gallo, Abbas Rahimi, Abu Sebastian"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=zo4zYTR8vn"
tags: ["query:edge-llm"]
score: 8.0
evidence: 使LLM适应噪声大、低精度的模拟存内计算硬件
tldr: 针对模拟存内计算硬件存在的噪声和量化约束，提出一种通用可扩展方法，使LLM能在该低精度、高噪声的硬件上实现接近4比特级别的性能，为LLM在专用边缘硬件上的高效推理铺平道路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1157, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1413, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1457, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1460, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1002, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1448, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1451, \"height\": 304, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1455, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 742, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1456, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zo4zytr8vn/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1461, \"height\": 1392, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1469, \"height\": 919, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1205, \"height\": 449, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1451, \"height\": 410, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1160, \"height\": 340, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1446, \"height\": 128, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1446, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1462, \"height\": 500, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1448, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1447, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1452, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1463, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1461, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1463, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1459, \"height\": 139, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1160, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1461, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1461, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 672, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1462, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-zo4zytr8vn/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1450, \"height\": 1532, \"label\": \"Table\"}]"
motivation: 现有LLM无法直接部署在模拟存内计算硬件上且保持较高精度。
method: 设计一种通用方法，使LLM适应模拟硬件的噪声和低精度计算。
result: 使LLM在模拟硬件上达到4比特量化水平的性能。
conclusion: 该方法弥合了LLM与新兴模拟硬件之间的差距，促进高效推理。
---

## Abstract
Analog in-memory computing (AIMC) is a promising compute paradigm to improve speed and power efficiency of neural network inference beyond the limits of conventional von Neumann-based architectures. However, AIMC introduces fundamental challenges such as noisy computations and strict constraints on input and output quantization. Because of these constraints and imprecisions, off-the-shelf LLMs are not able to achieve 4-bit-level performance when deployed on AIMC-based hardware. While researchers previously investigated recovering this accuracy gap on small, mostly vision-based models, a generic method applicable to LLMs pre-trained on trillions of tokens does not yet exist. In this work, we introduce a general and scalable method to robustly adapt LLMs for execution on noisy, low-precision analog hardware. Our approach enables state-of-the-art models — including Phi-3-mini-4k-instruct and Llama-3.2-1B-Instruct — to retain performance comparable to 4-bit weight, 8-bit activation baselines, despite the presence of analog noise and quantization constraints. Additionally, we show that as a byproduct of our training methodology, analog foundation models can be quantized for inference on low-precision digital hardware. Finally, we show that our models also benefit from test-time compute scaling, showing better scaling behavior than models trained with 4-bit weight and 8-bit static input quantization. Our work bridges the gap between high-capacity LLMs and efficient analog hardware, offering a path toward energy-efficient foundation models. Code is available at [github.com/IBM/analog-foundation-models](https://github.com/IBM/analog-foundation-models).

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

*   **研究背景**：随着大语言模型（LLM）规模激增，其训练与推理的能耗问题日益突出。模拟存内计算（AIMC）作为一种新兴计算范式，通过在存储权重数据的非易失性存储器（NVM）阵列中直接执行矩阵向量乘法（MVM），能从根本上消除数据搬移开销，从而大幅提升推理能效与吞吐量，被认为是突破传统冯·诺依曼架构瓶颈的潜力方案。
*   **核心问题**：AIMC虽具能效优势，但存在固有非理想性，包括**权重编程噪声、读取噪声、电导漂移**等模拟噪声，以及**输入/输出数模/模数转换（DAC/ADC）带来的严格、静态量化约束**。这些非理想性导致未经适配的“现成”LLM在AIMC硬件上的精度急剧下降，无法维持可比较的4比特级别性能。
*   **整体含义**：本文旨在填补“万亿参数级LLM”与“高效能模拟AI芯片”之间的技术鸿沟，提出一种通用且可扩展的方法，**将LLM鲁棒地适配到嘈杂、低精度的模拟硬件**上，从而为面向边缘或云端推理的高能效模拟基础模型开辟道路。

### 2. 论文提出的方法论

核心方法是一种结合**数据生成、知识蒸馏、硬件感知训练（HWA training）** 的可扩展训练流程，使模型在训练时就学习容忍模拟硬件的非理想性。

*   **整体流程**
    1.  **数据生成**：使用预训练的原始LLM（教师模型），从`<BOS>`令牌开始，通过多项分布迭代采样，**合成仅用于蒸馏的训练语料**。
    2.  **硬件感知训练**：在合成数据上，以原始LLM为教师，目标LLM为学生，**通过知识蒸馏损失进行训练**。在前向传播时，对线性层注入模拟硬件效应，以增强模型鲁棒性。
    3.  **部署**：训练完成后，模型可部署在AIMC硬件上，或直接进行后训练量化（RTN），部署到低精度数字硬件上。

*   **关键技术细节**
    *   **静态输入量化建模**：模拟DAC转换，将输入激活量化为8比特，使用可学习的、推理时固定的输入范围（`β_inp.quant`）。
    *   **全局固定输出量化建模**：模拟ADC转换，将MVM输出量化为8比特。其特别之处在于，输出量化范围（`λ_adc`）**在所有层间保持全局固定**，以模拟实际ADC不可逐层配置的硬件限制。
    *   **权重噪声注入**：为抵抗模拟MVM中的编程噪声，在每次前向传播中向权重注入逐通道的**加性高斯噪声**。噪声幅度与每通道的最大绝对值成比例。
    *   **迭代权重裁剪**：在每个优化器步骤后，按标准差的特定倍数（`α`）对权重进行**硬裁剪**。该方法通过去除离群值并收紧权重分布，迫使较小的权重映射到器件电导曲线上信噪比（SNR）更高的区域，从而极大地提升了模型的抗噪鲁棒性（实验证明其效果甚至优于噪声注入）。

### 3. 实验设计

*   **使用数据集/场景**：使用了**12个涵盖不同核心能力的基准测试**进行全面评估，包括：
    *   **推理与知识**：MMLU (5-shot)、GSM8K (CoT 8-shot)、BoolQ (0-shot)、ARC-C/E (10-shot)、MedQA (2-shot)、AGIEval (0-shot)、ANLI (7-shot)、MATH-500 (0-shot)。
    *   **常识与NLI**：HellaSwag (5-shot)。
    *   **指令遵循与安全性**：IFEval (0-shot)、XSTest (0-shot)。
*   **对比方法**：
    *   **原始模型**：FP16（W16）与注入真实硬件噪声的原始模型（W16_hw_noise）。
    *   **量化感知训练**：使用LLM-QAT训练的模型及其噪声注入版本（SI8-W4_hw_noise）。
    *   **后训练量化**：使用SpinQuant量化的模型，包括使用硬件友好的静态输入量化（SI8-W4）和动态输入量化（DI8-W4），及其噪声注入版本。
    *   **本文方法**：本文提出的模拟基础模型，包含静态8-8量化且无噪声版（SI8-W16_hw_noise-O8）和注入硬件噪声版（SI8-W16_hw_noise-O8）。
*   **实验模型**：在**Phi-3-mini-4k-instruct** (约38亿参数) 和 **Llama-3.2-1B-Instruct** (约13亿参数) 上验证。

### 4. 资源与算力

*   **模型训练**：
    *   **GPU**: 使用**96块NVIDIA V100 GPU**。
    *   **训练时长**: Phi-3-mini-4k-instruct训练约需**230小时**，Llama-3.2-1B-Instruct约需**90小时**。
    *   **其他配置**: 采用DeepSpeed ZeRO Stage 2，配合梯度检查点与CPU卸载以减少显存消耗。论文也指出，若使用8块A100 GPU，训练Phi-3-mini-4k-instruct模型的时间与48块V100相同，训练会更加高效。
*   **数据生成**：使用**vLLM**进行合成数据生成。

### 5. 实验数量与充分性

*   **实验组数**：作者进行了**非常多组的实验**，覆盖了主要方法对比、大量消融实验、噪声鲁棒性扫参、安全性测试、测试时计算扩展、分块架构影响、其他NVM噪声模型泛化性评估等。
*   **实验充分性**：**非常充分**。评估涵盖了12个不同维度的任务。模型由**两个不同规模的主流LLM**家族验证。为削弱随机性，**所有涉及噪声注入的评估均重复10次并报告均值和标准差**。
*   **客观性与公平性**：**客观且公平**。在对抗鲁棒性对比中，使用了相同的硬件噪声模型对所有方法进行评估。对比方法包括了QAT和PTQ这两大类最前沿的低精度部署技术，且均为其使用了硬件友好的静态量化配置，模拟了真实的AIMC部署限制。

### 6. 论文的主要结论与发现

*   **鲁棒性显著提升**：通过硬件感知训练，模拟基础模型在真实PCM芯片噪声下，性能可降至与**4比特量化权重+8比特静态量化激活**的基线相媲美的水平，极大地弥补了精度差距。
*   **权重裁剪是关键**：在增强LLM抗噪性的诸多技术中，**迭代权重裁剪比单纯的噪声注入更为有效**。裁剪能收紧权重分布，使权重映射到高SNR的器件电导区域，从而带来更强的鲁棒性。
*   **量化部署兼容性**：作为训练的副产品，所得模型的权重分布对量化噪声也具有鲁棒性，可直接通过RTN量化为4比特模型，其在数字硬件上的性能与QAT训练的专门量化模型相当，优于静态量化的PTQ模型。
*   **测试时计算扩展优势**：在增加推理计算量的“测试时计算扩展”场景下，模拟基础模型展现出比同等低比特量化模型**更优的扩展行为**，在MATH-500基准上随采样数增加能恢复更多性能。
*   **安全能力保留**：通过指令遵循（IFEval）和安全性（XSTest）基准测试证实，硬件感知训练过程**基本保留了预训练基座模型的对齐和安全能力**，不会因其训练而导致能力灾难性遗忘或安全性崩溃。

### 7. 优点

*   **问题新颖且现实意义强**：首次系统性地解决了将当前最先进LLM部署在模拟存内计算芯片上面临的鲁棒性挑战，这一问题直接影响到高能效AI推理的可行性，兼具学术前沿性和工业应用价值。
*   **方法论通用且可扩展性强**：提出的训练方法不依赖于具体的噪声模型或特定硬件，可应用于不同规模、不同家族的LLM，且训练机制与数字域量化（QAT）和测试时扩展等后期优化兼容，通用性好。
*   **评估全面，结论坚实**：在12个多维度基准上、用两种模型、与三大类基线方法进行了详细对比，并辅以充分的可重复性措施（10次重复），实验设计严谨，洞察发现（如裁剪优于噪声注入）深刻。

### 8. 不足与局限

*   **训练成本高昂**：即便只需极少量预训练tokens，训练数十亿参数LLM仍需大量高端GPU集群和上百小时，对许多研究者而言门槛较高，限制了方法的普适性。
*   **绝对精度仍有差距**：尽管鲁棒性极佳，但相比于FP16的全精度原始模型，模拟基础模型在一些硬核推理任务（如GSM8K、MATH-500）上的绝对性能仍有**明显下降**，其能力天花板受限于基准教师模型。
*   **噪声模型假设**：实验主要基于特定PCM芯片的**编程噪声模型**，虽然也测试了ReRAM噪声和漂移，但距离真实芯片部署中所有非理想性（如IR-drop、温度效应等）的复杂耦合效应可能仍有距离。
*   **训练收敛慢**：论文自述，硬件感知训练中引入的噪声和量化操作会**减慢模型收敛速度**，这进一步加剧了其算力和时间开销。

（完）
