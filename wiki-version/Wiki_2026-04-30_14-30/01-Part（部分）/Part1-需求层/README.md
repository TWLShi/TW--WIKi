---
title: README
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# Part 1：需求与场景层

**所属Part**：Part 1
**物理目录**：`01_Requirements` + `02_Scenarios`
**定位**：消防调派引擎的业务基础层

---

## 1. Part概述

**本Part是消防接处警指挥调度领域的业务需求与场景定义层**，以**子场景画像**为核心，定义12类警情场景的业务规则、规模计算模型和车辆/队站确定逻辑。

---

## 2. 核心内容

- 子场景画像（12类警情场景）
- 调派规模计算模型（N_total 7因子公式）
- 统一编成对照表
- 车辆/队站确定逻辑
- 业务规则总表

---

## 3. 目录结构

```
Part1_Requirements/
├── 01_Requirements/           # 需求定义
│   ├── SubScenario_Portraits/  # 12类子场景画像
│   ├── 01_Dispatch_Scale_Calculation_Model.md
│   ├── 04_Vehicle_Determination_Logic.md
│   └── 05_Station_Determination_Logic.md
│
└── 02_Scenarios/             # 场景模拟
    └── Full_Link_Simulations/  # 全链路场景
```

---

## 4. N_total 公式

```
N_total = N_base + α_sub + β_struct + G_special + M_support + Δ_confidence + Δ_scene
```

---

**相关链接**
[[Part 2 → 系统设计与数据模型]]
