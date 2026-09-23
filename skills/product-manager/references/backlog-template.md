# Task Backlog 模板

Task Backlog 把 PRD 中的每个 User Story 拆成后端任务（B*）和前端任务（F*），结构以 `Example_Task_Backlog` 为准。和 Example 的区别：去掉 Task Dependency Diagrams 和 Suggested Development Timeline，换成 **Critical Path & Start Order**（全部是表格，不画树状图）。

**生成前提（缺一不可）**：架构设计文档、数据库设计文档、已完善的 PRD（第 6 章不再是占位符）。任务中的框架、实体名、表名、字段、API 路径都以这三份文档为准，不自行发明。

- 用户用中文时，标题按文末的对照表翻译；任务 ID、SP、API 路径、类名和文件名保持原样

---

## 一、骨架

```markdown
# Task Assignment Document

# <Product Name>

> **Source documents:** `prd.md` (v<x.y>), `<architecture doc path>`, `<database design doc path>`
> **Last updated:** <YYYY-MM-DD>

---

## Task Assignment Notes

This document breaks down the User Stories from the PRD into concrete frontend and backend development tasks. Each task includes:

- The User Story it belongs to
- Task description
- Acceptance criteria
- Estimated hours
- Dependencies

**Team members:**

- **Backend developer:** <姓名或 "Backend developer">
- **Frontend developer:** <姓名或 "Frontend developer">

**Estimation basis:** <例如 "Ideal engineering hours for one developer; 1 SP ≈ 2–4 hours; ~15 available hours per developer per week">

---

## Sprint 1 Task Assignments (Week 1–3)

### Epic 1: <Epic Name>

---

#### User Story 1.1: <Story Name> (3 SP)

#### Backend Tasks

**Task B1.1.1: <动词开头的任务名>**

- **Description:** <一句话：做什么、在哪一层>
- **Acceptance criteria:**
    - [ ]  <可验证的完成标准>
- **Estimated hours:** <0.5–5> hours
- **Dependencies:** <任务 ID 列表，或 None>

#### Frontend Tasks

**Task F1.1.1: <...>**

（字段同上）

---

### Sprint 1 Task Summary

| Developer | Task list | Total hours |
| --- | --- | --- |
| **Backend** | B1.1.1, B1.1.2, ... | **<合计> hours** |
| **Frontend** | F1.1.1, F1.1.2, ... | **<合计> hours** |

**Sprint 1 total hours:** <两行之和> hours

---

## Sprint 2 Task Assignments (Week 4–6)

（同上）

---

## Future Iteration Task Assignments (Sprint 3+)

（同上，结尾是 Future Iteration Task Summary）

---

## Critical Path & Start Order

### Sprint 1

**Start order:**

| Role | Start now | Then, in order |
| --- | --- | --- |

**Cross-role blockers:**

| Waiting task | Waits for | Earliest unblock | Workaround |
| --- | --- | --- | --- |

**Critical path:** <任务链> = **<合计> hours**

<一两句话：关键路径上的哪一步最容易延误、延误会影响哪些 Story>

### Sprint 2

（同上）

---

## Appendix: API Endpoint List

### <模块> API

| Method | Path | Description |
| --- | --- | --- |
```

---

## 二、任务拆解规则

### 编号

- 格式：`B` 或 `F` + Story 编号 + 序号，例如 User Story 2.6 的第 1 个后端任务是 `B2.6.1`
- 编号在整个文档里唯一；一个任务只属于一个 Story
- 单人团队也保留 B / F 两条线，Team members 里两个角色写同一个人
- 项目确实有第三类工作（例如移动端、数据迁移）时，可以增加前缀（`M` 移动端、`D` 数据 / DevOps），并在 Task Assignment Notes 里说明

### 每个 Story 怎么拆

