# Obsidian插件系统与知识库构建

**标签**：#Obsidian #插件 #知识库 #第二大脑
**位置**：03_SystemDesign/

---

## 插件类型

| 类型 | 说明 | 推荐 |
|------|------|------|
| 核心插件 | 官方内置（Backlinks/Graph View/Daily Notes/Canvas/Bases） | 优先使用 |
| 社区插件 | 开源贡献（2500+），需关闭安全模式安装 | 选维护活跃、高下载量 |

---

## 必备基础插件

| 插件 | 用途 | 特点 |
|------|------|------|
| **Dataview** | 动态查询（SQL/JS），生成表格/列表/任务汇总 | 下载量 Top 3 |
| **Templater** | 高级模板引擎，支持 JS 脚本，自动插入元数据 | 标准化 Wiki 模板 |
| **Tasks** | 任务管理（优先级/截止日期/重复/看板视图） | 全局任务 Wiki |
| **Calendar + Periodic Notes** | 日记/周期笔记管理 | 知识沉淀日志 |
| **Excalidraw** | 无限画布绘图（思维导图/流程图/知识地图） | 下载量长期第一 |
| **Kanban** | 看板视图，笔记转任务板/项目进度板 | 项目管理 |

---

## 知识库增强插件

| 插件 | 用途 |
|------|------|
| **Bases** | Notion 式多维数据库（表格/看板/画廊/地图），2026 杀手级功能 |
| **Tag Wrangler** | 标签管理（重命名/合并/搜索） |
| **Omnisearch** | 增强搜索（模糊/语义） |
| **Auto Note Mover** | 自动移动笔记到对应文件夹 |
| **Linter** | 自动格式化笔记（规范） |

---

## AI 与智能检索（2026 热点）

| 插件 | 用途 |
|------|------|
| **Khoj** | 本地 AI 助手，语义搜索+聊天问答 |
| **Smart Connections** | 语义连接，自动推荐相关内容 |
| **Copilot** | 集成大模型，笔记总结/生成/问答 |
| **AI Transcriber** | 语音转 Markdown，会议录音转写 |

---

## 插件组合建议

| 场景 | 插件组合 |
|------|----------|
| 轻量个人 Wiki | Dataview + Templater + Bases + Calendar + Excalidraw |
| 团队/企业知识库 | 基础 + Smart Connections + Khoj + Tasks + Kanban + 同步插件 |
| 自动化知识管理 | Templater + Dataview + Auto Note Mover + Linter |
| 进阶结构化 | Bases（数据库视图）+ Dataview（动态内容）→ 类似 Confluence/Notion |

---

## 核心原则

- **少即是多**：先安装 5-10 个核心插件，逐步添加
- **安全优先**：选官方市场插件，查看 GitHub 星标和最近更新
- **定期维护**：用 Dataview 查询过时笔记，Linter 统一格式
- **性能优化**：插件过多时分组合启用

---

## 关联文档

- [[02_Wiki知识库构建与管理]] — Wiki 知识库构建与管理
- [[01_复杂业务系统设计可视化方法]] — 复杂业务系统设计可视化方法

## 变更记录

- 2026-04-24：提取 Obsidian 插件系统与知识库构建方法