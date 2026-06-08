---
title: "LoRO: Real-Time on-Device Secure Inference for LLMs via TEE-Based Low Rank Obfuscation"
title_zh: LoRO：通过基于TEE的低秩混淆实现LLM的实时片上安全推理
authors: "Gaojian Xiong, Yu Sun, Jianhua Liu, Jian Cui, Jianwei Liu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=de07K7kreI"
tags: ["query:edge-llm"]
score: 9.0
evidence: 利用TEE和低秩混淆在不可信边缘设备上实现实时安全的LLM推理。
tldr: LLM部署在不可信边缘设备上存在模型窃取风险。现有TEE安全推理方案存在统计脆弱性，LoRO提出利用低秩掩码对模型参数进行全面混淆。通过低秩因子高效生成稠密掩码，将TEE内计算复杂度从指数级降至多项式级，实现了实时安全的片上LLM推理，有效抵御模型窃取攻击，保护知识产权。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-de07k7krei/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1306, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-de07k7krei/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1334, \"height\": 354, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-de07k7krei/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1243, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-de07k7krei/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1433, \"height\": 309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-de07k7krei/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1431, \"height\": 301, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1307, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1302, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1157, \"height\": 568, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1440, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1085, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1437, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 539, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 656, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1116, \"height\": 183, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1270, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1290, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-neurips-2025-de07k7krei/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1002, \"height\": 221, \"label\": \"Table\"}]"
motivation: 边缘设备上部署LLM面临模型被窃取风险，现有TEE保护方案存在安全漏洞。
method: 设计低秩掩码机制，利用低秩因子生成稠密掩码混淆参数，降低TEE计算复杂度。
result: 实验表明LoRO在保证实时推理的同时，成功防御了模板窃取攻击，并提供安全保证。
conclusion: LoRO为边缘设备上的LLM安全推理提供了兼顾效率与安全的实用解决方案。
---

## Abstract
While Large Language Models (LLMs) have gained remarkable success, they are consistently at risk of being stolen when deployed on untrusted edge devices. As a solution, TEE-based secure inference has been proposed to protect valuable model property. However, we identify a statistical vulnerability in existing protection methods, and furtherly compromise their security guarantees by proposed Model Stealing Attack with Prior. To eliminate this vulnerability, LoRO is presented in this paper, which leverages dense mask to completely obfuscate parameters. LoRO includes two innovations: (1) Low Rank Mask, which uses low-rank factors to generate dense masks efficiently. The computing complexity in TEE is hence reduced by an exponential amount to achieve inference speed up, while providing robust model confidentiality. (2) Factors Multiplexing, which reuses several cornerstone factors to generate masks for all layers. Compared to one-mask-per-layer, the secure memory requirement is reduced from GB-level to tens of MB, hence avoiding the hundred-fold latency introduced by secure memory paging. Experimental results indicate that LoRO achieve a $0.94\times$ Model Stealing (MS) accuracy, while SOTA methods presents $3.37\times$ at least. The averaged inference latency of LoRO is only $1.49\times$, compared to the $112\times$ of TEE-shielded inference. Moreover, LoRO results no accuracy loss, and requires no re-training and structure modification. LoRO can solve the concerns regarding model thefts on edge devices in an efficient and secure manner, facilitating the wide edge application of LLMs.

---

## 论文详细总结（自动生成）

好的，我将基于您提供的论文内容，以资深学术论文分析助手的身份，用中文对该论文进行结构化、深入、客观的总结。

### 1. 核心问题与研究动机

*   **核心问题**：在不可信的边缘设备上部署大语言模型时，模型存在被窃取的风险。现有的、基于可信执行环境的模型保护方案存在统计层面的安全漏洞，无法有效抵御模型窃取攻击。
*   **研究动机**：
    *   **边缘部署需求**：自动驾驶、个人智能体等领域对低延迟和数据隐私有强烈需求，因此需要在用户边缘设备上部署LLM。
    *   **模型安全风险**：部署在边缘端的模型直接暴露于攻击者，由于LLM训练成本极高，它们成为了极具价值的窃取目标。
    *   **现有方案缺陷**：当前最先进的基于TEE的安全推理方案（如参数混淆方法）存在一个根本性的**统计脆弱性**。攻击者可以利用公开预训练模型与私有的微调后模型之间的统计相似性，恢复出混淆密钥，从而窃取模型。

