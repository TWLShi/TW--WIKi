# MOC-Index - Wiki 知识库总索引

**知识库名称**：消防调派智能系统 + 第二大脑
**组织方式**：PARA 方法 + Part逻辑分组 + MOC枢纽
**更新日期**：2025-04-26
**文档总数**：200+份

---

## 1. 全局导航（推荐从这里开始）

### **核心项目入口**
- **[[MOC-FireDispatchEngine.md]]** —— 消防调派智能系统全局导航（主枢纽）
- **[[00_GlobalNavigation/00_消防调派智能系统全局视图.md]]** —— 完整思维导图融合版
- **[[02_Part逻辑映射索引.md]]** —— Part逻辑映射表

### **Part快速跳转**
- **Part 1**：[[MOC-子场景画像.md]] → [[MOC-调派规模计算模型.md]] —— 需求与场景层
- **Part 2**：[[MOC-系统设计与数据模型.md]] —— 系统设计与数据模型
- **Part 3**：[[MOC-核心调派引擎-详细子模块.md]] —— **核心调派引擎**（重点）★
- **Part 4**：[[MOC-审计责任与数学模型.md]] —— 审计责任与数学模型

---

## 2. PARA 方法总览

| 层级 | 目录 | 用途 | 推荐入口MOC |
|------|------|------|-------------|
| **00** | Inbox | 快速捕获 + 待处理 | - |
| **01** | Projects | 具体项目 | [[MOC-FireDispatchEngine.md]] |
| **02** | Areas | 长期责任领域 | - |
| **03** | Resources | 可复用资源 | - |
| **04** | Archives | 归档 | - |
| **05** | **MOCs** | **全局导航枢纽** | **本文件** |
| **06** | ExternalMemory | 标签、向量、知识图谱 | - |

---

## 3. MOC 枢纽（05_MOCs/）

| MOC文件 | 说明 | 类型 |
|---------|------|------|
| [[MOC-Index.md]] | **全局总索引** | 👆 设为Wiki首页 |
| [[MOC-FireDispatchEngine.md]] | FireDispatchEngine项目导航 | 项目级 |
| [[MOC-系统设计与数据模型.md]] | Part 2导航 | 项目级 |
| [[MOC-核心调派引擎-详细子模块.md]] | Part 3导航 | 项目级 ★ |
| [[MOC-StateMachine.md]] | 状态机领域导航 | 专项 |
| [[MOC-Query_Routing问题路由专区.md]] | Query_Routing导航 | 专项 |
| [[MOC-调派规模计算模型.md]] | 规模计算导航 | 专项 |
| [[MOC-子场景画像.md]] | 12类场景导航 | 专项 |
| [[MOC-审计责任与数学模型.md]] | Part 4导航 | 项目级 |

---

## 4. 角色视角MOC（新增）

| MOC文件 | 说明 | 适用角色 |
|---------|------|----------|
| [[MOC-业务用户视角.md]] | 报警市民、一线消防员 | 业务用户 |
| [[MOC-指挥长视角.md]] | 现场指挥官 | 指挥长 |
| [[MOC-领导决策视角.md]] | 管理部门、领导 | 领导 |
| [[MOC-运维视角.md]] | 系统运维、SRE | 运维 |
| [[MOC-技术架构视角.md]] | 架构师、开发人员 | 技术 |

---

## 5. 核心模块导航

### **Part 1：需求与场景层**
- **入口**：[[MOC-子场景画像.md]]
- **核心模型**：[[MOC-调派规模计算模型.md]]
- **文档位置**：`01_Requirements/`（12类子场景画像）
- **文档数量**：29份

### **Part 2：系统设计与数据模型**
- **入口**：[[MOC-系统设计与数据模型.md]]
- **核心架构**：MultiAgent四Agent架构
- **文档位置**：`03_SystemDesign/` + `05_DataModel/`
- **文档数量**：45份

### **Part 3：核心调派引擎 ★**
- **入口**：[[MOC-核心调派引擎-详细子模块.md]]
- **核心模块**：Query_Routing + AI_Support + StateMachine
- **文档位置**：`06_DispatchEngine/`
- **文档数量**：31份

### **Part 4：审计责任、数学模型与附录**
- **入口**：[[MOC-审计责任与数学模型.md]]
- **核心**：人工确认 + 审计日志 + 数学模型
- **文档位置**：`07_Audit_And_Responsibility/` + `08_Math_And_Optimization/`
- **文档数量**：14份

---

## 6. 专项模块导航

| 模块 | MOC入口 | 文档位置 |
|------|---------|----------|
| 状态机模块 | [[MOC-StateMachine.md]] | `06_DispatchEngine/StateMachine/` |
| 问题路由专区 | [[MOC-Query_Routing问题路由专区.md]] | `06_DispatchEngine/Query_Routing/` |
| 子场景画像 | [[MOC-子场景画像.md]] | `01_Requirements/SubScenario_Portraits/` |
| 调派规模计算模型 | [[MOC-调派规模计算模型.md]] | `01_Requirements/` |
| 审计责任与数学模型 | [[MOC-审计责任与数学模型.md]] | `07_Audit_And_Responsibility/` |

