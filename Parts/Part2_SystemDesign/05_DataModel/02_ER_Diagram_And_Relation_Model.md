# 02_ER图与关系模型

**最后更新**：2026-04-23

## 1. 实体关系图（Mermaid）

```mermaid
erDiagram
    ALARM_EVENT ||--o{ EVENT_PORTRAIT : "包含"
    ALARM_EVENT ||--o{ DISPATCH_PLAN : "生成"
    ALARM_EVENT }|--|| ALARM_LEVEL : "映射"
    DISPATCH_RULE ||--|{ DISPATCH_RULE_DETAIL : "包含"
    DISPATCH_RULE_DETAIL }|--|| VEHICLE_TYPE : "指定"
    DISPATCH_PLAN }|--|| DISPATCH_RULE : "依据"
    FIRE_STATION_VEHICLE ||--o{ DISPATCH_PLAN : "分配"
    AUDIT_LOG }|--|| ALARM_EVENT : "记录"
```

## 2. 关键关系说明
- AlarmEvent 1:N DispatchPlan
- DispatchRule 1:N DispatchRuleDetail
- DispatchRuleDetail N:1 VehicleType

**相关链接**：[[03_数据库表结构]]