---
title: 价值点提取_12步Prompt体系
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# 12步Prompt体系 - 价值点提取

**标签**：#Prompt体系 #12步 #话术模板 #AI生成
**提取日期**：2025-04-25
**来源**：核心引擎v6.2-完整Prompt体系汇总.txt
**版本**：V1.0

---

## 1. Prompt体系概述

**温度控制建议**：
| 场景 | 温度 | 说明 |
|------|------|------|
| 大部分步骤 | 0.2-0.3 | 稳定性优先 |
| 预测Agent | 0.5 | 需要创造性 |

---

## 2. 各步Prompt模板

### Step 1：警情接收与初步解析
```text
输入：{{asr_text}}
输出JSON：address, building_type, fire_description,
         personnel_status, hazmat_mention, tags, confidence, missing_info
```

### Step 2：Query_Routing 智能问询
```text
输入：structured_alert_summary + missing_elements
输出：优先询问最高优先级缺失项（最多20字）
```

### Step 3：多维画像构建
```text
分析维度：空间/时间/规模/风险 4个维度
输出：完整画像JSON + confidence
```

### Step 4：等级判定
```text
输入：portrait_json + total_score
输出：final_level, confidence, main_reasons, risk_points
```

### Step 5：规模计算
```text
输入：level, base, ml_coefficient, top_shap
输出：自然语言解释（不超过60字）
```

### Step 7：约束校验
```text
输入：validation_report
输出：问题说明、调整方案、是否需要人工介入（不超过70字）
```

### Step 9：AI多智能体（核心）
```text
输入：perception + decision + execution + prediction + conflicts
输出：最终指挥方案JSON（包含arbitration_reason和overall_confidence）
```

### Step 10：人工二次确认
```text
显示：level, vehicles, eta, top_risks, explanation
记录：修改理由（用于审计与模型学习）
```

### Step 11：方案生成
```text
输入：approved_plan
输出：Markdown格式指挥单（警情概况/力量编成/行车路线/战术要点/注意事项）
```

---

## 3. 使用建议

| 建议 | 说明 |
|------|------|
| Few-shot | 每个Prompt加入1-2个高质量历史示例 |
| 版本管理 | Prompt放入配置文件，支持热更新 |
| 持续优化 | 人工确认修改作为Few-shot示例或微调数据 |

---

**文件结束**