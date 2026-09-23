# 数据架构

> 适用范围：数据库选型、托管数据库、缓存、一致性与分布式事务、多租户、扩展路径、迁移与备份
> 来源：《现代软件系统架构设计与托管部署参考手册》，章节编号 §x 与原手册一致，便于交叉引用。
> 时效：信息核验于 2026-09。版本号只写主版本；价格、免费额度、许可证以官网当期为准，输出方案时标注「需核验」。

**目录**：§6.1 数据库选型 · §6.2 托管数据库 · §6.3 缓存策略 · §6.4 一致性与分布式事务 · §6.5 多租户 · §6.6 扩展路径 · §6.7 数据迁移与备份

---

## 6. 数据架构

### 6.1 数据库选型

| 需求 | 选择 |
|---|---|
| 通用业务、需要事务 | **PostgreSQL**（默认首选：JSONB、全文检索、pgvector、扩展丰富） |
| 团队熟 MySQL、国内生态 | MySQL 8 / MariaDB |
| 文档结构多变、原型 | MongoDB（但多数场景 Postgres JSONB 即可） |
| 缓存、会话、排行榜、限流、分布式锁 | Redis / Valkey / Dragonfly |
| 全文搜索、日志 | Elasticsearch / OpenSearch |
| 分析、OLAP、埋点 | **ClickHouse**、DuckDB（嵌入式）、BigQuery、Snowflake |
| 时序 | TimescaleDB、InfluxDB |
| 图 | Neo4j |
| 向量 | pgvector（起步）、Qdrant、Milvus |
| 全球分布式 SQL | CockroachDB、YugabyteDB、TiDB、Spanner |
| 边缘/嵌入式 | SQLite、Turso(libSQL)、Cloudflare D1 |

### 6.2 托管数据库

| 服务 | 类型 | 特点 |
|---|---|---|
| **Neon** | Serverless Postgres | 分支、按量、scale to zero |
| **Supabase** | Postgres + BaaS | 认证、存储、实时、Edge Functions |
| AWS RDS / Aurora | Postgres/MySQL | 企业级 |
| Google Cloud SQL / AlloyDB | Postgres/MySQL | |
| PlanetScale | MySQL (Vitess) / Postgres | 无免费档，偏生产 |
| Turso | libSQL | 边缘、多副本 |
| MongoDB Atlas | MongoDB | |
| Upstash | Redis / Kafka / QStash | Serverless 按请求计费 |
| 阿里云 RDS / PolarDB、腾讯云 TDSQL | | 国内 |

Serverless 环境连接 Postgres 注意：使用连接池（PgBouncer / Neon pooler / Supabase Supavisor / RDS Proxy）或 HTTP 驱动。

### 6.3 缓存策略

- 模式：Cache-Aside（默认）、Read/Write-Through、Write-Behind
- 多级：浏览器/CDN → 应用本地（Caffeine / LRU）→ 分布式（Redis）→ DB
- 问题与对策：**穿透**（布隆过滤器/缓存空值）、**击穿**（互斥锁/逻辑过期）、**雪崩**（随机 TTL/多级缓存）
- Redis 许可证：Redis 8 起可选 AGPLv3（另有 RSALv2/SSPL）；Valkey 为 BSD 许可、Linux 基金会治理，已是 AWS ElastiCache 默认引擎。两者协议兼容，自建或分发时按许可证选择

### 6.4 一致性与分布式事务

| 场景 | 方案 |
|---|---|
| 单库内 | 本地 ACID 事务（首选，尽量把强一致数据放同一库） |
| 发消息 + 写库 | **Transactional Outbox**（+ Debezium CDC 或轮询） |
| 跨服务长流程 | **Saga**（编排式 Temporal / Camunda，或协同式事件） |
| 强一致跨库 | 2PC / Seata AT（性能代价大，慎用） |
| 接口重试 | **幂等键（Idempotency-Key）**、唯一约束、状态机 |
| 并发更新 | 乐观锁（version 字段）、`SELECT ... FOR UPDATE`、分布式锁（Redisson） |

### 6.5 多租户（SaaS）

| 模式 | 隔离性 | 成本 | 适用 |
|---|---|---|---|
| 共享表 + `tenant_id` | 低（需 RLS 或框架强制过滤） | 最低 | 大多数 SaaS 起步 |
| Postgres Row Level Security | 中 | 低 | Supabase / Postgres 用户 |
| 每租户 Schema | 中高 | 中 | 中等租户数 |
| 每租户数据库 | 高 | 高 | 企业客户、合规要求 |

### 6.6 扩展路径

读写分离（主从复制）→ 缓存 → 垂直拆库（按领域）→ 水平分片（ShardingSphere、Citus、Vitess）→ 分布式数据库。**分片是最后手段。**

### 6.7 数据迁移与备份

- Schema 迁移纳入版本控制：Flyway / Liquibase / Drizzle Kit / Prisma Migrate
- 零停机迁移：扩展-收缩（Expand-Contract）模式，先加字段兼容新旧代码，再清理
- 备份：自动快照 + PITR（时间点恢复）+ 异地副本，**定期演练恢复**

