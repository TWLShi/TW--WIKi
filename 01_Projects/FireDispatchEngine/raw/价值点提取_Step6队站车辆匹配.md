# Step6队站车辆精准匹配 - 价值点提取

**标签**：#Step6 #队站匹配 #GIS #多目标优化 #车辆匹配
**提取日期**：2025-04-25
**来源**：核心引擎v6.1-Step6队站车辆精准匹配完整版.txt
**版本**：V1.0

---

## 1. 匹配目标

**目标耗时**：10-25秒

---

## 2. 输入聚合

| 输入源 | 内容 |
|--------|------|
| 第5步三档规模方案 | 推荐/最小/最大 |
| 第3步画像 | 建筑类型、特殊场景 |
| 实时资源 | 全区车辆与中队状态 |

---

## 3. 匹配流程

```
GIS空间匹配 → 车辆精准匹配 → 多目标优化 → 方案生成排序
```

### 6.2 GIS空间匹配
- 计算所有中队到事发地的实时距离 + ETA
- 考虑路况、拥堵
- 筛选候选中队（ETA ≤ 10分钟优先）

### 6.3 车辆精准匹配
| 匹配维度 | 说明 |
|----------|------|
| 类型需求 | 水罐、泡沫、举高、特勤等 |
| 车辆状态 | 空闲、在勤、维修、保养、出警中 |
| 装备匹配度 | 是否携带必要器材 |

### 6.4 多目标优化
| 优化目标 | 说明 |
|----------|------|
| 距离最优 | ETA最小 |
| 负载均衡 | 单中队出车率≤70% |
| 专业匹配 | 装备与场景匹配 |

---

## 4. 异常处理

| 异常场景 | 处理逻辑 | 优先级 |
|----------|----------|--------|
| 附近无足够可用车辆 | 扩大搜索半径+触发跨区联动 | 最高 |
| ETA计算异常 | 使用历史平均速度替代 | 高 |
| 关键装备缺失 | 推荐最近替代中队 | 高 |
| 优化算法超时 | 回退到距离最优贪心算法 | 中 |
| 单中队负载超限 | 强制分散到多个中队 | 高 |
| GIS服务不可用 | 备用坐标+手动距离表 | 高 |

---

## 5. 数据库表结构

### station_vehicle_matching
```sql
CREATE TABLE station_vehicle_matching (
    incident_id      VARCHAR(32) PRIMARY KEY,
    primary_plan     JSONB,           -- 首选方案
    alternative_plans JSONB[],         -- 备选方案
    total_eta_minutes INTEGER,
    matching_score   NUMERIC(5,3),
    load_impact      JSONB,            -- 各中队负载变化
    explanation      TEXT,
    need_human_review BOOLEAN DEFAULT FALSE
);
```

### vehicle_assignment
```sql
CREATE TABLE vehicle_assignment (
    assignment_id  BIGSERIAL PRIMARY KEY,
    incident_id  VARCHAR(32),
    station_id   VARCHAR(20),
    vehicle_id   VARCHAR(30),
    vehicle_type VARCHAR(30),
    eta_minutes  INTEGER,
    match_score  NUMERIC(5,3),
    priority    INTEGER
);
```

---

## 6. API接口

### POST /api/v1/alerts/{incident_id}/matching/plan

```json
请求：
{
  "use_ml_optimizer": true,
  "max_eta_limit": 12,
  "allow_cross_district": true,
  "priority": "recommended"
}

响应：
{
  "primary_plan": {
    "stations": [{"station_id": "S001", "eta": 6, "vehicles": [...]}],
    "total_eta": 8,
    "matching_score": 0.94
  },
  "need_human_review": false
}
```

---

## 7. 核心特点

| 特点 | 说明 |
|------|------|
| GIS+实时资源+ML优化 | 三结合精准匹配 |
| 多目标平衡 | 速度、负载、专业性 |
| 为约束校验提供候选 | 第7步输入 |

---

**文件结束**