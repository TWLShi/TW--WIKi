# MOC-技术架构视角

**视角**：技术架构师/开发人员
**位置**：`05_MOCs/`
**更新日期**：2025-04-26

---

## 技术架构师关心什么？

技术架构师最关心的是：
- **系统架构**：整体设计
- **领域模型**：DDD设计
- **技术选型**：技术栈选择
- **扩展性**：系统演进能力

---

## 技术架构相关文档

### 系统架构

| 文档 | 说明 | 入口 |
|------|------|------|
| [[MOC-系统设计与数据模型.md]] | Part 2 | 系统设计 |
| [[01_Projects/FireDispatchEngine/03_SystemDesign/01_Overview_And_Goals.md]] | 系统概述 | 愿景目标 |
| [[01_Projects/FireDispatchEngine/03_SystemDesign/MultiAgent_Architecture/消防多智能体架构.md]] | MultiAgent | 四Agent |

### 领域模型（DDD）

| 文档 | 说明 | 入口 |
|------|------|------|
| [[01_Projects/FireDispatchEngine/05_DataModel/01_Core_Entities_And_Domain_Model.md]] | 核心实体模型 | 聚合根 |
| [[01_Projects/FireDispatchEngine/05_DataModel/02_ER_Diagram_And_Relation_Model.md]] | ER图 | 关系模型 |
| [[01_Projects/FireDispatchEngine/05_DataModel/03_Database_Table_Structure.md]] | 数据库表 | 表结构 |

### 核心引擎

| 文档 | 说明 | 入口 |
|------|------|------|
| [[MOC-核心调派引擎-详细子模块.md]] | Part 3 | 引擎总览 |
| [[MOC-StateMachine.md]] | 状态机 | XState实现 |
| [[MOC-Query_Routing问题路由专区.md]] | Query Routing | 智能问询 |

---

## 技术栈概览

| 层级 | 技术选型 | 说明 |
|------|----------|------|
| 前端 | React + Ant Design + ECharts | 监控大屏 |
| 状态机 | XState | 12步状态管理 |
| 后端 | Spring Boot / Node.js | API服务 |
| 数据库 | PostgreSQL + Neo4j | 关系+图 |
| 向量检索 | Faiss | 热词检索 |
| ASR | FunASR | 语音识别 |
| LLM | Qwen / GPT | 推理与蒸馏 |

---

## DDD领域设计

```
限界上下文：
├── 接警上下文（Step 1-2）
├── 调派上下文（Step 3-9）
└── 审计上下文（Step 10-12）

聚合根：
└── Incident（警情）
    ├── AlertStructured
    ├── IncidentPortrait
    ├── AlertLevelResult
    └── CommandPlan

领域服务：
├── Query_Routing（智能问询）
├── MultiAgent（AI决策）
└── ConstraintValidation（约束校验）
```

---

## 核心关注点

| 关注点 | 对应文档 |
|--------|----------|
| 整体架构 | [[MOC-系统设计与数据模型.md]] |
| 状态机实现 | [[MOC-StateMachine.md]] - XState |
| 领域模型 | [[01_Projects/FireDispatchEngine/05_DataModel/01_Core_Entities_And_Domain_Model.md]] |
| 技术选型 | [[01_Projects/FireDispatchEngine/03_SystemDesign/MultiAgent_Architecture/消防多智能体架构.md]] |

---

## 相关链接

- [[05_MOCs/MOC-Index.md]] - 全局总索引
- [[01_Projects/FireDispatchEngine/]] - 项目目录
