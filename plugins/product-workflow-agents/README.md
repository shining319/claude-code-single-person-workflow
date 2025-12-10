# Product Workflow Agents / 产品工作流代理

[English](#english) | [中文](#中文)

## English

### Overview

Intelligent workflow agents that orchestrate multiple skills for complete product development. Six specialized agents work together to guide you from idea to implementation.

### Available Agents

1. **Product Manager** - Requirements analysis and PRD creation
2. **Solution Architect** - Technical architecture and tech stack selection
3. **Database Architect** - Database schema design with ER diagrams
4. **UI/UX Designer** - Interface design and specifications
5. **Technical Writer** - Documentation and technical writing
6. **Full Stack Product Builder** - End-to-end orchestrator

### How It Works

Each agent specializes in a specific domain and can be invoked automatically based on your request:

- Say "Help me define product requirements" → **Product Manager** activates
- Say "Design technical architecture" → **Solution Architect** activates
- Say "Design a database for e-commerce" → **Database Architect** activates
- Say "Design UI for my product" → **UI/UX Designer** activates
- Say "Write technical documentation" → **Technical Writer** activates
- Say "I want to build a complete product" → **Full Stack Product Builder** activates

### Full Stack Product Builder Workflow

When you use the **Full Stack Product Builder**, it orchestrates all specialized agents in sequence:

```
Your Idea
   ↓
Product Manager → PRD + User Personas
   ↓
Solution Architect → Architecture + Tech Stack
   ↓
Database Architect → Database Schema + SQL
   ↓
UI/UX Designer → Design Specs + User Flows
   ↓
Technical Writer → Documentation + Guides
   ↓
Complete Product Package
```

### Installation

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-workflow-agents
```

### Use Cases

Perfect for:
- **Solo Entrepreneurs**: Build complete products systematically
- **Technical Founders**: Transform ideas into documented systems
- **Product Teams**: Maintain consistency across all deliverables
- **Developers**: Get comprehensive product specifications

### Output File Locations

All workflow deliverables are organized in `outputs/<project-name>/` with complete project structure:

```
outputs/
└── <project-name>/
    ├── docs/                    # Product documentation
    ├── architecture/            # Technical architecture
    ├── database/                # Database design
    ├── design/                  # UI/UX design
    └── writing/                 # Technical documentation
```

**File Naming Convention:**
- Use kebab-case for all files
- Include version/date when needed
- Use descriptive names

**Alternative:** Traditional project structure using `./docs/`, `./database/`, `./design/`, `./architecture/` directories.

---

## 中文

### 概述

智能工作流代理，编排多个技能完成完整的产品开发。六个专业代理协同工作，引导您从创意到实现。

### 可用代理

1. **产品经理** - 需求分析和PRD创建
2. **解决方案架构师** - 技术架构和技术栈选择
3. **数据库架构师** - 数据库架构设计和ER图
4. **UI/UX设计师** - 界面设计和规格说明
5. **技术文档专家** - 文档和技术写作
6. **全栈产品构建者** - 端到端编排

### 工作原理

每个代理专注于特定领域，并根据您的请求自动调用：

- 说"帮我定义产品需求" → **产品经理**激活
- 说"设计技术架构" → **解决方案架构师**激活
- 说"为电商设计数据库" → **数据库架构师**激活
- 说"为我的产品设计UI" → **UI/UX设计师**激活
- 说"编写技术文档" → **技术文档专家**激活
- 说"我想构建一个完整产品" → **全栈产品构建者**激活

### 全栈产品构建者工作流

当您使用**全栈产品构建者**时，它会按顺序编排所有专业代理：

```
您的想法
   ↓
产品经理 → PRD + 用户画像
   ↓
解决方案架构师 → 架构 + 技术栈
   ↓
数据库架构师 → 数据库架构 + SQL
   ↓
UI/UX设计师 → 设计规格 + 用户流程
   ↓
技术文档专家 → 文档 + 指南
   ↓
完整产品包
```

### 安装

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-workflow-agents
```

### 使用场景

非常适合：
- **独立创业者**: 系统化地构建完整产品
- **技术创始人**: 将想法转化为有文档的系统
- **产品团队**: 保持所有交付物的一致性
- **开发者**: 获得全面的产品规格

### 文件输出位置

所有工作流交付物按完整项目结构组织在 `outputs/<project-name>/` 目录下：

```
outputs/
└── <project-name>/
    ├── docs/                    # 产品文档
    ├── architecture/            # 技术架构
    ├── database/                # 数据库设计
    ├── design/                  # UI/UX 设计
    └── writing/                 # 技术文档
```

**文件命名规范：**
- 所有文件使用短横线命名法
- 需要时包含版本/日期
- 使用描述性名称

**替代方案：** 传统项目结构使用 `./docs/`、`./database/`、`./design/`、`./architecture/` 目录。

## License

MIT License
