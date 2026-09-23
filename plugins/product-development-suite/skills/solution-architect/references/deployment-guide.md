# 托管与部署指南

> 适用范围：托管模式选择、前后端托管、VPS 自托管、容器化、CI/CD、发布策略、IaC、环境与密钥、云厂商与地域、平台迁移
> 来源：《现代软件系统架构设计与托管部署参考手册》，章节编号 §x 与原手册一致，便于交叉引用。
> 时效：信息核验于 2026-09。版本号只写主版本；价格、免费额度、许可证以官网当期为准，输出方案时标注「需核验」。

**目录**：§7.1 托管模式对比 · §7.2 前端托管 · §7.3 后端托管 · §7.4 VPS 标准拓扑 · §7.5 容器化与编排 · §7.6 CI/CD · §7.7 发布策略 · §7.8 IaC · §7.9 环境与密钥 · §7.10 云厂商与地域 · §7.11 平台迁移路径

---

## 7. 托管与部署

### 7.1 托管模式对比

| 模式 | 代表 | 运维成本 | 灵活性 | 成本曲线 | 适用 |
|---|---|---|---|---|---|
| 前端/全栈 PaaS | Vercel、Netlify、Cloudflare Pages/Workers | 极低 | 低 | 小流量免费，大流量贵 | TS 全栈、前端 |
| 容器 PaaS | **Railway**、Render、Fly.io、Koyeb、Northflank | 低 | 中 | 线性 | Java/Node 后端、中小项目 |
| 云厂商 Serverless 容器 | **Google Cloud Run**、AWS App Runner / ECS Fargate、Azure Container Apps | 低-中 | 中高 | 按量 | 生产级后端首选之一 |
| FaaS | AWS Lambda、Cloudflare Workers、Vercel Functions | 低 | 受限 | 按调用 | 事件、轻 API |
| VPS + Docker | Hetzner、DigitalOcean、Vultr、Linode、Lightsail | 中 | 高 | 最便宜 | 学生、个人、预算敏感 |
| 自托管 PaaS | **Coolify**、**Dokploy**、Kamal、CapRover | 中 | 高 | VPS 价格 | 想要 Heroku 体验又不想付费 |
| Kubernetes | EKS、GKE、AKS、阿里云 ACK、k3s | 高 | 最高 | 基础成本高 | 微服务、多团队、大规模 |

### 7.2 前端托管

| 平台 | 特点 |
|---|---|
| **Vercel** | Next.js 最佳体验、Preview 部署；注意函数执行时长（量级：默认约 5 分钟，Pro 可调到十几分钟以上，需核验）与流量计费 |
| Netlify | 静态站与 Jamstack，表单、函数 |
| **Cloudflare Pages / Workers** | 全球边缘、免费额度大、无出口费；Next.js 通过 OpenNext 适配 |
| AWS Amplify / S3 + CloudFront | AWS 体系 |
| 自托管 Nginx / Caddy | SPA 静态文件 + 反向代理 |
| 阿里云 OSS + CDN / 腾讯云 COS + CDN | 国内（需备案） |

SPA 部署要点：`index.html` 不缓存，带 hash 的静态资源长期缓存；配置 history 路由回退。

### 7.3 后端托管（按技术栈）

**Java（Spring Boot）**
- 小型：Railway / Render / Fly.io（Dockerfile 或 Buildpacks）；VPS + Docker Compose
- 生产：**Cloud Run**、ECS Fargate、Azure Container Apps、Azure Spring Apps 替代方案、K8s
- JVM 内存：容器内设置 `-XX:MaxRAMPercentage=75`；小内存实例（<512MB）考虑 GraalVM Native 或调小堆
- 冷启动敏感（Serverless）：GraalVM Native、CRaC、Quarkus
- 注意：Vercel / Netlify **不适合**跑 Java 后端

**Node / TS**
- 全栈框架：Vercel、Netlify、Cloudflare、或 Docker 自托管（Next.js `output: 'standalone'`）
- 独立 API：Railway、Fly.io、Render、Cloud Run、Lambda（Hono 适配器）、Cloudflare Workers（Hono）
- Worker/队列消费者：必须部署为常驻进程（容器/VPS），不能放 Serverless Functions

### 7.4 VPS 自托管标准拓扑（预算最低、学习价值最高）

```
Internet → Cloudflare (DNS + CDN + WAF, 橙云代理)
        → VPS
            ├── Caddy / Traefik / Nginx（自动 HTTPS，反向代理）
            ├── frontend（静态文件或 Node SSR 容器）
            ├── backend（Spring Boot / Node 容器）
            ├── postgres（或外置托管 DB）
            └── redis / valkey
        备份：pg_dump / restic → R2 / S3（每日）
        监控：Uptime Kuma + Netdata / Beszel
        部署：GitHub Actions → 构建镜像推送 GHCR → SSH 执行 docker compose pull && up -d
              或 Coolify / Dokploy / Kamal
```

