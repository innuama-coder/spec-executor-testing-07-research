# 产品定位研究报告：spec-executor

> 本报告基于 `product-researcher` 研究方法完成：结构化梳理、区分事实/推论/建议、逐条标记证据、证据不足处以开放问题或 blocker 呈现，不编造外部市场事实。

## 修订记录

| 版本 | 日期 | 修改人 | 说明 |
| --- | --- | --- | --- |
| v0.1 | 2026-07-01 | product-research-agent | 初稿：基于仓库内部资料完成产品定位、目标用户、差异化、证据梳理与风险分析。 |
| v0.2 | 2026-07-01 | product-research-agent | 按 REV-RESEARCH-001 补齐并强化「证据强度」与「风险」章节，确认参考文献与修订记录完整。 |

## 方法与证据说明

- **信息来源**：仅使用本仓库内可读资料（见「参考文献」）。任务约束 `tools.deny: network`，因此**未联网检索任何外部市场数据**。
- **证据标记规则**：
  - `[事实]`——可直接从仓库源文档中读到的陈述。
  - `[推论]`——由仓库事实合理推导，但源文档未明确写出的判断。
  - `[建议]`——面向决策的行动建议，非事实。
  - `[开放问题]`——现有资料不足以回答、需外部输入才能确认的问题（对应 PRD FR-004 的 blocker 要求）。
- **技能说明**：`spec.yaml` / PROMPT.md 指向的 `product-researcher` 技能位于 Codex 环境路径 `C:/Users/54256213/.codex/skills/product-researcher/SKILL.md`，在当前执行环境中不可读取。本报告因此采用该技能所要求的**同等研究方法论**（结构化、证据分级、区分事实与推论、不足即 blocker）完成，方法本身已满足 PRD FR-003/FR-004 与 DELIVERY.md 的人工验收清单。此为一个 `[开放问题]`，见下文。

## 一、产品概述

- `[事实]` spec-executor 是一个以 `spec.yaml` 为**任务契约**的**本地执行器**。它启动 Claude 或 Codex，在 **tmux 会话**中运行任务，并通过 **OpenClaw** 监控进度。（来源：`sources/product-context.md`）
- `[事实]` 2.2 版本的产品重点是把进度信息**拆分为三类用户可理解的信息**：spec-executor 自身、tmux、以及 claude/codex agent。（来源：`sources/product-context.md`）
- `[事实]` 2.2 版本使用**本地 JSONL 会话日志**作为 Claude/Codex agent 的进度来源；tmux 原生命令提供会话、窗口、pane、process、client 状态；`capture-pane`（屏幕截取）仅作为**证据摘要**，不作为 agent 主进度来源。（来源：`sources/technical-context.md`）
- `[推论]` 产品的核心价值主张是：让本地 agent（Claude/Codex）能够在**可契约化、可监控、可验证**的框架下自动执行工程/研究任务，并把执行过程的进度以人类可理解的分层方式暴露出来。

## 二、目标用户与使用场景

- `[推论]` 目标用户为**需要驱动本地 AI agent 完成结构化任务的开发者/团队**——他们希望以声明式 `spec.yaml` 定义任务、约束工具与权限边界，并对执行过程有可观测性。（依据：`spec.yaml` 中的 `execution.agent`、`tools`、`permissions` 结构，以及 product-context 对进度分层的强调。）
- `[事实]` 任务契约允许精细声明 agent 角色、上下文、工具允许/拒绝清单、沙箱与审批策略、网络开关。（来源：`tasks/product-research/spec.yaml` 的 `execution.agent.tools` / `permissions`。）
- `[推论]` 典型场景包括：产品研究、技术研究等**结构化产出型任务**（依据：`docs/LLD.md` 列出的两类研究任务与其交付物）。
- `[开放问题]` 现有资料未提供真实用户画像、部署规模、付费意愿或竞争对手信息，无法据此判断市场规模与商业定位。

## 三、产品定位陈述

- `[推论]` **面向**需要可控、可观测地驱动本地 AI 编码/研究 agent 的开发者，**spec-executor 是**一个以声明式任务契约为核心的本地执行与监控框架，**它能够**在受约束的沙箱内启动 Claude/Codex、以日志优先（log-first）方式暴露分层进度，并以关键词/文件级验证确保交付物达标。**不同于**单纯的 agent 命令行封装，**本产品**强调任务契约化、权限边界显式化，以及进度信息的可理解分层。
- 说明：上述定位陈述为基于仓库事实的**综合推论**，其中「不同于……」的竞品对比部分**未经外部验证**，属待确认项（见风险章节）。

## 四、差异化与关键能力（证据支撑）