---

## 7. 12步流程快速导航

```mermaid
flowchart LR
    S1[Step1警情接收] --> S2[Step2智能问询]
    S2 --> S3[Step3画像构建]
    S3 --> S4[Step4等级判定]
    S4 --> S5[Step5规模计算]
    S5 --> S6[Step6车辆匹配]
    S6 --> S7[Step7约束校验]
    S7 --> S8[Step8反向模拟]
    S8 --> S9[Step9AI多智能体]
    S9 --> S10[Step10人工确认]
    S10 --> S11[Step11方案下达]
    S11 --> S12[Step12审计归档]

    classDef core fill:#f59e0b,stroke:#b45309,color:#000
    classDef safety fill:#ef4444,stroke:#dc2626,color:#fff
    class S7 safety
```

| Step | 核心MOC | 关键文档 |
|------|---------|----------|
| Step 1-2 | [[MOC-Query_Routing问题路由专区.md]] | ASR+NER、智能问询 |
| Step 3 | [[MOC-子场景画像.md]] | 4维画像构建 |
| Step 4-5 | [[MOC-调派规模计算模型.md]] | N_total公式、三档方案 |
| Step 6-8 | [[MOC-核心调派引擎-详细子模块.md]] | GIS匹配、五维校验、时间线推演 |
| Step 9 | [[MOC-核心调派引擎-详细子模块.md]] | 4-Agent + 仲裁 |
| Step 10 | [[MOC-审计责任与数学模型.md]] | 人工确认、责任关口 |
| Step 11-12 | [[MOC-审计责任与数学模型.md]] | 方案下达、审计留痕 |

---

## 8. 按角色推荐入口

| 角色 | 推荐MOC | 说明 |
|------|---------|------|
| **新成员** | MOC-Index.md | 全局总览，建立整体认知 |
| **业务用户** | MOC-业务用户视角.md → MOC-子场景画像.md | 业务需求理解 |
| **指挥长** | MOC-指挥长视角.md → MOC-核心调派引擎.md | 战术决策支持 |
| **领导** | MOC-领导决策视角.md → MOC-审计责任与数学模型.md | 价值与合规 |
| **运维** | MOC-运维视角.md → MOC-StateMachine.md | 监控与故障处理 |
| **架构师/开发** | MOC-技术架构视角.md → MOC-系统设计与数据模型.md | 技术架构设计 |
| **开发/技术** | Part 2 + Part 3 + [[MOC-StateMachine.md]] |
| **业务/调度** | Part 1 + Step 9、10人工确认 |
| **审计/领导** | Part 4 + 状态机容错 |
| **AI/ML相关** | Agent_Dispatch + DIKW MOC |

---

## 9. raw/ 原始文档库

**位置**：`01_Projects/FireDispatchEngine/raw/`
**说明**：永久存储的原始文档与价值点提取库

| 类型 | 数量 | 说明 |
|------|------|------|
| 原文_ | 39份 | 完整技术文档 |
| 价值点提取_ | 34份 | 精华提取 |
| FRICP_ | 12份 | FRICP方案文档 |

---

## 10. 目录结构总览

```
Wiki/
├── 00_Inbox/                    # 收集箱
├── 01_Projects/                 # 项目层
│   └── FireDispatchEngine/      # ★ 核心项目
│       ├── 00_GlobalNavigation/ # 全局导航
│       ├── 01_Requirements/    # Part 1
│       ├── 02_Scenarios/        # 场景库
│       ├── 03_SystemDesign/     # Part 2
│       ├── 04_DIKW_Examples/    # DIKW
│       ├── 05_DataModel/       # 数据模型
│       ├── 06_DispatchEngine/  # Part 3 ★
│       ├── 07_Audit_And_Responsibility/  # Part 4
│       ├── 08_Math_And_Optimization/     # 数学模型
│       ├── 09_Roadmap/          # 路线图
│       ├── 10_Appendix/         # 附录
│       └── raw/                 # 原始文档库
├── 02_Areas/                   # 领域层
├── 03_Resources/               # 资源层
├── 04_Archives/                # 归档层
├── 05_MOCs/                    # ★ MOC枢纽
├── 06_ExternalMemory/          # 外部记忆
└── README.md                   # Wiki总说明
```

---

## 11. 标签索引

#消防调派 #MultiAgent #状态机 #AI决策 #审计责任 #知识库 #PARA #DIKW

---

**最后更新**：2025-04-26
**维护提示**：本文件为Wiki全局索引，请定期更新链接有效性。
