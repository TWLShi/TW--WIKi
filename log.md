---
title: Wiki Log
---

# Wiki Log

- [2026-04-30] INIT vault_path="/Users/lx/Documents/TW--WIKi" categories=PARA-style (Projects, Areas, Resources, MOCs, Inbox)
- [2026-04-30] ADD dirs=concepts,entities,skills,references,synthesis,journal,_archives,_raw
- [2026-04-30] INGEST mode=full total_sources=6 total_pages=200+ notes="FireDispatchEngine项目知识库，包含12步调派流程、多智能体架构、审计责任体系"
- [2026-04-30] REORGANIZE non-wiki-template files into projects/ structure: Parts/, Scenes/, Steps/, Others/
- [2026-04-30] RENAME all directories and files to Chinese
- [2026-04-30] MOVE four folders from projects/ to root level (其他资料, 系统Parts, 场景枢纽, 核心流程)
- [2026-04-30] GROUP wiki template folders into wiki模板/ directory
- [2026-04-30] RENAME: 系统Parts → 四个Part, 核心流程 → 十二个流程, 场景枢纽 → 六个场景聚类
- [2026-04-30] REORDER directories: 四个Part, 十二个流程, 六个场景聚类, 其他资料
- [2026-04-30] LINT issues_found=370+ orphans=?, broken_links=1536, stale=?, contradictions=?, prov_issues=?, missing_summary=370, fragmented_clusters=?
  - WARNING: 81% of files (370/454) missing frontmatter
  - WARNING: 1536+ wikilinks pointing to old paths (need update after directory rename)
- [2026-04-30] WIKILINKS FIXED: Replaced 1536+ old path references (01_Projects/, 05_MOCs/, etc.) with new Chinese paths
- [2026-04-30] FRONTMATTER ADDED: Added frontmatter to 370 files (all 454 files now have frontmatter)
- [2026-05-06] LLM_WIKI_INIT: Reorganized into wiki/ folder - 01-Part、02-Step、03-Scene、版本管理、其他类、原始材料 moved to wiki/ subfolder
- [2026-05-06] REORG: 需求/ directory reorganized with new folders (调派核心模型, 约束校验, 问题路由, 多智能体架构, AI流程, 火灾预测, 审计体系, 责任机制)
- [2026-05-06] INGEST: _raw/语义/ PDFs → 需求/ subdirectories, 10+ new pages created
- [2026-05-13] INGEST source="llm-wiki-base/_raw/应急响应与调度指挥手册-天津.pdf" pages_created=8 pages_updated=0 mode=ocr notes="天津消防应急响应与调度指挥手册（158页扫描件OCR提取），7章24节"
- [2026-05-13] EXPAND pages_updated=7 mode=content-expansion notes="根据用户反馈'生成的内容不完整'，重新基于完整OCR文本扩展所有7个章节页面，增加原始文档完整话术脚本、规范用语、调度矩阵、信息报送模板、车辆分布明细等原始内容。清理临时OCR文件（ch_*.txt、OCR输出目录、Swift脚本）"
