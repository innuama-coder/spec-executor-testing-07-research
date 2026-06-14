# spec-executor-testing-07-research

研究型独立测试仓库。该仓库用于验证 spec-executor 是否能够驱动 Claude/Codex 使用已安装技能完成产品研究和技术研究，并产出可审阅的工作文档。

## 目录

- `docs/PRD.md`
- `docs/HLD.md`
- `docs/LLD.md`
- `docs/DELIVERY.md`
- `sources/product-context.md`
- `sources/technical-context.md`
- `tasks/product-research/`
- `tasks/technology-research/`

## 运行

```bash
spec-executor run --spec tasks/product-research/spec.yaml --workspace ./workspace
spec-executor run --spec tasks/technology-research/spec.yaml --workspace ./workspace
```
