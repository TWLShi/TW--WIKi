---
title: 05_消防接处警标签体系与PKM融合分析
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# 消防接处警标签体系与PKM融合分析

**标签**：#标签融合 #PKM #四层维度 #DDD #状态机 #Obsidian
**位置**：05_DataModel/

---

## 四层核心维度

| 维度 | 说明 | 示例 |
|------|------|------|
| **Type** | 内容形态（笔记角色与功能） | #type/capture、#type/permanent、#type/moc |
| **State** | 工作流状态（处理阶段） | #state/inbox、#state/processing、#state/published |
| **Source** | 来源（输入管道） | #source/book、#source/article、#source/original |
| **Topic** | 领域主题（少量顶层入口） | #topic/ai、#topic/writing |

---

## 进阶标签层

| 维度 | 说明 |
|------|------|
| **Cog** | 认知动作（#cog/insight、#cog/critique、#cog/ddd） |
| **Value** | 价值偏好（#value/high-signal、#value/reusable） |
| **Out** | 输出潜力（#out/x-post、#out/article） |

---

## 消防领域融合映射

| PKM维度 | 消防领域适配 |
|---------|-------------|
| **Type** | #type/design、#type/sop、#type/adr、#type/case、#type/spec |
| **State** | #state/inquiring、#state/assessed、#state/dispatched、#state/handling、#state/completed |
| **Source** | #source/raw、#source/history、#source/prd、#source/norm |
| **Topic** | #topic/接警问询、#topic/警情研判、#topic/资源调度、#topic/处警指挥 |

---

## 标签使用铁律

| 规则 | 说明 |
|------|------|
| **数量控制** | 每篇笔记 4-6 个标签 |
| **优先级** | Type → State → Source → Topic → Cog/Value/Out |
| **复杂关系** | 用 [[双链]] + Frontmatter，不用标签堆砌 |
| **命名规范** | 全小写 + 斜杠前缀（英文/拼音一致，便于 Dataview 查询） |

---

## 三层分工

| 工具 | 适合管理 |
|------|----------|
| **标签** | 类型/状态/来源/少量视角 |
| **Frontmatter（YAML）** | 时间/作者/评分/业务状态 |
| **双链 [[ ]]** | 概念关联/知识网络 |

---

## 核心优势

- 上文提供**消防领域骨架**（状态机/SOP/ADR/评审）
- 下文提供**标签纪律与检索效率**（四层前缀+克制原则）
- **Obsidian 原生能力放大**：状态标签驱动 Kanban 看板 + Dataview 查询
- **AI 自动化闭环**：raw/ → Ollama 自动打标 → wiki/ 带标签笔记

---

## Dataview 查询示例

```dataview
TABLE file.name AS "笔记", status, rating
FROM ""
WHERE contains(tags, "#state/inquiring") AND contains(tags, "#topic/接警问询")
SORT rating DESC
```

---

## 工作流示例

```
raw/历史警情
→ #state/inbox + #source/raw
→ 处理后 → #state/processing + #type/design + #topic/接警问询
→ 最终 → #state/accepted + #type/sop + #value/reusable
```

---

## 关联文档

- [[资源调度模块标签体系]] — 资源调度标签体系
- [[警情研判模块标签体系]] — 警情研判标签体系
- [[接警问询管理标签系统设计]] — 接警问询标签体系

## 变更记录

- 2026-04-25：提取消防接处警标签体系与 PKM 融合分析