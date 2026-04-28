# FRICP 事实核实上下文详细设计（完整版）

**版本**：V1.0（完整版）
**上下文定位**：最基础、最关键的上下文，负责将上游数据转化为干净的"已核实事实包"

---

## 上下文目标

只处理**客观、可验证的事实**核实，不允许任何预测分析或主观解读，最终输出干净的"已核实事实包"给报告生成上下文。

---

## 1. 聚合根：VerificationRecord（核实记录）

### 核心属性

| 属性 | 类型 | 说明 |
|------|------|------|
| VerificationId | String | 唯一ID |
| IncidentId | String | 关联警情ID（从接处警系统获取） |
| VerificationStatus | Enum | Pending / Partial / Completed |
| CreatedAt | Timestamp | 创建时间 |
| VerifiedBy | String | 核实人（后方指挥员） |
| FactItems | List<FactItem> | 事实项集合 |
| PublicInfoAttachments | List<PublicInfo> | 公共信息附件集合（仅参考） |
| AuditLogId | String | 关联合规审计记录 |

### 主要行为（方法）

#### AddFactItem(FactItem item)

| 要素 | 说明 |
|------|------|
| **目的** | 添加一条客观事实（支持人工录入补充伤亡等数据） |
| **输入** | FactItem（伤亡人数、被困人数、险情描述等） |
| **处理逻辑** | 校验是否为客观事实，标记来源和IsVerified状态 |
| **规则** | 禁止预测性语言，系统实时提示 |
| **自动状态** | 添加后自动标记为"待人工审核"（IsVerified = false） |

#### ReviewFactItem(FactItem item, Reviewer reviewer)

| 要素 | 说明 |
|------|------|
| **目的** | **一条条人工审核**关键数据 |
| **输入** | 具体FactItem + 审核人 |
| **处理** | 记录审核人、审核时间、审核意见（可选） |
| **输出** | 该FactItem的IsVerified = true |
| **强制规则** | 每一条关键数据（伤亡、被困等）必须单独调用此方法审核，**不能批量跳过** |

#### VerifyByPhone(PhoneCallResult result)

| 要素 | 说明 |
|------|------|
| **目的** | 记录消控室电话核实结果 |
| **输入** | 核实结果（文本 + 时间） |
| **处理逻辑** | 添加核实记录，标记为已核实 |
| **规则** | 自动记录拨打时间和核实人 |

#### AttachPublicInfo(PublicInfo info)

| 要素 | 说明 |
|------|------|
| **目的** | 附加外部公共信息（地震、气象等） |
| **输入** | 公共信息内容 |
| **处理逻辑** | 添加附件并**强制附加责任声明** |
| **规则** | 仅作辅助参考，**不能转为FactItem** |

#### MarkAsCompleted()

| 要素 | 说明 |
|------|------|
| **目的** | 标记整条核实记录完成 |
| **前置条件** | **所有关键FactItem都已一条条人工审核通过**（IsVerified = true） |
| **处理逻辑** | 检查所有关键FactItem是否已核实，更新Status为Completed |
| **输出** | 生成"已核实事实包"并推送给报告生成上下文 |
| **异常** | 若有关键数据未审核，阻止完成并提示 |

#### GenerateFactPackage()

| 要素 | 说明 |
|------|------|
| **目的** | 生成干净的事实包供报告使用 |
| **输出** | 仅包含已确认FactItem的FactPackage（**无预测、无舆情**） |
| **校验** | 每条FactItem必须带有IsVerified = true标记 |

---

## 2. 实体与值对象

### 实体：FactItem（事实项）

| 属性 | 类型 | 说明 |
|------|------|------|
| FactId | String | 唯一ID |
| FactType | Enum | CASUALTY（伤亡）/ TRAPPED（被困）/ HAZARD（险情）/ PROGRESS（处置） |
| Value | String | 具体内容 |
| Source | Enum | 现场回传 / 消控室核实 / 公共信息 / 人工录入 |
| Timestamp | Timestamp | 时间戳 |
| IsVerified | Boolean | 是否已人工审核 |
| VerifiedBy | String | 审核人 |
| VerifiedAt | Timestamp | 审核时间 |

