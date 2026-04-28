# MOC - Part 3：核心调派引擎 ★（详细子模块版）

**所属Part**：Part 3（系统核心）
**物理目录**：`06_DispatchEngine`
**更新日期**：2025-04-24
**文档数量**：18份

---

## 引擎总体架构

**核心定位**：从警情输入到最终方案输出的**完整智能决策引擎**
**设计原则**：规则兜底 + ML增强 + 多智能体协同 + 人工最终确认

---

## 子模块详细导航

### **1. 引擎基础机制**
- [[01_Alert_Level_Mapping.md]] —— 警情等级映射规则
- [[02_Reverse_Verification_Logic.md]] —— 反向校验逻辑
- [[03_Constraint_Validation_Mechanism.md]] —— **约束校验机制**（核心风控）
- [[04_Dispatch_Layer_Governance.md]] —— 调派层治理
- [[05_Dispatch_Engine_Implementation.md]] —— 引擎整体实现

### **2. Query_Routing 问题路由专区**（智能问询核心）
- [[Query_Routing/00_非对称问询路由设计.md]] —— 非对称路由设计（V2.0）
- [[Query_Routing/01_标准话术库V1.md]] —— 标准话术库
- [[Query_Routing/问题路由树.md]] —— 问题路由树（决策树）
- [[Query_Routing/问题维度映射体系.md]] —— 多维问题维度映射
- [[Query_Routing/多维问题与要素识别.md]] —— 多维要素识别
- [[Query_Routing/补充问题类型维度.md]] —— 补充问题类型

### **3. AI_Support 多智能体决策支持**（最重要模块）
- [[AI_Support/01_AILLM应急指挥智能决策支持.md]] —— LLM应急指挥决策
- [[MultiAgent_Architecture/消防多智能体架构.md]] —— 多智能体整体架构
- [[MultiAgent_Architecture/消防多智能体应用.md]] —— 多智能体实际应用
- [[MultiAgent_Architecture/接处警AI总体流程.md]] —— 接处警AI总体流程

### **4. 其他支撑模块**
- 调派引擎实现相关配置与治理文档
- 异常处理与故障容错机制（待补充）

---

## 引擎核心数据流（简图）

```mermaid
flowchart LR
    A[警情输入] --> B[Query_Routing]
    B --> C[多维画像]
    C --> D[等级判定]
    D --> E[规模计算]
    E --> F[车辆匹配]
    F --> G[约束校验]
    G --> H[反向模拟]
    H --> I[AI多智能体]
    I --> J[人工确认]
    J --> K[方案下达]
```

---

## 重要阅读路径推荐

**新成员路径**：
1. `05_Dispatch_Engine_Implementation.md`（总览）
2. `03_Constraint_Validation_Mechanism.md`（安全底线）
3. `AI_Support/` 目录（多智能体核心）
4. `Query_Routing/` 目录（问询能力）

**开发人员路径**：
- 重点阅读 `05_Dispatch_Engine_Implementation.md` + `AI_Support/` + 约束校验

**运维/审计路径**：
- 重点阅读治理文档 + 异常处理机制

---

## 标签索引

#核心引擎 #Query_Routing #MultiAgent #约束校验 #AI决策 #故障容错

---

## 相关链接

- [[Part 2 ← 系统设计与数据模型]]
- [[Part 4 → 审计责任与数学模型]]
- [[02_Part逻辑映射索引]]
- [[MOC-核心调派引擎]]（简版）

---

**文件结束**
此MOC为Part 3的**详细子模块导航**，建议定期更新。