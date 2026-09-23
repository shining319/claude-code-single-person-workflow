# 非功能性需求：性能、可靠性、安全、合规、成本

> 适用范围：NFR 设计与评审：性能优化、可靠性模式、OWASP 对照、合规要求、成本分级
> 来源：《现代软件系统架构设计与托管部署参考手册》，章节编号 §x 与原手册一致，便于交叉引用。
> 时效：信息核验于 2026-09。版本号只写主版本；价格、免费额度、许可证以官网当期为准，输出方案时标注「需核验」。

**目录**：§8.1 性能 · §8.2 可靠性 · §8.3 安全（OWASP Top 10） · §8.4 合规 · §8.5 成本分级参考

---

## 8. 非功能性需求：性能、可靠性、安全、合规、成本

### 8.1 性能

- 前端：Core Web Vitals（LCP、INP、CLS）；代码分割、图片优化、字体子集、预加载、减少客户端 JS
- 后端：N+1 查询检测、索引、分页（游标分页优于 offset）、连接池（HikariCP）、批处理、异步化
- 网络：HTTP/2/3、Brotli 压缩、CDN 边缘缓存、`Cache-Control` 与 ETag

### 8.2 可靠性

- 无状态服务 + 水平扩展；会话外置
- 健康检查（liveness / readiness）、优雅停机
- 超时、重试（指数退避 + 抖动）、熔断、舱壁隔离、降级
- 限流：网关层（令牌桶）+ 应用层（Bucket4j、Resilience4j、`@upstash/ratelimit`）
- 多可用区部署；关键数据跨区备份
- SLO + 错误预算；告警基于症状（用户可感知）而非原因

### 8.3 安全（OWASP Top 10 对照）

| 风险 | 措施 |
|---|---|
| 注入 | 参数化查询 / ORM；禁止字符串拼 SQL |
| 失效的访问控制 | 服务端逐接口鉴权；对象级权限（防 IDOR）；默认拒绝 |
| 认证缺陷 | 成熟认证库；MFA；登录限流；安全的密码哈希（Argon2 / bcrypt） |
| XSS | 框架默认转义；CSP；谨慎使用 `dangerouslySetInnerHTML` / `v-html` |
| CSRF | SameSite Cookie + CSRF Token（Cookie 会话时） |
| 敏感数据泄露 | 全链路 HTTPS；静态加密；日志脱敏；最小权限 IAM |
| 依赖漏洞 | Dependabot / Renovate；SCA 扫描；锁定版本 |
| SSRF | 出站请求白名单 |
| 配置错误 | CORS 精确配置、关闭调试端点、Actuator 不暴露公网、安全响应头 |
| 供应链 | 镜像签名（cosign）、SBOM、最小基础镜像 |

边界防护：Cloudflare WAF / AWS WAF、DDoS 防护、Bot 管理、Turnstile / reCAPTCHA。

### 8.4 合规

| 法规 | 要点 |
|---|---|
| **GDPR（欧盟）** | 合法基础、同意管理（Cookie Banner）、数据主体权利（导出/删除）、DPA、数据驻留与跨境传输（SCC）、隐私设计 |
| PIPL（中国） | 个人信息境内存储、出境安全评估、单独同意 |
| PCI DSS | 不自行存储卡号，使用 Stripe Elements / Checkout 等托管组件 |
| SOC 2 / ISO 27001 | B2B SaaS 企业客户常要求；审计日志、访问控制、变更管理 |
| HIPAA | 医疗数据，需签 BAA 的云服务 |
| 无障碍（WCAG / 欧盟 EAA） | 语义化 HTML、键盘可达、对比度；欧盟无障碍法案已对部分数字服务生效 |

### 8.5 成本分级参考（月，量级估算，需按当期价格核验）

| 档位 | 典型组合 | 量级 |
|---|---|---|
| $0 学习/MVP | Vercel Hobby / Cloudflare 免费 + Neon/Supabase 免费 + Upstash 免费 | $0（注意免费档商用限制与休眠） |
| 个人/小项目 | 单台 VPS（Hetzner / DO）+ Coolify + R2 | $5–$30 |
| 初创生产 | Vercel Pro + Railway/Render + 托管 Postgres + Sentry | $50–$300 |
| 成长期 | Cloud Run / ECS + RDS + Redis + CDN + 可观测性 SaaS | $300–$3000 |
| 企业 | K8s 多环境 + 多 AZ + 专业可观测性 | $3000+ |

成本陷阱：出口流量费、NAT Gateway、闲置 RDS、日志摄入量、Serverless 函数执行时长、托管平台按席位计费。