**关键规则**：必须有Source和IsVerified字段

### 值对象

| 值对象 | 说明 |
|--------|------|
| VerificationStatus | Pending / Partial / Completed |
| FactSource | 现场回传 / 消控室核实 / 公共信息 / 人工录入 |
| ResponsibilityStatement | 固定文本："外部提供，消防救援部门不对其准确性、完整性、及时性承担责任" |

---

## 3. 关键业务规则（强制执行）

| 规则 | 说明 |
|------|------|
| **客观事实规则** | 只允许记录已发生、可验证的事实，系统实时校验并阻止预测性词汇 |
| **责任标注强制规则** | 任何外部数据（公共信息、消控室、微型消防站）进入时**必须自动附加责任声明** |
| **人工核实优先规则** | 关键事实（伤亡、被困）必须有IsVerified = true才能标记Completed |
| **隔离规则** | 公共信息和舆情数据**只能以附件形式存在**，不能转为FactItem |
| **推送规则** | 只有Status为Completed时，才能生成FactPackage推送给报告生成上下文 |
| **逐条审核规则** | 每一条关键数据必须单独调用ReviewFactItem，**禁止批量跳过** |

---

## 4. 与其他上下文的交互

### 输入来源

| 来源 | 内容 | 处理方式 |
|------|------|----------|
| 现有接处警系统 | 初始警情要素 | 直接获取 |
| 现有现场指挥系统 | 客观回传数据 | 标记待审核 |
| 人工录入 | 指挥员手动补充事实 | 进入待审核队列 |
| 外部公共信息接口 | 地震、气象等 | **强制责任标注**，仅作参考 |

### 输出

| 输出 | 说明 |
|------|------|
| 已核实事实包 | 单向推送"已核实事实包"给报告生成上下文 |
| 合规审计记录 | 所有操作触发合规审计上下文存证 |

### 隔离规则

- **舆情数据**：仅在辅助参考区显示，**不进入事实包**
- **公共信息**：仅作附件存在，**不能转为FactItem**

---

## 5. 页面交互要点（事实核实工作台）

### 布局结构

```
┌─────────────────────────────────────────────────────────────────┐
│  顶部：警情概要 + 敏感情况标记 + 50分钟倒计时                    │
├───────────────┬─────────────────────┬───────────────────────────┤
│               │                     │                           │
│  左侧         │  中间               │  右侧                      │
│  已回传事实列表 │  人工录入表单       │  消控室核实区              │
│               │  - 结构化字段       │  - 一键拨打                │
│               │  - 快速标记按钮      │  - 记录                    │
│               │                     │  公共信息辅助（带责任标注） │
│               │                     │                           │
├───────────────┴─────────────────────┴───────────────────────────┤
│  底部：保存并推送事实包（仅在所有关键数据审核通过后可用）          │
└─────────────────────────────────────────────────────────────────┘
```

### 交互元素

| 区域 | 交互元素 | 说明 |
|------|----------|------|
| **事实列表** | 每条后独立的"审核确认"按钮 | 逐条人工审核 |
| **高亮显示** | "待人工审核"标签 | 未审核的关键数据高亮 |
| **底部按钮** | "完成核实并推送" | 仅在所有关键数据审核通过后可用 |
| **消控室核实** | 一键拨打 + 记录 | 快速核实电话 |
| **公共信息** | 辅助参考区 | 带责任标注，不进入报告 |

### 设计理念

- 以**人工录入**和**电话核实**为核心
- 操作路径短，减少指挥员负担
- 确保事实干净、可追溯

---

## 6. 状态机流转

### FactItem状态

