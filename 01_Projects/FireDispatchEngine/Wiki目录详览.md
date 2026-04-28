# FireDispatchEngine 完整Wiki目录详览

**项目**：消防调派智能系统（FireDispatchEngine）
**更新日期**：2025-04-26
**总文档数**：200+份

---

## 一、整体目录架构

```mermaid
graph TD
    FE["FireDispatchEngine/"]

    subgraph FE["Part目录（核心节点 - 红色高亮）"]
        GN["00_GlobalNavigation<br/>全局导航枢纽"]
        R1["01_Requirements<br/>Part 1：业务需求"]
        S2["02_Scenarios<br/>场景模拟与案例库"]
        SD["03_SystemDesign<br/>Part 2：系统设计"]
        DK["04_DIKW_Examples<br/>DIKW知识转化"]
        DM["05_DataModel<br/>核心数据模型"]
        DE["06_DispatchEngine<br/>★ Part 3：核心引擎"]
        AR["07_Audit_And_Responsibility<br/>Part 4：审计责任"]
        MO["08_Math_And_Optimization<br/>数学模型"]
        RM["09_Roadmap<br/>项目路线图"]
        AP["10_Appendix<br/>附录"]
        RW["raw/<br/>原始文档库"]
    end

    GN --- R1
    R1 --- S2
    S2 --- SD
    SD --- DK
    DK --- DM
    DM --- DE
    DE --- AR
    AR --- MO
    MO --- RM
    RM --- AP
    AP --- RW

    style R1 fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style S2 fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style SD fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style DK fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style DM fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style DE fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style AR fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style MO fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style RM fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style AP fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style RW fill:#ff6b6b,stroke:#c92a2a,color:#fff
    style GN fill:#51cf66,stroke:#2f9e44,color:#fff
```

**说明**：红色节点（01-10 + raw/）为Part核心目录，绿色节点（00_GlobalNavigation）为全局导航枢纽。

---

## 二、目录详解

### 00_GlobalNavigation（全局导航枢纽）

| 文件 | 说明 | 备注 |
|------|------|------|
| `00_消防调派智能系统全局视图.md` | **总览入口**，完整思维导图融合版 | 推荐新成员首先阅读 |
| `00_消防调派智能系统思维导图.md` | 思维导图原版 | |
| `01_知识库架构流程图.md` | 知识库架构总览 | |
| `02_Part逻辑映射索引.md` | Part之间逻辑关系映射 | |
| `02_目录调整对比说明.md` | 目录调整记录 | |

**备注**：全局导航是整个项目的入口枢纽，连接所有Part。

---

### 01_Requirements（Part 1：业务需求与场景层）

