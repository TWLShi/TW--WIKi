# ML混合判定机制 - 价值点提取

**标签**：#ML混合判定 #机器学习 #XGBoost #SHAP #规则引擎
**提取日期**：2025-04-25
**来源**：核心引擎v6.2-Step4机器学习混合判定版.txt
**版本**：V1.0

---

## 1. 混合判定流程

```
Step 1: 规则引擎预打分（快速路径）
         ↓
Step 2: ML模型判定（深度路径，200+维特征）
         ↓
Step 3: 加权融合 + 分歧检测
         ↓
Step 4: 人工复核（如需要）
```

---

## 2. 核心公式

```python
# 混合融合
final_score = 0.45 * rule_score + 0.55 * ml_score

# 置信度计算
confidence = rule_confidence * 0.4 + ml_confidence * 0.6

# 分歧检测
need_human_review = (divergence >= 2) or (confidence < 0.80)
```

---

## 3. 判定权重配置

| 模型 | 权重 | 说明 |
|------|------|------|
| 规则引擎 | 0.45 | 可解释、强约束 |
| ML模型 | 0.55 | 处理复杂非线性 |

---

## 4. 异常处理

| 异常场景 | 处理逻辑 | 优先级 |
|----------|----------|--------|
| ML模型服务超时/失败 | 回退纯规则引擎 | 高 |
| ML置信度极低(<0.6) | 提高规则权重至0.7 | 最高 |
| 规则与ML分歧≥2级 | 立即推送人工复核 | 最高 |
| 特征工程缺失关键字段 | 使用默认中位数填充 | 中 |
| 模型版本漂移 | 触发模型监控告警 | 高 |

---

## 5. SHAP可解释性

```python
# SHAP值解释
shap_values = explainer.shap_values(features)
# 生成自然语言解释供调度员理解
```

---

## 6. 数据库字段

```sql
alert_level_result表新增字段：
- rule_level: 规则判定等级
- ml_level: ML预测等级
- ml_probabilities: [P1, P2, P3, P4]概率分布
- model_version: 模型版本
- explanation_rule: 规则解释
- explanation_ml: ML解释（SHAP）
- shap_values: 特征重要性
- need_human_review: 是否需要人工复核
```

---

## 7. 混合判定优势

| 模型 | 优势 |
|------|------|
| 规则引擎 | 可解释、易维护、强约束 |
| ML模型 | 处理复杂非线性、持续学习 |
| 融合 | 准确率更高，分歧自动人工介入 |

---

**文件结束**