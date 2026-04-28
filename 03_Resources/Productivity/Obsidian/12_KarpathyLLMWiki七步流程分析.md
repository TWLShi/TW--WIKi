# Karpathy LLM Wiki 七步流程分析

**标签**：#知识管理 #LLMWiki #Karpathy #七步流程 #Obsidian
**位置**：03_SystemDesign/

---

## 7步流程

| 步骤 | 内容 |
|------|------|
| 1 | 数据采集 |
| 2 | raw/（原始数据存储） |
| 3 | LLM 编译 wiki/ |
| 4 | Obsidian 查看 |
| 5 | LLM 问答 |
| 6 | 输出回写 |
| 7 | 归档 + linting 自修复 |

---

## 与 IntelligenceForge 对应

| Karpathy 流程 | IntelligenceForge |
|---------------|-------------------|
| raw/ → wiki/ 编译 | Raw → Wiki → Schema 三层模型 |
| 输出回写 Wiki | Compounding artifact |
| Linting 自修复 | harness-creator + Hooks + Wiki Lint |
| 知识越查越厚 | 知识库自我增强 |

---

## 核心价值点

| 价值点 | 说明 |
|--------|------|
| **输出不是聊天记录** | 而是可复用的 .md / 幻灯片 / 图表 |
| **知识越查越厚** | 知识库 compounding 效果 |
| **LLM 主动维护 Wiki** | 主动写入而非被动查询 |
| **自我修复机制** | Linting 保持知识库健康 |

---

## 小幅优化建议

- Ingest Prompt 增加"输出回写 + 归档回流"步骤
- Weekly Checklist 增加"检查知识是否越查越厚"
- 可视化强调"一图胜过千言"的 Dashboard 设计

---

## 数据采集工具

- **Obsidian Web Clipper**：批量抓取网页 + 图片

---

## 关联文档

- [[08_Obsidian+OpenClaw+Claude知识库方案]] — 知识库方案
- [[04_AI驱动认知构建系统与标签体系]] — AI 驱动认知构建系统

## 变更记录

- 2026-04-24：提取 Karpathy LLM Wiki 七步流程分析