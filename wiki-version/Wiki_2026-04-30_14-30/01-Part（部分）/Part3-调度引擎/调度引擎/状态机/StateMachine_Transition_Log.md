---
title: StateMachine_Transition_Log
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# StateMachine_Transition_Log - 状态转换日志

**所属目录**：`06_DispatchEngine/StateMachine/`
**更新日期**：2025-04-25
**版本**：V1.0

---

## 1. 日志格式设计

### 1.1 转换日志结构
```json
{
  "log_id": "LOG-20250425-001",
  "incident_id": "INC-20250425-001",
  "transition_id": "TR-001",
  "from_state": "ALERT_RECEIVED",
  "to_state": "QUERY_ROUTING",
  "event": "PARSE_COMPLETE",
  "trigger_time": "2025-04-25T10:23:45.123Z",
  "duration_ms": 7650,
  "actions_executed": ["createIncident", "assignStructuredAlert"],
  "context_snapshot": {
    "structuredAlert": {...}
  },
  "user_id": null,
  "session_id": "SESSION-001"
}
```

---

## 2. 日志类型

### 2.1 转换日志 (TransitionLog)
| 字段 | 类型 | 说明 |
|------|------|------|
| log_id | string | 全局唯一标识 |
| incident_id | string | 关联警情ID |
| from_state | string | 源状态 |
| to_state | string | 目标状态 |
| event | string | 触发事件 |
| trigger_time | timestamp | 触发时间 |
| duration_ms | int | 状态持续时长 |
| actions | array | 执行的动作 |

### 2.2 审计日志 (AuditLog)
| 字段 | 类型 | 说明 |
|------|------|------|
| audit_id | string | 全局唯一标识 |
| incident_id | string | 关联警情ID |
| action | string | 操作类型 |
| operator | string | 操作人 |
| old_value | json | 旧值 |
| new_value | json | 新值 |
| reason | string | 变更原因 |
| timestamp | timestamp | 操作时间 |

---

## 3. 日志示例

### 3.1 正常流程
```json
{
  "log_id": "LOG-20250425-001",
  "incident_id": "INC-20250425-001",
  "transition": {
    "from": "ALERT_RECEIVED",
    "to": "QUERY_ROUTING",
    "event": "PARSE_COMPLETE"
  },
  "timing": {
    "trigger": "2025-04-25T10:23:45.123Z",
    "duration_ms": 7650
  }
}
```

### 3.2 回退流程
```json
{
  "log_id": "LOG-20250425-003",
  "incident_id": "INC-20250425-001",
  "transition": {
    "from": "CONSTRAINT_VALIDATION",
    "to": "SCALE_CALCULATION",
    "event": "VALIDATION_FAIL",
    "rollback": true
  },
  "fail_reason": {
    "code": "RESOURCE_UNAVAILABLE",
    "message": "举高车全部被占用",
    "suggestion": "降低举高车数量或跨区调派"
  }
}
```

### 3.3 人工介入
```json
{
  "log_id": "LOG-20250425-005",
  "incident_id": "INC-20250425-001",
  "transition": {
    "from": "HUMAN_CONFIRMATION",
    "to": "DISPATCH_ISSUING",
    "event": "MODIFIED",
    "human_intervention": true
  },
  "modifications": {
    "field": "vehicle_count",
    "old_value": 8,
    "new_value": 6,
    "reason": "实际可用车辆不足"
  },
  "operator": "调度员-001"
}
```

---

## 4. 日志查询

### 4.1 按警情查询
```sql
SELECT * FROM transition_logs
WHERE incident_id = 'INC-20250425-001'
ORDER BY trigger_time ASC;
```

### 4.2 按状态统计
```sql
SELECT
  to_state,
  COUNT(*) as count,
  AVG(duration_ms) as avg_duration
FROM transition_logs
WHERE trigger_time > NOW() - INTERVAL '1 hour'
GROUP BY to_state;
```

### 4.3 异常转换查询
```sql
SELECT * FROM transition_logs
WHERE event IN ('TIMEOUT', 'VALIDATION_FAIL', 'REJECTED')
AND trigger_time > NOW() - INTERVAL '24 hours';
```

---

## 5. 日志存储策略

### 5.1 分层存储
| 存储层 | 介质 | 保留时间 | 用途 |
|--------|------|----------|------|
| 热数据 | SSD | 7天 | 实时查询 |
| 温数据 | HDD | 90天 | 分析报表 |
| 冷数据 | 对象存储 | 3年 | 合规存档 |

### 5.2 归档策略
```
每日凌晨2点：归档前一天日志到温存储
每月1号：归档上月日志到冷存储
保留策略：热7天 + 温90天 + 冷3年
```

---

**标签**：#状态转换日志 #审计日志 #日志格式