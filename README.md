# Awesome Agent RSI（中文）

> **Agent 递归自我改进（Recursive Self-Improvement）公开文献导览**  
> 核验日：2026-09-24（Asia/Shanghai）  
> 原则：第一性原理 → 可检验判据 → 打开原始出处 → 再写结论。不编造论文、数字、日期或链接。

本仓库是一份 **awesome-list + 场景分析** 风格的中文导览，按场景整理 2023–2026（侧重 2025–2026）公开可核验的 agent 自我改进工作，并用统一的 **L0–L3** 透镜标注「改了什么」。

**建议仓库名：** `awesome-agent-rsi-zh`

---

## 核心问题

> 公开文献中，有哪些系统在何种场景下实现了可复核的自我改进？改进的是任务表现、脚手架，还是**改进机制本身**？是否存在跨代复合式增益，还是很快饱和？

「自我进化 agent」≠「RSI」。RSI 要求系统能改进**改进自身的那个过程**，并 ideally 产生跨代加速。

详解见 [`docs/00-definitions.md`](docs/00-definitions.md)。

## 自改进层级（L0–L3）

| 层级 | 定义 | 典型例子 |
|------|------|----------|
| **L0** | 固定优化器改进任务 agent | ADAS、AFlow、TextGrad、DSPy、AlphaEvolve、FunSearch、Eureka/DrEureka |
| **L1** | Agent 修改自身脚手架（代码/提示/记忆/工具） | DGM、SICA、HGM、Live-SWE-agent、Gödel Agent、Voyager、AWM、ExpeL |
| **L2** | Agent 修改改进机制本身（proposer/selector/evaluator/search） | STOP（部分）；Promptbreeder（部分）；多数公开系统仅「部分 L2」 |
| **L3** | 自生成数据/奖励更新权重 | STaR、Self-Rewarding、SPIN、Absolute Zero、R-Zero、STP、WebRL、DigiRL、DeepSeek-Prover |

附加标注：基础模型是否冻结、外层循环是否固定、验证信号、代际 compounding vs saturation、奖励黑客。

## 场景总览

| # | 场景 | 文档 | CSV 条数 | 为何（不）适合 RSI | 代表工作 |
|---|------|------|----------|-------------------|----------|
| 1 | 软件工程 / Coding | [01-coding](docs/01-coding.md) | 7 | 测试验证器强；易奖励黑客 | DGM、SICA、HGM、Live-SWE-agent、STOP、SEW、SWE-Gym |
| 2 | 科研自动化 | [02-ai-scientist](docs/02-ai-scientist.md) | 8 | 指标可自动，「新科学」弱 | AI Scientist v1/v2、AlphaEvolve、AI co-scientist、MLGym、RE/MLE/PaperBench |
| 3 | 数学与算法发现 | [03-math](docs/03-math.md) | 8 | Lean/执行器极强 | FunSearch、AlphaGeometry、AlphaProof、STP、DeepSeek-Prover、Absolute Zero |
| 4 | 具身 / 游戏 / 开放世界 | [04-embodied](docs/04-embodied.md) | 6 | 成就可自动；真机贵 | Voyager、JARVIS-1、Eureka、DrEureka、ExpeL、RoboGen |
| 5 | 工具 / 工作流 / 多智能体 | [05-workflow](docs/05-workflow.md) | 8 | 图与提示可搜索 | ADAS、AFlow、Gödel、Promptbreeder、DSPy、TextGrad、EvoAgentX、EvoAgent |
| 6 | 权重级自训练 | [06-weight](docs/06-weight.md) | 6 | 真改策略分布；对齐风险 | STaR、Self-Rewarding、SPIN、Meta-Rewarding、AZ、R-Zero |
| 7 | 网页 / GUI / OS | [07-web-gui](docs/07-web-gui.md) | 7 | 成功判定中等偏弱；轨迹合成可补 | WebRL、AWM、OS-Genesis、AgentTrek、DigiRL、WebEvolver、UI-TARS-2 |
| 8 | 评测与度量 | [08-evaluation](docs/08-evaluation.md) | 7 | 任务基准 ≠ RSI 基准 | METR 时间视野、RE-Bench、MLE-bench、PaperBench、MLGym、HGM/CMP、SWE-bench |
| 9 | 安全与治理 | [09-safety](docs/09-safety.md) | 3 | 前瞻情景 ≠ 已观测爆炸 | OpenAI PF v2、Anthropic RSP v3、DeepMind FSF 3.1、DGM hacking |
| — | 综述（索引） | — | 1 | — | Self-Evolution of LLMs survey |