安全基线：仅开放 80/443（与 SSH）；SSH 密钥登录、禁用 root 密码；UFW/云防火墙；fail2ban；自动安全更新；管理面板通过 WireGuard / Tailscale 访问；数据库不暴露公网。

### 7.5 容器化与编排

- Dockerfile：多阶段构建、非 root 用户、固定基础镜像版本、`.dockerignore`
- Java 镜像：Jib 或分层 jar（`spring-boot:build-image`），基础镜像用 Eclipse Temurin / distroless
- Node 镜像：`node:<lts>-slim` / distroless，`pnpm deploy` 精简依赖
- 本地开发：Docker Compose / Dev Containers
- K8s 生态：Helm / Kustomize、**Argo CD / Flux**（GitOps）、cert-manager、external-dns、Karpenter / HPA / KEDA（按队列长度伸缩）、Istio / Linkerd（服务网格，按需）

### 7.6 CI/CD

| 工具 | 适用 |
|---|---|
| **GitHub Actions** | 默认 |
| GitLab CI | GitLab 用户、自托管 |
| Jenkins | 传统企业、Java 存量 |
| Argo CD / Flux | K8s GitOps 持续部署 |
| Vercel / Netlify / Railway 内置 | PaaS 自动部署 |

标准流水线：
```
PR → lint + typecheck + 单元测试 + 安全扫描 → 构建镜像 → 预览环境（Preview）
main → 集成/E2E 测试 → 推送镜像（按 git sha 打 tag）→ 部署 staging → 冒烟测试
tag/手动审批 → 部署 production（金丝雀/滚动）→ 健康检查 → 失败自动回滚
```

Monorepo：Turborepo / Nx 远程缓存 + 按变更范围构建（affected）。

### 7.7 发布策略

滚动更新（默认）、蓝绿部署（快速回滚）、金丝雀发布（按比例放量）、功能开关（发布与上线解耦）、数据库迁移与代码部署分离（Expand-Contract）。

### 7.8 基础设施即代码（IaC）

| 工具 | 说明 |
|---|---|
| **Terraform / OpenTofu** | 事实标准，多云 |
| Pulumi | 用 TS / Java 等通用语言写 IaC |
| AWS CDK | AWS 专属，TS/Java |
| **SST** | TS 全栈在 AWS/Cloudflare 上部署的高层框架 |
| Ansible | 服务器配置管理 |

### 7.9 环境与密钥管理

- 环境：local → preview（每个 PR）→ staging → production，配置差异化只通过环境变量
- 密钥：**不要提交 `.env`**；使用 Doppler、Infisical、1Password Secrets、AWS Secrets Manager、GCP Secret Manager、Vault；K8s 用 External Secrets Operator
- 环境变量校验：TS 用 `@t3-oss/env` + Zod；Spring 用 `@ConfigurationProperties` + `@Validated`

### 7.10 云厂商与地域选择

| 目标市场 | 推荐 |
|---|---|
| 欧盟 | AWS eu-west-1（爱尔兰）/ eu-central-1、GCP europe-west、Azure、Hetzner（德/芬）、Scaleway、OVH；注意 GDPR 数据驻留 |
| 北美 | AWS us-east-1 / us-west-2、GCP、Azure |
| 全球 | Cloudflare 边缘 + 多区域容器（Fly.io / Cloud Run 多区域） |
| 中国大陆 | 阿里云、腾讯云、华为云；**必须 ICP 备案**才能用境内服务器提供网站服务；海外服务访问受限，需使用国内替代（支付、认证、推送、地图、CDN） |
| 中国 + 海外 | 两套独立部署，数据分区；香港/新加坡节点作海外部署或跨境过渡 |

### 7.11 平台迁移路径

架构演进时常见的两类托管迁移，按步骤推进，避免一次性切换：

| 场景 | 触发条件 | 步骤 |
|---|---|---|
| Serverless → 容器平台 | 函数时长/并发受限、需要常驻 worker 或 WebSocket、流量上来后账单陡增 | 1) 应用容器化（Next.js `standalone` / Spring Boot 镜像）2) 在 Railway / Fly.io / Cloud Run 建立同构环境 3) 数据库改用连接池或迁至同地域托管库 4) 蓝绿切流（DNS 或 CDN 权重）5) 观察一段时间后下线旧部署 |
| VPS 自托管 → 托管平台 | 团队扩大、运维负担过重、需要多可用区与自动伸缩 | 1) 用 IaC（Terraform / Pulumi）描述目标环境 2) 先迁无状态服务，再迁数据库（逻辑复制或只读副本追平后切主）3) 新旧环境并行运行一段时间 4) 完成切换并保留回滚窗口 |

原则：数据库迁移与应用切换分开进行；每一步都有回滚方案；迁移前后对比关键指标（延迟、错误率、成本）。
