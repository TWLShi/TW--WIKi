# MOC 高级应用技巧

**最后更新**：2026-04-24
**标签**：#MOC #高级技巧 #MapsOfContent #Obsidian #知识管理
**页面作用**：帮助你把 MOC 从"简单导航页"升级为**动态知识枢纽、仪表盘和团队协作中心**。

---

## 1. MOC 进阶理念

普通 MOC = 静态链接列表
**高级 MOC = 动态知识引擎**，能自动更新，按角色展示，支持查询和可视化。

核心思想：
- **MOC 是活的**：不是一次性写完，而是持续演化的"知识地图"
- **MOC 是多维的**：同一个知识点可以在多个 MOC 中被引用
- **MOC 是智能的**：结合 Dataview、Templater、Canvas 等插件实现自动化

---

## 2. 高级技巧合集

### 技巧 1：动态 MOC（Dataview 自动生成）

```dataview
TABLE WITHOUT ID
    file.link AS "页面",
    file.mtime AS "更新时间"
FROM "03_调派引擎"
WHERE contains(file.tags, "N_total") OR contains(file.tags, "子场景")
SORT file.mtime DESC
```

**用途**：自动显示所有与 N_total 相关的最新页面。

### 技巧 2：角色导向 MOC（Callout + Dataview）

```markdown
> **[!tip] 接警员专区**
> - [[11大子场景推荐编成统一对照表]]

> **[!note] 开发专区**
> - [[调派规模计算模型]]
```

### 技巧 3：嵌套 MOC + 嵌入（Embed）

在主 MOC 中嵌入子 MOC：
```markdown
![[MOC-调派规模计算模型#英雄区]]
```

### 技巧 4：Canvas + MOC 混合使用

- 在 Canvas 中把 MOC 做成可视化大脑
- 把重要 MOC 节点拖入 Canvas，连接成流程图

### 技巧 5：Templater 自动创建 MOC

创建一个模板文件 `Templates/MOC-Template.md`：
```markdown
# MOC-{{title}}

**最后更新**：{{date}}

## 英雄区
## 核心内容导航
## 变更记录
```

### 技巧 6：MOC 维护自动化

- 每周运行 Dataview 查询，检查哪些页面尚未被任何 MOC 引用
- 使用 Templater 脚本"一键把新页面加入对应 MOC"

### 技巧 7：Graph View 优化

- 在 MOC 中加入 `---` 分隔线 + `%%` 注释，让 Graph View 只显示核心节点
- 使用 `aliases` 为 MOC 设置简短显示名称

### 技巧 8：多层 MOC 架构（推荐）

- **Level 0**：全局总 MOC（00_Index）
- **Level 1**：模块总 MOC（MOC-业务模型、MOC-调派引擎）
- **Level 2**：专题 MOC（MOC-调派规模计算模型、MOC-审计与责任机制）
- **Level 3**：具体内容页面

---

## 3. 本 Wiki 中的高级应用建议

| 模块 | 推荐高级 MOC 技巧 | 具体实现建议 |
|------|-------------------|--------------|
| 业务模型 | 动态子场景列表 + 速查表 | Dataview 查询 11 大子场景 |
| 调派规模计算模型 | 角色导向 + 公式嵌入 + 速查表 | 英雄区 + 思维导图 |
| 数据模型 | ER 图 + 表结构嵌入 | Canvas + Embed |
| 审计与责任机制 | 全链路流程图 + 报告模板预览 | Mermaid + Callout |

---

## 4. 高级 MOC 维护流程（推荐每周执行）

1. 新增页面 → 立即在对应 MOC 中添加链接
2. 修改核心内容 → 检查所有引用该页面的 MOC
3. 每周运行 Dataview 查询，找出"孤岛页面"（未被任何 MOC 引用）
4. 每季度 Review 一次所有 MOC，删除过时链接

---

## 5. 推荐插件组合

- **Dataview**：动态列表、查询
- **Templater**：自动创建 MOC
- **Advanced Tables**：快速编辑表格
- **Canvas**：可视化大脑
- **Obsidian Git**：版本控制 MOC 变更

---

## 6. 相关链接

- [[MOC释义及分析]]
- [[00_Index]]
- [[02_业务模型/MOC-业务模型]]
- [[02_业务模型/MOC-调派规模计算模型]]
- [[04_数据模型/MOC-数据模型]]
- [[05_审计与责任机制/MOC-审计与责任机制]]

## 7. 变更记录

- 2026-04-24：发布 MOC 高级应用技巧，包含动态查询、角色导向、Templater 等进阶用法