```
PENDING_REVIEW（待审核）
       ↓
REVIEWED（已审核）→ USED_IN_REPORT（已入报告）
       ↓
REJECTED（已驳回）→ MODIFIED（已修正）→ PENDING_REVIEW
```

### VerificationRecord状态

```
DRAFT（草稿）
   ↓
IN_REVIEW（审核中）← 每添加一个FactItem自动进入
   ↓
COMPLETED（已完成）← 所有关键FactItem审核通过
   ↓
PUSHED（已推送）← FactPackage已发送给报告生成上下文
```

---

## 7. 数据库表结构

### verification_record

```sql
CREATE TABLE verification_record (
    verification_id   VARCHAR(64) PRIMARY KEY,
    incident_id      VARCHAR(32) NOT NULL,
    status           VARCHAR(20) NOT NULL,  -- Pending/Partial/Completed
    created_at       TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_by       VARCHAR(32),
    completed_at     TIMESTAMP,
    audit_log_id     VARCHAR(64)
);
```

### fact_item

```sql
CREATE TABLE fact_item (
    fact_id          VARCHAR(64) PRIMARY KEY,
    verification_id  VARCHAR(64) NOT NULL,
    fact_type        VARCHAR(20) NOT NULL,  -- CASUALTY/TRAPPED/HAZARD/PROGRESS
    value            TEXT NOT NULL,
    source           VARCHAR(50) NOT NULL,
    source_timestamp TIMESTAMP,
    is_verified      BOOLEAN DEFAULT FALSE,
    verified_by      VARCHAR(32),
    verified_at      TIMESTAMP,
    created_at       TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_fact_verification ON fact_item(verification_id);
CREATE INDEX idx_fact_verified ON fact_item(is_verified);
```

### public_info_attachment

```sql
CREATE TABLE public_info_attachment (
    attachment_id    VARCHAR(64) PRIMARY KEY,
    verification_id VARCHAR(64) NOT NULL,
    info_type       VARCHAR(50),   -- earthquake/weather/emergency
    content         TEXT NOT NULL,
    responsibility_stmt TEXT,      -- 自动附加责任声明
    created_at      TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### phone_verification_log

```sql
CREATE TABLE phone_verification_log (
    log_id          VARCHAR(64) PRIMARY KEY,
    verification_id VARCHAR(64) NOT NULL,
    phone_number    VARCHAR(20),
    call_result     TEXT,
    called_at       TIMESTAMP,
    called_by       VARCHAR(32)
);
```

---

## 8. API接口

### POST /api/v1/verification/{incident_id}/facts

添加事实项

```json
请求：
{
  "fact_type": "CASUALTY",
  "value": "已确认3人被困",
  "source": "人工录入"
}

响应：
{
  "fact_id": "FACT-xxx",
  "is_verified": false,
  "status": "PENDING_REVIEW"
}
```

### POST /api/v1/verification/{verification_id}/facts/{fact_id}/review

逐条人工审核

```json
请求：
{
  "reviewer_id": "USER-xxx",
  "reviewer_role": "值班主任",
  "result": "PASS",
  "comment": "已与现场指挥员确认"
}

响应：
{
  "fact_id": "FACT-xxx",
  "is_verified": true,
  "verified_by": "USER-xxx",
  "verified_at": "2026-04-26T10:30:00Z"
}
```

### POST /api/v1/verification/{verification_id}/complete

完成核实并生成事实包

```json
请求：{}

响应：
{
  "status": "COMPLETED",
  "fact_package_id": "PKG-xxx",
  "fact_count": 5,
  "all_verified": true
}
```

---

## 9. 合规审计联动

每条关键操作都会触发合规审计上下文：

| 操作 | 审计记录 |
|------|----------|
| 添加FactItem | 操作人、时间、内容 |
| 逐条审核 | 审核人、被审核数据、结果、意见 |
| 标记完成 | 操作人、时间、FactItem总数、已审核数 |
| 生成事实包 | 包ID、内容摘要、推送时间 |

---

**文件结束**