### 2. 方法论

论文提出了 **LoRO**，一个基于TEE的高效安全推理框架。其核心思想是使用**稠密掩码**对模型参数进行全面混淆，以消除统计相关性，并通过两项创新解决稠密掩码带来的计算和内存挑战：

*   **核心技术一：低秩掩码**
    *   **目标**：解决稠密掩码在TEE内计算复杂度高的问题。
    *   **关键思想**：不直接存储和计算一个巨大的稠密掩码 `D`，而是使用两个低秩因子 `B` 和 `A` 来生成它，即 `D = BA`。
    *   **算法流程**：
        1.  **参数混淆 (REE侧)**：将模型权重 `W` 混淆为 `W' = W + BA`，并卸载到REE侧用加速器进行主要计算 `xW'`。
        2.  **安全去混淆 (TEE侧)**：在TEE内部，利用低秩因子进行轻量级计算 `xBA`。由于两个因子 `B` 和 `A` 的维度远小于 `W`，计算复杂度从 `O(n³)` 降为 `O(n²)`。
        3.  **结果恢复**：最终结果通过TEE内的运算恢复：`y = xW' - xBA = xW`，保证了模型精度无损。
*   **核心技术二：因子复用**
    *   **目标**：解决为每一层都生成并存储专属掩码因子所带来的巨大安全内存需求（GB级别）。
    *   **关键思想**：不再为每一层准备独立的 `B` 和 `A` 因子对，而是预先在TEE内生成一小批**基石因子**集合。对于任意层，通过从基石因子集合中**随机抽取并进行线性组合**来动态生成该层的掩码 `D = ∑ α Bj Ai`。
    *   **效果**：此方法将安全内存需求从1.02 GB（针对70亿参数模型）降低到仅26 MB，避免了因安全内存分页导致的百倍延迟。

### 3. 实验设计

*   **数据集与场景**：实验覆盖了广泛的NLP和CV任务。
    *   **NLP任务**：SQuAD（阅读理解）、GSM8k（数学）、Spider（代码生成）、GLUE基准测试（MRPC, SST-2, MNLI）、MATH（数学）。
    *   **CV任务**：CIFAR100、Food101。
*   **基准模型**：在多种规模和架构的代表性模型上进行评估，包括RoBERTa、BART、ViT、Qwen系列 (1.5B, 3B, 7B) 和LLaMA3系列 (1.5B, 3B, 8B)。
*   **对比方法**：全面对比了多种最先进的TEE安全推理方案。
    *   **去混淆保护型**：Magnitude（加法掩码）、SOTER（乘法噪声）、ShadowNet（加乘结合）、TLG（置换）。
    *   **完全/部分屏蔽型**：MLCapsule、Serdab、DarkneTz。
*   **硬件平台**：
    *   **安全评估**：在配备NVIDIA RTX 4090 GPU的服务器上进行。
    *   **性能评估**：在两种主流边缘TEE平台上测试：
        *   Intel SGX（配备Intel Core I9-10885H CPU, Quadro T2000 GPU）
        *   ARM TrustZone（配备NVIDIA Jetson Orin NX, OP-TEE OS）

### 4. 资源与算力

*   **算力资源**：论文明确说明，模型保密性和精度实验是在**装有2块NVIDIA RTX 4090 GPU的服务器**上进行的。推理效率则在Intel SGX笔记本电脑和ARM TrustZone开发板上分别测试。文中未提及具体的训练或实验总时长。

### 5. 实验数量与充分性

实验设计非常全面、客观且公平。

