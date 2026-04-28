# 完整Obsidian标签体系

**标签**：#Obsidian #标签体系 #知识管理 #四层维度
**位置**：03_SystemDesign/

---

## 核心四层维度

| 维度 | 前缀 | 示例 |
|------|------|------|
| **内容形态** | #type/ | capture、literature、permanent、moc、project、output |
| **工作流状态** | #state/ | inbox、processing、review、published、archive |
| **来源** | #source/ | flomo、book、article、podcast、original、voice、webclip |
| **领域主题** | #topic/ | ai、writing、productivity、cognition、management（≤10个顶层） |

### 进阶自我画像（可选，克制使用）

| 维度 | 前缀 | 示例 |
|------|------|------|
| **认知动作** | #cog/ | insight、critique、synthesis、question |
| **价值偏好** | #value/ | high-signal、reusable、foundational、inspiring |
| **输出潜力** | #out/ | x-post、article、thread、summary |

---

## 三层分工

| 工具 | 适合管理 |
|------|----------|
| **标签** | 视角与过滤（类型/状态/来源/顶层主题/自我画像） |
| **属性（Frontmatter）** | 结构化元数据（日期/作者/评分/优先级） |
| **双链 [[ ]]** | 知识网络与关系（概念/因果/对比/例子） |

### Frontmatter 示例

```yaml
---
created: 2026-04-04
updated: 2026-04-04
author: 
rating: 8/10
priority: high
aliases: [别名1, 别名2]
---
```

---

## 与四层架构互补

| 层级 | 主要标签 |
|------|----------|
| **Capture** | #type/capture + #state/inbox + #source/xxx |
| **Aggregate** | AI 自动补全标签 + 建议双链和属性 |
| **Organize** | 标签 + 双链 + MOC 共同构建知识图谱 |
| **Output** | #out/xxx + #type/output + #state/published |

---

## 最佳实践

- **数量控制**：每篇笔记 3-6 个标签
- **层级限制**：≤ 3 级（如 #type/permanent/ai）
- **前缀固定**：使用 #type/、#state/ 等前缀
- **定期维护**：每周/每月 review inbox 和 processing 笔记

---

## Dataview 查询示例

```
TABLE file.name
WHERE contains(tags, "#state/processing") AND contains(tags, "#topic/ai")
SORT file.mtime DESC
```

---

## 关联文档

- [[04_AI驱动认知构建系统与标签体系]] — AI 驱动认知构建系统
- [[03_Obsidian插件系统与知识库构建]] — Obsidian 插件系统

## 变更记录

- 2026-04-24：提取完整 Obsidian 标签体系