# FireDispatchEngine 项目总说明

**项目目标**：基于「干净数据 + 小认知核心 + 外部记忆」架构，构建高精度、高可靠的智能消防调派引擎，实现从119报警到精准调派、实时指挥、事后学习的全闭环。

## 目录结构

- `01_Requirements/`：需求、子场景画像、计算模型、业务规则
- `02_Scenarios/`：全链路场景模拟与典型案例
- `03_SystemDesign/`：多智能体架构、状态机、数据流
- `04_DIKW_Examples/`：普通/危化/救援类 DIKW 转化模板
- `05_DataModel/`：核心实体、ER图、数据库结构
- `06_DispatchEngine/`：调派引擎核心逻辑（定级、路由、约束）
- `07_TimeAxis_Roadmap/`：时间轴与开发路线图
- `08_Simulation_Data/`：模拟、审计、责任机制
- `09_Appendix/`：公式、参考、附录

## 核心原则

- 所有内容必须遵循 DIKW v2.1 模板
- 新场景必须先走 `01_Requirements` → `02_Scenarios` → `04_DIKW_Examples`
- 每周更新 Roadmap 与 Simulation_Data

## 核心概念

| 概念 | 说明 |
|------|------|
| 小认知核心 | 负责接收报警信息，提取关键槽位 |
| 外部记忆 | 向量检索标签 + 知识图谱索引 |
| DIKW | Data→Information→Knowledge→Wisdom 层级转化 |

## N_total 公式

```
N_total = N_base + α_sub + β_struct + G_special + M_support + Δ_confidence + Δ_scene
```

**最后更新**：2026-04-24
**版本**：v1.0
**负责人**：yong
