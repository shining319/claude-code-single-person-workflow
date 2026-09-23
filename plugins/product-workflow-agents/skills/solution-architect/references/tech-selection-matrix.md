# 通用分层技术选型矩阵

> 适用范围：A/B 两条线共用的分层选型：跨端、状态、通信、消息、存储、认证、支付、通知、CMS、搜索、AI、i18n、功能开关、测试、可观测性
> 来源：《现代软件系统架构设计与托管部署参考手册》，章节编号 §x 与原手册一致，便于交叉引用。
> 时效：信息核验于 2026-09。版本号只写主版本；价格、免费额度、许可证以官网当期为准，输出方案时标注「需核验」。

**目录**：§5.1 跨端 · §5.2 前端状态 · §5.3 API 与通信 · §5.4 数据库 · §5.5 消息队列 · §5.6 存储与 CDN · §5.7 认证与授权 · §5.8 支付 · §5.9 通知与邮件 · §5.10 CMS · §5.11 搜索 · §5.12 AI 集成 · §5.13 i18n · §5.14 功能开关 · §5.15 代码质量与测试 · §5.16 可观测性

---

## 5. 通用分层技术选型矩阵

### 5.1 跨端

| 终端 | 方案 | 说明 |
|---|---|---|
| iOS/Android | **React Native + Expo**（EAS 构建、OTA 更新） | TS 团队首选 |
| | Flutter | 性能与 UI 一致性好，需 Dart |
| | Capacitor / Ionic | Web 应用包壳，快速上架 |
| | 原生 Swift / Kotlin | 性能与系统能力要求极高 |
| 桌面 | **Electron** | 生态成熟，体积大 |
| | **Tauri 2** | 体积小、Rust 后端，也支持移动端；需处理各平台 WebView 差异 |
| 小程序 | **uni-app**（Vue）、**Taro**（React） | 一套代码多端小程序 + H5 + App |

### 5.2 前端状态（拆成两个维度）

| 类型 | 说明 | React | Vue |
|---|---|---|---|
| 服务端状态 | 远端数据的缓存、同步、失效、重试 | TanStack Query、SWR | TanStack Query、Pinia Colada |
| 客户端状态 | UI 状态、跨组件共享 | Zustand、Jotai、Redux Toolkit | Pinia |
| URL 状态 | 筛选、分页 | nuqs、TanStack Router search params | Vue Router query |
| 表单状态 | | React Hook Form、TanStack Form | VeeValidate、FormKit |

### 5.3 API 与通信

| 协议 | 适用 |
|---|---|
| REST + OpenAPI | 默认，对外 API |
| GraphQL | 多客户端数据聚合 |
| tRPC / RPC | TS 内部 |
| **gRPC** | 服务间高性能通信（Java ↔ Go/Java） |
| **SSE** | 单向推送、AI 流式输出（优先于 WebSocket） |
| WebSocket / Socket.IO | 双向实时：聊天、协作、游戏 |
| Webhooks | 第三方回调（支付、Git） |
| 托管实时 | Pusher、Ably、Supabase Realtime、Liveblocks（协作）、PartyKit |

### 5.4 数据库（详见 §6）

PostgreSQL（默认）、MySQL、MongoDB、Redis/Valkey、Elasticsearch/OpenSearch、ClickHouse、向量库。

### 5.5 消息队列 / 事件流

| 产品 | 模型 | 适用 |
|---|---|---|
| **Kafka**（或 Redpanda） | 分布式日志、可回放 | 事件流、日志、CDC、高吞吐 |
| **RabbitMQ** | 传统消息代理、灵活路由 | 任务分发、业务消息 |
| RocketMQ | 事务消息、延迟消息 | 国内电商、金融 |
| NATS | 轻量、低延迟 | 微服务通信、IoT |
| AWS SQS/SNS、GCP Pub/Sub | 托管 | 云上免运维 |
| Redis Streams / BullMQ | 轻量 | 小规模任务队列 |

### 5.6 存储与 CDN

- 对象存储：AWS S3、**Cloudflare R2**（无出口流量费）、GCS、阿里云 OSS、腾讯云 COS、自建 MinIO
- 上传：预签名 URL 直传，**不要让文件流经应用服务器**
- 图片处理：Cloudflare Images、imgproxy、Next.js Image、阿里云 OSS 图片处理
- CDN：Cloudflare、CloudFront、Fastly、阿里云 CDN

### 5.7 认证与授权

| 场景 | 方案 |
|---|---|
| TS 全栈、自托管 | **Better Auth**（新项目首选）；Auth.js（原 NextAuth.js，2025 年起由 Better Auth 团队维护，存量项目可继续用）；Lucia 已不再是库，只作「从零实现会话认证」的学习资料 |
| 托管、快速 | **Clerk**、Auth0、Supabase Auth、Firebase Auth、Stack Auth |
| Java | Spring Security + Keycloak / Spring Authorization Server |
| 企业 SSO（SAML/OIDC）、B2B | WorkOS、Auth0、Keycloak、Zitadel |
| 授权（权限模型） | RBAC 起步；复杂场景 ABAC / ReBAC：**OpenFGA**、Casbin、Permit.io、Cerbos |

