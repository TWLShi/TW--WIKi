---
title: StateMachine_Guards_Actions
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# StateMachine_Guards_Actions - 守卫与动作

**所属目录**：`06_DispatchEngine/StateMachine/`
**更新日期**：2025-04-25
**版本**：V1.0

---

## 1. Guards（守卫）定义

守卫是决定是否允许状态转换的条件表达式。

### 1.1 全局守卫

| 守卫名 | 条件表达式 | 说明 |
|--------|------------|------|
| `hasValidInput` | `input != null && input.isValid()` | 输入有效性 |
| `hasEnoughInfo` | `portrait.completeness >= 0.85` | 信息完整度 |
| `isNotTimeout` | `elapsedTime < maxAllowedTime` | 未超时 |
| `isHumanApproved` | `humanConfirmation == true` | 人工已确认 |
| `isLowRisk` | `riskScore < 0.3` | 低风险 |

### 1.2 各步守卫

#### Step 7 (CONSTRAINT_VALIDATION) 守卫
```
guard_ST07_Pass = validation_report.status == "PASS"
guard_ST07_Warning = validation_report.status == "WARNING"
guard_ST07_Fail = validation_report.status == "FAIL"
guard_ST07_Retry = failedChecks.size <= 2 && canAutoRepair
```

#### Step 10 (HUMAN_CONFIRMATION) 守卫
```
guard_ST10_Approved = confirmed == true
guard_ST10_Modified = modified == true && modifications.acceptable
guard_ST10_Rejected = rejected == true
guard_ST10_Timeout = elapsedTime > 300 && autoProceed == true
```

---

## 2. Actions（动作）定义

动作是在状态进入或退出时执行的副作用。

### 2.1 入口动作 (entry/)

| 动作名 | 执行内容 | 异步 |
|--------|----------|------|
| `entry_ST01` | 创建incident_id，初始化日志 | 否 |
| `entry_ST02` | 初始化路由树，加载话术库 | 否 |
| `entry_ST03` | 启动特征提取管道 | 是 |
| `entry_ST04` | 触发规则引擎 + ML模型 | 是 |
| `entry_ST05` | 查询编成表，启动系数计算 | 是 |
| `entry_ST06` | 调用GIS服务，计算ETA | 是 |
| `entry_ST07` | 启动五维校验引擎 | 是 |
| `entry_ST08` | 启动时间线模拟器 | 是 |
| `entry_ST09` | 并行调用4个Agent | 是 |
| `entry_ST10` | 生成确认方案，推送显示 | 否 |
| `entry_ST11` | 生成指挥单，触发多端推送 | 是 |
| `entry_ST12` | 锁定日志，写入哈希链 | 是 |

### 2.2 出口动作 (exit/)

| 动作名 | 执行内容 | 异步 |
|--------|----------|------|
| `exit_ST01` | 冻结解析结果，关闭输入 | 否 |
| `exit_ST02` | 冻结画像，关闭问询 | 否 |
| `exit_ST03` | 冻结4维向量，关闭构建 | 否 |
| `exit_ST04` | 冻结等级结果，关闭判定 | 否 |
| `exit_ST05` | 冻结规模方案，关闭计算 | 否 |
| `exit_ST06` | 冻结匹配结果，关闭GIS | 否 |
| `exit_ST07` | 冻结校验报告，关闭校验 | 否 |
| `exit_ST08` | 冻结模拟结果，关闭推演 | 否 |
| `exit_ST09` | 冻结仲裁结果，关闭Agent | 否 |
| `exit_ST10` | 冻结最终方案，关闭确认 | 否 |
| `exit_ST11` | 冻结下发状态，关闭推送 | 否 |
| `exit_ST12` | 关闭归档，流程结束 | 否 |

---

## 3. 转换动作 (transition/)

| 转换 | 动作 | 说明 |
|------|------|------|
| ST_01 → ST_02 | `trans_01_02` | 传递structured_alert |
| ST_02 → ST_03 | `trans_02_03` | 传递补全画像 |
| ST_03 → ST_04 | `trans_03_04` | 传递incident_portrait |
| ST_04 → ST_05 | `trans_04_05` | 传递alert_level |
| ST_05 → ST_06 | `trans_05_06` | 传递scale_result |
| ST_06 → ST_07 | `trans_06_07` | 传递matching_result |
| ST_07 → ST_08 | `trans_07_08` | 传递Pass/Warning |
| ST_07 → ST_05 | `trans_07_05` | 触发回退，记录Fail原因 |
| ST_08 → ST_09 | `trans_08_09` | 传递simulation_result |
| ST_09 → ST_10 | `trans_09_10` | 传递command_plan |
| ST_10 → ST_11 | `trans_10_11` | 传递final_approved_plan |
| ST_10 → END | `trans_10_end` | 记录终止原因 |
| ST_11 → ST_12 | `trans_11_12` | 传递dispatch_package |
| ST_12 → END | `trans_12_end` | 完成归档 |

---

## 4. 守卫与动作组合示例

### XState语法示例
```javascript
const dispatchMachine = {
  id: 'dispatch',
  initial: 'ALERT_RECEIVED',
  states: {
    ALERT_RECEIVED: {
      entry: 'entry_ST01',
      exit: 'exit_ST01',
      on: {
        PARSE_COMPLETE: {
          target: 'QUERY_ROUTING',
          cond: 'hasValidInput',
          actions: 'trans_01_02'
        }
      }
    },
    QUERY_ROUTING: {
      entry: 'entry_ST02',
      exit: 'exit_ST02',
      on: {
        PORTRAIT_COMPLETE: {
          target: 'PORTRAIT_BUILDING',
          cond: 'hasEnoughInfo',
          actions: 'trans_02_03'
        },
        TIMEOUT: {
          target: 'PORTRAIT_BUILDING',
          actions: 'forceContinue'
        }
      }
    },
    // ... 其他状态
  }
}
```

---

**标签**：#Guards #Actions #XState #状态转换