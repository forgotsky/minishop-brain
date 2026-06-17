# MiniShop Brain

MiniShop 的脑力仓库 — 运行时工作产物。

| 目录 | 内容 | 生命周期 |
|------|------|---------|
| `.ai/tasks/` | Agent 任务看板 | 进行中 → 完成即删 |
| `.ai/agents/` | Agent 能力池定义 | 长期 |
| `.ai/checkpoints/` | Workflow 断点快照 | 自动创建/清理 |
| `.ai/outputs/` | Story 间结果传递 | 下游消费后可清理 |
| `.ai/logs/` | Agent 执行日志 | 归档用 |

## 不在这个仓库的

| 内容 | 在哪 | 为什么 |
|------|------|--------|
| `docs/stories/` | [minishop 代码库](https://github.com/forgotsky/minishop) | 设计文档属于代码知识体系 |
| `scripts/` | [minishop 代码库](https://github.com/forgotsky/minishop) | 部署脚本属于基础设施代码 |
| 前后端代码 | [minishop](https://github.com/forgotsky/minishop) | 代码 |
