# StateMachine_Overview - 状态机整体架构

**所属目录**：`06_DispatchEngine/StateMachine/`
**更新日期**：2025-04-25
**版本**：V1.0

---

## 1. 状态机设计目标

| 目标 | 说明 |
|------|------|
| **确定性** | 相同输入始终产生相同状态转换 |
| **可观测性** | 每步转换完整记录 + 实时监控 |
| **可恢复性** | 故障自动重试 + 多级降级策略 |
| **可追溯性** | 不可篡改日志 + 责任到人 |

---

## 2. 状态机架构

```mermaid
flowchart TB
    subgraph States["状态层"]
        S1[ALERT_RECEIVED<br/>警情接收]
        S2[QUERY_ROUTING<br/>智能问询]
        S3[PORTRAIT_BUILDING<br/>画像构建]
        S4[LEVEL_DETERMINATION<br/>等级判定]
        S5[SCALE_CALCULATION<br/>规模计算]
        S6[VEHICLE_MATCHING<br/>车辆匹配]
        S7[CONSTRAINT_VALIDATION<br/>约束校验]
        S8[REVERSE_SIMULATION<br/>反向模拟]
        S9[MULTI_AGENT<br/>AI多智能体]
        S10[HUMAN_CONFIRMATION<br/>人工确认]
        S11[DISPATCH_ISSUING<br/>方案下达]
        S12[AUDIT_ARCHIVING<br/>审计归档]
    end

    subgraph Transitions["转换规则"]
        T1[Step1 → Step2]
        T2[Step2 → Step3]
        T3[Step3 → Step4]
        T4[Step4 → Step5]
        T5[Step5 → Step6]
        T6[Step6 → Step7]
        T7[Step7 → Step8/Pass]
        T8[Step7 → Step5/Fail]
        T9[Step8 → Step9]
        T10[Step9 → Step10]
        T11[Step10 → Step11/确认]
        T12[Step10 → 终止]
        T13[Step11 → Step12]
    end

    S1 --> T1 --> S2
    S2 --> T2 --> S3
    S3 --> T3 --> S4
    S4 --> T4 --> S5
    S5 --> T5 --> S6
    S6 --> T6 --> S7
    S7 --> T7 --> S8
    S7 -.-> T8 -.-> S5
    S8 --> T9 --> S9
    S9 --> T10 --> S10
    S10 --> T11 --> S11
    S10 -.-> T12 -.-> [*]
    S11 --> T13 --> S12
    S12 --> [*]
```

---

## 3. 状态定义表

| 状态名 | 编码 | 入口动作 | 出口动作 | 超时处理 |
|--------|------|----------|----------|----------|
| ALERT_RECEIVED | ST_01 | 创建incident_id | NER解析 | 30s降级人工 |
| QUERY_ROUTING | ST_02 | 初始化话术 | 画像补全 | 60s强制下一步 |
| PORTRAIT_BUILDING | ST_03 | 特征提取 | 向量生成 | 15s使用默认值 |
| LEVEL_DETERMINATION | ST_04 | 规则引擎 | 等级输出 | 10s ML降级规则 |
| SCALE_CALCULATION | ST_05 | 查询编成表 | 三档方案 | 20s最小档输出 |
| VEHICLE_MATCHING | ST_06 | GIS计算 | 匹配结果 | 30s本地最优 |
| CONSTRAINT_VALIDATION | ST_07 | 五维校验 | Pass/Warning/Fail | Fail直接回退 |
| REVERSE_SIMULATION | ST_08 | 时间线推演 | 冲突检测 | 25s使用推荐档 |
| MULTI_AGENT | ST_09 | 四Agent并行 | 仲裁结果 | 60s加权投票 |
| HUMAN_CONFIRMATION | ST_10 | 方案展示 | 人工决策 | 300s自动通过 |
| DISPATCH_ISSUING | ST_11 | 指令生成 | 多端推送 | 15s重试3次 |
| AUDIT_ARCHIVING | ST_12 | 日志锁定 | 哈希链更新 | 10s同步写入 |

---

## 4. 设计原则

### 4.1 核心原则
```
1. 单一入口：每个状态只有明确的进入条件
2. 明确出口：每个状态转换都有清晰的出口动作
3. 有限状态：状态数量有限，转换可枚举
4. 确定性：相同上下文永远转换到相同状态
```

### 4.2 安全原则
```
1. 任何故障都倾向于保守方案
2. 人工介入优先级高于自动决策
3. 不可逆操作需要二次确认
4. 关键状态转换必须留痕
```

---

## 5. 技术实现

### 5.1 推荐框架
| 框架 | 适用场景 | 优缺点 |
|------|----------|--------|
| **XState** | 复杂状态机 | 功能强大，可视化好 |
| **Airflow** | 批处理流程 | 成熟稳定，监控完善 |
| **Temporal** | 分布式工作流 | 容错强，持久化好 |

### 5.2 状态存储
```
当前状态 → Redis（实时）
转换历史 → PostgreSQL（持久）
审计日志 → 不可篡改存储
```

---

## 相关链接

- [[MOC-StateMachine.md]] —— 状态机MOC
- [[StateMachine_12Step_Definition.md]] —— 12步状态定义
- [[StateMachine_Fault_Tolerance.md]] —— 容错机制

---

**标签**：#状态机架构 #设计原则 #XState