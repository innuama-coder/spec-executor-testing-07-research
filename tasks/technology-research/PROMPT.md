# PROMPT.md

## 任务目标

使用 `technology-researcher` 技能，基于仓库资料完成 JSONL 消息源技术研究报告。

## 必读上下文

1. `C:/Users/54256213/.codex/skills/technology-researcher/SKILL.md`
2. `docs/HLD.md`
3. `docs/LLD.md`
4. `sources/technical-context.md`

## 交付物

- `reports/jsonl-source-research.md`

## 验收标准

- 使用简体中文。
- 覆盖 JSONL 来源、游标、诊断、隐私和风险。
- 区分事实、推论和建议。

## Handoff

最终回复包含报告路径、关键结论和风险。

## spec-executor 2.3 Agent Task Lifecycle 约束

- 本任务包通过 `spec.yaml` 的 `execution.agent` 声明 Agent 角色、上下文、工具和权限边界。
- `ENV` 仅用于 tmux session 环境变量注入，不作为普通上下文文件读取、总结或输出。
- 默认输出、报告和交付说明不得包含 `ENV` 变量值。
- `spec.yaml` 中存在 review items 时，必须在同一 JOB 内逐条完成修复、验证和交付记录。
- 运行过程必须保持 log-first detection 边界；screen capture 只作为显式查看或失败证据。
