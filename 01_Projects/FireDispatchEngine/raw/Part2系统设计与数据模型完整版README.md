# Part 2：系统设计与数据模型

**所属Part**：Part 2
**物理目录**：`03_SystemDesign` + `04_DIKW_Examples` + `05_DataModel`
**文档数量**：45份
**最后更新**：2025-04-24

**一句话定义**：
本Part聚焦**系统架构设计**、**知识体系构建**和**数据模型**，是连接需求与引擎实现的关键桥梁，包含MultiAgent架构、核心实体模型和DIKW转化示例。

---

## 1. 目录概述

### 核心内容
- 系统概述、数据流、状态机设计
- Obsidian知识库体系与MultiAgent架构
- 核心实体模型、ER图、数据库表结构
- DIKW转化示例

### 核心技术
- MultiAgent多智能体架构（感知、决策、执行、预测）
- DIKW模型（Data → Information → Knowledge → Wisdom）
- 实体关系建模 + 数据库表结构设计
- 标签体系设计（Type/State/Source/Topic + Transition）

---

## 2. MultiAgent架构详解

### 四Agent职责

| Agent | 职责 | 输入 | 输出 | 权重 |
|-------|------|------|------|------|
| 感知Agent | 场景理解与事实基础 | 画像+模拟结果 | 场景标签+历史案例 | 15% |
| 决策Agent | 战术规划与力量分工 | 感知输出 | 主攻方向+任务分工+战术要点 | **40%** |
| 执行Agent | 可执行性验证与指令生成 | 决策输出 | 时间线+指令模板+资源消耗 | 20% |
| 预测Agent | 前瞻性风险与态势预测 | 全局+决策输出 | 火势蔓延+增援需求+次生灾害 | 25% |

### 仲裁机制（5阶段）
1. 结果标准化（统一JSON Schema）
2. 交叉验证（检测Agent间不一致）
3. 加权投票（默认权重：决策40%、预测25%、执行20%、感知15%）
4. LLM仲裁器（当分歧>0.3时触发）
5. 二次验证（送回执行+预测再校验）

---

## 3. 核心文档清单（优先阅读顺序）

1. `01_Overview_And_Goals.md` —— 系统概述与目标
2. `MultiAgent_Architecture/消防多智能体架构.md` —— 多智能体架构详解
3. `05_DataModel/01_Core_Entities_And_Domain_Model.md` —— 核心实体模型
4. `05_DataModel/02_ER_Diagram_And_Relation_Model.md` —— ER图与关系模型
5. `05_DataModel/03_Database_Table_Structure.md` —— 数据库表结构
6. `04_DIKW_Examples/MOC-DIKW转化示例.md` —— DIKW转化示例

---

## 4. 数据模型要点

### 核心实体
- `Incident`（警情）
- `AlertStructured`（结构化警情）
- `IncidentPortrait`（警情画像）
- `AlertLevelResult`（等级判定）
- `DispatchScaleResult`（规模计算）
- `StationVehicleMatching`（队站匹配）
- `CommandPlan`（指挥方案）
- `AuditTrace`（审计轨迹）

### 关键关系
```
Incident → AlertStructured → IncidentPortrait → AlertLevelResult
→ DispatchScaleResult → StationVehicleMatching → CommandPlan → AuditTrace
```

---

## 5. 阅读与使用建议

- **开发人员**：重点阅读MultiAgent架构和DataModel目录
- **架构师**：重点阅读系统概述、数据流、状态机设计
- **数据工程师**：重点阅读ER图和数据库表结构

---

## 6. 版本记录

- **v2.1**（2025-04-24）：增加MultiAgent架构详解和仲裁机制
- **v2.0**：完成5个Part拆分思维导图

---

**相关链接**
[[02_Part逻辑映射索引]] | [[Part 1 ← 需求与场景]] | [[Part 3 → 核心调派引擎]]