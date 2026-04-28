# IntelligenceForge v13.0 模块关系图

**标签**：#模块关系 #Mermaid #流程图 #IntelligenceForge
**位置**：03_SystemDesign/

---

## Mermaid 代码

```mermaid
flowchart LR
    %% 模块定义
    A[1. 知识采集与摄入模块]
    B[2. 知识编译与维护模块]
    C[3. 知识查询与交互模块]
    D[4. 持久记忆与状态模块]
    E[5. 执行护栏与伦理模块]
    F[6. 框架生成与自优化模块]
    G[7. 可视化与人机飞轮模块]

    %% 底层支撑
    VKFS[VKFS 虚拟知识文件系统\n底层支撑]

    %% 输入流
    A -->|原始材料| B
    A -->|Web Clipper| B

    %% 编译与记忆
    B -->|结构化Wiki| D
    B -->|回写| D

    %% 查询执行流
    C -->|复杂查询| E
    C -->|自动路由| E

    %% 护栏与执行
    E -->|安全审批 + 高效路由| F
    D -->|持久状态 + 连续谱| E
    D -->|上下文| C

    %% 自优化与输出
    F -->|harness-creator| B
    F -->|AGENTS.md 优化| C
    C -->|idea file 输出| B
    C -->|可复用输出| outputs[最终产出]

    %% 人机飞轮与反馈
    G -->|Dashboard + 粒子UI| C
    G -->|Weekly Checklist| human[人类最终判断]
    human -->|架构决策 + 品味| F
    human -->|签字确认| E

    %% 循环与进化
    B -.->|知识越查越厚| D
    F -.->|自修复 + Lint| B
    G -.->|可视化反馈| human

    %% 样式
    classDef input fill:#e3f2fd,stroke:#1976d2
    classDef core fill:#f3e5f5,stroke:#7b1fa2
    classDef guard fill:#ffebee,stroke:#c62828
    classDef human fill:#e8f5e9,stroke:#388e3c

    class A input
    class B,C,D core
    class E guard
    class G,F human
    class human human

    subgraph "IntelligenceForge v13.0 模块关系图"
        direction TB
        A --> B --> D --> E --> F --> C
    end
```

---

## 关系说明

| 流向 | 说明 |
|------|------|
| **输入流** | A(采集) → B(编译) → D(记忆) |
| **执行流** | C(查询) → E(护栏) → F(框架优化) |
| **输出流** | C 输出 idea file → B 回写 Wiki |
| **反馈进化** | G(可视化) → 人类决策 → F 自优化 → 全系统进化 |
| **底层** | VKFS 贯穿 B/C/D |

---

## 使用方式

- **Obsidian**：安装 Mermaid 插件，复制代码到 `.md` 文件，切换阅读视图
- **在线工具**：mermaid.live 直接渲染

---

## 关联文档

- [[16_IntelligenceForge功能模块划分]] — 功能模块划分
- [[15_IntelligenceForge产品价值点矩阵]] — 产品价值点矩阵

## 变更记录

- 2026-04-24：提取 IntelligenceForge v13.0 模块关系图（Mermaid）