# 00 · 核心定义与判定标准

> 核验日：2026-09-24（Asia/Shanghai）  
> 原则：先定义问题与可检验判据，再列证据；无法打开原始出处的条目标「未核实」。

## 1. 问题陈述

本仓库只回答一个可操作问题：

> **公开文献中，有哪些系统在何种场景下实现了可复核的「自我改进」？其改进的是任务表现、脚手架，还是改进机制本身？是否存在跨代复合式（compounding）增益，还是很快饱和？**

「自我进化 agent」≠「递归自我改进（RSI）」。前者是宽标签；后者要求系统能改进**改进自身的那个过程**，并 ideally 产生跨代加速。

## 2. 自改进层级（L0–L3）

| 层级 | 定义 | 典型改动对象 | 外层循环 | 示例（已核验） |
|------|------|--------------|----------|----------------|
| **L0** | 固定优化器改进任务 agent | 提示词、工作流图、agent 代码（由固定 meta 搜索） | 固定 | ADAS / Meta Agent Search；AFlow；TextGrad；DSPy |
| **L1** | Agent 修改自身脚手架 | 自身代码 / 提示 / 记忆 / 工具 / 技能库 | 常固定；agent 在循环内自改 | DGM；SICA；HGM；Live-SWE-agent；Gödel Agent；Voyager |
| **L2** | Agent 修改改进机制本身 | proposer / selector / evaluator / 搜索算法 | 部分可变 | STOP（改 improver）；Promptbreeder（突变提示也可进化）；HGM 的 CMP 选择仍属固定算法 |
| **L3** | 通过自生成数据/奖励改权重 | 模型参数 | 训练循环固定或半固定 | STaR；Self-Rewarding；SPIN；Absolute Zero；R-Zero；STP；WebRL |

**判定细则：**

1. 仅用固定 meta-agent 搜索更好的子 agent → **L0**（哪怕子 agent 很强）。
2. 任务 agent 在运行期改自己的工具/代码/记忆，但「如何选下一代」的算法由作者写死 → **L1**。
3. 只有当 proposer/selector/evaluator/search **本身被系统改写**且改写进入后续代 → 才标 **L2**（多数公开系统仅「部分 L2」）。
4. 用自生成轨迹/奖励做 RL/SFT 更新权重 → **L3**（可与 L0–L2 脚手架并存）。

## 3. 附加标注维度（每条必填）

| 维度 | 取值 |
|------|------|
| 基础模型是否冻结 | yes / no / unknown |
| 外层循环是否固定 | yes / no / partial |
| 验证信号 / 奖励 | 单元测试、Lean 检查器、执行器、人类偏好模型、自模型打分等 |
| 代际证据 | compounding（跨代持续抬升）/ saturation（很快平台）/ unclear |
| 奖励黑客 | 作者是否报告 reward hacking / sandbox 逃逸 |

## 4. 何谓「复合式递归改进」证据边界

本仓库采用**严格证据边界**：

| 声称 | 需要的最低证据 |
|------|----------------|
| 任务表现自改进 | 同一评测上多代分数；披露成本与种子 |
| 元生产力（metaproductivity）自改进 | 如 HGM 的 CMP：子代在**新任务**上的改进能力被度量 |
| 改进机制自改进（接近经典 RSI） | 对 proposer/selector/evaluator 的修改被继承，且带来可测加速 |
| 「智能爆炸」曲线 | 公开、可复核的跨代加速度指标——**截至核验日，公开文献中未见** |

作者自述「不是 full RSI」时，本仓库**采信作者表述**，不升格。

## 5. 场景适合 RSI 的第一性原理

一个场景是否适合 agent RSI，主要看三点：

1. **验证器（verifier）是否便宜、可靠、可自动**  
   - 强：单元测试、Lean、代码执行、竞赛评测机  
   - 弱：开放式科研品味、网页主观成功、对齐价值判断  
2. **修改空间是否可程序化**  
   - 代码/提示/工作流图易改；权重需训练栈；硬件/具身另有通道  
3. **是否能量化「改进改进」而不只是「改进任务」**  
   - 缺 metaproductivity 度量时，易把过拟合评测当成 RSI  

## 6. 与先验报告的关系

本仓库复用并扩展 `/workspace/agent-self-evolution-rsi.md`（2026-09-24）已核验条目：STOP、Gödel Agent、ADAS、DGM、SICA、HGM、AlphaEvolve、Voyager、AI Scientist、Self-Rewarding LMs，以及 OpenAI PF v2、Anthropic RSP、DeepMind FSF。新增条目均经 WebSearch/WebFetch 打开 arXiv abs/HTML、官方博客或作者 README。

## 7. 引用约定

- 论文标题保持英文原文。  
- 链接优先 arXiv abs：`https://arxiv.org/abs/<id>`。  
- 日期取 arXiv 首发或官方发布日；不确定标「未核实」。  
- `verified_date` 一律为打开页面的日期（本仓库为 2026-09-24）。
