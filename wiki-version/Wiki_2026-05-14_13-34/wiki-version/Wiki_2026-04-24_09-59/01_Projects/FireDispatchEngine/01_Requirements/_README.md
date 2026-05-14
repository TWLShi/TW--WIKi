# 01_Requirements / 需求与规则

**标签**：#README
**文件夹职责**：消防调派引擎的所有需求定义、业务规则和计算模型

**核心内容**：
- 子场景画像（11个）
- 调派规模计算模型
- 车辆/队站确定逻辑
- 业务规则总表

## 使用方法

所有新子场景必须先在此建立画像，再进入 `02_Scenarios` 做全链路模拟。

## 目录结构

- `SubScenario_Portraits/` —— 11个子场景画像模板
- `01_Dispatch_Scale_Calculation_Model.md` —— N_total 7因子公式
- `02_Ten_Subscenario_Calculation_Examples.md` —— 详细计算示例
- `03_Unified_Dispatch_Composition_Table.md` —— 统一编成对照表
- `04_Vehicle_Determination_Logic.md` —— 车辆确定逻辑
- `05_Station_Determination_Logic.md` —— 队站确定逻辑
- `06_Dispatch_Business_Logic.md` —— 业务逻辑核心

## 命名规范

- 文件名：`NN_<English_Name>.md`（序号_英文名）
- 图片/附件：随同名 md 文件放置

## N_total 公式

```
N_total = N_base + α_sub + β_struct + G_special + M_support + Δ_confidence + Δ_scene
```

**更新频率**：每次新增场景或规则变更时立即更新

**相关链接**：
- [[02_Scenarios]] —— 场景模拟
- [[06_DispatchEngine]] —— 调派引擎