要点：
- 浏览器端优先 **HttpOnly Secure Cookie 会话**；JWT 适合服务间 / 移动端，短有效期 + Refresh Token 轮换
- 支持 Passkeys（WebAuthn）、MFA
- 多租户 SaaS：租户隔离策略见 §6.5

### 5.8 支付

| 方案 | 说明 |
|---|---|
| **Stripe** | 全球首选，订阅、发票、税务（Stripe Tax） |
| PayPal / Braintree | 补充支付方式 |
| **Paddle / Polar / Creem**（MoR） | 平台代为处理全球销售税/VAT，独立开发者友好；Lemon Squeezy 被 Stripe 收购后仍在运营，Stripe 另推出自带 MoR 的 **Stripe Managed Payments**（2026 公开预览，需核验） |
| Adyen | 大型企业、多本地支付方式 |
| 支付宝 / 微信支付 | 中国大陆 |
| RevenueCat | App 内订阅管理 |

> 支付设计必做：**Webhook 幂等处理**、以支付平台为订阅状态唯一真相源、订单状态机。

### 5.9 通知与邮件

邮件：Resend（+ React Email）、Postmark（事务邮件送达率高）、AWS SES（便宜）、SendGrid、Mailgun。
短信/推送：Twilio、Expo Push、FCM / APNs、阿里云短信。
多渠道编排：Novu、Knock。

### 5.10 内容管理（CMS）

Sanity、Contentful、Strapi（开源）、**Payload CMS**（TS、可嵌入 Next.js）、Directus、Storyblok。

### 5.11 搜索

Elasticsearch / OpenSearch（全能）、**Meilisearch** / **Typesense**（轻量即时搜索）、Algolia（托管）、PostgreSQL 全文检索（起步够用）。

### 5.12 AI 集成

| 层 | TS | Java |
|---|---|---|
| 模型 SDK | OpenAI、Anthropic、Google SDK | 同左的 Java SDK |
| 应用框架 | **Vercel AI SDK**、LangChain.js、Mastra | **Spring AI**、LangChain4j |
| Agent / 工具协议 | MCP（Model Context Protocol） | Spring AI MCP |
| 向量存储 | pgvector、Qdrant、Pinecone、Weaviate、Milvus | 同左 |
| 网关/观测 | LiteLLM、OpenRouter、Langfuse、Helicone | Langfuse |
| 评测 | promptfoo、Braintrust | |

AI 设计要点：流式输出用 SSE；成本与速率限制；提示注入防护；敏感数据脱敏；结果缓存；模型可替换（抽象 provider）。

### 5.13 国际化（i18n）

next-intl、react-i18next、vue-i18n、@nuxtjs/i18n；翻译平台 Crowdin、Lokalise、Tolgee；Java 侧 `MessageSource`。注意时区（存 UTC）、货币、RTL。

### 5.14 功能开关与实验

PostHog（分析 + 开关 + 录屏一体）、LaunchDarkly、Unleash（开源）、GrowthBook、Statsig。

### 5.15 代码质量与测试

| 类型 | TS | Java |
|---|---|---|
| Lint/格式 | ESLint + Prettier，或 **Biome**（一体、快） | Checkstyle、Spotless、SpotBugs、Error Prone |
| Git Hooks | Husky + lint-staged / Lefthook | 同左 |
| 单元测试 | **Vitest**、Jest | JUnit 5、Mockito |
| 集成测试 | Testcontainers (Node)、MSW | **Testcontainers** |
| E2E | **Playwright**、Cypress | 同左 |
| 契约测试 | Pact | Pact、Spring Cloud Contract |
| 负载测试 | k6、Artillery | Gatling、JMeter |
| 静态安全扫描 | Semgrep、CodeQL、Snyk、Dependabot/Renovate | 同左 + OWASP Dependency-Check |

### 5.16 可观测性

| 支柱 | 开源自建 | 托管 |
|---|---|---|
| 统一标准 | **OpenTelemetry**（强烈建议从第一天接入） | — |
| 指标 | Prometheus + Grafana | Grafana Cloud、Datadog |
| 日志 | Loki、ELK/OpenSearch | Better Stack、Axiom、Datadog |
| 链路 | Jaeger、Tempo、SkyWalking | Honeycomb、Datadog |
| 错误 | Sentry（可自建） | Sentry |
| 前端/产品分析 | Plausible、Umami、PostHog | Google Analytics、Mixpanel、Amplitude |
| 会话回放 | PostHog、OpenReplay | LogRocket |
| 可用性监控 | Uptime Kuma | Better Stack、Checkly |

