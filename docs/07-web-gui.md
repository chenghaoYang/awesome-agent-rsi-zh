# 07 · 网页 / GUI / OS Agents 自进化

## 场景定义

在 WebArena、浏览器、桌面 GUI、移动 OS 等环境中，通过课程 RL、工作流记忆、轨迹合成飞轮或自进化世界模型提升成功率与泛化。

## 为什么适合 / 不适合 RSI

| 因素 | 评估 |
|------|------|
| 验证器 | **中**：任务成功常依赖规则 ORM / GPT 评判 / 环境重置；真实网站与像素 GUI 脆弱 |
| 适合 | 可重置仿真站；课程与轨迹合成可扩展 |
| 不适合 | 真实站点 TOS/安全；成功判定噪声大；易过拟合特定站 |

## 论文 / 系统表

| 标题 | 机构 | 日期 | 链接 | 层级 | 改了什么 | 验证信号 | 作者报告结果 | 局限 |
|------|------|------|------|------|----------|----------|--------------|------|
| WebRL | 清华 / 智谱 | 2024-11 | [2411.02337](https://arxiv.org/abs/2411.02337) | L3 + 自进化课程 | 在线课程 RL + ORM；更新开放 LLM 权重 | WebArena-Lite | Llama-3.1-8B：4.8%→42.4%；GLM-4-9B：6.1%→43%；超 GPT-4-Turbo 17.6%（作者） | 外环课程/ORM 设计固定；真实 web 另议 |
| Agent Workflow Memory (AWM) | CMU / MIT | 2024-09 | [2409.07429](https://arxiv.org/abs/2409.07429) | L1 | 从轨迹归纳可复用工作流写入记忆 | Mind2Web / WebArena | Mind2Web 相对 SR +24.6%；WebArena 相对 +51.1%；跨站/域仍增益（作者） | 工作流外环与诱导协议固定；非改权重 |
| OS-Genesis | 上海 AI Lab 等 | 2024-12 | [2412.19723](https://arxiv.org/abs/2412.19723) | L0–L1（数据合成） | 反向任务合成 + 轨迹奖励模型 | AndroidWorld / WebArena 等 | AndroidWorld 上 Qwen2-VL 等相对任务驱动基线大幅提升（如约 9.8%→17.4% 量级，作者表） | 合成管线人类设计；轨迹≠改改进机制 |
| AgentTrek | — | 2024-12 | [2412.09605](https://arxiv.org/abs/2412.09605) | L0–L1（数据合成） | 教程引导重放合成轨迹 | WebArena 等 | 约 $0.55/轨迹；Qwen2.5-32B + AgentTrek 数据 WebArena 约 22.4%（作者） | 合成外环固定 |
| DigiRL | Berkeley / Google DeepMind | 2024-06 | [2406.11896](https://arxiv.org/abs/2406.11896) | L3 | 离线→在线 AWR 式 RL 微调 VLM | Android-in-the-Wild | 1.3B VLM：成功率约 17.7%→67.2%（作者摘要）；超 filtered BC / 部分专有 VLM wrapper | 训练协议固定；真实设备非平稳 |
| WebEvolver | 腾讯 AI Lab | 2025-04 | [2504.21024](https://arxiv.org/abs/2504.21024) | L1–L3（自改进 + 世界模型） | 共进化世界模型：合成轨迹 + 推理时前瞻 | Mind2Web-Live / WebVoyager / GAIA-web | 相对 OpenWebVoyager 式自进化基线约 +10%（作者） | 世界模型幻觉；外环仍固定 |
| UI-TARS-2 | ByteDance Seed | 2025-09 | [2509.02544](https://arxiv.org/abs/2509.02544) | L3 + 数据飞轮 | 多轮 RL + 数据飞轮；混合 GUI/终端 | OSWorld / AndroidWorld / Online-Mind2Web | OSWorld 47.5；AndroidWorld 73.3；Online-Mind2Web 88.2（作者） | 飞轮与沙箱人类设计；部分指标依赖内部设施 |

> 检索中出现的 SkillRL、WebXSkill、BAGEL 等：本轮未完整打开 abs 核对结果者标 **未核实**，不写入正式表。

## 场景小结

- **公开路径最清晰的几条**：课程+ORM 的 L3（WebRL）、工作流记忆 L1（AWM）、轨迹合成飞轮（OS-Genesis / AgentTrek）、以及 2025 自进化世界模型 / GUI RL 飞轮（WebEvolver、UI-TARS-2、DigiRL）。  
- GUI/OS **成功判定弱于** 单元测试 / Lean，故「任务分↑」更易被 ORM 噪声与站点漂移污染。  
- 轨迹/任务合成（OS-Genesis、AgentTrek）默认标 **L0–L1**，除非 agent 重写合成器本身。

## 开放问题

1. 跨网站技能迁移的度量，而非单站刷分。  
2. GUI 下不可篡改、低噪声的成功验证器。  
3. 世界模型合成轨迹的幻觉如何进入奖励黑客。
