# Teacher蒸馏小模型训练细节

**来源**：119消防接警规则与热词联合加载
**版本**：V1.0

---

## 1. 训练目标
- 输入：当前画像已知要素（特征向量）
- 输出：激活的规则组 + 热词组 + boost权重
- 核心能力：上下文感知的联合加载

---

## 2. Teacher Prompt模板

```text
你是119消防接警规则提炼专家。
当前日志：
问题：{question}
转录：{asr_text}
已知画像要素：{known_elements}

请严格遵守消防规范，输出结构化规则加载建议：
{
  "condition": "触发条件描述",
  "activate_rule_groups": ["rule_id1", "rule_id2"],
  "activate_hotword_groups": ["group1", "group2"],
  "boost_weights": {"group1": 3.8, "group2": 2.5},
  "reasoning": "CoT解释"
}
```

---

## 3. 训练数据格式

```json
{
  "input_features": {
    "ignition_point": "厨房",
    "victim_category": "儿童",
    "smoke_condition": "浓烟",
    "fire_development": "猛烈阶段"
  },
  "target_rules": ["kitchen_child_high_risk", "residential_smoke_development"],
  "target_hotwords": ["kitchen_fire", "child_risk"],
  "boost_weights": {"kitchen_fire": 4.2, "child_risk": 3.8},
  "confidence": 0.93
}
```

---

## 4. 推荐模型选择

| 模型 | 可解释性 | 训练难度 | 适用场景 |
|------|----------|----------|----------|
| XGBoost/LightGBM | 最高（白盒） | 低 | 起步首选 |
| TinyBERT/DistilBERT | 中 | 中 | 需更强泛化 |
| Qwen2-0.5B LoRA | 中低 | 高 | 极致性能 |

---

## 5. XGBoost训练配置

- 特征：One-hot/Embedding编码已知要素
- 损失：多标签分类 + 回归（boost权重）
- 超参：树深度6-10，学习率0.05-0.1
- 评估：Precision@K、召回率、F1

---

## 6. 蒸馏技巧
- 软标签蒸馏：KL散度损失
- 规则约束：SHACL验证损失
- 多任务：同时预测规则组+热词组+权重

---

**文件结束**
