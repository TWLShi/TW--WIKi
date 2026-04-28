# Step7约束校验机制 - 价值点提取

**标签**：#Step7 #约束校验 #五维校验 #自动修复 #回退机制
**提取日期**：2025-04-25
**来源**：核心引擎v6.1-Step7约束校验机制完整版.txt
**版本**：V1.0

---

## 1. 约束校验目标

**目标耗时**：8-18秒

---

## 2. 输入聚合

| 输入源 | 内容 |
|--------|------|
| 第6步匹配方案 | 首选 + 备选 |
| 第5步规模方案 | 基础编成 |
| 第3步画像 | 特殊环境标签 |
| 全局约束规则库 | 最新版本规则 |

---

## 3. 五维校验体系

| 维度 | 检查内容 |
|------|----------|
| **资源可用性** | 实时车辆状态、中队出车率 |
| **时间窗约束** | ETA是否满足等级要求 |
| **特殊环境约束** | 城中村、窄巷、高层、化工等 |
| **规模合法性** | 最小/最大车辆限制 |
| **政策与预案** | 跨区调派权限、重大活动限制 |

---

## 4. 校验流程

```
输入聚合 → 多维检查 → 冲突检测评分 → 自动修复建议 → 输出分流
```

| 步骤 | 输出 |
|------|------|
| 全部Pass | 触发Step8（反向模拟） |
| 存在Warning | 带警告继续Step8 |
| 存在Fail | 回退到Step5或Step6 |

---

## 5. 异常处理分支

| 异常场景 | 处理逻辑 | 优先级 |
|----------|----------|--------|
| 实时资源数据同步失败 | 使用缓存 + 标记"数据可能滞后" | 高 |
| 特殊环境规则缺失 | 使用默认保守约束 | 高 |
| 校验引擎超时 | 回退到基础规则检查 | 高 |
| 多个严重Fail项 | 直接回退Step5重新计算 | 最高 |
| 跨区联动权限不足 | 自动降级为本地方案 | 高 |
| GIS路况数据不可用 | 使用历史平均ETA | 中 |

---

## 6. 数据库表结构

### constraint_validation_report
```sql
CREATE TABLE constraint_validation_report (
    incident_id      VARCHAR(32) PRIMARY KEY,
    overall_status    VARCHAR(10),  -- PASS/WARNING/FAIL
    overall_score     NUMERIC(5,2),
    checks_detail    JSONB,       -- 每条规则检查结果
    suggestions       JSONB[],      -- 修复建议
    repair_applied    BOOLEAN DEFAULT FALSE,
    created_at       TIMESTAMP
);
```

### constraint_check_items
```sql
CREATE TABLE constraint_check_items (
    check_id        BIGSERIAL PRIMARY KEY,
    incident_id     VARCHAR(32),
    rule_type       VARCHAR(50),  -- resource/time/special/scale/policy
    rule_name       VARCHAR(100),
    status          VARCHAR(10),   -- PASS/WARNING/FAIL
    score_factor    NUMERIC(4,3),
    details         JSONB
);
```

---

## 7. API接口

### POST /api/v1/alerts/{incident_id}/constraint/validate

```json
请求：
{
  "strict_mode": false,
  "allow_auto_repair": true,
  "max_repair_attempts": 2
}

响应：
{
  "code": 200,
  "data": {
    "incident_id": "INC-...",
    "overall_status": "WARNING",
    "overall_score": 82.5,
    "checks": [...],
    "suggestions": ["建议替换1辆举高车为轻型抢险车"],
    "need_human_review": true,
    "next_step": "Step8_ReverseSimulation"
  }
}
```

---

## 8. 核心特点

| 特点 | 说明 |
|------|------|
| 多层防御 | 资源、时间、环境、规模、政策五维校验 |
| 自动修复 | Warning/Fail自动生成调整方案 |
| 人工兜底 | 无法修复时强制人工介入 |
| 全链路可解释 | 每步校验都有理由说明 |

---

**文件结束**