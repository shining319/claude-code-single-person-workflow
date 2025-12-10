# Solution Architect / 解决方案架构师

[English](#english) | [中文](#中文)

## English

### Overview

Solution architect for technical architecture design, technology selection, and deployment planning. Transform product requirements into practical, scalable technical architectures.

### Features

- **Architecture Design**: System architecture and component design
- **Technology Selection**: Tech stack recommendations with trade-off analysis
- **Deployment Planning**: Cloud platform comparison and infrastructure design
- **Cost Estimation**: Development and operational cost analysis
- **Best Practices**: Pragmatic, team-friendly technology choices

### Installation

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/solution-architect
```

### Usage

Use this plugin when you need to:
- Design technical architecture
- Choose technology stack
- Plan deployment strategy
- Review existing architecture
- Estimate infrastructure costs

### Deliverables

- Technical Architecture Design Document
- System Architecture Diagram
- Technology Stack Recommendations
- Deployment Architecture
- Cloud Platform Comparison
- Cost Estimates
- Architecture Decision Records (ADRs)

### Output File Locations

All architecture documents are saved to `outputs/<project-name>/architecture/`:

```
outputs/
└── <project-name>/
    └── architecture/
        ├── system-architecture.md
        ├── tech-stack.md
        ├── deployment-plan.md
        └── architecture-decisions.md
```

**File Naming Convention:**
- Use kebab-case: `microservices-architecture.md`
- Include version/date when needed: `system-architecture-v1.0.md`
- Use descriptive names: `e-commerce-deployment-plan.md`

**Alternative:** Traditional project structure using `./architecture/` directory.

---

## 中文

### 概述

解决方案架构师，负责技术架构设计、技术选型和部署规划。将产品需求转化为实用、可扩展的技术架构。

### 功能特性

- **架构设计**: 系统架构和组件设计
- **技术选型**: 技术栈推荐及权衡分析
- **部署规划**: 云平台对比和基础设施设计
- **成本估算**: 开发和运维成本分析
- **最佳实践**: 务实、团队友好的技术选择

### 安装

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/solution-architect
```

### 使用场景

当您需要以下帮助时使用此插件：
- 设计技术架构
- 选择技术栈
- 规划部署策略
- 评审现有架构
- 估算基础设施成本

### 交付物

- 技术架构设计文档
- 系统架构图
- 技术栈推荐
- 部署架构
- 云平台对比
- 成本估算
- 架构决策记录（ADRs）

### 文件输出位置

所有架构文档保存到 `outputs/<project-name>/architecture/` 目录：

```
outputs/
└── <project-name>/
    └── architecture/
        ├── system-architecture.md
        ├── tech-stack.md
        ├── deployment-plan.md
        └── architecture-decisions.md
```

**文件命名规范：**
- 使用短横线命名法：`microservices-architecture.md`
- 需要时包含版本/日期：`system-architecture-v1.0.md`
- 使用描述性名称：`e-commerce-deployment-plan.md`

**替代方案：** 传统项目结构使用 `./architecture/` 目录。

## License

MIT License