| 文件/目录 | 说明 | 备注 |
|-----------|------|------|
| `Part1-README.md` | **Part 1总览**，DDD业务需求定义 | 业务需求定义专用章节 |
| `01_Dispatch_Scale_Calculation_Model.md` | **核心**：调派规模计算模型 | 包含N_total公式、基础编成表 |
| `02_Ten_Subscenario_Calculation_Examples.md` | 十类场景计算示例 | 包含普通住宅、高层、化工等 |
| `03_FireCommandAI项目定义.md` | 项目定义文档 | |
| `03_Unified_Dispatch_Composition_Table.md` | 统一调派编成表 | |
| `04_Vehicle_Determination_Logic.md` | 车辆判定逻辑 | |
| `05_Station_Determination_Logic.md` | 队站判定逻辑 | |
| `05_消防接处警系统竞品对比分析.md` | 竞品分析 | |
| `06_Dispatch_Business_Logic.md` | 调派业务逻辑总览 | |
| `MOC-调派规模计算模型.md` | 规模计算MOC导航 | 知识枢纽 |
| `MOC-调派规模计算模型对比分析.md` | 模型对比 | |
| **SubScenario_Portraits/** | **子场景画像目录** | 12类场景详细建模 |
| **SubScenario_Portraits/MOC-子场景画像.md** | 子场景画像总导航 | 推荐阅读起点 |
| **SubScenario_Portraits/01_普通住宅火灾画像.md** | 普通住宅场景 | RES-01 |
| **SubScenario_Portraits/02_高层住宅火灾画像.md** | 高层住宅场景 | HIGH-01，垂直蔓延特征 |
| **SubScenario_Portraits/03_地下车库火灾画像.md** | 地下车库场景 | UGRD-01 |
| **SubScenario_Portraits/04_商业综合体火灾画像.md** | 商业综合体场景 | MALL-01 |
| **SubScenario_Portraits/05_工业厂房火灾画像.md** | 工业厂房场景 | FACT-01 |
| **SubScenario_Portraits/06_化工园区火灾画像.md** | 化工园区场景 | CHEM-01，爆炸/毒气/次生灾害 |
| **SubScenario_Portraits/07_锂电池火灾画像.md** | 锂电池场景 | SPEC-01，新兴风险 |
| **SubScenario_Portraits/08_电动车火灾画像.md** | 电动车场景 | SPEC-01 |
| **SubScenario_Portraits/09_人员密集场所火灾画像.md** | 人员密集场所 | HOSP-01/SCHL-01 |
| **SubScenario_Portraits/10_物流冷库火灾画像.md** | 物流冷库场景 | STOR-01 |
| **SubScenario_Portraits/11_洪水救援场景画像模板.md** | 洪水救援场景 | FLOOD-01，特殊救援 |
| **SubScenario_Portraits/洪水救援调派案例_0412.md** | 洪水救援实际案例 | FC-2025-0412-Flood |

**备注**：
- Part 1是整个项目的业务需求基础
- 子场景画像涵盖12类典型消防救援场景
- 规模计算模型是核心业务规则

---

### 02_Scenarios（场景模拟与案例库）

| 文件/目录 | 说明 | 备注 |
|-----------|------|------|
| `01_Typical_Scenario_Examples.md` | 典型场景示例 | 包含11类场景 |
| **Full_Link_Simulations/** | **全链路模拟目录** | 5份端到端模拟 |
| **Full_Link_Simulations/一级火灾场景全链路模拟.md** | 一级火灾全链路 | 最低级别 |
| **Full_Link_Simulations/一级火灾场景全链路模拟2.md** | 一级火灾（第二版） | |
| **Full_Link_Simulations/二级火灾场景全链路模拟.md** | 二级火灾全链路 | |
| **Full_Link_Simulations/城中村火灾场景全链路模拟.md** | 城中村火灾 | VILL-01 |
| **Full_Link_Simulations/高层医院火灾场景全链路模拟.md** | 高层医院火灾 | HIGH-01 + HOSP-01 |

**备注**：全链路模拟覆盖从接警到审计归档的完整12步流程。

---

### 03_SystemDesign（Part 2：系统设计与数据模型）

| 文件/目录 | 说明 | 备注 |
|-----------|------|------|
| `Part2-README.md` | **Part 2总览**，DDD领域分层 | 限界上下文/领域服务/核心实体 |
| `01_Overview_And_Goals.md` | 系统概述与目标 | |
| `01_复杂业务系统设计可视化方法.md` | 系统设计方法论 | |
| `02_Data_Flow_And_State_Machine.md` | 数据流与状态机 | |
| `02_Wiki知识库构建与管理.md` | 知识库构建 | |
| `03_Obsidian插件系统与知识库构建.md` | Obsidian知识库 | |
| `04_AI驱动认知构建系统与标签体系.md` | AI认知系统 | |
| `05_完整Obsidian标签体系.md` | 标签体系 | |
| **MultiAgent_Architecture/** | **多智能体架构目录** | 核心领域服务 |
| **MultiAgent_Architecture/消防多智能体架构.md** | 多智能体架构详解 | 四Agent权重/仲裁机制 |
| **MultiAgent_Architecture/消防多智能体应用.md** | 多智能体应用 | |
| **MultiAgent_Architecture/接处警AI总体流程.md** | AI总体流程 | |
| **MultiAgent_Architecture/消防多智能体系统知识体系.md** | 知识体系 | |
| **MultiAgent_Architecture/对接处警系统审计.md** | 审计对接 | |

**备注**：
- Part 2是系统设计与数据模型的领域层
- MultiAgent架构是核心领域服务，包含四Agent（感知/决策/执行/预测）
- 采用DDD限界上下文设计

---

### 04_DIKW_Examples（DIKW知识转化示例）

| 文件 | 说明 | 备注 |
|------|------|------|
| `01_Ordinary_Fire_DIKW.md` | 普通火灾DIKW模板 | Data→Information→Knowledge→Wisdom |
| `02_Hazmat_Fire_DIKW.md` | 危化品火灾DIKW模板 | |
| `03_Rescue_DIKW.md` | 救援类DIKW模板 | |

**备注**：DIKW（Data-Information-Knowledge-Wisdom）是知识转化框架，每类场景有对应模板。

---

### 05_DataModel（核心数据模型）

| 文件 | 说明 | 备注 |
|------|------|------|
| `01_Core_Entities_And_Domain_Model.md` | **核心实体模型** | 聚合根/实体/值对象 |
| `02_ER_Diagram_And_Relation_Model.md` | ER图与关系模型 | |
| `03_Database_Table_Structure.md` | 数据库表结构 | |
| `04_Leveling_And_Composition_Mechanism.md` | 定级与编成机制 | |
| `05_Event_Portrait_Slot_Definition.md` | 事件画像槽位定义 | |
| `06_Dispatch_Rule_Model.md` | 调派规则模型 | |
| `07_Vehicle_And_Resource_Model.md` | 车辆与资源模型 | |
| `08_Config_Dictionary_And_Enumerations.md` | 配置字典与枚举 | |
| `01_接警问询管理标签系统设计.md` | 接警问询标签 | |
| `02_警情研判模块标签体系.md` | 警情研判标签 | |
| `03_警情处置闭环技术模板.md` | 处置闭环模板 | |
| `04_资源调度模块标签体系.md` | 资源调度标签 | |
| `05_消防接处警标签体系与PKM融合分析.md` | PKM融合分析 | |

**备注**：
- 核心实体包括Incident（警情聚合根）、AlertStructured、IncidentPortrait等
- 采用DDD领域模型设计

---

### 06_DispatchEngine（Part 3：核心指挥调度引擎）★

| 文件/目录 | 说明 | 备注 |
|-----------|------|------|
| `Part3-README.md` | **Part 3总览**，DDD领域服务 | 12步流程领域服务 |
| `01_Alert_Level_Mapping.md` | 警情等级映射规则 | 1-4级 |
| `02_Reverse_Verification_Logic.md` | 反向校验逻辑 | |
| `04_Constraint_Validation_Mechanism.md` | **约束校验机制** | 五维校验、安全底线 |
| `05_Constraint_Validation_Details.md` | 约束校验详情 | |
| `06_Dispatch_Layer_Governance.md` | 调派层治理 | |
| `07_Dispatch_Engine_Implementation.md` | 引擎实现总览 | |
| `08_核心引擎流程v3.1纯文字版.md` | 核心引擎流程 | |
| `09_核心引擎全流程6级详尽目录v6.2.md` | 6级详尽目录 | |
| `MOC-核心调派引擎-详细子模块.md` | 核心引擎MOC导航 | 知识枢纽 |
| **Query_Routing/** | **问题路由目录** | 智能问询领域服务 |
| **Query_Routing/MOC-Query_Routing问题路由专区.md** | 问题路由MOC | 知识枢纽 |
| **Query_Routing/00_非对称问询路由设计.md** | 非对称路由设计 | |
| **Query_Routing/01_标准话术库V1.md** | 标准话术库 | |
| **Query_Routing/问题路由树.md** | 问题路由树V2.0 | 动态优先级 |
| **Query_Routing/问题维度映射体系.md** | 问题维度映射 | |
| **Query_Routing/多维问题与要素识别.md** | 多维问题识别 | |
| **Query_Routing/补充问题类型维度.md** | 补充问题类型 | |
| **Query_Routing/问题路由.md** | 问题路由基础 | |
| **AI_Support/** | **AI多智能体目录** | 领域服务 |
| **AI_Support/01_AILLM应急指挥智能决策支持.md** | LLM应急指挥决策 | |
| **StateMachine/** | **状态机目录** | 领域事件管理 |
| **StateMachine/MOC-StateMachine.md** | 状态机MOC | 知识枢纽 |
| **StateMachine/StateMachine_Overview.md** | 状态机概览 | |
| **StateMachine/StateMachine_12Step_Definition.md** | 12步状态定义 | 核心文档 |
| **StateMachine/StateMachine_Guards_Actions.md** | 守卫与动作 | |
| **StateMachine/StateMachine_Fault_Tolerance.md** | 容错机制 | 4级容错 |
| **StateMachine/StateMachine_Performance_Optimization.md** | 性能优化 | |
| **StateMachine/StateMachine_Monitoring_Dashboard.md** | 监控仪表盘 | |
| **StateMachine/StateMachine_Implementation_XState.md** | XState实现 | |
| **StateMachine/StateMachine_Transition_Log.md** | 状态转换日志 | |
| **StateMachine/价值点提取_StateMachine核心知识点.md** | 价值点提取 | |

**备注**：
- Part 3是整个系统的核心引擎，12步指挥调度流程
- 约束校验（Step 7）是安全底线，主要回退点
- 状态机管理12步流程中的领域事件

---

### 07_Audit_And_Responsibility（Part 4：审计责任）

| 文件 | 说明 | 备注 |
|------|------|------|
| `Part4-README.md` | **Part 4总览**，DDD领域事件 | 责任追溯/审计留痕 |
| `01_Human_Confirmation_And_Responsibility.md` | **人工确认与责任** | 关键责任关口 |
| `02_Audit_Mechanism_And_Report_Template.md` | 审计机制与报告模板 | |
| `03_Audit_Log_And_Responsibility_Model.md` | 审计日志与责任模型 | |
| `04_Audit_Log_Table_Structure.md` | 审计日志表结构 | |
| `07_Human_Responsibility_Confirmation_Simulation.md` | 人工确认模拟 | |
| `08_Dispatcher_Duty_Collection_Dialog.md` | 调度员责任对话 | |
| `10_Dispatch_System_Audit.md` | 调派系统审计 | |
| `11_Dispatch_Responsibility_Mechanism_And_Human_Confirmation_Nodes.md` | 责任机制与人工确认节点 | |

**备注**：
- Part 4是系统的审计与责任保障层
- 人工确认（Step 10）是最终责任边界
- 审计日志不可篡改（SHA256哈希链）

---

### 08_Math_And_Optimization（数学模型与优化）

| 文件 | 说明 | 备注 |
|------|------|------|
| `05_Math_Model_Full_Link.md` | **数学模型全链路** | 核心公式汇总 |
| `06_Optimization_Suggestions_And_Audit_Findings.md` | 优化建议与审计发现 | |
| `09_Dispatch_Plan_Work_Content_And_Plan.md` | 调派工作计划 | |

**备注**：
- 包含N_total警情等级计算公式
- 混合判定公式：`final_score = 0.45 × rule_score + 0.55 × ml_score`
- 约束优化模型

---

### 09_Roadmap（项目路线图）

| 目录 | 说明 | 备注 |
|------|------|------|
| `Roadmap/` | Roadmap子目录 | |
| `TimeAxis/` | 时间轴子目录 | |
| `_README.md` | Roadmap总览 | |

**备注**：项目演进规划与迭代计划。

---

### 10_Appendix（附录）

| 文件 | 说明 | 备注 |
|------|------|------|
| `10_附录/公式汇总.md` | **公式速查** | N_total、混合判定等 |
| `10_附录/index.md` | 附录索引 | |

**备注**：包含所有核心公式的速查汇总。

---

### raw（原始文档与价值点提取）

| 分类 | 文件数 | 说明 |
|------|--------|------|
| **原文_** | 39份 | 原始技术文档，保持完整内容 |
| **价值点提取_** | 34份 | 价值点精华提取，便于快速浏览 |
| **FRICP_** | 12份 | FRICP建设方案相关文档 |
| **MOC模板_** | 8份 | 各Part的MOC模板 |
| **其他** | 若干 | 知识框架、标注体系等 |

**raw/原文_核心文档示例**：
| 文件 | 说明 |
|------|------|
| `原文_12步状态机完整设计.md` | 完整Mermaid状态图、12状态定义 |
| `原文_核心调派引擎12步流程导航.md` | 12步总览表、快速入口 |
| `原文_洪水救援调派案例.md` | FC-2025-0412-Flood完整案例 |
| `原文_多Agent消防社会救助方案.md` | 4-Agent并行架构 |
| `原文_RAG增强接警槽位填充方案.md` | RAG+蒸馏混合路线 |

**raw/价值点提取_核心文档示例**：
| 文件 | 说明 |
|------|------|
| `价值点提取_核心知识点汇总.md` | Multi-Agent、仲裁机制、12步数据流 |
| `价值点提取_StateMachine核心知识点.md` | 12步状态定义、容错4级 |
| `价值点提取_约束校验机制.md` | 五维校验、校验分流 |
| `价值点提取_洪水救援场景案例.md` | 洪水救援完整流程 |
| `价值点提取_审计责任体系.md` | 不可篡改审计、责任链条 |

**备注**：
- raw目录是整个项目的知识精华库
- 原文保持完整技术细节
- 价值点提取便于快速了解核心内容

---

## 三、Part间逻辑关联

```
Part 1（业务需求）
    ↓ 为Part 2提供业务规则和场景基础
Part 2（系统设计与数据模型）
    ↓ 为Part 3提供领域模型和技术实现
Part 3（核心指挥调度引擎）
    ↓ 输出可执行方案
Part 4（审计责任）
    ↓ 输入Part 3决策事件
    ↓ 输出审计记录+模型训练数据（持续优化）
```

---

## 四、核心MOC（知识枢纽）导航

| MOC | 位置 | 说明 |
|-----|------|------|
| `00_消防调派智能系统全局视图.md` | 00_GlobalNavigation/ | **全局总入口** |
| `MOC-子场景画像.md` | 01_Requirements/SubScenario_Portraits/ | Part 1场景入口 |
| `MOC-调派规模计算模型.md` | 01_Requirements/ | 规模计算入口 |
| `MOC-核心调派引擎-详细子模块.md` | 06_DispatchEngine/ | Part 3核心入口 |
| `MOC-StateMachine.md` | 06_DispatchEngine/StateMachine/ | 状态机入口 |
| `MOC-Query_Routing问题路由专区.md` | 06_DispatchEngine/Query_Routing/ | 智能问询入口 |

---

## 五、12步核心流程总览

```
Step 1: 警情接收与初步解析     → ASR + NER
Step 2: Query_Routing智能问询  → 路由树 + 话术库（回退点）
Step 3: 多维画像构建           → 4维画像（回退点）
Step 4: 警情等级判定          → N_total公式
Step 5: 调派规模计算          → 三档方案（回退点）
Step 6: 队站车辆匹配          → GIS + 多目标优化（回退点）
Step 7: 约束校验机制          → 五维校验【主要回退点】
Step 8: 反向模拟与冲突解决    → 时间线推演（回退点）
Step 9: AI多智能体决策        → 4-Agent + 仲裁
Step 10: 人工二次确认         → 责任关口
Step 11: 方案生成与下达       → dispatch_package
Step 12: 审计留痕            → audit_trace（不可篡改）
```

---

## 六、快速导航建议

| 角色 | 推荐入口 | 重点文档 |
|------|---------|----------|
| **新成员** | 00_全局视图 → Part1-README → MOC-子场景画像 | 建立整体认知 |
| **业务分析** | Part1子场景画像 → 规模计算模型 → 全链路模拟 | 理解业务需求 |
| **架构师** | Part2 Part2-README → MultiAgent → 领域模型 | 系统架构设计 |
| **开发人员** | Part3 核心引擎 → 状态机 → 约束校验 → Query_Routing | 技术实现依据 |
| **审计人员** | Part4 审计责任 → 数学模型 → 责任机制 | 合规与追溯 |

---

**文件结束**