- **后端**：数据层（实体 / 表 / 迁移，已有就不重复建）→ 接口实现 → 单元测试。每个包含后端工作的 Story 至少有一个单元测试任务
- **前端**：页面或组件 → API 集成（加载状态、错误处理、成功反馈）。纯前端交互的 Story 可以没有 API 集成任务
- Story 只涉及一侧时，省略另一侧的小节（例如 Example 中 US 2.3 只有 Frontend Tasks）
- 单个任务 0.5–5 小时；超过 5 小时就拆开
- PRD 中该 Story 的每条验收标准，至少要被一个任务的验收标准覆盖

### 字段写法

- **Description**：一句话写清做什么。后端写接口或服务名，前端写组件或页面文件名；文件名后缀跟技术栈走（Vue 用 `.vue`，React 用 `.tsx`）
- 一个任务涉及多个接口时，每个接口都写完整的「方法 + 路径」（例如 `PUT /api/v1/categories/{id}`），不要简写成 `GET / POST / PUT /api/v1/categories`，否则无法和附录 API 清单逐条对应
- **Acceptance criteria**：
  - 后端写接口路径、请求体、校验规则、返回和错误码
  - 前端写界面元素、交互、校验、反馈状态
  - 单元测试任务列出要覆盖的场景和覆盖率要求
- **Estimated hours**：理想工时，精度 0.5 小时
- **Dependencies**：只写直接依赖。可以依赖同一 Sprint 或之前 Sprint 的任务，不能依赖之后 Sprint 的任务；没有依赖写 `None`
- 后端表名、字段、实体名以数据库设计文档为准；API 路径和风格以架构文档为准

### Sprint 归属

- Sprint 的划分和 Story 顺序完全按照 PRD 第 7 章；PRD 第 7 章以外的 Story 放到 Future Iteration
- Sprint Task Summary 的合计必须等于明细工时之和

### Critical Path & Start Order

只给已排入 Sprint 的部分写（Future Iteration 不写）。每个 Sprint 三张表：

1. **Start order**：每个角色第一天就能开工的任务（没有依赖，或依赖都在之前的 Sprint 中），再给出建议的后续顺序。排序原则：
   - 先做关键路径上的任务
   - 先做会阻塞另一个角色的小任务
   - 其余按 Story 顺序排
2. **Cross-role blockers**：前端任务在等哪个后端任务（或反过来）。只列同一 Sprint 内的阻塞，之前 Sprint 已完成的不列。
   - Earliest unblock：按被等待方的建议顺序累加工时，算出最早在第几个小时解除阻塞
   - Workaround：给一个解除等待的办法，例如按接口约定先用 mock 数据
3. **Critical path**：沿依赖关系累加工时，最长的那条链（不考虑人手限制），写成 `A → B → C = N hours`；再用一两句话说明风险点

---

## 三、示例片段（报刊亭管理系统，Sprint 2）

技术栈取自 PRD 第 6 章：Spring Boot 4.x + MyBatis-Plus + MySQL 8.4 LTS；Vue 3 + Element Plus + Pinia。

```markdown
#### User Story 2.6: Complete the Sale (5 SP)

#### Backend Tasks

**Task B2.6.1: Implement the create-sales-order API**

- **Description:** Implement the POST /api/sales endpoint
- **Acceptance criteria:**
    - [ ]  Endpoint path: POST /api/sales
    - [ ]  Request body: {items: [{productId, quantity}]}
    - [ ]  Validate that the cart is not empty and every item has sufficient stock (a second check)
    - [ ]  Deduct stock and create the order and its line items in one transaction
    - [ ]  Use optimistic locking to prevent concurrent overselling
    - [ ]  Returns the created order
- **Estimated hours:** 5 hours
- **Dependencies:** B2.1.1, B2.1.2

**Task B2.6.2: Write unit tests**

- **Acceptance criteria:**
    - [ ]  Test a normal sale, insufficient stock, an empty cart
    - [ ]  Test concurrent sales (optimistic locking)
    - [ ]  Test coverage >= 80%
- **Estimated hours:** 3 hours
- **Dependencies:** B2.6.1

#### Frontend Tasks

**Task F2.6.1: Implement the complete-sale functionality**

- **Description:** Add the "Complete Sale" button and its logic to SalesPage.vue
- **Acceptance criteria:**
    - [ ]  Validates that the cart is not empty before proceeding
    - [ ]  Calls POST /api/sales with a loading state
    - [ ]  Clears the cart and opens the receipt after success
    - [ ]  Shows a clear error message on failure
- **Estimated hours:** 3 hours
- **Dependencies:** B2.6.1, F2.5.1
```

