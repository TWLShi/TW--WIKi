# MOC - 审计责任与数学模型

**所属目录**：`Wiki/05_MOCs/`
**定位**：Part 4 审计责任 + 数学模型 导航枢纽
**更新日期**：2025-04-25
**版本**：V1.0

---

## 1. Part 4 概览

| 模块 | 文件数 | 核心文档 |
|------|--------|----------|
| 审计与责任 | 8 | 01_Human_Confirmation_And_Responsibility.md |
| 数学模型 | 3 | 05_Math_Model_Full_Link.md |
| 附录 | 2 | 公式汇总.md |
| Roadmap | 1 | _README.md |

---

## 2. 目录结构

```
07_Audit_And_Responsibility/
├── Part4-README.md                    # Part 4 入口
├── 01_Human_Confirmation_And_Responsibility.md  # 人工确认与责任
├── 02_Audit_Mechanism_And_Report_Template.md   # 审计机制
├── 03_Audit_Log_And_Responsibility_Model.md    # 审计日志模型
├── 04_Audit_Log_Table_Structure.md            # 审计日志表结构
├── 07_Human_Responsibility_Confirmation_Simulation.md
├── 08_Dispatcher_Duty_Collection_Dialog.md
├── 10_Dispatch_System_Audit.md
└── 11_Dispatch_Responsibility_Mechanism_And_Human_Confirmation_Nodes.md

08_Math_And_Optimization/
├── 05_Math_Model_Full_Link.md        # 数学模型全链路 ⭐
├── 06_Optimization_Suggestions_And_Audit_Findings.md
└── 09_Dispatch_Plan_Work_Content_And_Plan.md

10_Appendix/
└── 公式汇总.md                        # 公式速查 ⭐

09_Roadmap/
└── _README.md
```

---

## 3. 责任闭环

```
AI辅助决策 → 人工最终确认 → 方案锁定 → 审计留痕 → 责任追溯
```

### 责任主体映射

| 步骤 | 主要责任人 | 责任类型 |
|------|-----------|----------|
| Step 1-2 | 接警员 | 信息采集 |
| Step 3-8 | AI系统 | 分析与方案生成 |
| Step 10 | 调度员 | 最终确认（关键责任关口） |
| Step 11-12 | 系统 | 执行与审计 |

---

## 4. 数学模型核心公式

| 公式 | 描述 | 约束 |
|------|------|------|
| `推荐车辆数 = round(基础车辆数 × 总系数)` | 规模计算 | - |
| `总系数 = 建筑系数 × 风险系数 × 时间系数 × 面积系数` | 系数计算 | 上限3.5 |
| `final_score = 0.45 × rule_score + 0.55 × ml_score` | 混合判定 | - |
| `单中队出车率 ≤ 70%` | 资源约束 | 上限70% |
| `priority_score = 风险权重×0.55 + 信息缺失度×0.25 + 时间敏感度×0.15 + 历史匹配度×0.05` | 路由优先级 | - |

---

## 5. 审计日志设计

| 字段 | 说明 |
|------|------|
| `trace_hash` | SHA-256区块链式哈希链 |
| `responsibility` | 每个步骤的责任人 + 贡献度 |
| `human_modifications` | 所有修改记录（old/new/reason） |
| `timestamp` | 不可篡改时间戳 |

---

## 6. 价值点提取

| 文档 | 说明 |
|------|------|
| [[价值点提取_审计责任体系.md]] | 责任闭环、责任主体映射、审计日志设计 |
| [[价值点提取_约束校验机制.md]] | 五维校验、校验分流、API接口 |
| [[价值点提取_MultiAgent多智能体架构.md]] | 四Agent权重、仲裁机制 |
| [[价值点提取_ML混合判定机制.md]] | 混合融合公式、SHAP可解释性 |
| [[价值点提取_12步Prompt体系.md]] | 12步Prompt模板 |

---

## 7. 相关链接

| 链接 | 说明 |
|------|------|
| [[Part4-README.md]] | Part 4 入口 |
| [[05_Math_Model_Full_Link.md]] | 数学模型全链路 |
| [[公式汇总.md]] | 公式速查 |

---

**文件结束**
