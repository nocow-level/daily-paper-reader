---
title: "Two Heads are Better than One: Simulating Large Transformers with Small Ones"
title_zh: 双头胜于一头：用小模型模拟大Transformer
authors: "Hantao Yu, Josh Alman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Xeb2EYBKkr"
tags: ["query:edge-llm"]
score: 6.0
evidence: 用小Transformer模拟大Transformer以利用优化短序列的硬件
tldr: 该论文证明长序列大Transformer可用多个短序列小Transformer高效模拟，从而利用现代硬件对短输入的良好优化。理论上，任意输入长度N的Transformer可由O((N/M)^2)个输入长度为M的小Transformer模拟。这为在内存有限的硬件上处理长序列提供了一种新的分治策略。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-xeb2eybkkr/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1219, \"height\": 648, \"label\": \"Figure\"}]"
motivation: 自注意力二次复杂度限制长序列扩展，而现代硬件对短序列处理更优。
method: 从理论上证明大Transformer可通过多个小Transformer模拟，实现长序列的分段处理。
result: 任意大Transformer可被多个小Transformer高效模拟，计算开销为O((N/M)^2)。
conclusion: 该模拟方法使得资源有限的设备能够间接处理长序列，提升了Transformer的部署灵活性。
---

## Abstract
The quadratic complexity of self‑attention prevents transformers from scaling effectively to long input sequences. On the other hand, modern GPUs and other specialized hardware accelerators are well-optimized for processing small input sequences in transformers during both training and inference. A natural question arises: can we take advantage of the efficiency of small transformers to deal with long input sequences?

In this paper, we show that transformers with long input sequences (large transformers) can be efficiently simulated by transformers that can only take short input sequences (small transformers). Specifically, we prove that any transformer with input length $N$ can be efficiently simulated by only $O((N/M)^2)$ transformers with input length $M \ll N$, and that this cannot be improved in the worst case. However, we then prove that in various natural scenarios including average-case inputs, sliding window masking and attention sinks, the optimal number $O(N/M)$ of small transformers suffice.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：标准 Transformer 的自注意力机制具有输入长度 \(N\) 的二次复杂度，难以高效处理长序列；而现代 GPU 和专用硬件却高度优化了短至中等长度（如 128～2048）序列的处理。由此产生一个自然问题：能否通过组合多个只能处理短序列的“小 Transformer”，来等价地完成大 Transformer（长序列）的计算？
- **整体含义**：论文从表达能力（representational strength）的角度正面回答了这一问题，证明任何大 Transformer 都可以被多个小 Transformer 高效模拟；在最坏情况下需要 \(O((N/M)^2)\) 个小 Transformer（\(M\) 为小 Transformer 的最大输入长度），而在平均输入、滑动窗口注意力、注意力池（attention sinks）等实际场景中，\(O(N/M)\) 个小 Transformer 即已足够。这一结果为在硬件资源受限时用“分而治之”的方式处理长上下文提供了理论基础。

### 2. 方法论
论文的核心方法论是将大 Transformer 的一次前向计算分解为对“小 Transformer 预言机（oracle）”的多次调用，仅允许在调用之外进行极简单的数据编排（拼接、常数填充）。主要技术要点包括：

- **分块模拟注意力机制**  
  将 \(N \times N\) 的注意力矩阵划分成若干 \(M \times M\) 的块。每一块对应两段长为 \(M\) 的输入子区间（一段用作 Query，一段用作 Key/Value）。每个小 Transformer oracle 负责计算该块内注意力分数之和以及加权值之和。  
  关键困难在于小 Transformer 只能输出整个序列的最终结果，无法直接给出局部和。为此，论文通过向输入序列添加一个“合成 token”（synthetic token）并固定其注意力分数，使小 Transformer 的输出中显式地包含所需的局部和项，再通过 MLP 解线性方程反推出真实值。

- **多注意力头与多层的利用**  
  论文证明了：一个具有 \(L'\) 层、每层 \(H'\) 个头的 oracle，其每个注意力头可以独立地模拟一个单头单层的小 Transformer，因此一个 oracle 实际上可以模拟 \(H' L'\) 个独立的单头单层小 Transformer。通过这种“头-层解耦”策略，只需 \(O((N/M)^2 \cdot HL/(H'L'))\) 个 oracle 即可模拟具有 \(L\) 层、每层 \(H\) 个头的大 Transformer。

- **因果掩码的兼容性**  
  所有构造均可通过类似的分块技巧自然扩展到带因果掩码（causal masking）的情况，包括滑动窗口注意力和 StreamingLLM 中的注意力池。在这些场景下，每个小 Transformer oracle 用来计算各局部因果窗口内的注意力，所需 oracle 数量降至 \(O(N/M \cdot HL/(H'L'))\)。

