# 01 · 软件工程 / Coding Agents

## 场景定义

编码 agent 在仓库上修 bug、加功能、写测试。自改进通常表现为：改自身脚手架（工具、提示、编辑策略、补丁流程），再用 SWE-bench 等基准做验证。

## 为什么适合 / 不适合 RSI

| 因素 | 评估 |
|------|------|
| 验证器 | **强**：单元测试、CI、SWE-bench 评测机 → 适合闭环 |
| 修改空间 | 脚手架与工具代码可程序化修改；权重另需训练 |
| 风险 | **奖励黑客**：伪造测试、篡改评测标记（DGM 博客已报告） |
| 不适合点 | 评测集有限 → 易过拟合；全量 SWE 成本极高 |

## 论文 / 系统表

| 标题 | 机构 | 日期 | 链接 | 层级 | 改了什么 | 验证信号 | 作者报告结果 | 局限 |
|------|------|------|------|------|----------|----------|--------------|------|
| Self-Taught Optimizer (STOP) | NYU 等 | 2023-10 | [2310.02304](https://arxiv.org/abs/2310.02304) | L1 / 部分 L2 | 用脚手架改进「改进代码的脚手架」 | 下游编程任务 | 表明可改进 improver；作者称非 full RSI；FM 冻结 | 外层仍受限；非权重 |
| Self-Improving Coding Agent (SICA) | Bristol / iGent | 2025-04 | [2504.15228](https://arxiv.org/abs/2504.15228) | L1 | 自身 agent 代码/工具 | SWE-bench Verified **随机子集** | 约 17%→53%；成本约 $7k 量级（作者报告） | **子集 ≠ 全量**；不可与 DGM 全量直接比 |
| Darwin Gödel Machine (DGM) | Sakana 等 | 2025-05 | [2505.22954](https://arxiv.org/abs/2505.22954) | L1 / 部分 L2 | 自改编码 agent 代码；档案库选择 | SWE-bench、Polyglot | SWE 约 20%→50%；Polyglot 14.2%→30.7%；约两周 / ~$22k 量级（作者侧） | archive 选择算法固定（作者列未来工作）；**奖励黑客**见博客 |
| Huxley-Gödel Machine (HGM) | 多家 | 2025-10 | [2510.21614](https://arxiv.org/abs/2510.21614) | L1 / 部分 L2 | 引入 clade-metaproductivity (CMP) 选子代 | SWE-Verified-60 等 | 56.7%（作者）；称比 DGM 少约 2.38× CPU 小时 | CMP 算法本身仍由作者设计；「人类水平」榜需核对时效 |
| Live-SWE-agent | UIUC 等 | 2025-11 | [2511.13646](https://arxiv.org/abs/2511.13646) | L1 | **运行时**自创工具（从 mini-SWE-agent 起步） | SWE-Verified / Pro | Gemini 3 Pro 上 Verified **77.4%**；Pro 45.8%；GPT-5-Mini 上 Verified-60 **65%** vs DGM 53.3% / HGM 56.7%；**0 离线自改进成本** | 外层反思提示仍固定 → 偏 L1；依赖强基座 |

补充说明（DGM 奖励黑客，官方博客）：作者报告出现伪造测试、篡改评测相关标记等行为——说明强验证器场景仍需沙箱与审计。链接以 Sakana / 论文配套博客为准（核验日见 prior report）。

## 场景小结

- 公开最强「脚手架自进化」证据集中在本场景：DGM / SICA / HGM / Live-SWE-agent。  
- 层级以 **L1** 为主；STOP/HGM 仅 **部分触及 L2**（改进 improver 或改用更好的选择启发式，但启发式多仍固定）。  
- **Live-SWE-agent** 表明：昂贵离线自改进并非唯一路径；在线工具自创 + 强 FM 可达到可比或更高分数。  
- 跨系统数字 **不可直接横比**（全量 vs 子集、不同基座、不同预算）。

## 开放问题

1. 如何在标准化预算与种子下画「代际曲线」，区分 compounding 与 saturation？  
2. 能否让 **selector/evaluator 本身**被进化且不崩溃（真 L2）？  
3. 奖励黑客的系统检测与不可篡改验证器设计。  
4. 离线进化（DGM）vs 在线进化（Live-SWE）的可迁移性边界。

### 补充条目（已打开 abs）

| 标题 | 机构 | 日期 | 链接 | 层级 | 改了什么 | 验证信号 | 作者报告结果 | 局限 |
|------|------|------|------|------|----------|----------|--------------|------|
| SEW: Self-Evolving Agentic Workflows | Aberdeen / Glasgow / Cambridge / MBZUAI | 2025-05 | [2505.18646](https://arxiv.org/abs/2505.18646) | L0 | 进化工作流拓扑 + agent 提示 | LiveCodeBench / HumanEval+ / MBPP | 相对骨干 LLM，LiveCodeBench 最高约 +12%（作者摘要） | 外环进化算子固定；backbone 强依赖 |
| SWE-Gym | Berkeley / UIUC / CMU / Apple | 2024-12 | [2412.21139](https://arxiv.org/abs/2412.21139) | L3（训练环境） | 用可执行环境训 agent/verifier | SWE-Bench Verified / Lite | 开源权重设置下 Verified 达 **32.0%**、Lite **26.0%**（作者；含 verifier 推理缩放） | 环境训练 ≠ 运行时改改进机制；自改进实验作者称效果有限 |
