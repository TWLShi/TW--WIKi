---
title: README
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# Part 3：核心指挥调度引擎 ★

**所属Part**：Part 3
**物理目录**：`06_DispatchEngine`
**定位**：消防调派引擎的核心领域服务层

---

## 1. Part概述

**本Part是消防接处警指挥调度领域的核心领域服务层**，以**12步指挥调度流程**为核心，构建从接警到方案下达的完整智能决策闭环。

---

## 2. 核心内容

- 12步完整指挥调度流程
- Query_Routing智能问询
- AI多智能体协同决策（4-Agent + 仲裁）
- 状态机实现、约束校验、反向模拟

---

## 3. 目录结构

```
Part3_DispatchEngine/
└── 06_DispatchEngine/         # 核心引擎
    ├── AI_Support/             # AI支持
    ├── Query_Routing/          # 智能问询路由
    ├── StateMachine/            # 状态机
    └── 12步流程文件...
```

---

## 4. 12步全链路引擎

```mermaid
flowchart LR
    S1[Step1警情接收] --> S2[Step2智能问询]
    S2 --> S3[Step3画像构建]
    S3 --> S4[Step4等级判定]
    S4 --> S5[Step5规模计算]
    S5 --> S6[Step6车辆匹配]
    S6 --> S7[Step7约束校验]
    S7 --> S8[Step8反向模拟]
    S8 --> S9[Step9AI多智能体]
    S9 --> S10[Step10人工确认]
    S10 --> S11[Step11方案下达]
    S11 --> S12[Step12审计归档]
```

---

## 5. 与其他Part的关联

- **输入**：Part 1业务场景 + Part 2领域模型
- **输出**：可执行的指挥调度方案（供Part 4审计）

---

**相关链接**
[[Part 2 ← 系统设计与数据模型]] | [[Part 4 → 审计责任与数学模型]]
