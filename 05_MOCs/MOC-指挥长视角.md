# MOC-指挥长视角

**视角**：指挥长（现场指挥官）
**位置**：`05_MOCs/`
**更新日期**：2025-04-26

---

## 指挥长关心什么？

指挥长最关心的是：
- **态势感知**：实时掌握救援进展
- **决策支持**：AI辅助的战术建议
- **资源调配**：消防力量合理分配
- **风险预警**：次生灾害预警

---

## 指挥长相关文档

### 决策支持

| 文档 | 说明 | 入口 |
|------|------|------|
| [[MOC-核心调派引擎-详细子模块.md]] | Part 3引擎 | 12步流程 |
| [[MOC-StateMachine.md]] | 状态机 | 步骤状态 |
| [[01_Projects/FireDispatchEngine/06_DispatchEngine/AI_Support/01_AILLM应急指挥智能决策支持.md]] | AI决策支持 | 4-Agent |

### 资源与调度

| 文档 | 说明 | 入口 |
|------|------|------|
| [[MOC-调派规模计算模型.md]] | 规模计算 | N_total公式 |
| [[01_Projects/FireDispatchEngine/06_DispatchEngine/04_Constraint_Validation_Mechanism.md]] | 约束校验 | 五维校验 |

### 审计与责任

| 文档 | 说明 | 入口 |
|------|------|------|
| [[MOC-审计责任与数学模型.md]] | Part 4 | 责任闭环 |
| [[01_Projects/FireDispatchEngine/07_Audit_And_Responsibility/01_Human_Confirmation_And_Responsibility.md]] | 人工确认 | 责任关口 |

---

## 12步流程（指挥长视角）

| Step | 关键动作 | 指挥长关注 |
|------|---------|-----------|
| Step 3-4 | 画像构建+等级判定 | 被困人员情况 |
| Step 5-6 | 规模计算+车辆匹配 | 资源是否充足 |
| Step 7 | 约束校验 | 安全底线 |
| Step 8 | 反向模拟 | 方案可行性 |
| Step 9 | AI多智能体决策 | 战术建议 |
| Step 10 | **人工确认** | ★ 指挥长决策点 |
| Step 11-12 | 下达+审计 | 执行记录 |

---

## 核心关注点

| 关注点 | 对应文档 |
|--------|----------|
| 实时态势 | [[MOC-StateMachine.md]] - 监控仪表盘 |
| 战术建议 | [[MOC-核心调派引擎-详细子模块.md]] - Step 9 |
| 风险预警 | [[01_Projects/FireDispatchEngine/06_DispatchEngine/04_Constraint_Validation_Mechanism.md]] |
| 责任追溯 | [[MOC-审计责任与数学模型.md]] |

---

## 相关链接

- [[05_MOCs/MOC-Index.md]] - 全局总索引
- [[05_MOCs/MOC-FireDispatchEngine.md]] - 项目导航
- [[01_Projects/FireDispatchEngine/]] - 项目目录
