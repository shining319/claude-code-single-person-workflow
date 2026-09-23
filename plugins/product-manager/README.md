# Product Manager / 产品经理

[English](#english) | [中文](#中文)

## English

### Overview

Senior product manager that turns an idea into two documents with a fixed structure: a **PRD** and a **Task Backlog**. The PRD says what to build, for whom and in which order; the Task Backlog breaks every user story into backend and frontend tasks with hours and dependencies.

### Features

- **PRD (11 sections)**: product overview, scope and assumptions, success metrics, user personas, epics and user stories with acceptance criteria and story points, core flows, priority matrix, NFRs (including accessibility and privacy), technical architecture, sprint planning, definition of done, risks, open questions, next steps
- **Task Backlog**: backend (B*) and frontend (F*) tasks per story with acceptance criteria, hours and dependencies; sprint summaries; Critical Path & Start Order (start-now tasks, cross-role blockers, critical path hours); API endpoint list
- **Self-check**: epic points equal the sum of their stories, sprint and hour totals add up, backlog frameworks match the PRD, every dependency ID exists
- **Language**: follows your language; Chinese output translates headings and keeps IDs and API paths unchanged

### ⚠️ Recommended Order: PRD First, Task Backlog Last

The Task Backlog names real frameworks, tables and API paths, so it needs **three prerequisites**:

1. Architecture design document (`/solution-architect`)
2. Database design document (`/database-designer`)
3. Completed PRD (Section 6 "Technical Architecture" filled in)

```
/product-manager "your idea"          → prd.md (Section 6 = placeholders if no stack is given)
/solution-architect "prd.md"          → architecture document
/database-designer "prd.md + architecture"  → database design
/product-manager "prd.md + architecture + database design"  → PRD Section 6 filled + task-backlog.md
```

- If you give no architecture document and no tech stack, PRD Section 6 is written as placeholders marked **"pending architecture design"**. Nothing is guessed.
- Every PRD ends with Section 11 "Next Steps: Task Backlog", a checklist of the three prerequisites.
- If you ask for the backlog before all three exist, the plugin tells you what is missing instead of generating it.

### Installation

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-manager
```

### Usage

```bash
/product-manager "newsstand inventory and sales system, 2 developers, two 3-week sprints"
/product-manager "generate the task backlog from docs/prd.md, architecture/system-architecture.md and database/schema-design.md"
```

### Deliverables

- `prd.md`: Product Requirements Document
- `task-backlog.md`: Task Backlog (after the three prerequisites)

### Output File Locations

```
outputs/
└── <project-name>/
    └── docs/
        ├── prd.md             # always
        └── task-backlog.md    # after architecture + database design + completed PRD
```

**Alternative:** Traditional project structure using `./docs/` directory.

---

## 中文

### 概述

资深产品经理，把一个想法变成两份结构固定的文档：**PRD** 和**任务 Backlog**。PRD 说明做什么、给谁用、按什么顺序做；Backlog 把每个用户故事拆成前后端任务，并写清工时和依赖。

### 功能特性

- **PRD（11 章）**：产品概述、范围与假设、成功指标、用户画像、Epic 与用户故事（验收标准、故事点）、核心流程、优先级矩阵、非功能需求（含无障碍与隐私）、技术架构、Sprint 规划、完成定义、风险、待确认问题、下一步
- **任务 Backlog**：每个故事拆成后端（B*）和前端（F*）任务，写明验收标准、工时和依赖；每个 Sprint 有工时汇总；关键路径与开工顺序（立即可做的任务、跨角色阻塞、关键路径工时）；API 接口清单
- **自检**：Epic 故事点等于其下故事之和，Sprint 和工时合计正确，Backlog 用到的框架与 PRD 一致，依赖 ID 都存在
- **语言**：跟随你的语言；中文输出时标题翻译，ID 和 API 路径保持不变

### ⚠️ 推荐顺序：先出 PRD，最后出任务 Backlog

任务 Backlog 里会写真实的框架、表名和 API 路径，所以需要**三项前置条件**：

1. 架构设计文档（`/solution-architect`）
2. 数据库设计文档（`/database-designer`）
3. 完善后的 PRD（第 6 章「技术架构」已填写）

```
/product-manager "你的想法"            → prd.md（未指定技术栈时第 6 章为占位符）
/solution-architect "prd.md"          → 架构文档
/database-designer "prd.md + 架构文档"  → 数据库设计
/product-manager "prd.md + 架构文档 + 数据库设计"  → 回填 PRD 第 6 章 + 生成 task-backlog.md
```

- 如果你没有提供架构文档，也没有指定技术栈，PRD 第 6 章会写成占位符，并标注**「等待架构设计后补充」**，不做任何猜测。
- 每份 PRD 的最后一章是「下一步：任务 Backlog」，列出三项前置条件的完成状态。
- 如果三项前置条件没有全部满足就要求生成 Backlog，插件会告诉你还缺什么，不会直接生成。

### 安装

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-manager
```

### 使用示例

```bash
/product-manager "报刊亭库存与销售系统，2 名开发，两个 3 周的 Sprint"
/product-manager "根据 docs/prd.md、architecture/system-architecture.md 和 database/schema-design.md 生成任务 Backlog"
```

### 交付物

- `prd.md`：产品需求文档
- `task-backlog.md`：任务 Backlog（三项前置条件满足后）

### 文件输出位置

```
outputs/
└── <project-name>/
    └── docs/
        ├── prd.md             # 始终生成
        └── task-backlog.md    # 架构文档、数据库设计、完善后的 PRD 齐全后生成
```

**替代方案：** 传统项目结构使用 `./docs/` 目录。

## License

MIT License