Critical Path & Start Order（Sprint 2 的工时和依赖与 Example 一致）：

```markdown
### Sprint 2

**Start order:**

| Role | Start now | Then, in order |
| --- | --- | --- |
| Backend | B2.2.1, B2.1.1, B2.1.2 | B2.6.1 → B2.7.1 → B2.8.1 → B2.6.2 |
| Frontend | F2.1.1 | F2.2.2 → F2.2.3 → F2.5.1 → F2.3.1 → F2.3.2 → F2.4.1 → F2.2.1 → F2.6.1 → F2.7.1 → F2.7.2 → F2.8.1 |

**Cross-role blockers:**

| Waiting task | Waits for | Earliest unblock | Workaround |
| --- | --- | --- | --- |
| F2.3.2 | B2.2.1 | Backend hour 1 | — |
| F2.6.1 | B2.6.1 | Backend hour 10 | Build against a mock POST /api/sales response |
| F2.7.1 | B2.7.1 | Backend hour 11 | Use the order returned by POST /api/sales as mock data |
| F2.8.1 | B2.8.1 | Backend hour 13 | Mock a paged order list |

**Critical path:** B2.1.1 → B2.6.1 → B2.7.1 → F2.7.1 → F2.8.1 = **16 hours** (B2.1.2 runs in parallel with B2.1.1)

B2.6.1 is the bottleneck: it gates Complete Sale, the receipt and sales history. The backend should start it as soon as the entities and order number generator are done.
```

说明：B2.2.1 只有 1 小时，却阻塞 F2.3.2，所以排在后端第一个；B2.6.1 在后端建议顺序中累计到第 10 小时完成（1 + 2 + 2 + 5）。

---

## 四、中英标题对照表

| English | 中文 |
| --- | --- |
| Task Assignment Document | 任务分配文档 |
| Source documents / Last updated | 依据文档 / 最后更新 |
| Task Assignment Notes | 任务分配说明 |
| Team members / Backend developer / Frontend developer | 团队成员 / 后端开发 / 前端开发 |
| Estimation basis | 估算依据 |
| Sprint N Task Assignments (Week x–y) | Sprint N 任务分配（第 x–y 周） |
| Backend Tasks / Frontend Tasks | 后端任务 / 前端任务 |
| Task B1.1.1 | 任务 B1.1.1 |
| Description / Acceptance criteria / Estimated hours / Dependencies | 描述 / 验收标准 / 预估工时 / 依赖 |
| None | 无 |
| Sprint N Task Summary | Sprint N 任务汇总 |
| Developer / Task list / Total hours | 开发者 / 任务列表 / 总工时 |
| Future Iteration Task Assignments (Sprint 3+) | 未来迭代任务分配（Sprint 3+） |
| Critical Path & Start Order | 关键路径与开工顺序 |
| Start order / Start now / Then, in order | 开工顺序 / 立即开工 / 后续顺序 |
| Cross-role blockers | 跨角色阻塞 |
| Waiting task / Waits for / Earliest unblock / Workaround | 等待任务 / 等待对象 / 最早解除时间 / 应对办法 |
| Critical path | 关键路径 |
| Appendix: API Endpoint List | 附录：API 接口清单 |
| Method / Path / Description | 方法 / 路径 / 说明 |
