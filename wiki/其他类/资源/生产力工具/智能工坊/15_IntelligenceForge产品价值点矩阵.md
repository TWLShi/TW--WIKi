---
title: 15_IntelligenceForge产品价值点矩阵
created: 2026-04-30
updated: 2026-04-30
tags: []
---

# IntelligenceForge v13.0 产品价值点矩阵

**标签**：#价值点矩阵 #产品设计 #Roadmap #决策记录
**位置**：03_SystemDesign/

---

## 已采用（11个）

| 价值点 | 来源 | 体现位置 |
|--------|------|----------|
| LLM Wiki 三层架构 | Karpathy + lxfater | Raw/ + wiki/ + 00-Shared/ 三层结构 |
| Obsidian 第二大脑 IDE | Obsidian 实战帖 + Karpathy | Graph View + Canvas + Dashboard.md |
| VKFS 虚拟知识文件系统 | VKFS GitHub | wiki/ 通过 VKFS 挂载，支持 ls/cat/grep/search |
| ReGenesis 有状态多代理 | @aurakairegen | Trinity Core + NexusMemory + 10-catalyst consensus |
| Ethical Governor 伦理自治 | ReGenesis + Hooks 哲学 | 9-Domain Matrix + Severity Ladder |
| Claude Code Hooks 护栏 | Hooks 帖 + @huangserva | 8 个 Hooks + Pre/Post ToolUse |
| harness-creator 元 Skill | 推荐帖 | 元 Skill 自动生成 AGENTS.md + 诊断 |
| 人机飞轮 + 自动路由 | Jack/Nathan Oyler 等 | 自动路由 + "自动做我想做的事" |
| 7 步知识管理流程 | @lxfater | Ingest/Query/Lint + Weekly Checklist |
| Prompt Caching 张力处理 | Nathan Oyler | Context Guard + 智能自动路由 |
| idea file 理念 | Jack Dorsey + Karpathy | AGENTS.md / claude.md 作为 idea file |

---

## 未采用（8个）

| 价值点 | 来源 | 暂缓原因 | 未来引入 |
|--------|------|----------|----------|
| 全自动 Commit Hooks | Hooks 第8条 | Git 历史混乱风险 | 审计日志+人类确认替代 |
| 合成数据+微调 | Karpathy 未来方向 | 成本高/隐私风险 | v14.0+ |
| 动态 Sub-agent 生成 | Clawdbot/ReGenesis | 复杂度与调试难度 | v14.0+ 评估 |
| 完整 Android 原生部署 | ReGenesis | 维护成本高 | 可选扩展路径 |
| Feature Flag 爆炸管理 | 源码泄露案例 | 易导致混乱 | harness-creator 集中管理 |
| 纯本地 KV 缓存主记忆 | NexusMemory 极端版 | 牺牲可读性与一致性 | VKFS+三层混合记忆 |
| 完全无人类审查自主进化 | 极端自动化方案 | 违反人类最终判断原则 | Weekly Checklist+人类签字 |
| 直接卖模型能力/Prompt | 商业化讨论 | 违背卖场景战略 | 坚持卖完整场景 |

---

## 总结

- **已采用 11 个**：构成 v13.0 核心骨架，方向清晰、逻辑自洽、实战性强
- **未采用 8 个**：复杂度控制、可靠性优先、人类在环原则、成本与维护性权衡
- 未采用点非永久放弃，可根据用户反馈和技术成熟度有序引入（v14.0+）

---

## 关联文档

- [[IntelligenceForge价值点清单]] — 价值点清单
- [[IntelligenceForge智锻v13完整版]] — v13.0 完整版

## 变更记录

- 2026-04-24：提取 IntelligenceForge v13.0 产品价值点矩阵