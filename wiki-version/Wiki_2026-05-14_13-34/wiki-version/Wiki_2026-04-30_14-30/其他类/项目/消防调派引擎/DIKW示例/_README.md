---
title: _README
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# 04_DIKW_Examples / DIKW 转化示例库

**标签**：#README #Part2
**文件夹职责**：各类警情下的 DIKW 完整转化模板，是小认知核心最重要的知识来源
**所属 Part**：Part 2 - 系统设计与数据模型

## 现有模板

- `01_Ordinary_Fire_DIKW.md` —— 普通火灾
- `02_Hazmat_Fire_DIKW.md` —— 危化火灾
- `03_Rescue_DIKW.md` —— 救援类（最高优先级）

## 使用规范

- 每次新增警情类型必须在此建立对应 DIKW 示例
- 所有示例必须包含：Data / Information / Knowledge / Wisdom + 调派句 JSON
- 与 `06_DispatchEngine` 中的路由逻辑保持同步

## DIKW 结构

```
D (Data) → 原始报警描述
I (Information) → 结构化槽位信息
K (Knowledge) → 规则/公式/N_total计算
W (Wisdom) → 超越规则的智慧决策
```

## 命名规范

- 文件名：`NN_<Type>_DIKW.md`
- Type：Ordinary_Fire / Hazmat_Fire / Rescue

## 使用场景

- AI 训练样本
- 规则说明示例
- 新人培训材料

**模板来源**：`03_Resources/Templates/DIKW_Template.md`

**相关链接**：
- [[DIKW_MOC_v2026-04]]
- [[需求]] —— N_total公式
- [[场景]] —— 完整场景模拟
