# DELIVERY - 研究型测试仓库

## 验收用途

本文档用于人工复核研究类任务是否满足事实约束、证据约束和报告结构要求。执行者无需修改本文档，但最终回复必须说明报告路径、核心结论和证据强度。

## 交付物

| 任务 | 交付物 | 验收要点 |
| --- | --- | --- |
| 产品研究 | `reports/product-positioning.md` | 使用 `product-researcher`，包含修订记录、证据标记、结论、风险和参考文献。 |
| 技术研究 | `reports/jsonl-source-research.md` | 使用 `technology-researcher`，覆盖 JSONL 来源、游标、诊断、隐私和风险。 |

## 验收命令

```bash
test -s reports/product-positioning.md
test -s reports/jsonl-source-research.md
```

## 人工验收清单

- 报告使用简体中文。
- 报告区分事实、推论和建议。
- 报告包含修订记录、证据标记和参考文献。
- 证据不足的问题以 blocker 或开放问题呈现，不编造外部事实。
- 最终回复说明报告路径、关键结论、证据强度和风险。
