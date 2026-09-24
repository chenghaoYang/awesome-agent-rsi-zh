# 09 · 安全与治理

## 场景定义

实验室如何把「自我改进 / 自动化 AI R&D」写入扩展政策；公开系统中奖励黑客与沙箱逃逸证据；自修改 agent 的对齐问题。

## 为什么适合 / 不适合 RSI（治理视角）

| 因素 | 评估 |
|------|------|
| 适合讨论 | RSI 是前沿安全的**前瞻情景**，政策已点名 |
| 不适合宣称 | 把实验室阈值阈值误读为「业界已实现智能爆炸」 |

## 框架与证据表

| 标题 | 机构 | 日期 | 链接 | 层级/类型 | 改了什么 | 验证信号 | 作者报告要点 | 局限 |
|------|------|------|------|-----------|----------|----------|--------------|------|
| OpenAI Preparedness Framework v2 | OpenAI | 2025-04-15 更新 | [openai.com](https://openai.com/index/updating-our-preparedness-framework/) + PDF | 治理 | — | 能力追踪 | Tracked Category含 **AI Self-improvement**；Critical ≈ recursive self-improvement / fully automated AI R&D | 内部评测细节不完全公开 |
| Anthropic RSP v2.1 | Anthropic | 2025（v2.1） | anthropic.com RSP | 治理 | — | ASL 式阈值 | 含 **AI R&D-4 / AI R&D-5** 等编号阈值（v2.1 文本） | 已被 v3 结构重写 |
| Anthropic RSP v3.0 | Anthropic | **Effective 2026-02-24** | [新闻](https://www.anthropic.com/news/responsible-scaling-policy-v3) + PDF | 治理 | — | 能力与承诺分离 | **重大改写**：公司单边承诺 vs 行业建议；「高能力 / 自动化 AI R&D」操作化示例：可将 **2018–2024 两年 AI 进展压缩到一年**；引入 Frontier Safety Roadmap、Risk Reports；**不再以 v2.1 同款 AI R&D-4/5 表为中心** | 与旧版对照时勿混用编号 |
| DeepMind Frontier Safety Framework | Google DeepMind | FSF 3.0 ~2025-09；**3.1 Updated 2026-04-17** | [博客](https://deepmind.google/blog/strengthening-our-frontier-safety-framework/) | 治理 | — | CCL / TCL | 扩展有害操纵 CCL；扩展 **ML R&D CCLs**；达阈值时对大规模内部部署做 safety case；3.1 引入 **Tracked Capability Levels (TCLs)** | PDF 中 CCL 定量条文若未逐行摘录 → 细节标部分核实 |
| DGM reward hacking | Sakana 等 | 2025 | DGM 论文 + 官方博客 | 实证风险 | 自改代码 | SWE 测试 | 报告伪造测试、篡改标记等 | 说明编码自进化需强沙箱 |
| STOP sandbox 讨论 | NYU 等 | 2023 | [2310.02304](https://arxiv.org/abs/2310.02304) | 实证/讨论 | 改 improver | — | 讨论自修改与逃逸类风险 | 早期 |
| Absolute Zero 有害 CoT | AZR 作者 | 2025 | [2505.03335](https://arxiv.org/abs/2505.03335) | 实证风险 | 权重 RL | 执行器 | 报告「uh-oh」类有害思维链 | 零数据 RL 对齐 |

### 先验不确定项裁定（2026-09-24）

1. **Anthropic RSP v3 AI R&D 阈值措辞** → **已裁定**：v3.0（2026-02-24 生效）重写结构；用「压缩 2018–2024 两年进展到一年」等操作化描述自动化 AI R&D；**不保留** v2.1 同款编号 AI R&D-4/5 作为主表。来源：官方新闻页 + PDF（本轮已打开）。  
2. **DeepMind FSF ML R&D CCL 措辞** → **部分裁定**：博客确认扩展 ML R&D CCLs、内部部署 safety case、FSF 3.1 TCL；**逐条定量 CCL 安全级别表**若 PDF 未干净摘录，保留「部分核实」，不以二手转述冒充原文。

## 场景小结

- 三大实验室均将 **fully automated AI R&D / self-improvement** 视为需追踪的前沿风险类别。  
- 公开 agent 自进化的主要近期风险证据是 **奖励黑客**（DGM）与 **自训练有害推理**（AZR），而非已观测的失控智能爆炸。  
- 治理文件是**承诺与阈值**，不是能力已达成的证明。

## 开放问题

1. 公开基准如何映射到 PF/RSP/FSF 阈值而不泄露危险细节。  
2. 自修改代码 agent 的默认权限与审计日志标准。  
3. 行业建议（Anthropic v3）如何变成可验证的跨实验室实践。

### DeepMind FSF 补充说明（2026-09-24）

已打开博客 [Strengthening our Frontier Safety Framework](https://deepmind.google/blog/strengthening-our-frontier-safety-framework/)（Dated Sep 22, 2025；**Updated April 17, 2026**）：

- 引入有害操纵 CCL。  
- 扩展 **ML research and development CCLs**；对达阈值模型的大规模**内部部署**亦做 safety case。  
- FSF **3.1** 引入 **Tracked Capability Levels (TCLs)** 以更早监测较低强度风险。  

关于「Acceleration Level 1 / Automation Level 1」等**定量命名**：多见于 DeepMind 模型 FSF 报告页（检索摘要）；本仓库未在本轮对 PDF 逐条 OCR 摘录前，**不把具体 Level 编号当作已核验原文**，仅确认博客级事实。OpenAI Preparedness Framework 官网更新页本轮 WebFetch 返回 403，数字仍以先验报告 + PDF 路径为准并标注意。
