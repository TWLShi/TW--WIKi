# MOC - 核心调派引擎 ★（详细子模块版）

**所属Part**：Part 3
**物理目录**：`06_DispatchEngine/`
**更新日期**：2025-04-25
**文档数量**：31份（含子模块）

---

## 1. 引擎概述

**核心定位**：
消防调派智能系统的**大脑与执行中枢**，负责从119接警到最终方案下达的**完整12步智能决策闭环**。

**设计原则**：
- 安全第一（多重约束 + 人工最终确认）
- 可解释性（规则 + ML SHAP + Agent仲裁）
- 可审计性（全程不可篡改日志）
- 持续学习（人工反馈驱动模型迭代）

---

## 2. 12步核心流程总览

```mermaid
flowchart LR
    Start((119接警)) --> S1[1.接收解析] --> S2[2.智能问询] --> S3[3.画像构建]
    S3 --> S4[4.等级判定] --> S5[5.规模计算] --> S6[6.车辆匹配]
    S6 --> S7[7.约束校验] --> S8[8.反向模拟] --> S9[9.AI多智能体]
    S9 --> S10[10.人工确认] --> S11[11.方案下达] --> S12[12.审计归档]

    classDef core fill:#f59e0b,stroke:#b45309,color:#000,stroke-width:3px
    class S5,S6,S7,S8,S9,S10 core
```

**主要回退点**（保障安全）：
- 第7步约束校验失败 → 回退第5/6步
- 第8步模拟冲突 → 回退第5/6步
- 第10步重大修改 → 重新校验第7步

---

## 3. 子模块详细导航

### **3.1 引擎基础机制**
- [[07_Dispatch_Engine_Implementation.md]] —— 引擎整体实现总览
- [[01_Alert_Level_Mapping.md]] —— 警情等级映射
- [[02_Reverse_Verification_Logic.md]] —— 反向校验逻辑
- [[04_Constraint_Validation_Mechanism.md]] —— **约束校验机制**（核心风控）
- [[06_Dispatch_Layer_Governance.md]] —— 调派层治理

### **3.2 Query_Routing 问题路由专区**
- [[Query_Routing/MOC-Query_Routing问题路由专区.md]] —— **路由专区导航**
- [[Query_Routing/00_非对称问询路由设计.md]] —— 非对称路由设计 V2.0
- [[Query_Routing/问题路由树.md]] —— 问题路由决策树
- [[Query_Routing/01_标准话术库V1.md]] —— 标准话术库

### **3.3 AI多智能体决策支持**（最重要模块）
- [[AI_Support/01_AILLM应急指挥智能决策支持.md]] —— LLM应急指挥决策
- [[AI_Support/消防多智能体架构.md]] —— 多智能体整体架构
- [[AI_Support/消防多智能体应用.md]] —— 多智能体实际应用
- [[AI_Support/接处警AI总体流程.md]] —— 接处警AI总体流程

### **3.4 状态机模块**（核心支撑）
- [[StateMachine/MOC-StateMachine.md]] —— **状态机模块导航**
- [[StateMachine/StateMachine_12Step_Definition.md]] —— 12步状态定义
- [[StateMachine/StateMachine_Fault_Tolerance.md]] —— 容错机制
- [[StateMachine/StateMachine_Performance_Optimization.md]] —— 性能优化
- [[StateMachine/StateMachine_Monitoring_Dashboard.md]] —— 监控仪表盘

---

## 4. 核心价值点

- **12步完整闭环**：从接警到审计的全流程智能决策
- **混合智能架构**：规则 + ML + 多智能体 + 人工确认
- **强约束与容错**：多重校验 + 状态机容错机制
- **可解释与可审计**：每一步都有解释 + 不可篡改日志
- **持续学习**：人工确认结果反馈到模型训练

---

## 5. 阅读路径推荐

**新成员**：
1. 本MOC → [[Query_Routing/MOC-Query_Routing问题路由专区.md]]
2. [[StateMachine/MOC-StateMachine.md]]
3. [[AI_Support/01_AILLM应急指挥智能决策支持.md]]

**开发人员**：
- 重点阅读 `07_Dispatch_Engine_Implementation.md` + 状态机 + 多智能体

**调度/业务人员**：
- 重点阅读 Step 9（AI决策）和 Step 10（人工确认）

---

## 标签索引

#核心引擎 #12步流程 #MultiAgent #状态机 #约束校验 #Query_Routing #AI决策

---

## 价值点提取（知识精华汇总）

| 文档 | 说明 | 位置 |
|------|------|------|
| [[价值点提取_核心知识点汇总.md]] | Multi-Agent架构、仲裁机制、故障处理、约束校验、12步数据流 | **raw/** |
| [[价值点提取_StateMachine核心知识点.md]] | 12步状态定义、容错4级，性能KPI | raw/ |
| [[价值点提取_12步状态机必要性分析.md]] | 状态转换图，回退路径、技术选型 | raw/ |
| [[价值点提取_性能优化策略.md]] | 分层优化、瓶颈分析、实施计划 | raw/ |
| [[价值点提取_监控仪表盘实时设计.md]] | 实时管道图、告警中心、历史记录 | raw/ |
| [[价值点提取_高级状态机实现细节.md]] | XState实现、Guards/Actions、Context | raw/ |
| [[价值点提取_性能监控仪表盘设计.md]] | 仪表盘布局、KPI阈值、技术栈 | raw/ |
| [[价值点提取_约束校验机制.md]] | 五维校验、校验分流、API接口 | raw/ |
| [[价值点提取_Step7约束校验机制.md]] | 约束校验完整流程、五维校验、自动修复 | raw/ |
| [[价值点提取_MultiAgent多智能体架构.md]] | 四Agent权重、仲裁机制、动态权重矩阵 | raw/ |
| [[价值点提取_多智能体仲裁机制.md]] | 5阶段仲裁、权重矩阵、LLM仲裁 | raw/ |
| [[价值点提取_多智能体故障处理机制.md]] | 4级容错、Fallback策略、故障恢复 | raw/ |
| [[价值点提取_Step6队站车辆匹配.md]] | GIS匹配、多目标优化、车辆分配 | raw/ |
| [[价值点提取_Step8反向模拟冲突解决.md]] | 时间线推演、冲突检测、自动调整 | raw/ |
| [[价值点提取_12步Prompt体系.md]] | 12步Prompt模板，温度控制、Few-shot建议 | raw/ |
| [[价值点提取_ML混合判定机制.md]] | 混合融合公式、SHAP可解释性、异常处理 | raw/ |

---

## 相关链接

- [[Part3-README.md]]（Part 3 入口）
- [[05_MOCs/MOC-FireDispatchEngine.md]]（全局总枢纽）
- [[StateMachine/MOC-StateMachine.md]]（状态机专区）
- [[Query_Routing/MOC-Query_Routing问题路由专区.md]]（问询专区）

---

**文件结束**
此MOC为Part 3核心引擎的**知识导航中心**，建议作为日常工作入口。
