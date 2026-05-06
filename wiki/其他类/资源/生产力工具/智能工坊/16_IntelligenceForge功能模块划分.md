---
title: 16_IntelligenceForge功能模块划分
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# IntelligenceForge v13.0 功能模块划分

**标签**：#功能模块 #系统设计 #七模块 #IntelligenceForge
**位置**：03_SystemDesign/

---

## 7大核心模块

| 模块 | 名称 | 核心职责 | 关键组件 |
|------|------|----------|----------|
| **M1** | 知识采集与摄入 | 将散乱原始材料整理成干净的 raw 层 | Obsidian Web Clipper、Ingest Prompt、VKFS |
| **M2** | 知识编译与维护 | LLM 主动将 raw 编译成结构化 Wiki | LLM Wiki 编译器、Lint Prompt、输出回写 |
| **M3** | 知识查询与交互 | 复杂问题查询、自动路由、多代理协作 | Query Prompt、Trinity Core、idea file 输出 |
| **M4** | 持久记忆与状态 | 三层混合记忆，支持连续谱适应 | VKFS + NexusMemory + Context Guard |
| **M5** | 执行护栏与伦理 | 运行时纪律 + 显式控制，安全审批 | Ethical Governor、8 Hooks、SafetyAllowlist |
| **M6** | 框架生成与自优化 | AI 自动生成/优化 AGENTS.md，实现元级自维护 | harness-creator 元 Skill、Lint 自修复 |
| **M7** | 可视化与人机飞轮 | 实时 UI + Graph/Canvas + Weekly Checklist | Dashboard + 粒子物理 UI |

---

## 模块关系（闭环飞轮）

```
输入流: M1(采集) → M2(编译) → M4(记忆)
执行流: M3(查询) → M5(护栏) → M6(框架优化)
输出流: M3 输出 idea file → M2 回写 Wiki
反馈:   M7(可视化+Checklist) → 人类决策 → M6自优化 → 全系统进化
底层:   VKFS 贯穿 M2/M3/M4
```

---

## 设计原则

- **7 模块克制**：避免碎片化，便于维护和扩展
- **人机分工清晰**：M5（伦理护栏）+ M7（人机飞轮）确保人类最终判断权
- **平衡哲学**：运行时纪律 vs 显式控制层，避免 Feature Flag 爆炸
- **可扩展**：v14.0 可在 M6 加动态 Sub-agent，M4 加合成数据微调

---

## 关联文档

- [[IntelligenceForge产品价值点矩阵]] — 产品价值点矩阵
- [[IntelligenceForge智锻v13完整版]] — v13.0 完整版

## 变更记录

- 2026-04-24：提取 IntelligenceForge v13.0 功能模块划分