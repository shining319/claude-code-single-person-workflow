# 架构模式与选型决策

> 适用范围：选择后端架构模式、前端渲染模式、前端组织模式；确定主技术栈（A 线 / B 线）；常见二选一取舍
> 来源：《现代软件系统架构设计与托管部署参考手册》，章节编号 §x 与原手册一致，便于交叉引用。
> 时效：信息核验于 2026-09。版本号只写主版本；价格、免费额度、许可证以官网当期为准，输出方案时标注「需核验」。

**目录**：§2.1 后端架构模式 · §2.2 前端渲染模式 · §2.3 前端组织模式 · §10.1 主栈决策树 · §10.3 常见二选一速查

---

## 2. 架构模式选择

### 2.1 后端架构模式

| 模式 | 适用 | 优点 | 缺点 | 团队规模 |
|---|---|---|---|---|
| **单体（Monolith）** | MVP、小团队、业务未定型 | 开发部署简单、事务简单、调试容易 | 规模化后耦合、发布相互影响 | 1–8 人 |
| **模块化单体（Modular Monolith）** ⭐默认推荐 | 大多数中小型产品 | 模块边界清晰，未来可拆；仍单进程部署 | 需要纪律维护边界 | 3–30 人 |
| **微服务（Microservices）** | 多团队并行、各域扩展需求差异大 | 独立部署/扩展、技术异构 | 分布式事务、运维、可观测性成本高 | 30+ 人或多团队 |
| **Serverless / FaaS** | 突发流量、事件驱动、低运维 | 按量计费、零运维 | 冷启动、执行时长限制、厂商锁定 | 任意 |
| **事件驱动（EDA）** | 解耦异步流程、审计、数据同步 | 高解耦、可回放 | 最终一致性、排障难 | 中大型 |
| **CQRS + Event Sourcing** | 审计要求强、读写模型差异大（金融、订单） | 完整历史、读写分别优化 | 复杂度高，不要默认用 | 有经验团队 |
| **Cell-based / 单元化** | 超大规模、多地域隔离 | 故障隔离 | 极高复杂度 | 大厂 |

**模块化单体实践要点**
- Java：Maven/Gradle 多模块 + **Spring Modulith 2.x** 校验模块依赖；按领域（DDD 限界上下文）分包，不按技术分层分包
- TS：monorepo 中 `packages/<domain>`，用 ESLint boundaries / Nx module boundaries 限制跨域引用
- 模块间通过接口或进程内事件通信，**禁止跨模块直接查别人的表**——这是未来拆服务的前提

### 2.2 前端渲染模式

| 模式 | 说明 | 适用 | 代表框架 |
|---|---|---|---|
| CSR / SPA | 浏览器渲染 | 后台管理、登录后应用、不需要 SEO | Vite + React/Vue |
| SSR | 每次请求服务端渲染 | 个性化且需要 SEO 的页面 | Next.js、Nuxt、TanStack Start、React Router v7 |
| SSG | 构建时生成静态页 | 文档、博客、营销站 | Astro、Next.js、Nuxt、VitePress |
| ISR / 按需重验证 | 静态 + 定时/触发更新 | 电商商品页、内容站 | Next.js、Nuxt |
| RSC（React Server Components） | 组件级服务端渲染，减少客户端 JS | 内容 + 交互混合的 React 应用 | Next.js App Router |
| Islands | 静态为主，局部水合 | 内容站 | Astro |
| Streaming SSR | 分块流式输出 | 首屏性能敏感 | Next.js、Nuxt、SvelteKit |

**选择规则**：登录后的业务系统 → SPA 足够；面向公众且依赖 SEO → SSR/SSG；内容为主 → SSG/Astro。

### 2.3 前端组织模式

| 模式 | 适用 |
|---|---|
| 单一 SPA / 全栈应用 | 默认 |
| **BFF（Backend for Frontend）** | 多端（Web/App/小程序）需求差异大；Java 微服务前面放一层 Node BFF 做聚合、裁剪、SSR |
| 微前端（qiankun、Module Federation、single-spa） | 多团队独立交付大型后台；**小团队不要用** |
| Monorepo 多应用 | 多个前端 + 共享组件/类型 |


## 10. 选型决策

### 10.1 主栈选择

```
团队主力是 Java？
├─ 是 → A 线
│   ├─ 需要 SEO / SSR？ 是 → 方案 F（Node BFF + Java）或 Thymeleaf/HTMX 轻量方案
│   │                   否 → 方案 D（SPA + Spring Boot）
│   └─ 多团队且 QPS/域复杂度高？ 是 → 方案 E
└─ 否（TS 为主）→ B 线
    ├─ MVP / 独立开发 → 方案 A
    ├─ 多端（App/后台） → 方案 C
    └─ 生产、需控成本/长任务 → 方案 B
面向中国大陆？ → 叠加方案 H 的替换清单
内容为主？ → 方案 G
AI / 实时？ → 叠加方案 I / J
```

### 10.3 常见二选一速查

| 问题 | 倾向 A | 倾向 B |
|---|---|---|
| JPA vs MyBatis-Plus | 领域模型复杂、少手写 SQL → JPA | SQL 复杂、需精细调优、国内团队习惯 → MyBatis-Plus |
| Prisma vs Drizzle | DX、schema 优先、成熟迁移 → Prisma（v7 起无 Rust 引擎，Serverless 差距已缩小） | 轻量、贴近 SQL、边缘运行时 → Drizzle |
| NestJS vs Hono | Java 背景、大型、需要 DI → NestJS | 轻量、边缘、多运行时 → Hono |
| Kafka vs RabbitMQ | 事件流、回放、高吞吐 → Kafka | 任务队列、复杂路由、简单运维 → RabbitMQ |
| Session vs JWT | 浏览器 Web → Session Cookie | 移动端/服务间 → JWT |
| REST vs GraphQL vs tRPC | 对外/多语言 → REST | 多客户端聚合 → GraphQL；纯 TS 内部 → tRPC |
| Vercel vs 容器平台 | Next.js 前端、低运维 → Vercel | 后端/长任务/Java/成本控制 → Railway/Cloud Run/VPS |
| Electron vs Tauri | 生态与兼容性优先 → Electron | 体积与内存优先 → Tauri |
| RN/Expo vs Flutter | TS 团队 → Expo | 高 UI 一致性、无 TS 包袱 → Flutter |
| ECS/Cloud Run vs K8s | <10 服务 → Cloud Run/ECS | 大量服务、平台团队 → K8s |
