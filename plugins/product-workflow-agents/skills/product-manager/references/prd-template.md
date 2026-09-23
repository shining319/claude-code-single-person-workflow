# PRD 模板

PRD 固定为 11 章，结构以 `Example_PRD` 为准，并增补了 4 处：1.4、每个 P0 Epic 的 Core flow、5.5、第 10 章。第 11 章「Next Steps」固定存在，用来告诉读者 Task Backlog 的前置条件。

- 章节编号必须连续，不能跳号
- 用户用中文提需求时，标题按文末的对照表翻译；Epic ID、Story 编号、SP、API 路径、代码标识保持原样
- 骨架中 `<...>` 是填写说明，`[TBD ...]` 是允许保留在成品中的占位符

---

## 一、骨架

```markdown
# Product Requirements Document (PRD)

# <Product Name>

> **Status:** Draft — Technical Architecture pending; Task Backlog not yet generated
> **Version:** 0.1 | **Last updated:** <YYYY-MM-DD>

---

## 1. Product Overview

### 1.1 Product Positioning

<一段话：产品是什么、给谁用、解决什么问题。技术栈未定时不要在这里写技术名词。>

### 1.2 Business Goals

- **Primary goal**: <...>
- **Secondary goal**: <...>
- **Long-term goal**: <...>

### 1.3 Constraints

- **Time constraint**: <MVP 期限，如 "MVP in 2 sprints (6 weeks)">
- **Team constraint**: <人数与角色，如 "2 developers (1 backend + 1 frontend)" 或 "1 full-stack developer">
- **Technical constraint**: <用户指定的技术约束；没有就写 "None specified — see Section 6">
- **Budget constraint**: <...>

### 1.4 Out of Scope & Assumptions

**Out of scope (this release):**

- <本期明确不做的功能，与第 4 章 P2 对应>

**Assumptions:**

- <估算和设计所依据的假设，如 "Single store, single currency (EUR)">

### 1.5 Success Metrics

- <可度量指标，每条都带数字或比例>

---

## 2. User Persona

### 2.1 Primary User: <角色名>

**Basic information:**

- Age: <...>
- Occupation: <...>
- Technical proficiency: <Low / Average / High + 一句说明>

**Goals & motivations:**

- <...>

**Pain points & challenges:**

- <...>

**Behavioral traits:**

- <...>

### 2.2 Secondary User: <角色名>（可选，有第二类用户时才写）

---

## 3. Epic Breakdown & Prioritization

### Epic Overview

| Epic ID | Epic Name | Priority | Story Points | Target Sprint |
| --- | --- | --- | --- | --- |
| E001 | <...> | P0 | <= 该 Epic 下 Story SP 之和> | Sprint 1 |

### Epic 1: <Epic Name> (E001)

**Priority: P0 - Blocking** | **Sprint 1**

**Epic description:**
<这个 Epic 做什么、为什么是基础。>

**User value:**

- <...>

**Core flow:**（仅 P0 Epic）

1. <主流程第 1 步>
2. <...>（3–6 步）

- **Exception:** <异常分支及系统表现>

---

#### User Story 1.1: <Story Name>

**As a** <角色>
**I want to** <行为>
**So that** <价值>

**Acceptance criteria:**

- [ ]  <可验证的一条行为或规则>

**Story Points:** <1/2/3/5/8>
**Priority:** <P0/P1/P2>

---

## 4. Feature Priority Matrix

### P0 - Blocking (MVP required)

- <Epic 或 Story>

### P1 - High Priority

- <...>

### P2 - Medium Priority (future iterations)

- <...>

---

## 5. Non-Functional Requirements

### 5.1 Performance Requirements

### 5.2 Security Requirements

### 5.3 Usability Requirements

### 5.4 Compatibility Requirements

### 5.5 Accessibility & Privacy

---

## 6. Technical Architecture

<两种写法二选一，见下文「第 6 章写法」>

---

## 7. Sprint Planning

### Sprint 1 (Week 1–3): <主题>

**Goal:** <...>

| User Story | Story Points | Cumulative |
| --- | --- | --- |
| US 1.1: <...> | 3 | 3 |

**Sprint 1 total story points:** <= 最后一行 Cumulative>

---

## 8. Definition of Done

### Code level

### Testing level

### Documentation level

### Deployment level

---

## 9. Risks & Dependencies

### 9.1 Risks

| Risk | Impact | Probability | Mitigation |
| --- | --- | --- | --- |

### 9.2 Dependencies

- <...>

---

## 10. Open Questions

| # | Question | Owner | Affects | Needed by |
| --- | --- | --- | --- | --- |
| Q1 | <...> | <Product owner / Developer> | <US 2.7> | <Sprint 2 planning> |

---

## 11. Next Steps: Task Backlog

<固定内容，见下文「第 11 章写法」>
```

