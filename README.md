# Single Person Workflow Marketplace

**[English](#english) | [中文](#中文)**

<p align="center">
  <strong>Comprehensive Claude Code plugin marketplace for solo developers and creators</strong>
</p>

<p align="center">
  <a href="#installation">Installation</a> •
  <a href="#plugins">Plugins</a> •
  <a href="#documentation">Documentation</a> •
  <a href="#license">License</a>
</p>

---

## English

### Overview

A curated collection of Claude Code plugins designed specifically for single-person product development workflows. From writing documentation to designing databases, from product management to UI/UX design and solution architecture - everything you need in one marketplace.

### Features

- 🎯 **Specialized Skills**: 6 focused plugins for specific tasks
- 📦 **All-in-One Suite**: Complete toolkit in one installation
- 🤖 **Intelligent Agents**: 7 workflow agents for automated orchestration
- 🌏 **Bilingual Support**: Full Chinese and English documentation
- 🚀 **Production-Ready**: Battle-tested workflows and best practices

### Available Plugins

| Plugin | Description | Type |
|--------|-------------|------|
| **[academic-writing](plugins/academic-writing)** | Professional academic writing for Chinese and English | Skill |
| **[database-designer](plugins/database-designer)** | Complete database schema design with ER diagrams | Skill |
| **[product-manager](plugins/product-manager)** | Requirements analysis and PRD creation | Skill |
| **[ui-designer](plugins/ui-designer)** | UI/UX design with detailed specifications | Skill |
| **[solution-architect](plugins/solution-architect)** | Technical architecture and deployment planning | Skill |
| **[ui-ux-pro-max](plugins/ui-ux-pro-max)** | Data-driven UI/UX design intelligence with searchable knowledge base | Skill |
| **[product-development-suite](plugins/product-development-suite)** | All skills in one package | Suite |
| **[product-workflow-agents](plugins/product-workflow-agents)** | 7 intelligent workflow agents | Agents |

### Quick Start

#### Install Individual Plugin

```bash
# Install a specific skill
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

#### Install All-in-One Suite

```bash
# Get all skills at once
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-development-suite
```

#### Install Workflow Agents

```bash
# Get intelligent workflow orchestration
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-workflow-agents
```

#### Install Entire Marketplace

```bash
# Install everything
claude plugin install github:shining319/claude-code-single-person-workflow
```

### How to Use

Once installed, you can activate skills in two ways:

#### Method 1: Natural Language (Automatic)
Simply describe what you need:

- "Design a database for an e-commerce system" → Database Designer activates
- "Create a PRD for my mobile app" → Product Manager activates
- "Design the UI for my dashboard" → UI Designer activates
- "Help me choose a tech stack" → Solution Architect activates
- "Write technical documentation" → Academic Writing activates
- "I want to build a complete product" → Full Stack Product Builder orchestrates everything

#### Method 2: Slash Commands (Explicit)
Use direct commands for guaranteed activation:

**Individual Plugin Commands:**
```bash
/database-designer "e-commerce system with products, orders, payments"
/product-manager "mobile fitness tracking app"
/ui-designer "user dashboard with analytics widgets"
/solution-architect "microservices architecture for real-time chat"
/academic-writing "technical report on cloud computing"
/ui-ux-pro-max "design a SaaS dashboard with glassmorphism style"
```

**Suite Plugin Commands (spw = single-person workflow):**
```bash
/spw-db "blog database with users, posts, comments"
/spw-prd "task management application"
/spw-ui "admin panel interface"
/spw-arch "SaaS platform architecture"
/spw-writing "research paper on AI ethics"
/spw-ui-pro-max "color palette for healthcare SaaS application"
```

**Workflow Command:**
```bash
/build-dev-workflow "complete e-commerce platform with payment integration"
```

> **Tip:** Slash commands provide faster, more precise skill activation compared to natural language.

### Quick Command Reference

| Task | Individual Command | Suite Command |
|------|-------------------|---------------|
| Database Design | `/database-designer [requirements]` | `/spw-db [requirements]` |
| Product Requirements | `/product-manager [idea]` | `/spw-prd [idea]` |
| UI/UX Design | `/ui-designer [page/feature]` | `/spw-ui [page/feature]` |
| Architecture Design | `/solution-architect [system]` | `/spw-arch [system]` |
| Academic Writing | `/academic-writing [topic]` | `/spw-writing [topic]` |
| Data-Driven Design | `/ui-ux-pro-max [design query]` | `/spw-ui-pro-max [design query]` |
| Full Workflow | `/build-dev-workflow [product description]` | — |

**Note on Data-Driven Design Commands:**
- `/ui-ux-pro-max` invokes the **skill** directly (lightweight, quick design queries)
- `/spw-ui-pro-max` invokes the **agent** workflow (comprehensive 4-phase process: Requirements → Search → Framework Guidance → Recommendations)

### Output File Locations

All generated files are organized in `outputs/<project-name>/` directory:

```
outputs/
└── <project-name>/              # Your project name (e.g., my-saas-platform)
    ├── docs/                    # Product documentation
    ├── architecture/            # Technical architecture
    ├── database/                # Database design
    ├── design/                  # UI/UX design
    └── writing/                 # Academic/technical writing
```

**Example:**
```
outputs/
└── my-saas-platform/
    ├── docs/prd.md
    ├── database/schema.sql
    └── design/ui-specification.md
```

**Advantages:**
- ✅ Each project isolated in its own directory
- ✅ Easy cleanup and management
- ✅ Automation-friendly for scripting
- ✅ Follows Claude Code official standards

**Alternative:** Traditional structure using `./docs/`, `./database/`, `./design/`, `./architecture/` directories.

For details, see [User Guide](docs/en/user-guide.md#saving-output).

### Documentation

- [Installation Guide](docs/en/installation.md)
- [User Guide](docs/en/user-guide.md)
- [Architecture](docs/en/architecture.md)

### Who Is This For?

- **Solo Entrepreneurs**: Building complete products alone
- **Technical Founders**: Need comprehensive product specifications
- **Indie Developers**: Want professional-grade deliverables
- **Product Designers**: Require end-to-end design workflows
- **Technical Writers**: Need structured documentation support

---

## 中文

### 概述

专为单人产品开发工作流设计的 Claude Code 插件精选集合。从编写文档到设计数据库，从产品管理到UI/UX设计和解决方案架构 - 您需要的一切都在一个市场中。

### 功能特性

- 🎯 **专业技能**: 6个专注于特定任务的插件
- 📦 **一体化套件**: 一次安装即获得完整工具包
- 🤖 **智能代理**: 7个工作流代理用于自动编排
- 🌏 **双语支持**: 完整的中英文文档
- 🚀 **生产就绪**: 经过实战检验的工作流和最佳实践

### 可用插件

| 插件 | 描述 | 类型 |
|------|------|------|
| **[academic-writing](plugins/academic-writing)** | 中英文专业学术写作 | 技能 |
| **[database-designer](plugins/database-designer)** | 完整的数据库架构设计和ER图 | 技能 |
| **[product-manager](plugins/product-manager)** | 需求分析和PRD创建 | 技能 |
| **[ui-designer](plugins/ui-designer)** | UI/UX设计及详细规格 | 技能 |
| **[solution-architect](plugins/solution-architect)** | 技术架构和部署规划 | 技能 |
| **[ui-ux-pro-max](plugins/ui-ux-pro-max)** | 数据驱动的UI/UX设计智能，含可搜索的知识库 | 技能 |
| **[product-development-suite](plugins/product-development-suite)** | 所有技能合一 | 套件 |
| **[product-workflow-agents](plugins/product-workflow-agents)** | 7个智能工作流代理 | 代理 |

### 快速开始

#### 安装单个插件

```bash
# 安装特定技能
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

#### 安装一体化套件

```bash
# 一次获得所有技能
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-development-suite
```

#### 安装工作流代理

```bash
# 获取智能工作流编排
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-workflow-agents
```

#### 安装整个市场

```bash
# 安装所有内容
claude plugin install github:shining319/claude-code-single-person-workflow
```

### 如何使用

安装后,您可以通过两种方式激活技能:

#### 方法一:自然语言(自动)
只需描述您的需求:

- "为电商系统设计数据库" → 数据库设计器激活
- "为我的移动应用创建PRD" → 产品经理激活
- "为我的仪表板设计UI" → UI设计师激活
- "帮我选择技术栈" → 解决方案架构师激活
- "编写技术文档" → 学术写作激活
- "我想构建一个完整产品" → 全栈产品构建者编排一切

#### 方法二:斜杠命令(显式)
使用直接命令以保证激活:

**单个插件命令:**
```bash
/database-designer "包含商品、订单、支付的电商系统"
/product-manager "移动健身追踪应用"
/ui-designer "包含分析小部件的用户仪表板"
/solution-architect "实时聊天的微服务架构"
/academic-writing "关于云计算的技术报告"
/ui-ux-pro-max "为SaaS仪表板设计玻璃拟态风格"
```

**套件插件命令 (spw = 单人工作流):**
```bash
/spw-db "包含用户、文章、评论的博客数据库"
/spw-prd "任务管理应用"
/spw-ui "管理面板界面"
/spw-arch "SaaS平台架构"
/spw-writing "关于AI伦理的研究论文"
/spw-ui-pro-max "医疗SaaS应用配色方案"
```

**工作流命令:**
```bash
/build-dev-workflow "具有支付集成的完整电商平台"
```

> **提示:** 与自然语言相比,斜杠命令提供更快速、更精确的技能激活。

### 快速命令参考

| 任务 | 单个插件命令 | 套件命令 |
|------|------------|---------|
| 数据库设计 | `/database-designer [需求]` | `/spw-db [需求]` |
| 产品需求 | `/product-manager [想法]` | `/spw-prd [想法]` |
| UI/UX设计 | `/ui-designer [页面/功能]` | `/spw-ui [页面/功能]` |
| 架构设计 | `/solution-architect [系统]` | `/spw-arch [系统]` |
| 学术写作 | `/academic-writing [主题]` | `/spw-writing [主题]` |
| 数据驱动设计 | `/ui-ux-pro-max [设计查询]` | `/spw-ui-pro-max [设计查询]` |
| 完整工作流 | `/build-dev-workflow [产品描述]` | — |

**数据驱动设计命令说明：**
- `/ui-ux-pro-max` 直接调用 **skill**（轻量级，快速设计查询）
- `/spw-ui-pro-max` 调用 **agent** 工作流（完整4阶段流程：需求分析 → 设计搜索 → 框架指导 → 推荐输出）

### 文件输出位置

所有生成的文件组织在 `outputs/<project-name>/` 目录中：

```
outputs/
└── <project-name>/              # 您的项目名称（如：my-saas-platform）
    ├── docs/                    # 产品文档
    ├── architecture/            # 技术架构
    ├── database/                # 数据库设计
    ├── design/                  # UI/UX 设计
    └── writing/                 # 学术/技术写作
```

**示例：**
```
outputs/
└── my-saas-platform/
    ├── docs/prd.md
    ├── database/schema.sql
    └── design/ui-specification.md
```

**优势：**
- ✅ 每个项目独立目录隔离
- ✅ 易于清理和管理
- ✅ 适合自动化脚本处理
- ✅ 遵循 Claude Code 官方标准

**替代方案：** 使用传统结构 `./docs/`、`./database/`、`./design/`、`./architecture/` 目录。

详情请参阅[用户指南](docs/zh/user-guide.md#保存输出)。

### 文档

- [安装指南](docs/zh/installation.md)
- [用户指南](docs/zh/user-guide.md)
- [架构说明](docs/zh/architecture.md)

### 适用人群

- **独立创业者**: 独自构建完整产品
- **技术创始人**: 需要全面的产品规格
- **独立开发者**: 想要专业级交付物
- **产品设计师**: 需要端到端设计工作流
- **技术文档工程师**: 需要结构化文档支持

---

## License

MIT License - See [LICENSE](LICENSE) for details

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history and updates.

---

<p align="center">
  Made with ❤️ for solo developers and creators
</p>
