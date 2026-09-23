# B 线：TypeScript 全栈技术栈

> 适用范围：团队以 TypeScript 为主，使用 Node.js / Bun 与 React / Vue 全栈框架
> 来源：《现代软件系统架构设计与托管部署参考手册》，章节编号 §x 与原手册一致，便于交叉引用。
> 时效：信息核验于 2026-09。版本号只写主版本；价格、免费额度、许可证以官网当期为准，输出方案时标注「需核验」。

**目录**：§4.1 全栈框架 · §4.2 独立后端 · §4.3 API 与类型安全 · §4.4 数据访问 · §4.5 后台任务与队列 · §4.6 Monorepo

---

## 4. B 线：TypeScript 全栈技术栈

### 4.1 全栈框架

| 框架 | 生态 | 特点 | 适用 |
|---|---|---|---|
| **Next.js 16** | React | RSC、App Router、生态最大；与 Vercel 深度绑定但可自托管（standalone / OpenNext） | 通用首选 |
| **React Router v7（原 Remix，framework mode）** | React | Web 标准导向、loader/action、部署灵活；注意 Remix 3 已改为不基于 React 的独立框架，勿混淆 | 偏好 Web 标准、多平台部署 |
| **TanStack Start 1.x**（需核验） | React | 类型安全路由、Vite 驱动、服务端函数；RSC 支持仍在推进 | 重视类型安全、新项目 |
| **Nuxt 4** | Vue | Vue 全栈首选，Nitro 服务端可部署到几乎任何平台 | Vue 团队 |
| **SvelteKit** | Svelte | 轻量、性能好 | 小团队、性能敏感 |
| **Astro** | 多框架 | 内容优先、Islands | 营销站、文档、博客 |

### 4.2 独立后端（API 服务）

| 框架 | 特点 | 适用 |
|---|---|---|
| **Hono** | 极轻，基于 Web 标准，可跑在 Node / Bun / Deno / Cloudflare Workers / Lambda | 边缘、轻量 API、BFF |
| **Fastify** | 高性能、插件体系成熟 | 中型 API 服务 |
| **NestJS** | 依赖注入、模块化，风格接近 Spring | Java 背景团队、大型后端 |
| Elysia | Bun 优先，类型推导强 | Bun 生态 |
| Express | 老牌，生态大但设计陈旧 | 维护旧项目 |

运行时：**Node.js 24 LTS**（默认；22 为维护 LTS，自 Node 27 起每年一个大版本且均为 LTS）、**Bun**（启动快、内置工具）、Deno（安全模型、原生 TS）。

### 4.3 API 与类型安全

| 方案 | 适用 |
|---|---|
| **tRPC** | 前后端同在 TS monorepo、只服务自家前端 |
| **Server Actions / Server Functions** | Next.js / TanStack Start 内部表单与变更 |
| **Hono RPC** | Hono 后端 + TS 前端 |
| **oRPC / ts-rest** | 想要 tRPC 式体验同时输出 OpenAPI |
| REST + OpenAPI（zod-openapi） | 需要对外开放 API、多语言客户端 |
| GraphQL（Pothos / GraphQL Yoga / Apollo） | 多客户端、数据图复杂 |

### 4.4 数据访问

| 工具 | 特点 |
|---|---|
| **Drizzle ORM** | SQL-like、轻量、Serverless/边缘友好；稳定版为 0.x，1.0 处于 beta/RC（需核验） |
| **Prisma 7** | Schema 驱动、DX 好、迁移工具成熟；已移除 Rust 引擎，包体大幅缩小，Serverless 部署更友好 |
| Kysely | 类型安全查询构建器 |
| Mongoose | MongoDB |
| Zod / Valibot | 运行时校验，贯穿前后端 |

### 4.5 后台任务与队列（TS）

BullMQ（Redis）、**Trigger.dev**、**Inngest**（托管的持久化工作流）、pg-boss（基于 Postgres）、Temporal（TS SDK）、Upstash QStash（Serverless 场景）。

> Serverless（Vercel / Workers）上无法运行常驻 worker，长任务必须外置到队列服务或独立容器。

### 4.6 Monorepo

**pnpm workspace + Turborepo**（默认）或 **Nx**（大型、需要代码生成与边界约束）。

```
apps/
  web/        # Next.js
  admin/      # Vite SPA
  mobile/     # Expo
  api/        # Hono / NestJS
packages/
  ui/         # 共享组件
  db/         # Drizzle schema + client
  validators/ # Zod schema，前后端共享
  config/     # eslint / tsconfig / tailwind 预设
```

