# MOC - 系统设计与数据模型

**所属目录**：`Wiki/05_MOCs/`
**定位**：Part 2 系统设计 + 数据模型 导航枢纽
**更新日期**：2025-04-25
**版本**：V1.0

---

## 1. Part 2 概览

| 模块 | 文件数 | 核心文档 |
|------|--------|----------|
| 系统架构设计 | 19 | 01_Overview_And_Goals.md |
| MultiAgent多智能体 | 4 | 消防多智能体架构.md |
| 数据模型 | 13 | 01_Core_Entities_And_Domain_Model.md |
| DIKW知识体系 | 4 | 01_Ordinary_Fire_DIKW.md |

---

## 2. 目录结构

```
03_SystemDesign/
├── Part2-README.md                    # Part 2 入口
├── README.md                          # 数据模型README
├── 01_Overview_And_Goals.md           # 系统概览与目标
├── 02_Data_Flow_And_State_Machine.md  # 数据流与状态机
│
├── MultiAgent_Architecture/           # 多智能体架构
│   ├── 消防多智能体架构.md
│   ├── 消防多智能体应用.md
│   ├── 接处警AI总体流程.md
│   └── 对接处警系统审计.md
│
├── 04_DIKW_Examples/                  # DIKW知识体系
│   ├── 01_Ordinary_Fire_DIKW.md
│   ├── 02_Hazmat_Fire_DIKW.md
│   └── 03_Rescue_DIKW.md
│
└── 05_DataModel/                     # 数据模型
    ├── 01_Core_Entities_And_Domain_Model.md
    ├── 02_ER_Diagram_And_Relation_Model.md
    ├── 03_Database_Table_Structure.md
    ├── 06_Dispatch_Rule_Model.md
    └── 08_Config_Dictionary_And_Enumerations.md
```

---

## 3. MultiAgent四Agent架构

| Agent | 职责 | 权重 | 输入 | 输出 |
|-------|------|------|------|------|
| 感知Agent | 场景理解与事实基础 | 15% | 画像+模拟结果 | 场景标签+历史案例 |
| 决策Agent | 战术规划与力量分工 | **40%** | 感知输出 | 主攻方向+任务分工 |
| 执行Agent | 可执行性验证与指令生成 | 20% | 决策输出 | 时间线+指令模板 |
| 预测Agent | 前瞻性风险与态势预测 | 25% | 全局+决策输出 | 火势蔓延+次生灾害 |

### 仲裁机制（5阶段）
1. 结果标准化（统一JSON Schema）
2. 交叉验证（检测Agent间不一致）
3. 加权投票（默认权重）
4. LLM仲裁器（分歧>0.3时触发）
5. 二次验证（送回再校验）

---

## 4. 核心数据模型

### 警情核心实体
- `Incident` - 警情根实体
- `AlertStructured` - 结构化警情
- `IncidentPortrait` - 警情画像
- `AlertLevelResult` - 等级判定结果
- `DispatchScaleResult` - 规模计算结果
- `CommandPlan` - 指挥方案

---

## 5. 相关链接

| 链接 | 说明 |
|------|------|
| [[Part2-README.md]] | Part 2 入口 |
| [[消防多智能体架构.md]] | MultiAgent架构详解 |
| [[01_Core_Entities_And_Domain_Model.md]] | 核心实体模型 |

---

## 6. 价值点

| 文档 | 说明 |
|------|------|
| [[价值点提取_MultiAgent多智能体架构.md]] | 四Agent权重、仲裁机制 |
| [[价值点提取_核心知识点汇总.md]] | 含Multi-Agent架构说明 |

---

**文件结束**
