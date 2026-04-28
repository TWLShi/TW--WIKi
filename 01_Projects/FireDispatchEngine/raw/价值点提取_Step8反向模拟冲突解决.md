# Step8反向模拟与冲突解决 - 价值点提取

**标签**：#Step8 #反向模拟 #冲突检测 #时间线推演 #火势蔓延
**提取日期**：2025-04-25
**来源**：核心引擎v6.1-Step8反向模拟冲突解决完整版.txt
**版本**：V1.0

---

## 1. 模拟目标

**目标耗时**：15-35秒

---

## 2. 输入聚合

| 输入源 | 内容 |
|--------|------|
| 第7步校验报告 | Pass/Warning |
| 第6步匹配方案 | 首选+备选 |
| 第5步规模方案 | 三档方案 |
| 第3步画像 | 场景画像 |

---

## 3. 模拟推演内容

| 模拟类型 | 说明 |
|----------|------|
| **时间线推演** | T+0 到 T+60分钟 |
| **火势蔓延模拟** | 基于画像+预测模型 |
| **资源消耗模拟** | 水、泡沫、人员疲劳 |
| **覆盖能力模拟** | 火场控制概率 |

---

## 4. 冲突检测类型

| 冲突类型 | 说明 |
|----------|------|
| 资源冲突 | 同一中队超负荷 |
| 时间冲突 | ETA超标 |
| 装备冲突 | 缺少关键器材 |
| 战术冲突 | 方案与场景不匹配 |
| 次生风险冲突 | 坍塌、爆炸、毒气 |

---

## 5. 处理流程

```
输入聚合 → 方案推演模拟 → 冲突全面检测 → 自动调整优化 → 输出分流
```

| 结果状态 | 后续动作 |
|----------|----------|
| PASS | 触发Step9（AI多智能体） |
| ADJUSTED | 自动调整后触发Step9 |
| FAIL | 回退Step5或Step6 |

---

## 6. 异常处理

| 异常场景 | 处理逻辑 | 优先级 |
|----------|----------|--------|
| 模拟引擎超时 | 使用简化规则推演 | 高 |
| 火势预测模型不可用 | 回退到静态规模评估 | 高 |
| 严重冲突无法自动修复 | 直接推送人工确认 | 最高 |
| 资源数据实时性差 | 保守估算+增加缓冲 | 中 |
| 多方案均不可行 | 强制回退Step5 | 最高 |

---

## 7. 数据库表结构

### reverse_simulation_result
```sql
CREATE TABLE reverse_simulation_result (
    incident_id        VARCHAR(32) PRIMARY KEY,
    status            VARCHAR(20),   -- PASS/ADJUSTED/FAIL
    feasibility_score NUMERIC(5,2),
    simulation_timeline JSONB,         -- 时间线推演
    conflicts         JSONB[],         -- 冲突清单
    adjusted_plans   JSONB[],         -- 调整后方案
    explanation      TEXT
);
```

### simulation_conflicts
```sql
CREATE TABLE simulation_conflicts (
    conflict_id      BIGSERIAL PRIMARY KEY,
    incident_id     VARCHAR(32),
    conflict_type   VARCHAR(50),   -- resource/time/tactical/risk
    severity        VARCHAR(10),   -- low/medium/high/critical
    description     TEXT,
    suggested_repair JSONB
);
```

---

## 8. API接口

### POST /api/v1/alerts/{incident_id}/simulation/reverse

```json
请求：
{
  "simulation_depth": "full",
  "include_fire_spread": true,
  "max_adjustment_attempts": 3
}

响应：
{
  "status": "ADJUSTED",
  "feasibility_score": 88.5,
  "conflicts": [{"type": "time", "severity": "medium"}],
  "next_step": "Step9_AIMultiAgent"
}
```

---

## 9. 核心特点

| 特点 | 说明 |
|------|------|
| 先推演再执行 | 实现闭环校验 |
| 自动修复 | 大幅降低人工干预频率 |
| 为Step9提供高质量方案 | AI多智能体输入 |

---

**文件结束**