- **平均输入下的线性模拟**  
  当 Query、Key 的注意力分数均落在有界范围（\(1/C \le \exp(\langle q_i,k_j\rangle) \le C\)）且 Value 向量的范数满足一定条件时，通过随机排列 Key 并只对 \(M\) 个采样进行估计，可以用 \(O(N/M)\) 个 oracle 调用获得 \((1+\varepsilon)\) 近似输出，成功概率不低于 0.9。

- **信息论下界**  
  利用已知结果“近似注意力需要 \(\Omega(N^{2-o(1)})\) 时间”，并结合小 Transformer oracle 自身时间与调用次数的关系，推出在最坏情形下 \(O((N/M)^2)\) 个 oracle 是几乎紧的下界。

### 3. 实验设计
- 本文为**纯理论工作，不包含任何实验**。论文中明确指出“This is a purely theoretical paper with no experiment”。
- 文中没有使用任何数据集、benchmark 或与基线方法进行实证比较。所有结论完全基于形式推理和复杂度分析。

### 4. 资源与算力
- 由于没有实验，论文**未使用任何 GPU 或计算资源**，也未报告任何训练或推理时长。所有分析与证明均在数学层面完成。

### 5. 实验数量与充分性
- 实验数量为 **0**。论文通过严格的理论证明和引理（如引理 3.1、定理 3.4、定理 4.1、定理 5.1 以及相应的下界论证）来支持其结论。
- 从纯理论角度看，这些证明是充分且自洽的：论文给出了最坏情况下的模拟算法及其下界，并进一步讨论了平均输入、滑动窗口、注意力池等现实类场景的改进，理论与实际场景的衔接较紧密。但由于完全缺失实证验证，无法直接判断模拟算法在真实硬件上的 wall-clock 加速效果。

### 6. 主要结论与发现
- **最坏情况**：任意大 Transformer（输入长度 \(N\)）可以由 \(O((N/M)^2)\) 个最大输入长度为 \(M\) 的小 Transformer 精确模拟，且该数量在最坏情况下几乎是最优的（无法降至 \(o((N/M)^2)\)）。
- **实际常见场景**：在平均输入假设、采用滑动窗口注意力或注意力池等场景下，\(O(N/M)\) 个小 Transformer 即可实现模拟，为分层 Transformer（Hierarchical Transformers）等现有方法提供了理论保障。
- **向下兼容性**：若小 Transformer 支持因果掩码，同样可以模拟带掩码的大 Transformer；滑动窗口和 StreamingLLM 也可用线性数量的小 Transformer 模拟。
- **表达能力保持**：与诸多“次二次”替代方案不同，该模拟方法保留了标准 Transformer 的完整表达能力，因为其本质是在用多个完全相同结构的子模型精确分解原计算。

### 7. 优点
- **理论严密性高**：给出了紧的上界和下界，明确了不同假设条件下模拟所需的 oracle 数量，结果具有很强的理论指导意义。
- **与硬件趋势契合**：论文抓住了现有硬件对短上下文的极致优化这一现实趋势，为利用专用硬件处理长序列提供了可行的抽象框架。
- **支持多种注意力机制**：不仅覆盖标准/带掩码的注意力，还进一步分析了滑动窗口和注意力池，使理论结论贴近当前大语言模型的工程实践。
- **算法简单且并行度高**：模拟算法仅依赖于简单的矩阵编排操作，oracle 调用可在 \(O(L)\) 轮内高度并行执行，且梯度可自然传递，便于训练。

### 8. 不足与局限
- **完全缺少实验验证**：文中所有结论均停留在理论层面，未在真实硬件（如 GPU）上测试 wall-clock 时间是否真的有显著下降，也未验证理论假设（如常数边界、精度要求）在实际数据上是否成立。
- **oracle 假设的理想化**：小 Transformer 被建模为“预言机”，仅通过调用次数衡量成本；但在实际中，小 Transformer 仍有推理开销，且分块后额外的数据搬移和同步成本可能抵消理论上的并行收益。
- **参数效率问题**：尽管论文指出参数可共享，因此总参数量不会随 \(N\) 膨胀，但在某些模拟构造中，每个 oracle 可能需要不同的 WQ、WK、WV 配置，若不能充分共享，仍会导致庞大的参数总量。
- **仅适用于固定长度的“大 Transformer”**：论文假设大 Transformer 的输入长度 \(N\) 是给定的，而未讨论如何自适应处理变长序列或流式输入。
- **常数项未优化**：大 O 记号隐藏了可能相当大的常数因子，在实际部署时实际加速比可能大打折扣。

（完）
