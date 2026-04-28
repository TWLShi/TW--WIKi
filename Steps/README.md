# Steps - 消防接处警指挥调度12步全链路流程

**定位**：FireDispatchEngine项目的12步核心业务流程
**说明**：从119报警到精准调派、实时指挥、事后学习的全闭环

---

## 12步全链路引擎

```mermaid
flowchart LR
    S1[Step1接警接收] --> S2[Step2智能问询]
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

    classDef core fill:#f59e0b,stroke:#d97706
    classDef safety fill:#ef4444,stroke:#dc2626,color:#fff
    classDef wisdom fill:#8b5cf6,stroke:#7c3aed,color:#fff
    class S1,S2,S3,S4,S5,S6 core
    class S7,S8,S9,S10 safety
    class S11,S12 wisdom
```

---

## 12步流程概览

| Step | 名称 | 核心内容 | DIKW对应 | 关键文档 |
|------|------|----------|----------|----------|
| **Step 1** | 接警接收与初步研判 | 119接警、ASR转写、初步标签 | Data | [[Step1_接警接收与初步研判/]] |
| **Step 2** | 智能问询与信息补全 | Query_Routing、非对称问询 | Data→Information | [[Step2_智能问询与信息补全/]] |
| **Step 3** | 多维画像构建 | 空间/时间/规模/风险4维分析 | Information | [[Step3_多维画像构建/]] |
| **Step 4** | 警情等级智能判定 | 规则+ML混合等级判定 | Knowledge | [[Step4_警情等级智能判定/]] |
| **Step 5** | 调派规模智能计算 | 规模模型 + 三档方案 | Knowledge | [[Step5_调派规模智能计算/]] |
| **Step 6** | 资源匹配与任务分配 | 队站车辆匹配 + 初步分工 | Knowledge | [[Step6_资源匹配与任务分配/]] |
| **Step 7** | 约束校验与风险评估 | 五维约束校验 | Knowledge | [[Step7_约束校验与风险评估/]] |
| **Step 8** | 反向模拟与方案预演 | 时间线推演 + 冲突解决 | Knowledge→Wisdom | [[Step8_反向模拟与方案预演/]] |
| **Step 9** | AI多智能体协同指挥 | 4-Agent决策 + 仲裁生成指挥方案 | **Wisdom** | [[Step9_AI多智能体协同指挥/]] |
| **Step 10** | 人工指挥确认与授权 | 调度员最终确认 + 责任签字 | Wisdom | [[Step10_人工指挥确认与授权/]] |
| **Step 11** | 指挥指令下达与协同 | 多端推送 + 现场指挥官指令 | Wisdom | [[Step11_指挥指令下达与协同/]] |
| **Step 12** | 全程审计与优化反馈 | 不可篡改日志 + 模型训练反馈 | Wisdom（闭环） | [[Step12_全程审计与优化反馈/]] |

---

## 目录结构

```
Steps/
├── README.md                              # 全局入口
├── 原文_核心调派引擎12步流程导航.md         # 12步总览
├── 核心引擎v6.2-全流程总览Mermaid图.txt    # 流程图
│
├── Step1_接警接收与初步研判/               # Data层
├── Step2_智能问询与信息补全/               # Data→Information
├── Step3_多维画像构建/                     # Information层
├── Step4_警情等级智能判定/                 # Knowledge层
├── Step5_调派规模智能计算/                 # Knowledge层
├── Step6_资源匹配与任务分配/                # Knowledge层
├── Step7_约束校验与风险评估/               # Knowledge层
├── Step8_反向模拟与方案预演/               # Knowledge→Wisdom
├── Step9_AI多智能体协同指挥/                # Wisdom层 ★
├── Step10_人工指挥确认与授权/              # Wisdom层
├── Step11_指挥指令下达与协同/              # Wisdom层
└── Step12_全程审计与优化反馈/              # Wisdom闭环
```

---

## 阅读路径建议

| 角色 | 推荐路径 |
|------|----------|
| 调度员 | Step 1→2→3→9→10→11（核心流程） |
| 开发人员 | Step 1→12（完整链路）→重点Step深入 |
| 指挥长 | Step 4→5→9→10→11→12（决策关键点） |
| 新成员 | Steps README → Step 1 → Step 9 → Step 12 |

---

## 核心公式

```
N_total = N_base + α_sub + β_struct + G_special + M_support + Δ_confidence + Δ_scene
final_score = 0.45 × rule_score + 0.55 × ml_score
单中队出车率 ≤ 70%
```

---

## 相关链接

- [[Parts/]] —— 四大Part总览
- [[MOC-FireDispatchEngine.md]] —— 项目全局MOC枢纽
- [[06_DispatchEngine/]] —— 核心引擎源目录
