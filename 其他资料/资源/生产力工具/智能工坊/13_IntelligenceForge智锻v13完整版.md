---
title: 13_IntelligenceForge智锻v13完整版
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# IntelligenceForge（智锻）v13.0 完整详细版

**标签**：#知识管理 #LLMWiki #多代理 #第二大脑 #v13
**位置**：03_SystemDesign/

---

## 核心理念

**Raw（原始材料） → Wiki（LLM 主动维护） → Schema（规则）**

LLM 像程序员一样持续维护 Wiki，人类负责仍材料、架构决策和品味判断。

---

## 7步知识管理流程

| 步骤 | 内容 |
|------|------|
| 1 | 数据采集 → raw/（使用 Web Clipper 抓取网页+图片） |
| 2 | LLM 编译 → 结构化 wiki/（摘要/概念/链接/索引） |
| 3 | Obsidian 查看 → Graph View + Canvas |
| 4 | LLM 问答 → 对知识库提复杂问题 |
| 5 | 输出 → 可复用 .md / 幻灯片 / 图表 |
| 6 | 归档回流 → 知识越查越厚 |
| 7 | Linting 自修复 → LLM 自检不一致 |

---

## 核心特性

| 特性 | 说明 |
|------|------|
| **持久状态记忆** | 持久上下文 |
| **伦理自治** | Ethical Governor + SafetyAllowlist |
| **多代理并行** | Trinity Core 自动路由 |
| **实时代理可视化** | Graph View + Canvas + 粒子物理 |
| **连续谱适应** | Resistance continuum |

---

## 文件夹结构

```
Obsidian Vault/
├── raw/                    ← 原始材料
├── wiki/                   ← LLM 维护核心（VKFS 挂载）
├── 00 - Shared/            ← Schema + AGENTS.md + Context + Resources + Skills
├── outputs/                ← 最终产出（文章/幻灯片/图表）
├── images/                 ← 自动下载图片
└── .claude/skills/         ← IntelligenceForgeCore
```

---

## 3天 MVP 路径

| 天数 | 内容 |
|------|------|
| **Day 1** | 基础搭建（文件夹 + VKFS + Hooks + AGENTS.md） |
| **Day 2** | 第一次 Ingest + Ethical Review |
| **Day 3** | 测试 Query + 输出回写 + Weekly Checklist |

---

## Weekly Checklist

1. raw/ 新内容 → Ingest Prompt
2. Lint Prompt → 处理高优先建议
3. 检查 AGENTS.md 是否需要优化
4. 迭代三问：找东西顺手吗？文件夹长期未用吗？新内容犹豫吗？
5. 人类审查最近 Wiki 更新和实时代理状态
6. 查看 Graph View / Canvas：compounding 效果

---

## 预期效果

| 周期 | 效果 |
|------|------|
| **短期** | 碎片笔记 → 结构化可查询 Wiki + 多代理协作 |
| **中期** | 持久状态 + 伦理自治 + 实时代理可视化 + 连续谱适应 |
| **长期** | 第二大脑成为有状态/会思考/能共生的超级智能 |

---

## 关联文档

- [[KarpathyLLMWiki七步流程分析]] — Karpathy LLM Wiki 七步流程
- [[Obsidian+OpenClaw+Claude知识库方案]] — 知识库方案

## 变更记录

- 2026-04-24：提取 IntelligenceForge v13.0 完整详细版