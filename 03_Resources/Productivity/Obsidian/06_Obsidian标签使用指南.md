# Obsidian标签使用指南

**标签**：#Obsidian #标签使用 #Dataview #Frontmatter #双链
**位置**：03_SystemDesign/

---

## 标签基本规则

| 规则 | 说明 |
|------|------|
| 书写格式 | `#标签名` 或 Frontmatter 中 tags 数组 |
| 嵌套标签 | 使用 `/` 分隔层级（如 `#type/permanent/ai`） |
| 层级限制 | ≤ 3 级 |
| 数量控制 | 每篇笔记 3-6 个标签 |

### Frontmatter 示例

```yaml
---
tags:
  - type/permanent
  - state/processing
  - topic/ai
  - value/high-signal
aliases: [别名]
created: 2026-04-04
---
```

---

## 三层分工

| 工具 | 适合管理 |
|------|----------|
| **标签 #** | 检索视角与过滤（类型/状态/来源/顶层主题） |
| **属性 Frontmatter** | 结构化元数据（日期/评分/作者/优先级）便于 Dataview 排序计算 |
| **双链 [[ ]]** | 知识网络与关系（具体概念/想法/人物） |

### 判断原则

- 值得拥有独立页面并不断丰富 → 用双链
- 分类/状态/来源/检索视角 → 用标签
- 日期/评分/作者等固定字段 → 用 Frontmatter 属性

---

## 日常流程（结合四层架构）

| 层级 | 标签操作 |
|------|----------|
| **Capture** | 新建笔记：`#type/capture #state/inbox #source/flomo` |
| **Aggregate** | AI 自动建议/补全标签（AI Tagger / Auto Tagger） |
| **Organize** | 转为永久笔记：`#type/permanent #state/review` + 建立双链 |
| **Output** | 发布时：`#type/output #out/x-post #state/published` |

---

## Dataview 查询示例

```sql
-- 查看所有处理中的 AI 笔记
TABLE file.name AS "笔记", file.mtime AS "更新时间"
WHERE contains(tags, "#state/processing") AND contains(tags, "#topic/ai")
SORT file.mtime DESC

-- 输出潜力仪表盘
TABLE file.name
WHERE contains(tags, "#out/")
SORT rating DESC
```

---

## 最佳实践

- **命名规范**：小写英文 + `/` 嵌套，避免中英混用
- **定期维护**：每周 review inbox/processing，每月合并不活跃标签
- **从少到多**：先在 10-20 篇常用笔记上实践，观察效果再全库推广

---

## 避坑指南

| 错误 | 正确做法 |
|------|----------|
| 标签堆砌摘要 | 用双链建立具体概念关系 |
| 标签数量超过 6 个 | 超出时转为双链或属性 |
| 宽泛标签（#效率、#成长） | 用嵌套标签细分（#topic/productivity） |
| 用标签代替双链 | 具体概念用 [[wikilink]] |

---

## 关联文档

- [[05_完整Obsidian标签体系]] — 完整标签体系
- [[04_AI驱动认知构建系统与标签体系]] — AI 驱动认知构建系统
- [[03_Obsidian插件系统与知识库构建]] — Obsidian 插件系统

## 变更记录

- 2026-04-24：提取 Obsidian 标签使用指南