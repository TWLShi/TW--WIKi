# Claude Code 小型团队应用场景

**标签**：#ClaudeCode #小型团队 #AI协作 #Subagents #Skills
**位置**：03_SystemDesign/

---

## 核心痛点与解决

| 痛点 | 解决 |
|------|------|
| 人手少，多角色切换 | Subagents 并行分工 |
| 知识分散 | Memory + CLAUDE.md 共享上下文 |
| 流程不一致 | Skills + Hooks 标准化 |
| 上下文切换成本高 | 代理协调减少切换 |

---

## 典型场景（按频率排序）

| 场景 | 占比 | 说明 |
|------|------|------|
| **日常开发迭代** | ~60% | Slash Commands 生成计划/PR审查/测试 |
| **新功能开发与重构** | 高价值 | Orchestrator + Subagents 并行（前端/后端/审查/测试） |
| **知识管理与 onboarding** | 长期价值 | Memory + Checkpoints 保留项目历史 |
| **CI/CD 维护自动化** | 自动化 | Hooks 自动 review/测试/安全扫描 |

---

## Subagents 实现模式（FireCommand AI 启发）

```
Orchestrator（主代理）
├── 灾情分析 Agent
├── 资源调派 Agent
├── 风险评估 Agent
└── 方案生成 Agent
```

---

## 成功关键

1. 从 **CLAUDE.md** 开始定义团队规范
2. 优先建立 3-5 个核心 **Skills**（review、test、plan）
3. 使用 **Subagents** 而非过度复杂 Agent Teams
4. 保持透明：所有代理动作记录可查

---

## 费用与限制

| 项目 | 建议 |
|------|------|
| 方案 | Pro 方案，监控 token 使用量 |
| 幻觉控制 | Reviewer Subagent + 人机最终确认 |
| 初始设定 | 1-2 天（claude-howto 可大幅缩短） |

---

## 关联文档

- [[08_Obsidian+OpenClaw+Claude知识库方案]] — 知识库方案
- [[03_SystemDesign/系统架构设计]] — 系统架构设计

## 变更记录

- 2026-04-24：提取 Claude Code 小型团队应用场景