# 03 · 数学与算法发现

## 场景定义

在数学证明、组合构造、算法优化等有形式或可执行验证的领域，用搜索 / 自对弈 / 程序进化发现更好对象。

## 为什么适合 / 不适合 RSI

| 因素 | 评估 |
|------|------|
| 验证器 | **极强**：Lean/证明助手、执行器、精确目标函数 |
| 适合 | 最接近「可无限自我改进」的理想条件之一 |
| 不适合 | 从形式证明到开放数学直觉仍难；权重自训练可能学到脆弱策略 |

## 论文 / 系统表

| 标题 | 机构 | 日期 | 链接 | 层级 | 改了什么 | 验证信号 | 作者报告结果 | 局限 |
|------|------|------|------|------|----------|----------|--------------|------|
| FunSearch | DeepMind | 2023-12（Nature） | [Nature](https://www.nature.com/articles/s41586-023-06924-6) | L0 | LLM 生成程序 + 进化档案 | 可执行评估函数 | 在 cap set 等问题上给出可发表级构造（官方） | 框架固定；非改改进机制 |
| AlphaGeometry | DeepMind | 2024-01（Nature） | [Nature](https://www.nature.com/articles/s41586-023-06747-5) | L0–L3 混合 | 神经符号；约 1 亿条合成数据训语言模型 | IMO 几何 | IMO-AG-30：**25/30** vs 先验 SOTA 10；金牌选手均分约 25.9（官方博客/Nature） | 合成数据管线与符号引擎人类设计 |
| AlphaProof / AlphaGeometry 2 | DeepMind | 2024-07（博客） | [DeepMind IMO 2024](https://deepmind.google/discover/blog/ai-solves-imo-problems-at-silver-medal-level/) | L3 倾向（Lean RL） | Lean 形式化上强化学习；AG2 增强 | IMO 2024 | 银牌等价：**28/42**；解答经 Lean 验证（官方博客） | 完整方法论文部分后置；本行以博客为准 |
| AlphaEvolve | DeepMind | 2025-05 / [2506.13131](https://arxiv.org/abs/2506.13131) | arXiv | L0 | 见 02；算法与系统优化 | 性能/正确性 | 见 02 场景 | 同左 |
| STP (Self-play Theorem Prover) | — | 2025-02 | [2502.00212](https://arxiv.org/abs/2502.00212) | L3 | Conjecturer + Prover 自对弈；更新证明策略 | Lean 等 | LeanWorkbook 约 28.5%（对照 expert iter 13.2%）；miniF2F 65% pass@3200（作者） | 外层自对弈协议固定 |
| DeepSeek-Prover-V1.5 | DeepSeek | 2024-08 | [2408.08152](https://arxiv.org/abs/2408.08152) | L3 | RLPAF + RMaxTS | miniF2F / ProofNet | miniF2F-test **63.5%**；ProofNet **25.3%**（作者） | 训练协议固定 |
| DeepSeek-Prover-V2 | DeepSeek | 2025-04 | [2504.21801](https://arxiv.org/abs/2504.21801) | L3 | 子目标分解 + RL | miniF2F | miniF2F-test **88.9%** Pass@8192（671B CoT，作者） | 算力与采样预算高；外环固定 |
| Absolute Zero / AZR | — | 2025-05 | [2505.03335](https://arxiv.org/abs/2505.03335) | L3 | 零外部数据：自提任务+求解；执行器验证 | 代码执行 | 相对「零数据」基线 SOTA（作者）；报告过有害思维链「uh-oh」类现象 | 安全；任务分布自举偏差 |

## 场景小结

- 形式验证器使 **L0 程序搜索**与 **L3 自对弈/RL** 都特别有效。  
- FunSearch / AlphaEvolve = 冻结或调用 FM + 固定进化外环。  
- AlphaGeometry → AlphaProof/AG2 强化了「合成数据 + 形式验证 → 可竞赛级」路径。  
- DeepSeek-Prover 系列与 STP / Absolute Zero = 权重级自我改进，更接近「模型变强」，但 **外环协议仍人类设计**。  
- Absolute Zero 同时把 **对齐风险**推到前台。

## 开放问题

1. 自产生猜想的分布如何避免模式坍缩？  
2. 将 L3 证明器与 L1 编码脚手架结合的复合系统。  
3. 安全：零数据 RL 中出现的有害推理如何监测。
