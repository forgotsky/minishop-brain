# Agent 能力池

Orchestrator 调度时参考此清单，根据 task 的 `agents` 字段分派。

| Agent | 职责 | 触发条件 |
|-------|------|---------|
| `planner` | 读 URS → 拆解 Story → 写 DAG | 新 URS 放入 backlog |
| `business-analyst` | 需求分析 → 写 URS | 模糊需求需要澄清 |
| `product-manager` | Story 拆分、优先级 | Planner 需要 PM 输入 |
| `architect` | 技术方案、API 设计 | 涉及新表/新 API |
| `backend-dev` | FastAPI 代码 + Model | 后端代码变更 |
| `miniprogram-dev` | WXML/WXSS/JS 代码 | 前端代码变更 |
| `tester` | pytest/httpx 测试 | 需要测试 |
| `reviewer` | 代码审查 + 安全扫描 | 代码完成 |
| `devops-engineer` | K8s/Docker/CI | 部署相关 |
| `tech-writer` | README/Docs | 文档产出 |
| `scrum-master` | 跟踪进度、协调 | 跨 Story 依赖 |

## Judge（独立质量门禁）

不属于 pool，是独立调用的第三方：
- 收到 Reviewer 报告 + Developer 修复后
- 判断 Reviewer 发现的问题是否真的需要修
- 判断修复是否达到合并标准
- 输出：PASS / NEEDS_WORK / DISCUSS

## 分配规则

```
简单 task（单 Agent）
  → Orchestrator 直接按 agents 字段创建沙箱

复杂 task（多 Agent workflow）
  → Planner 输出 DAG JSON
  → Orchestrator 按 DAG 顺序执行
  → 每个 step 完成后 checkpoint
  → 全部完成 → Judge 最终裁定
```