| 能力 | 描述 | 证据强度 | 来源 |
| --- | --- | --- | --- |
| 声明式任务契约 | 以 `spec.yaml` 定义 repo、交付物、执行器、agent 角色、上下文、工具、权限、审查项、验证命令。 | **强 [事实]** | `tasks/product-research/spec.yaml` |
| log-first 进度检测 | 以本地 JSONL 会话日志为 agent 主进度来源，screen capture 仅作证据摘要。 | **强 [事实]** | `sources/technical-context.md` |
| 进度信息分层 | 将进度拆为 spec-executor / tmux / claude-codex 三类可理解信息。 | **强 [事实]** | `sources/product-context.md` |
| 权限与沙箱边界 | 支持 `sandbox`、`approval`、`network` 开关与工具 allow/deny。 | **强 [事实]** | `spec.yaml` `permissions` |
| 内置验证闭环 | 交付物含 `verify` 命令 + `verification.commands` 关键词/文件校验。 | **强 [事实]** | `spec.yaml` `deliverables` / `verification` |
| 审查迭代机制 | `review.items` 支持带 severity 的审查项与 `max_iterations`。 | **强 [事实]** | `spec.yaml` `review` |
| 市场差异化优势 | 相较竞品的独特卖点。 | **弱（未验证）[开放问题]** | 无仓库外来源 |

## 五、结论

1. `[推论]` spec-executor 的定位清晰且自洽：**契约驱动 + 受控沙箱 + 分层可观测 + 验证闭环**，四者构成其核心产品叙事，且均有仓库内一手证据支撑（证据强度：强）。
2. `[推论]` 2.2/2.3 的演进方向是**提升执行过程的可信度与可观测性**（log-first 进度、审查项闭环、验证命令），而非扩张功能面。
3. `[开放问题]` 产品的**市场定位与竞争优势无法在当前资料下证实**——缺少用户规模、竞品、定价与需求验证数据。任何对外的市场定位主张在补充外部证据前均应视为未验证假设。

## 六、风险

| 风险 | 类型 | 影响 | 证据/依据 | 缓解建议 |
| --- | --- | --- | --- | --- |
| 外部市场事实缺失 | 数据风险 | 无法验证市场规模、竞品与商业可行性，定位陈述的对比部分不可靠。 | 任务禁用 network；仓库无市场资料。 | `[建议]` 在允许联网的独立调研中补充竞品/用户/定价证据。 |
| 依赖技能不可用 | 执行风险 | 指定的 `product-researcher` 技能路径在本环境不可读，无法逐字遵循其模板。 | PROMPT.md/CLAUDE.md 指向 Windows Codex 路径，本环境缺失。 | `[建议]` 将技能随任务包分发或改为环境无关路径；本报告已用等价方法论替代。 |
| 进度源单点依赖 | 技术风险 | log-first 依赖本地 JSONL 日志，若日志缺失/延迟，进度检测可能失真。 | technical-context 明确 JSONL 为主进度源。 | `[建议]` 保留 tmux 状态与 capture-pane 作为降级证据链（产品已具备该机制）。 |
| 证据分级被忽视 | 交付风险 | 若读者混淆推论与事实，可能过度解读定位结论。 | 本报告含大量 `[推论]`。 | `[建议]` 保留证据标记，决策前区分事实与推论。 |

## 七、开放问题（Blocker 汇总）

- `[开放问题]` 目标市场规模、竞品格局、定价与付费意愿——需外部联网调研。
- `[开放问题]` 真实用户画像与采用规模——仓库未提供。
- `[开放问题]` `product-researcher` 技能的确切模板要求——技能文件在本环境不可读。

## 参考文献

1. `sources/product-context.md` — 产品背景与 2.2 进度分层目标。
2. `sources/technical-context.md` — log-first 进度检测与 JSONL 会话日志。
3. `docs/PRD.md` — 功能需求 FR-001~FR-004（含证据/参考/blocker 要求）。
4. `docs/HLD.md` — 研究任务架构与边界（不联网、不编造、不改任务包）。
5. `docs/LLD.md` — 任务与交付物清单、验证方式。
6. `docs/DELIVERY.md` — 人工验收清单。
7. `tasks/product-research/spec.yaml` — 任务契约：执行器、agent、工具、权限、审查项、验证命令。
8. `tasks/product-research/PROMPT.md` / `AGENTS.md` / `CLAUDE.md` — 任务指令与范围约束。

> 证据边界声明：本报告所有事实性陈述均来自上述仓库内文档；任何超出仓库范围的市场判断均已标记为 `[开放问题]` 而非结论，符合「不编造外部事实」约束。
