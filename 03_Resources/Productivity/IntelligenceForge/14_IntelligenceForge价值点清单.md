# IntelligenceForge v13.0 价值点清单

**标签**：#价值点 #产品设计 #决策分析 #v13 #Roadmap
**位置**：03_SystemDesign/

---

## 已采用价值点（核心支柱）

| # | 价值点 | 说明 |
|---|--------|------|
| 1 | **LLM Wiki 三层架构** | Raw → Wiki → Schema，知识编译一次持续更新 |
| 2 | **Obsidian 作为第二大脑 IDE** | Graph View + Canvas + Web Clipper + 粒子物理 UI |
| 3 | **VKFS 虚拟知识文件系统** | 向量库包装成 Unix-like 文件系统 |
| 4 | **ReGenesis 有状态多代理系统** | Trinity Core + NexusMemory + 10-catalyst consensus |
| 5 | **Ethical Governor 伦理自治层** | 9-Domain Matrix + Severity Ladder + 连续谱思维 |
| 6 | **Claude Code Hooks 护栏系统** | 8 个 Hooks，运行时纪律 vs 显式控制平衡 |
| 7 | **harness-creator 元 Skill** | 一键生成 AGENTS.md + 自动诊断优化 |
| 8 | **人机飞轮 + 自动路由** | 人类架构决策，AI 执行记忆迭代 |
| 9 | **7 步知识管理流程** | 数据采集→编译→查看→问答→输出→回流→自修复 |
| 10 | **Prompt Caching 张力处理** | Context Guard + 智能自动路由平衡 |
| 11 | **idea file 理念** | AGENTS.md 作为 idea file，让代理自定义构建 |

---

## 未采用价值点（暂缓原因）

| # | 价值点 | 暂缓原因 |
|---|--------|----------|
| 1 | 全自动 Commit Hooks | 争议大，易导致 Git 历史混乱。用"审计日志+人类确认"替代 |
| 2 | 合成数据+微调 | 成本高、隐私风险大。先把 Wiki+VKFS 做扎实 |
| 3 | 动态 Sub-agent 生成 | 增加复杂度与调试难度。固定多代理+harness-creator 优化 |
| 4 | 完整 Android 原生部署 | 桌面+Termux 混合方案已满足。可选扩展路径 |
| 5 | Feature Flag 爆炸管理 | 用 harness-creator+AGENTS.md 集中管理，避免混乱 |
| 6 | 纯本地 KV 缓存主记忆 | 性能权衡，选 VKFS+三层混合记忆 |
| 7 | 完全无人类审查自主进化 | 违反"人类最终判断"核心原则 |
| 8 | 直接卖模型能力/Prompt | 遵循"卖场景，不卖能力"战略 |

---

## 权衡原则

| 维度 | 决策依据 |
|------|----------|
| 复杂度 vs 可靠性 | 优先可维护、可解释、人类在环 |
| 成本 vs 收益 | 稳健路线，不追求极致自动化 |
| 原则 vs 灵活性 | 保留 Weekly Checklist + 人类签字环节 |

---

## Roadmap 参考

未采用价值点可有序引入：
- **v14.0+**：动态 Sub-agent 生成可行性评估
- **v14.0+**：合成数据微调探索

---

## 关联文档

- [[13_IntelligenceForge智锻v13完整版]] — IntelligenceForge v13.0 完整版
- [[12_KarpathyLLMWiki七步流程分析]] — Karpathy LLM Wiki 分析

## 变更记录

- 2026-04-24：提取 IntelligenceForge v13.0 价值点清单