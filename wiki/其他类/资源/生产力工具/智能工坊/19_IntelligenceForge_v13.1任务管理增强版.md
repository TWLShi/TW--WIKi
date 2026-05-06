---
title: 19_IntelligenceForge_v13.1任务管理增强版
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# IntelligenceForge v13.1 任务管理增强版

**标签**：#v13.1 #任务管理 #敏捷 #BuildAgileTaskPlan #UserStory
**位置**：03_SystemDesign/

---

## 主要更新点

| 模块 | 更新内容 |
|------|----------|
| **M3 查询与交互** | 重大增强：Deliverable → Agile Task Plan 自动编排 |
| **M2 知识编译** | 支持标记 `[[workflow-node]]` |
| **M4 持久记忆** | 支持 workflow-node 专用索引 |
| **M6 框架自优化** | 支持任务计划模板自动生成 |
| **M7 可视化飞轮** | 新增敏捷看板与 Gantt 可视化 |

---

## 新增 Skill：BuildAgileTaskPlan

**触发条件**：用户提供明确的产出物（Deliverable）

**核心流程**：
1. 从 Wiki/VKFS 提取工作流级节点（workflow-node）
2. 构建 User Stories + Acceptance Criteria
3. 生成 WBS 任务分解
4. 识别依赖关系（串行/并行/里程碑）
5. 估算 Story Points
6. 输出：Markdown 清单 + Mermaid Gantt + Flowchart + Canvas 模板
7. 建议 WIP Limits、Sprint 长度、Definition of Done
8. Ethical Governor 审查
9. 建议是否存入 Wiki 作为模板

---

## 输出格式

| 格式 | 说明 |
|------|------|
| Markdown 任务清单 | 带优先级与负责人建议 |
| Mermaid Gantt 图 | 时间线 + 里程碑 |
| Mermaid Flowchart | 依赖关系 |
| Obsidian Canvas | Kanban Board 结构 |

---

## 敏捷原则

- 小批量交付
- 清晰 Acceptance Criteria（Given-When-Then）
- 可视化 + 频繁反馈
- 人类最终确认里程碑

---

## 关联文档

- [[敏捷任务管理方法完整指南]] — 敏捷任务管理方法
- [[IntelligenceForge功能模块划分]] — 功能模块划分（v13.0）

## 变更记录

- 2026-04-25：提取 IntelligenceForge v13.1 任务管理增强版