机器可读索引：[`papers.csv`](papers.csv)（**61** 条；含跨场景交叉列出的评测/科学/数学视角行）。  
编年：[`docs/timeline.md`](docs/timeline.md)。

---

## 跨场景关键结论（扩展至完整调研后）

1. **公开实证以 L0–L1（脚手架）与 L3（权重自训练）为主**；真正 **L2（改改进机制本身）** 稀少，且外层调度常仍固定。作者多自述「不是 full RSI」。
2. **验证器决定场景是否适合 RSI 式闭环**：单元测试 / Lean / 代码执行器强；开放科研品味与 GUI 成功判定偏弱——但 **轨迹合成飞轮**（OS-Genesis、AgentTrek）与 **课程+ORM RL**（WebRL、DigiRL）可部分补强。
3. **任务分上升 ≠ 自我改进能力上升**。HGM 的 metaproductivity / CMP 是重要纠偏；SWE 子集与全量、不同基座不可横比（SICA 子集 vs DGM 全量）。
4. **代际增益常见但易饱和，且成本高**（DGM 作者侧约两周 / ~$22k 量级；SICA ~$7k）。Live-SWE-agent 显示**在线工具自创**可在 0 离线自改进成本下达到可比或更高分数，但外层反思仍固定 → 仍偏 L1。
5. **Web/GUI**：公开路径已清晰分化为 (a) 课程+ORM RL（WebRL）、(b) 工作流记忆（AWM）、(c) 逆任务/引导轨迹合成（OS-Genesis、AgentTrek）、(d) 2025 自进化世界模型 / GUI RL 飞轮（WebEvolver、UI-TARS-2、DigiRL）。
6. **具身**：Eureka / DrEureka = LLM **改写奖励（与域随机化）代码**，外环固定 → **L0**；ExpeL = 自然语言洞察记忆、**不更新权重** → **L1**；RoboGen = 提出–生成–学习的数据飞轮（L0–L1）。
7. **科研 / Auto ML R&D**：AI co-scientist（锦标赛假设）与 MLGym 补强「AI Scientist」叙事；MLGym 作者：前沿模型在开放 AI 研究任务上**多靠调超参**，少见新算法。AlphaEvolve 仍是强验证器 + 程序进化的部署标杆。
8. **数学**：AlphaGeometry → AlphaProof/AG2 与 DeepSeek-Prover 系列强化「**形式验证器 → L3 自对弈/RL**」主线；Absolute Zero / STP 把零外部数据 L3 推到前台（含安全「uh-oh」类 CoT 风险）。
9. **评测**：METR **50% 时间视野约每 7 个月加倍**（o3 约 110 分钟）是与「自动化软件劳动」最接近的公开能力趋势度量，**仍非**直接的「改进改进机制」基准。RE-Bench：短时 agent 可超人类、长时人类更好；PaperBench Claude 3.5 Sonnet 约 21% vs 人类子集约 41.4%。
10. **安全**：DGM 官方报告奖励黑客。实验室框架将 fully automated AI R&D / RSI 视为**前瞻阈值**，非已观测常态。截至 2026-09-24，公开文献中**未见**可复核的「智能爆炸」跨代加速度曲线。

---

## 证据边界：「是否已有复合式递归改进？」

| 声称 | 截至核验日的公开证据 |
|------|----------------------|
| 任务表现多代自改进 | **有**（DGM/SICA/HGM/WebRL 等），常伴随饱和与高成本 |
| 元生产力度量 | **有苗头**（HGM CMP），未成社区标准 |
| 改进机制被系统改写并继承 | **稀少 / 部分**（STOP、Promptbreeder）；外环多仍人类设计 |
| 智能爆炸曲线 | **未见**公开可复核证据 |

