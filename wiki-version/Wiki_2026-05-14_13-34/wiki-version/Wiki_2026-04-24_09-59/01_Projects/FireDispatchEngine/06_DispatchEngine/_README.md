# 06_DispatchEngine / 调派引擎核心

**标签**：#README
**文件夹职责**：整个消防调派引擎的"大脑"，包含警情定级、路由决策、约束校验等核心逻辑

## 主要内容

- `Query_Routing/` —— 问询路由
- `01_Alert_Level_Mapping.md` —— 警情定级映射规则（1-5级）
- `02_Reverse_Verification_Logic.md` —— 定级反向验证逻辑
- `04_Constraint_Validation_Mechanism.md` —— 约束校验机制
- `05_Constraint_Validation_Details.md` —— 约束校验实现细节
- `06_Dispatch_Layer_Governance.md` —— 编排层治理
- `07_Dispatch_Engine_Implementation.md` —— 调派引擎实现细节

## 与其他模块关系

- 依赖 `05_DataModel` 的实体定义
- 输出结果写入 `08_Simulation_Data`
- 决策逻辑供小认知核心直接调用

## 核心原则

**干净数据优先 + 小核心决策 + 外部记忆检索**

## 核心流程

```
接警登记 → 事件画像 → N_total计算 → 约束校验 → 调派方案 → 出动反馈
```

## 命名规范

- 文件名：`NN_<Feature>_<Name>.md`
- 序号按逻辑流程排列（01定级→02校验→03...）

**相关链接**：
- [[01_Requirements]] —— N_total公式
- [[05_DataModel]] —— 数据模型
- [[08_Simulation_Data]] —— 审计与责任
