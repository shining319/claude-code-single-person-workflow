# Solution Architect / 解决方案架构师

[English](#english) | [中文](#中文)

## English

### Overview

Senior solution architect that turns product requirements into an architecture a small team can build, run and evolve. It quantifies requirements, estimates capacity, defaults to a modular monolith and PostgreSQL, picks between two stack lines, tailors a reference architecture, and delivers design docs with ADRs.

### Features

- **7-Step Workflow**: requirements → NFRs → capacity estimate → pattern and stack line → per-layer selection → deployment → design doc and ADRs
- **Two Stack Lines**: Line A (React/Vue + Java Spring Boot / Spring Cloud) and Line B (TypeScript full-stack: Next.js, Nuxt, TanStack Start, React Router, Hono, NestJS)
- **10 Reference Architectures**: MVP SaaS, TS production, TS monorepo multi-client, classic SPA + Spring Boot, Java microservices, Node BFF + Java, content sites, mainland China, AI apps (RAG/Agent), real-time/IM
- **Data Architecture**: database choice, caching, consistency and distributed transactions, multi-tenancy, scaling path, backups
- **Hosting and Deployment**: PaaS vs containers vs VPS vs K8s, CI/CD, release strategy, IaC, secrets, regions (EU / North America / China)
- **NFR, Security and Compliance**: reliability patterns, OWASP Top 10, GDPR / PIPL / ICP / PCI DSS / HIPAA, cost tiers
- **Architecture Review**: 12-point review checklist and anti-pattern list
- **Hard Rules**: every design covers auth, backups, observability, CI/CD and secrets; versions and prices are marked "needs verification"

### Installation

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/solution-architect
```

### Usage

```bash
/solution-architect "EU B2B SaaS, 5-person Java team, budget under $300/month"
/solution-architect "Next.js or Spring Boot for a mini-program + web e-commerce MVP?"
/solution-architect "review this architecture: docs/architecture.md"
```

Use this plugin when you need to:
- Design a system architecture from a PRD or an idea
- Choose a tech stack or decide monolith vs microservices
- Estimate capacity and infrastructure cost
- Plan hosting, CI/CD and releases
- Review an existing architecture

### Deliverables

- System Architecture Design Document (15 sections, Mermaid diagrams)
- Architecture Decision Records (ADRs)
- Capacity Estimate and NFR Targets
- Technology Selection Table with Rejected Alternatives
- Deployment Plan with Launch Checklist
- Cost Estimate by Stage
- Evolution Roadmap with Trigger Metrics
- Architecture Review Report

### Output File Locations

All architecture documents are saved to `outputs/<project-name>/architecture/`:

```
outputs/
└── <project-name>/
    └── architecture/
        ├── system-architecture.md      # Always
        ├── architecture-decisions.md   # Always (ADRs)
        ├── tech-stack.md               # Selection-heavy requests
        ├── deployment-plan.md          # When deployment is in scope
        └── cost-estimate.md            # When budget is a key constraint
```

**File Naming Convention:**
- Use kebab-case: `microservices-architecture.md`
- Include version/date when needed: `system-architecture-v1.1.md`

**Alternative:** Traditional project structure using `./architecture/` directory.

---

## 中文

### 概述

资深解决方案架构师，把产品需求转化为小团队能开发、能运维、能演进的系统架构。它会量化需求、估算容量，默认采用模块化单体和 PostgreSQL，在两条技术线中选型，基于参考架构裁剪方案，并输出设计文档和 ADR。

### 功能特性

- **7 步工作流**：需求澄清 → 非功能需求 → 容量估算 → 架构模式与技术线 → 分层选型 → 部署 → 设计文档与 ADR
- **两条技术线**：A 线（React/Vue + Java Spring Boot / Spring Cloud）；B 线（TypeScript 全栈：Next.js、Nuxt、TanStack Start、React Router、Hono、NestJS）
- **10 套参考架构**：MVP SaaS、TS 生产级、TS Monorepo 多端、经典前后端分离、Java 微服务、Node BFF + Java、内容站、中国大陆业务、AI 应用（RAG/Agent）、实时协作/IM
- **数据架构**：数据库选型、缓存、一致性与分布式事务、多租户、扩展路径、备份
- **托管与部署**：PaaS、容器、VPS、K8s 对比，CI/CD、发布策略、IaC、密钥、地域（欧盟/北美/中国）
- **非功能需求、安全与合规**：可靠性模式、OWASP Top 10、GDPR / PIPL / ICP 备案 / PCI DSS / HIPAA、成本分级
- **架构评审**：12 项评审检查表和反模式清单
- **硬规则**：每个方案都包含认证授权、备份、可观测性、CI/CD、密钥管理；版本和价格标注「需核验」

### 安装

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/solution-architect
```

### 使用示例

```bash
/solution-architect "面向欧盟的 B2B SaaS，Java 团队 5 人，预算每月 300 美元以内"
/solution-architect "小程序 + Web 电商 MVP，用 Next.js 还是 Spring Boot？"
/solution-architect "评审这份架构：docs/architecture.md"
```

适用场景：
- 根据 PRD 或想法设计系统架构
- 技术选型，或决定单体还是微服务
- 估算容量和基础设施成本
- 规划托管、CI/CD 和发布
- 评审现有架构

### 交付物

- 系统架构设计文档（15 节，含 Mermaid 图）
- 架构决策记录（ADR）
- 容量估算与非功能需求指标
- 分层选型表（含被否决方案）
- 部署方案与上线检查清单
- 分阶段成本估算
- 演进路线与触发指标
- 架构评审报告

### 文件输出位置

所有架构文档保存到 `outputs/<project-name>/architecture/` 目录：

```
outputs/
└── <project-name>/
    └── architecture/
        ├── system-architecture.md      # 必出
        ├── architecture-decisions.md   # 必出（ADR）
        ├── tech-stack.md               # 以选型为主的需求
        ├── deployment-plan.md          # 涉及部署时
        └── cost-estimate.md            # 预算是关键约束时
```

**文件命名规范：**
- 使用短横线命名法：`microservices-architecture.md`
- 需要时包含版本/日期：`system-architecture-v1.1.md`

**替代方案：** 传统项目结构使用 `./architecture/` 目录。

## License

MIT License
