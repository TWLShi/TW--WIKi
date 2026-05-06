---
title: DispatchJSON_Template
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# DispatchJSON_Template（调派句 JSON 模板）

**最后更新**：2026-04-24
**标签**：#模板 #调派句 #JSON #消防调派

---

## 模板说明

标准调派句 JSON 结构，用于 Agent 生成调派指令。

---

## 标准结构

```json
{
  "alarm_id": "{{alarm_id}}",
  "timestamp": "{{timestamp}}",
  "scene_type": "{{scene_type}}",
  "severity_level": {{severity_level}},

  "event_profile": {
    "disaster_type": "{{disaster_type}}",
    "location": "{{location}}",
    "trapped_count": {{trapped_count}},
    "fire_intensity": "{{fire_intensity}}",
    "development_trend": "{{development_trend}}"
  },

  "dispatch_plan": {
    "N_total": {{N_total}},
    "recommended_fleet": [
      {
        "vehicle_type": "{{vehicle_type}}",
        "count": {{count}},
        "purpose": "{{purpose}}"
      }
    ],
    "dispatch_sequence": "{{dispatch_sequence}}",
    "response_time_target": "{{response_time_target}}分钟"
  },

  "constraint_validation": {
    "personnel_check": "{{PASS/FAIL}}",
    "road_check": "{{PASS/FAIL}}",
    "air_defense_check": "{{PASS/FAIL}}"
  },

  "human_confirmation_required": {{boolean}},

  "audit_hash": "{{hash}}"
}
```

---

## 字段说明

| 字段 | 类型 | 说明 | 必填 |
|------|------|------|------|
| alarm_id | String | 警情ID | 是 |
| timestamp | String | 时间戳 | 是 |
| scene_type | String | 场景类型 | 是 |
| severity_level | Integer | 严重等级 1-5 | 是 |
| event_profile | Object | 事件画像 | 是 |
| dispatch_plan | Object | 调派方案 | 是 |
| constraint_validation | Object | 约束校验结果 | 是 |
| human_confirmation_required | Boolean | 是否需要人工确认 | 是 |
| audit_hash | String | 审计哈希 | 是 |

---

## 使用说明

1. 填充 event_profile 字段
2. 调用调派引擎计算 N_total
3. 生成 dispatch_plan
4. 进行约束校验
5. 如需人工确认，标记并等待
6. 生成 audit_hash 存入审计日志

---

## 相关链接

- [[调派规模计算模型]]
- [[警情定级映射规则]]
- [[约束校验实现细节]]
