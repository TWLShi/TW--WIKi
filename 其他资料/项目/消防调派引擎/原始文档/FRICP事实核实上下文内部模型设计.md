---
title: FRICP事实核实上下文内部模型设计
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# FRICP 事实核实上下文内部模型设计（DDD风格）

**版本**：V1.0
**定位**：整个FRICP最核心的上下文之一

---

## 1. 上下文边界

| 要素 | 说明 |
|------|------|
| **名称** | 事实核实上下文 (Fact Verification Context) |
| **核心职责** | 只处理客观、可验证的事实核实，不允许进行任何预测分析或主观解读 |
| **输入** | 接处警系统要素、现场指挥系统回传、消控室电话核实结果、外部公共信息 |
| **输出** | 干净的"已核实事实包"（仅事实部分），推送给报告生成上下文 |
| **严格规则** | 所有外部数据必须标注责任声明；事实与辅助完全分离 |

---

## 2. 核心领域模型

### 聚合根（Aggregate Root）

**FactVerificationRecord**（事实核实记录）

| 属性 | 类型 | 说明 |
|------|------|------|
| VerificationId | String | 唯一ID |
| IncidentId | String | 关联警情ID（从接处警系统获取） |
| VerificationTime | Timestamp | 核实时间 |
| Status | Enum | Pending / Partial / Completed |
| VerifiedBy | String | 核实人（后方指挥员） |

**行为**：
| 方法 | 说明 |
|------|------|
| AddFactItem() | 添加一条已核实事实 |
| MarkAsVerified() | 标记整条记录为已核实 |
| AttachPublicInfo() | 附加外部公共信息（带责任标注） |
| GenerateFactPackage() | 生成干净的事实包（推送给报告生成上下文） |

### 实体（Entities）

**FactItem**（事实项）

| 属性 | 类型 | 说明 |
|------|------|------|
| FactType | Enum | 伤亡情况/被困情况/险情描述/处置进展等 |
| Value | String | 具体事实内容（例如"已确认3人被困"） |
| Source | Enum | 现场回传/消控室核实/公共信息/接处警记录 |
| Timestamp | Timestamp | 事实发生或确认时间 |
| ConfidenceLevel | Enum | 高/中/低（仅内部参考） |
| IsVerified | Boolean | 是否已人工核实 |

**规则**：FactItem必须包含Source和IsVerified字段

**PublicInfoAttachment**（公共信息附件）

| 属性 | 类型 | 说明 |
|------|------|------|
| InfoType | String | 地震烈度/气象风场/"三断"信息等 |
| RawData | String | 原始公共信息内容 |
| ResponsibilityStatement | String | 固定文本："外部公共信息，消防救援部门不承担准确性责任" |
| AttachmentTime | Timestamp | 获取时间 |

**规则**：只能作为辅助参考，不能直接转为FactItem

### 值对象（Value Objects）

| 值对象 | 说明 |
|--------|------|
| VerificationStatus | Pending / Partial / Completed |
| FactSource | 现场回传/消控室核实/公共信息/接处警记录（必须携带责任声明文本） |

### 领域事件（Domain Events）

| 事件 | 说明 |
|------|------|
| FactVerified | 某条事实已核实（携带FactItem） |
| PublicInfoAttached | 外部公共信息已获取并标注（携带PublicInfoAttachment） |
| FactPackageReady | 已核实事实包已准备好，可推送给报告生成上下文 |
| VerificationCompleted | 整条核实记录完成 |

---

## 3. 关键业务规则（绿色规则）

| 规则 | 说明 |
|------|------|
| **事实不可预测规则** | FactItem只能包含已确认的客观事实，不允许包含"可能""预计"等预测性词汇 |
| **责任标注强制规则** | 任何来自外部的数据（公共信息、消控室、微型消防站）必须自动附加责任声明，且无法移除 |
| **人工审核强制规则** | 所有FactItem在进入"已核实"状态前必须有指挥员人工确认记录 |
| **隔离规则** | 公共信息和舆情数据只能以PublicInfoAttachment形式存在，不能直接转为FactItem |
| **推送规则** | 只有VerificationStatus为Completed时，才能生成FactPackage推送给报告生成上下文 |

---

## 4. 与其他上下文的交互

| 交互方向 | 来源 | 内容 |
|----------|------|------|
| **输入** | 现有接处警系统 | 初始警情要素 |
| **输入** | 现有现场指挥系统 | 回传数据 |
| **输入** | 外部公共信息接口 | 地震/气象数据 |
| **输出** | 报告生成上下文 | 仅"已核实事实包"（干净、无预测内容） |
| **不直接交互** | 舆情模块 | 仅在辅助参考区显示，不进入事实包 |

---

## 5. 实现建议（极简技术方案）

| 建议 | 说明 |
|------|------|
| **实体存储** | 使用关系型数据库（FactVerificationRecord为主表，FactItem为子表） |
| **状态机** | FactVerificationRecord使用简单状态机管理 Pending → Partial → Completed |
| **责任标注** | 在数据进入上下文时，通过拦截器或领域服务自动添加责任声明 |
| **推送机制** | 使用领域事件驱动，当FactPackageReady事件发生时，通过消息队列（或API）推送给报告生成上下文 |
| **界面支持** | 后方指挥中心界面显示"待核实事实清单"，支持一键标记"已核实"并添加备注 |

---

**文件结束**