---

## 二、各章写作规则

### 状态行

- 只要第 6 章还是占位符，状态就写 `Draft — Technical Architecture pending; Task Backlog not yet generated`
- 在 Backlog 模式下回填第 6 章之后，改成 `Ready — Architecture confirmed; Task Backlog generated (see task-backlog.md)`，并更新 Version 和日期

### 1.x 概述

- 1.3 Team constraint 必须写清角色，因为 Backlog 按角色分配任务
- 1.4 Out of scope 要和第 4 章的 P2 呼应；Assumptions 里每一条都应能在后续被证实或推翻，推翻风险大的同时写进第 10 章
- 1.5 Success Metrics 每条都要可测，不写「用户体验好」这类说法

### 2. 用户画像

- 至少 1 个画像，四个小节齐全。Behavioral traits 要能推导出设计决策，例如「Easily interrupted」推导出「操作可随时中断且不丢数据」
- 需要更细的画像时参考 `user-persona-templates.md`

### 3. Epic 与 User Story

- Epic ID 用 `E001` 递增；Story 编号用 `<Epic 序号>.<Story 序号>`
- Epic Overview 表的 Story Points **必须等于**该 Epic 下所有 Story 的 SP 之和（Example 中 E001 写 40、实际只有 21，这种错误不允许出现）
- Story Points 只用 1 / 2 / 3 / 5 / 8。估到 13 及以上时拆成多个 Story
- 验收标准每条只写一件可验证的事，写行为和规则（校验、边界、空状态、错误提示），不写实现方式
- 每个 Story 至少覆盖：正常路径、一条校验或边界、一条反馈（成功或失败提示）
- Core flow 只给 P0 Epic 写，主流程 3–6 步，异常分支单独列出；它是 UI 和数据库设计的直接输入

### 4. 优先级矩阵

- P0：不做就无法上线；P1：重要，可以晚一个 Sprint；P2：本期不做，放进未来迭代
- 单个 Story 的优先级和所在 Epic 不同时（例如 P0 Epic 里的 P1 Story），在这里单独列出

### 5. 非功能需求

- 5.1–5.4 都写可测数字（例如「API response time < 500ms」）
- 5.5 Accessibility & Privacy 按产品需要写，至少考虑：
  - 可访问性：对比度、字号、键盘操作、屏幕阅读器标签、触控目标尺寸
  - 友好反馈：错误提示说明原因和下一步，不责怪用户
  - 隐私：只收集必要数据、授权说明、用户可导出或删除自己的数据；涉及个人数据时注明 GDPR / PIPL 等适用法规
- 产品确实不涉及个人数据时，写一句 "No personal data is collected beyond ..."，不要整节删除

### 6. Technical Architecture（两种写法）

**写法 A：已有架构文档，或用户明确指定了技术栈**

```markdown
## 6. Technical Architecture

> Source: `architecture/system-architecture.md` (solution-architect, <YYYY-MM-DD>)

### 6.1 Backend Technology Stack

- **Framework:** Spring Boot 4.x
- **Database:** MySQL 8.4 LTS
- **ORM:** MyBatis-Plus
- **Build tool:** Maven

### 6.2 Frontend Technology Stack

- **Framework:** Vue 3 + Vite
- **UI component library:** Element Plus
- **State management:** Pinia
- **HTTP client:** Axios

### 6.3 API Design Principles

- RESTful API, unified response format, error code standards, API versioning
```