---

## 不确定项裁定（相对先验报告）

| 项 | 状态 | 说明 |
|----|------|------|
| Anthropic RSP v3 AI R&D 阈值措辞 | **已裁定** | v3.0 于 **2026-02-24** 生效；重写为公司单边承诺 vs 行业建议；高能力/自动化 AI R&D 操作化示例：可将 **2018–2024 两年进展压缩到一年**；**不再以 v2.1 同款 AI R&D-4/5 编号表为中心** |
| DeepMind FSF ML R&D CCL | **部分裁定** | 博客确认扩展 ML R&D CCLs、内部部署 safety case、FSF 3.1 TCL（**2026-04-17**）；逐条定量 Level 表未在本轮 PDF 干净摘录前不当作已核验原文 |
| OpenAI PF v2 | **沿用已核验** | 2025-04-15 更新；Tracked Category 含 AI Self-improvement；Critical ≈ RSI / fully automated AI R&D（官网本轮 WebFetch 403，数字依先验 PDF/博客） |
| PaperBench 数字 | **已裁定** | 打开 [2504.01848](https://arxiv.org/abs/2504.01848) 与 [openai.com/index/paperbench](https://openai.com/index/paperbench/)：Claude 3.5 Sonnet **21.0%**；PhD 子集 **41.4%** |
| HGM「人类水平」榜时效、跨种子稳健性 | **未核实 / 开放** | |
| METR 时间视野外推至「月级」软件自治 | **部分裁定** | [2503.14499](https://arxiv.org/abs/2503.14499) 报告约 7 个月加倍与 o3≈110 分钟已打开；**外推**依赖外部效度，作者亦强调限制 |
| Genie 系具身 / 独立 AIDE 论文 / Skill-library GUI 若干 | **未纳入主键** | 本轮未打开合格主键 → 不写确定性条目 |
| 实验室内部非公开 RSI 结果 | **不可评论** | |

---

## 新人阅读路径

1. [`docs/00-definitions.md`](docs/00-definitions.md) — 问题与 L0–L3  
2. [`docs/01-coding.md`](docs/01-coding.md) — 最强公开脚手架自进化证据  
3. [`docs/06-weight.md`](docs/06-weight.md) — 权重级自我改进  
4. [`docs/08-evaluation.md`](docs/08-evaluation.md) — 如何（不）测 RSI  
5. [`docs/09-safety.md`](docs/09-safety.md) — 治理与奖励黑客  
6. 其余场景按兴趣；[`docs/timeline.md`](docs/timeline.md) 看编年  

## 目录结构

```
awesome-agent-rsi-zh/
├── README.md
├── LICENSE                 # CC BY 4.0
├── papers.csv              # 机器可读主键表
└── docs/
    ├── 00-definitions.md
    ├── 01-coding.md
    ├── 02-ai-scientist.md
    ├── 03-math.md
    ├── 04-embodied.md
    ├── 05-workflow.md
    ├── 06-weight.md
    ├── 07-web-gui.md
    ├── 08-evaluation.md
    ├── 09-safety.md
    └── timeline.md
```

## 引用与日期说明

- 正文中文；**论文标题保持英文**。  
- 优先引用 arXiv abs / 官方博客 / 作者 README；二手综述不替代主键。  
- 无法打开出处 → 标 **未核实**，不写入确定性数字。  
- `verified_date` = 打开页面日期（本版统一 2026-09-24）。

## 贡献指南（简）

1. 只提交你**亲自打开**过的主键链接。  
2. 用 L0–L3 + 冻结 FM / 外环 / 验证信号 / compounding / 奖励黑客 五维标注。  
3. 更新对应 `docs/0x-*.md` 表行，并同步 `papers.csv` 一行。  
4. 不要把任务刷榜升格为 RSI；作者否认 full RSI 时请保留。

## 许可

[CC BY 4.0](LICENSE)

## 免责声明

本仓库整理公开安全与能力讨论，**不提供**任何攻击、逃逸或绕过评测的操作指南。奖励黑客条目仅作风险文献索引。
