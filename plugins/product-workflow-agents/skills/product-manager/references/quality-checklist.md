# 交付前自检清单

写完文档后逐项检查，发现问题直接改正再交付。发现的问题不写进文档，也不需要向用户逐条汇报；只有无法自行解决的问题（例如需求本身矛盾）才写进 PRD 第 10 章 Open Questions。

这些检查项来自 Example 中出现过的真实错误：Epic SP 与 Story 之和不一致、PRD 和 Backlog 技术栈不一致、章节编号跳号。

## A. PRD 自检（每次都做）

**结构**

- [ ] 11 章齐全，编号连续（1–11），没有跳号
- [ ] 标题下有 Status 行，并且和第 6 章、第 11 章的实际状态一致
- [ ] 输出语言和用户一致；中文输出的标题按对照表翻译，ID、SP、API 路径保持原样

**数字**

- [ ] Epic Overview 中每个 Epic 的 Story Points 等于该 Epic 下所有 Story 的 SP 之和
- [ ] 所有 SP 都是 1 / 2 / 3 / 5 / 8；没有 13 及以上
- [ ] Sprint Planning 每张表的 Cumulative 逐行累加正确，最后一行等于 Sprint 总 SP
- [ ] Epic Overview 的 Target Sprint 和第 7 章的实际排期一致

**内容**

- [ ] 每个 Story 都有 As a / I want to / So that、验收标准、SP、Priority
- [ ] 每个 P0 Epic 都有 Core flow，包括至少一个异常分支
- [ ] 第 4 章的优先级和各 Story 的 Priority 一致；1.4 Out of scope 和 P2 呼应
- [ ] 1.5 和第 5 章的指标都能测量（带数字）
- [ ] 5.5 Accessibility & Privacy 已按产品实际情况填写

**技术栈与前置条件**

- [ ] 用户没提供架构文档、也没指定技术栈时，第 6 章全部是 `[TBD — pending architecture design]`，开头有 Pending 提示块，没有任何猜测的技术名词
- [ ] 第 6 章写的版本只来自架构文档或用户；自己写的版本标了「需核验」和日期
- [ ] 第 11 章三项前置条件的 ✅ / ⬜ 和实际情况一致
- [ ] 所有靠假设推进的地方都写进了 1.4 Assumptions 或第 10 章 Open Questions

## B. Backlog 自检（只在生成 Backlog 时做）

**前置条件**

- [ ] 架构设计文档、数据库设计文档都已提供，PRD 第 6 章已回填，PRD 状态行和第 11 章已更新

**覆盖**

- [ ] PRD 第 7 章中的每个 Story 在 Backlog 对应 Sprint 下都有任务；Future Iteration 覆盖其余 Story
- [ ] PRD 中每条验收标准都至少被一个任务覆盖
- [ ] 每个包含后端工作的 Story 都有单元测试任务

**编号与依赖**

- [ ] 任务 ID 唯一，格式为 `B/F + Story 编号 + 序号`
- [ ] Dependencies 中的每个 ID 都存在于文档中
- [ ] 没有循环依赖；没有任务依赖之后 Sprint 的任务
- [ ] 每个任务 0.5–5 小时

**数字**

- [ ] 每个 Sprint Task Summary 的 Task list 包含该 Sprint 的全部任务，Total hours 等于明细之和
- [ ] Sprint total hours 等于两个角色之和

**一致性**

- [ ] 任务中出现的框架、组件库、状态管理、ORM 和 PRD 第 6 章完全一致
- [ ] 表名、实体名、字段和数据库设计文档一致；API 路径风格和架构文档一致
- [ ] 附录 API 清单和任务中出现的接口一一对应，没有多也没有少

**Critical Path & Start Order**

- [ ] 每个已排期的 Sprint 都有 Start order、Cross-role blockers、Critical path 三部分
- [ ] Start now 里的任务确实没有同 Sprint 的依赖
- [ ] Earliest unblock 按被等待方的建议顺序累加计算
- [ ] Critical path 的工时之和计算正确，并且确实是最长的依赖链
- [ ] 文档中没有依赖树状图，也没有按周排的时间线表