- 只写主版本号；版本来自架构文档或用户，不自己编。需要自己写版本时标「需核验」和核验日期
- 这里出现的每个框架都必须和 Backlog 任务中使用的一致（Example 中 PRD 写 React + MobX，Backlog 却用 Vue + Pinia，这是错误）

**写法 B：没有架构文档，用户也没指定技术栈（默认）**

```markdown
## 6. Technical Architecture

> ⚠️ **Pending — to be completed after architecture design.**
> No architecture document or technology stack has been provided yet. Every item below is a placeholder.
> Run `/solution-architect` (or `/spw-arch`) with this PRD, then update this section before generating the Task Backlog.

### 6.1 Backend Technology Stack

- **Framework:** _[TBD — pending architecture design]_
- **Database:** _[TBD — pending architecture design]_
- **ORM / data access:** _[TBD — pending architecture design]_
- **Build tool:** _[TBD — pending architecture design]_

### 6.2 Frontend Technology Stack

- **Framework:** _[TBD — pending architecture design]_
- **UI component library:** _[TBD — pending architecture design]_
- **State management:** _[TBD — pending architecture design]_

### 6.3 API Design Principles

- _[TBD — pending architecture design]_
```

- 不猜技术栈，也不写「推荐使用 XX」
- 用户只指定了部分技术（例如只说「后端用 Java」）时：已指定的照写，其余写占位符，提示块保留

### 7. Sprint Planning

- 每个 Sprint 表的 Cumulative 逐行累加，最后一行等于 Sprint 总 SP
- 按优先级排：P0 先排；P1 放在 P0 之后，容量允许时才放进当前 Sprint
- Sprint 容量参考 1.3 的团队和时间；如果每个 Sprint 的 SP 差距很大，在第 9 章写明风险

### 8. Definition of Done

- 沿用 Example 的四个层面；单元测试覆盖率、静态检查工具等按团队实际情况写，技术栈未定时写通用要求

### 9. 风险与依赖

- 至少写 3 条风险，包括进度、需求变更、1 个技术难点
- 9.2 依赖中必须包含「Architecture design confirmed」和「Database design confirmed」，除非它们已经完成

### 10. Open Questions

- 把所有没问清、靠假设推进的地方都列进来。每条写明影响哪些 Story、最晚什么时候需要答案
- 没有待确认问题时写 "No open questions at this time."

### 11. Next Steps: Task Backlog（固定内容）

按实际情况勾选：

```markdown
## 11. Next Steps: Task Backlog

The Task Backlog (backend/frontend task breakdown with hours and dependencies) is **not generated yet**.
It needs all three prerequisites below, because tasks reference real frameworks, tables and API paths:

| Prerequisite | Status | How to complete |
| --- | --- | --- |
| Architecture design document | ⬜ Pending | `/solution-architect` or `/spw-arch` with this PRD |
| Database design document | ⬜ Pending | `/database-designer` or `/spw-db` with this PRD and the architecture document |
| PRD Section 6 completed | ⬜ Pending | Fill Section 6 from the architecture document |

**Recommended order:** PRD (this document) → architecture design → database design → update PRD Section 6 → run `/product-manager` (or `/spw-prd`) again with all three documents to generate `task-backlog.md`.
```

- 生成 Backlog 后，三行都改成 ✅ Done，首句改成 "The Task Backlog has been generated: `task-backlog.md`."

---

## 三、示例片段（报刊亭管理系统）

以下片段展示填写粒度；它已修正 Example 中的 SP 合计和技术栈错误。

