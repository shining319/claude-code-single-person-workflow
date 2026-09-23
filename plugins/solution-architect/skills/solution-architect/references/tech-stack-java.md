# A 线：React/Vue + Java 前后端分离技术栈

> 适用范围：团队主力是 Java（Spring Boot / Spring Cloud），前端为 React 或 Vue 的 SPA
> 来源：《现代软件系统架构设计与托管部署参考手册》，章节编号 §x 与原手册一致，便于交叉引用。
> 时效：信息核验于 2026-09。版本号只写主版本；价格、免费额度、许可证以官网当期为准，输出方案时标注「需核验」。

**目录**：§3.1 前端（分离模式） · §3.2 后端（Java / JVM） · §3.3 Java 微服务生态 · §3.4 工程结构参考

---

## 3. A 线：React/Vue + Java 前后端分离技术栈

### 3.1 前端（分离模式）

| 层 | React 方案 | Vue 方案 |
|---|---|---|
| 构建 | Vite | Vite |
| 路由 | React Router / TanStack Router | Vue Router |
| 客户端状态 | Zustand / Jotai / Redux Toolkit | Pinia |
| 服务端状态 | TanStack Query / RTK Query / SWR | TanStack Query (Vue) / Pinia Colada |
| UI 组件 | shadcn/ui、Ant Design、MUI、Mantine | Element Plus、Ant Design Vue、Naive UI、Vuetify、shadcn-vue |
| 后台模板 | Ant Design Pro、Refine | vue-element-admin 系、Vben Admin、Soybean Admin |
| 样式 | Tailwind CSS v4、CSS Modules | Tailwind CSS v4、UnoCSS |
| 表单校验 | React Hook Form + Zod | VeeValidate + Zod / Valibot |
| API 客户端 | 从 OpenAPI 生成：orval / openapi-typescript / hey-api | 同左 |

> **关键实践**：后端用 springdoc-openapi 导出 OpenAPI 规范 → 前端 CI 自动生成 TS 类型和请求函数，获得接近 tRPC 的端到端类型安全。

### 3.2 后端（Java / JVM）

| 层 | 推荐 | 备选 / 说明 |
|---|---|---|
| 语言版本 | **Java 25 LTS**（新项目首选）/ Java 21 LTS（存量） | Kotlin（更简洁，Spring 一等公民） |
| 框架 | **Spring Boot 4.x**（新项目；3.x 仅用于存量维护） | Quarkus、Micronaut（启动快、适合云原生/Serverless） |
| 并发 | **虚拟线程**（Java 21+，`spring.threads.virtual.enabled=true`） | WebFlux 响应式（仅在确有必要时，复杂度高） |
| Web | Spring MVC | Spring WebFlux |
| 持久层 | **Spring Data JPA (Hibernate)** / **MyBatis-Plus** | jOOQ（类型安全 SQL）、Spring Data JDBC |
| 数据库迁移 | **Flyway** / Liquibase | |
| 校验 | Jakarta Bean Validation | |
| 对象映射 | MapStruct | |
| API 文档 | springdoc-openapi | |
| 安全 | **Spring Security** + OAuth2 Resource Server（JWT） | Sa-Token（国内常用，轻量） |
| 身份服务 | Keycloak（自建）、Auth0、Okta、Cognito、Spring Authorization Server | |
| 缓存 | Spring Cache + Caffeine（本地）+ Redis/Valkey（分布式） | Redisson（分布式锁） |
| 消息 | Spring Kafka、Spring AMQP（RabbitMQ）、RocketMQ | Spring Cloud Stream |
| 定时任务 | Spring `@Scheduled` + ShedLock | Quartz、XXL-JOB（国内）、JobRunr |
| 工作流 | Temporal、Camunda、Flowable | |
| 测试 | JUnit 5 + Mockito + **Testcontainers** + AssertJ | ArchUnit（架构约束测试） |
| 构建 | Maven / Gradle (Kotlin DSL) | |
| 镜像 | **Jib** / Spring Boot Buildpacks | GraalVM Native Image（冷启动敏感场景） |
| 可观测 | Micrometer + OpenTelemetry + Actuator | |
| AI | **Spring AI 2.x** / LangChain4j | |

### 3.3 Java 微服务生态（仅当 §2 判定需要微服务时）

| 能力 | 国际主流 | 国内主流（Spring Cloud Alibaba） | K8s 原生替代 |
|---|---|---|---|
| 网关 | Spring Cloud Gateway | Spring Cloud Gateway | Ingress / Gateway API、Kong、APISIX |
| 注册发现 | Consul、Eureka（仍在 Spring Cloud 发布列车中维护；Hystrix/Ribbon/Zuul 1 已移除） | **Nacos** | K8s Service DNS |
| 配置中心 | Spring Cloud Config、Consul | **Nacos**、Apollo | ConfigMap / Secret + External Secrets |
| 服务调用 | OpenFeign、RestClient / HTTP Interface | OpenFeign、Dubbo | gRPC |
| 熔断限流 | Resilience4j | **Sentinel** | Istio / Envoy |
| 分布式事务 | Saga（Temporal / 自研）+ Outbox | **Seata** | — |
| 链路追踪 | OpenTelemetry + Jaeger/Tempo | SkyWalking | OTel |

> **原则**：部署在 K8s 上时，优先用平台能力（Service 发现、ConfigMap、Service Mesh），减少应用层中间件，避免"双重治理"。

### 3.4 Java 工程结构参考（模块化单体）

```
backend/
├── app/                 # 启动模块，组装各领域
├── modules/
│   ├── user/            # api / domain / infra / web 分层
│   ├── order/
│   └── payment/
├── common/              # 通用工具，严格控制膨胀
└── build.gradle.kts
```