*   **实验数量充足**：
    *   **安全防御力**：在超过16种“模型-数据集”组合上进行了模型窃取攻击测试，并与5种主流方案和黑盒基线进行对比。
    *   **推理效率**：在2种不同硬件TEE平台上，对6种不同规模模型进行了延迟测试，与4种其他方案及纯REE推理进行对比。
    *   **模型精度**：在多个模型和任务上验证了原始模型、LoRO保护和混淆后模型（暴露在REE中）的精度。
    *   **消融与补充实验**：提供了延迟分解、不同攻击数据量下的表现、安全内存需求对比等详细分析。
*   **客观性与公平性**：
    *   **攻击假设强大**：威胁模型假设攻击者控制TEE外的所有环境，并拥有模型架构知识、公开预训练模型和少量微调数据（10%），这使得防御评估更具挑战性。
    *   **从防御方角度报告结果**：为评估最强攻击者，模型窃取准确率报告的是**五次独立实验中的最高值**，而非平均值，这体现了对安全性评估的严苛要求。

### 6. 主要结论与发现

1.  **揭露现有漏洞**：成功识别出SOTA TEE推理方案的统计脆弱性，并提出的MSP攻击能够突破其防御，达到接近原始模型的窃取精度。
2.  **实现强安全防御**：LoRO能够将攻击者的模型窃取精度降至**黑盒水准 (0.94倍)**，而现有SOTA方案的窃取精度至少是黑盒的3.37倍，证明了LoRO的鲁棒安全性。
3.  **达到实时推理性能**：LoRO平均仅引入**1.49倍**的推理延迟，相比现有TEE完全屏蔽方案的**112倍**以上延迟，实现了数量级的性能飞跃，能满足实时应用需求。
4.  **零精度损失与即插即用**：LoRO不会降低模型原始精度，且无需对模型结构进行修改或重新训练，具有良好的兼容性和易用性。

### 7. 优点

*   **深刻的安全洞察**：论文不仅仅是提出一个新方法，更关键的是深入分析了现有方案的**统计脆弱性**根源，并据此设计了针对性的攻击和防御，其视角具有高度创新性。
*   **方法设计的精巧性**：
    *   **低秩掩码**巧妙地利用低秩分解，解决了“全面混淆”与“高效计算”之间的矛盾。
    *   **因子复用**创造性地通过“组合复用”思想，解决了“大模型参数保护”与“小容量安全内存”之间的矛盾，极具工程智慧。
*   **实验评估的全面与严谨**：实验覆盖了多种任务、多规模模型、两种主流TEE硬件，并从安全性、效率和精度三个维度进行了全面对比。对攻击能力的“最强假设”和对防御效果的“报告最高攻击值”都体现了安全评估的严谨性。
*   **极强的实用性**：该方法实现零精度损失、无需重新训练，并且显著降低了延迟和内存开销，是解决边缘设备上LLM部署安全问题的非常有前景的实用方案。

### 8. 不足与局限

*   **侧信道攻击的考虑**：论文明确指出，其威胁模型建立在TEE本身是绝对安全的基础上，**未将侧信道攻击**可能导致的隐私泄露等威胁纳入考量。作者认为这是TEE安全领域一个独立的研究范畴。
*   **缺少对可信GPU的探讨**：论文没有讨论结合可信GPU（如NVIDIA Confidential Computing）的可能性，但指出因其成本高昂，短期内TEE+普通加速器仍是边缘设备的主流方案。
*   **生成任务评估指标单一**：对于GSM8k和Spider这类生成任务，论文仅以“完全匹配”作为正确的标准。这种严格的评估方式可能未能完全反映模型输出质量的细微差异，例如一个思路正确但计算有误的GSM8k答案。
*   **延迟测试细节**：虽然提供了延迟倍数，但缺少不同方法在REE和TEE上及数据传输的**绝对延迟时间（毫秒级）**分布和端到端综合延迟的总览图，读者难以对实际运行速度有更直观的感受。

（完）