```markdown
### Epic Overview

| Epic ID | Epic Name | Priority | Story Points | Target Sprint |
| --- | --- | --- | --- | --- |
| E001 | Product & Inventory Management | P0 | 21 | Sprint 1 |
| E002 | Sales Processing & Receipts | P0 | 31 | Sprint 2 |
| E003 | Data Queries & Reporting | P1 | 11 | Sprint 3+ |

### Epic 1: Product & Inventory Management (E001)

**Priority: P0 - Blocking** | **Sprint 1**

**Epic description:**
Enables the newsstand to manage all products for sale (newspapers, magazines) and their stock. Without it, sales cannot happen.

**User value:**

- Clerks can quickly view current inventory
- New products can be easily added to the system
- Low stock can be detected in time

**Core flow:**

1. Clerk opens the product list
2. Clerk clicks "Add Product" and fills in name, type, price and initial stock
3. System validates the input and saves the product
4. The new product appears at the top of the list

- **Exception:** duplicate name → the form keeps the input and shows "A product with this name already exists"

---

#### User Story 1.1: Add a New Product

**As a** clerk
**I want to** add a new newspaper or magazine to the system
**So that** I can sell new products

**Acceptance criteria:**

- [ ]  The system provides an "Add Product" entry point
- [ ]  Product name, type (newspaper/magazine), price, and initial stock can be entered
- [ ]  Price must be greater than 0; initial stock must be ≥ 0
- [ ]  Product name cannot be empty or duplicated
- [ ]  A success message is shown after saving and the product appears in the list

**Story Points:** 3
**Priority:** P0

---

#### User Story 1.6: Low Stock Alert

**As a** clerk
**I want to** see products that are low in stock
**So that** I can restock them in time

**Acceptance criteria:**

- [ ]  A low-stock alert area is displayed at the top of the product list page
- [ ]  Products with stock ≤ 10 are shown in the alert area with name and current stock
- [ ]  The alert area is hidden when no product is low in stock

**Story Points:** 3
**Priority:** P1
```

---

## 四、中英标题对照表

| English | 中文 |
| --- | --- |
| Product Requirements Document (PRD) | 产品需求文档（PRD） |
| Status / Version / Last updated | 状态 / 版本 / 最后更新 |
| 1. Product Overview | 1. 产品概述 |
| 1.1 Product Positioning | 1.1 产品定位 |
| 1.2 Business Goals | 1.2 业务目标 |
| 1.3 Constraints | 1.3 约束条件 |
| 1.4 Out of Scope & Assumptions | 1.4 范围外事项与假设 |
| 1.5 Success Metrics | 1.5 成功指标 |
| 2. User Persona | 2. 用户画像 |
| Basic information / Goals & motivations / Pain points & challenges / Behavioral traits | 基本信息 / 目标与动机 / 痛点与挑战 / 行为特征 |
| 3. Epic Breakdown & Prioritization | 3. Epic 拆解与优先级 |
| Epic Overview | Epic 总览 |
| Epic description / User value / Core flow / Exception | Epic 描述 / 用户价值 / 核心流程 / 异常 |
| User Story | 用户故事 |
| As a / I want to / So that | 作为 / 我想要 / 以便 |
| Acceptance criteria | 验收标准 |
| Story Points / Priority | 故事点 / 优先级 |
| 4. Feature Priority Matrix | 4. 功能优先级矩阵 |
| 5. Non-Functional Requirements | 5. 非功能需求 |
| 5.1 Performance / 5.2 Security / 5.3 Usability / 5.4 Compatibility | 5.1 性能 / 5.2 安全 / 5.3 易用性 / 5.4 兼容性 |
| 5.5 Accessibility & Privacy | 5.5 无障碍与隐私 |
| 6. Technical Architecture | 6. 技术架构 |
| [TBD — pending architecture design] | [待定 — 等待架构设计] |
| 7. Sprint Planning | 7. Sprint 规划 |
| Goal / Cumulative / total story points | 目标 / 累计 / 故事点合计 |
| 8. Definition of Done | 8. 完成定义（DoD） |
| 9. Risks & Dependencies | 9. 风险与依赖 |
| Impact / Probability / Mitigation | 影响 / 概率 / 应对措施 |
| 10. Open Questions | 10. 待确认问题 |
| Question / Owner / Affects / Needed by | 问题 / 负责人 / 影响范围 / 最晚确认时间 |
| 11. Next Steps: Task Backlog | 11. 下一步：任务 Backlog |
| Prerequisite / Status / How to complete | 前置条件 / 状态 / 如何完成 |
