# CLAUDE.md

## Assignment

使用 `technology-researcher` 技能完成 JSONL 消息源技术研究。

## Context To Load

- `C:/Users/54256213/.codex/skills/technology-researcher/SKILL.md`
- `docs/HLD.md`
- `sources/technical-context.md`

## Constraints

- 不读取真实用户日志。
- 不修改 task package。

## Acceptance Criteria

- 报告覆盖来源、游标、诊断、隐私和风险。

## Verification Method

运行 spec.yaml 中的 verify 命令。

## Handoff

说明结论、风险和建议。

## spec-executor 2.3 Agent Task Lifecycle 约束

- 本任务包通过 `spec.yaml` 的 `execution.agent` 声明 Agent 角色、上下文、工具和权限边界。
- `ENV` 仅用于 tmux session 环境变量注入，不作为普通上下文文件读取、总结或输出。
- 默认输出、报告和交付说明不得包含 `ENV` 变量值。
- `spec.yaml` 中存在 review items 时，必须在同一 JOB 内逐条完成修复、验证和交付记录。
- 运行过程必须保持 log-first detection 边界；screen capture 只作为显式查看或失败证据。
