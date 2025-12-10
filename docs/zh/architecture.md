# 架构文档

## 概述

单人工作流市场被设计为 Claude Code 的模块化、可扩展插件系统。本文档解释了架构、设计决策以及组件如何协同工作。

## 系统架构

```
Claude Code CLI
    │
    ├─── 单人工作流市场（根目录）
    │       │
    │       ├─── 独立技能
    │       │     ├─── academic-writing（学术写作）
    │       │     ├─── database-designer（数据库设计器）
    │       │     ├─── product-manager（产品经理）
    │       │     ├─── ui-designer（UI设计师）
    │       │     └─── solution-architect（解决方案架构师）
    │       │
    │       ├─── 技能套件
    │       │     └─── product-development-suite（产品开发套件）
    │       │           （打包所有5个技能）
    │       │
    │       └─── 工作流代理
    │             └─── product-workflow-agents（产品工作流代理）
    │                   ├─── 全栈产品构建者
    │                   ├─── 产品需求分析师
    │                   ├─── 数据库架构规划师
    │                   ├─── UI/UX设计协调员
    │                   ├─── 技术解决方案设计师
    │                   └─── 文档生成器
```

## 核心概念

### 1. 技能（Skills）

**定义:** 技能是 Claude Code 可以调用来执行特定任务的专门能力。

**特征:**
- 单一职责(一个技能,一个目的)
- 通过自然语言或斜杠命令触发
- 产生特定的输出格式
- 无状态(每次调用都是独立的)

**激活方法:**
1. **自然语言**: 基于用户意图的自动检测
   - 示例: "为我的应用设计数据库" → 数据库设计器激活
2. **斜杠命令**: 通过命令显式激活
   - 示例: `/database-designer "电商系统"` → 直接激活

**实现：**
```
plugins/
  └─── skill-name/
       ├─── skill.md          # 技能提示和说明
       └─── examples/         # 使用示例（可选）
```

### 2. 技能套件（Skill Suites）

**定义：** 为方便起见而捆绑在一起的相关技能集合。

**优势：**
- 一次安装多个技能
- 能力的逻辑分组
- 降低安装复杂性

**实现：**
```
plugins/
  └─── suite-name/
       ├─── skill.md          # 套件元数据
       └─── skills/           # 捆绑的独立技能
            ├─── skill-1/
            ├─── skill-2/
            └─── skill-3/
```

### 3. 工作流代理（Workflow Agents）

**定义：** 编排多个技能和任务以完成复杂工作流的智能代理。

**能力：**
- 多步骤任务协调
- 自动技能选择
- 跨步骤的上下文管理
- 决策制定和规划

**实现：**
```
plugins/
  └─── workflow-agents/
       ├─── agent.md          # 代理配置
       └─── agents/
            ├─── agent-1/
            ├─── agent-2/
            └─── agent-3/
```

## 插件结构

### 最小插件

```
plugin-name/
├─── .claude-plugin/
│    └─── plugin.json      # 插件元数据
├─── skills/               # 技能定义
│    └─── skill-name/
│         └─── SKILL.md
└─── README.md             # 可选:文档
```

### 带斜杠命令的完整插件

```
plugin-name/
├─── .claude-plugin/
│    └─── plugin.json      # 插件元数据
├─── skills/               # 技能定义
│    └─── skill-name/
│         ├─── SKILL.md
│         └─── references/ # 参考资料
├─── commands/             # 斜杠命令
│    ├─── command-1.md
│    └─── command-2.md
├─── README.md             # 文档
└─── LICENSE.txt           # 许可证
```

### 斜杠命令结构

每个斜杠命令都是 `commands/` 目录中的一个 Markdown 文件:

```markdown
---
description: 简要命令描述
argument-hint: "[参数提示]"
---

使用 SKILL_NAME 技能。用户输入: $ARGUMENTS
```

**示例:** `/database-designer` 命令文件:
```markdown
---
description: 完整的数据库架构设计和ER图
argument-hint: "[业务领域或需求]"
---

使用 database-designer 技能。用户输入: $ARGUMENTS
```

## 技能定义格式

### 基本结构（skill.md）

```markdown
---
name: skill-name
description: 技能功能的简要描述
triggers:
  - keyword1
  - keyword2
  - phrase pattern
---

# 技能说明

Claude 如何执行此技能的详细说明。

## 输入

预期的输入格式和参数。

## 处理

处理输入的步骤。

## 输出

预期的输出格式和结构。
```

### 示例：数据库设计器

```markdown
---
name: database-designer
description: 完整的数据库架构设计和ER图
triggers:
  - 数据库设计
  - 架构设计
  - ER图
  - 数据模型
---

# 数据库设计器技能

您是数据库设计专家...

[详细说明如下]
```

## 命令使用模式

### 概述

本市场遵循标准化的命令命名约定，以确保所有插件的一致性和可发现性。

### 命名约定

#### 1. 单个技能插件

**模式:** `/plugin-name`

**示例:**
- `/database-designer` - 数据库架构设计
- `/product-manager` - 产品需求和PRD
- `/ui-designer` - UI/UX设计规格
- `/solution-architect` - 技术架构设计
- `/academic-writing` - 学术写作辅助

**用途:** 直接激活单个技能

#### 2. 套件插件

**模式:** `/spw-*` (spw = 单人工作流)

**示例:**
- `/spw-db` - 数据库设计（来自 product-development-suite）
- `/spw-prd` - 产品需求（来自 product-development-suite）
- `/spw-ui` - UI设计（来自 product-development-suite）
- `/spw-arch` - 架构设计（来自 product-development-suite）
- `/spw-writing` - 学术写作（来自 product-development-suite）

**用途:** 快速访问 product-development-suite 包中的技能

#### 3. 工作流插件

**模式:** 描述性工作流名称

**示例:**
- `/build-dev-workflow` - 完整的产品开发工作流

**用途:** 编排多个技能的完整端到端工作流

### 命令 Frontmatter 规范

命令在 `plugins/*/commands/*.md` 文件中定义，使用 YAML frontmatter。

#### 允许的字段

- `description` - 命令的英文描述
- `argument-hint` - 命令参数的提示文本（在CLI中显示）
- `allowed-tools` - 命令可以使用的工具（可选）
- `model` - 模型配置（通常为 `inherit`）

#### 重要说明

- 命令 frontmatter **不支持** `description_zh`
- 中文描述应在 README 文件和文档中维护
- 保持命令定义简洁，专注于技能激活
- 使用 `$ARGUMENTS` 变量将用户输入传递给技能

#### 命令文件示例

```markdown
---
description: "Design database schema with ER diagrams"
argument-hint: "[requirements]"
model: inherit
---

使用提供的需求激活 database-designer 技能: $ARGUMENTS
```

### 命令发现

用户可以通过以下方式发现可用命令：
1. **自动补全** - 在 Claude Code CLI 中
2. **文档** - 在 README 文件和用户指南中
3. **自然语言** - 命令也可以通过对话请求发现

## 模型配置策略

### 概述

本市场使用基于继承的模型配置策略，在保持灵活性的同时提供合理的默认值。

### 配置层次结构

#### 1. 技能（Skills）（无 model 字段）

**行为:**
- 技能在其 frontmatter 中**不**指定 `model` 字段
- 它们从调用上下文继承模型
- 这允许同一技能根据调用方式使用不同的模型

**理由:**
- 为用户提供最大灵活性
- 技能保持模型无关性
- 用户可以为其用例选择最佳模型

#### 2. 代理（Agents）（默认: `model: inherit`）

**行为:**
- 工作流代理通常在其 frontmatter 中使用 `model: inherit`
- 这允许代理使用用户或系统指定的模型
- 仅在代理任务需要特定模型时才覆盖

**示例:**
```yaml
---
name: product-manager
description: 产品需求分析和PRD创建
model: inherit
---
```

#### 3. 命令（Commands）（默认: `model: inherit`）

**行为:**
- 斜杠命令通常使用 `model: inherit`
- 这尊重用户的模型偏好
- 仅在命令需要特定模型能力时才覆盖

**示例:**
```yaml
---
description: "Design database schema with ER diagrams"
argument-hint: "[requirements]"
model: inherit
---
```

#### 4. 插件配置（无 model 字段）

**行为:**
- `plugin.json` 文件**不**配置模型
- 模型选择在技能/代理/命令级别处理
- 这使插件元数据专注于结构信息

### 何时覆盖

**仅**在以下情况使用显式模型值（`opus`, `haiku`, `sonnet`）:

1. **需要特定能力**
   - 任务需要只有 `opus` 才能处理的复杂推理
   - 示例: 多步骤架构决策

2. **性能优化**
   - 简单任务可以使用 `haiku` 以获得更快响应
   - 示例: 快速格式转换或简单验证

3. **质量差异**
   - 测试显示模型之间存在显著的质量差异
   - 在注释或文档中记录原因

### 支持的模型值

- `inherit` - 使用调用上下文的模型（推荐默认值）
- `opus` - Claude Opus（最高能力，较慢，成本较高）
- `haiku` - Claude Haiku（快速，高效，成本较低）
- `sonnet` - Claude Sonnet（能力和性能平衡）

### 最佳实践

1. **从 `inherit` 开始** - 所有新代理和命令
2. **记录原因** - 如果覆盖为特定模型
3. **使用不同模型测试** - 验证覆盖是否必要
4. **参考 `.claude/CLAUDE.md`** - 获取详细的模型配置指南
5. **考虑用户偏好** - 用户可能有成本或性能限制

### 配置示例

**良好 - 使用 inherit（推荐）:**
```yaml
---
name: database-architect
description: 数据库架构设计工作流
model: inherit
---
```

**可接受 - 有理由的覆盖:**
```yaml
---
name: complex-architecture-planner
description: 需要深度推理的多系统架构设计
model: opus  # 需要 opus 进行复杂的多步骤推理
---
```

**避免 - 不必要的覆盖:**
```yaml
---
name: simple-formatter
description: 格式化文本输出
model: opus  # ❌ 不必要 - haiku 或 inherit 就可以
---
```

## 代理架构

### 代理类型

1. **编排代理**
   - 协调多个技能
   - 示例：全栈产品构建者

2. **专家代理**
   - 在某一领域具有深厚专业知识
   - 示例：数据库架构规划师

3. **实用代理**
   - 支持和辅助功能
   - 示例：文档生成器

### 代理决策流程

```
用户请求
    │
    ├─── 代理分析请求
    │       │
    │       ├─── 确定所需技能
    │       ├─── 规划执行顺序
    │       └─── 分配资源
    │
    ├─── 代理执行步骤
    │       │
    │       ├─── 步骤1：激活技能A
    │       ├─── 步骤2：激活技能B
    │       └─── 步骤N：激活技能N
    │
    └─── 代理交付结果
            │
            ├─── 组合输出
            ├─── 验证完整性
            └─── 呈现给用户
```

## 与 Claude Code 集成

### 技能激活

技能可以通过两种路径激活:

#### **方法一:自然语言激活**
1. **用户输入:** 用户输入自然语言请求
2. **模式匹配:** Claude Code 将请求与技能触发器匹配
3. **技能加载:** 加载相应的 SKILL.md
4. **上下文注入:** 技能说明被注入到上下文中
5. **执行:** Claude 使用技能说明处理请求
6. **输出:** 格式化并呈现结果

#### **方法二:斜杠命令激活**
1. **用户输入:** 用户输入斜杠命令(例如 `/database-designer "需求"`)
2. **命令解析:** Claude Code 解析命令和参数
3. **直接技能加载:** 直接激活相应的技能
4. **上下文注入:** 命令扩展为技能调用
5. **执行:** Claude 使用技能说明处理
6. **输出:** 格式化并呈现结果

**斜杠命令的优势:**
- 保证技能激活(无歧义)
- 执行更快(不需要模式匹配)
- 显式意图声明
- 更适合自动化和脚本

### 上下文管理

```
会话上下文
    │
    ├─── 用户请求历史
    ├─── 活动技能上下文
    ├─── 生成的输出
    └─── 工作流状态（用于代理）
```

## 设计原则

### 1. 模块化

每个技能都是独立的，可以单独安装/卸载。

**优势：**
- 用户只安装需要的内容
- 易于维护和更新
- 清晰的关注点分离

### 2. 可组合性

技能和代理可以组合创建复杂的工作流。

**示例：**
- 产品经理 → 数据库设计器 → UI设计师
- 解决方案架构师 ← 数据库设计器 → UI设计师

### 3. 可发现性

技能可以通过多种方式发现和激活。

**实现:**
- **自然语言触发器**: 广泛的模式以提高灵活性
  - 相关技能的重叠触发器
  - 基于对话的上下文激活
- **斜杠命令**: 直接命令发现
  - Claude Code 界面中的自动补全
  - 帮助文档列出所有命令
  - 正确使用的参数提示

### 4. 一致性

所有技能遵循相似的模式以提供可预测的用户体验。

**标准：**
- 一致的输出格式
- 可预测的文件位置
- 统一的文档结构

## 文件输出约定

### 推荐方案（遵循 Claude Code 官方规范）

所有生成的文件保存到 `outputs/<project-name>/` 目录，按类型组织：

```
outputs/
└── <project-name>/              # 项目名称（如：task-management-app）
    ├── docs/                    # 产品文档（product-manager）
    │   ├── prd.md
    │   ├── user-personas.md
    │   └── requirements.md
    ├── architecture/            # 技术架构（solution-architect）
    │   ├── system-architecture.md
    │   ├── tech-stack.md
    │   └── deployment-plan.md
    ├── database/                # 数据库设计（database-designer）
    │   ├── schema-design.md
    │   ├── schema.sql
    │   ├── drawdb-schema.json
    │   └── drawdb-schema.dbml
    ├── design/                  # UI/UX 设计（ui-designer）
    │   ├── ui-specification.md
    │   ├── design-system.md
    │   └── user-flows.md
    └── writing/                 # 学术/技术写作（academic-writing）
        ├── technical-analysis.md
        └── project-documentation.md
```

**示例：**
```
outputs/
├── task-management-app/
│   ├── docs/
│   │   └── prd.md
│   ├── database/
│   │   └── schema.sql
│   └── design/
│       └── ui-specification.md
└── e-commerce-platform/
    ├── docs/
    │   └── prd-v1.0.md
    └── architecture/
        └── system-architecture.md
```

**优势：**
- ✅ 隔离性好：每个项目独立目录
- ✅ 易于清理：删除整个项目目录即可
- ✅ 适合自动化：标准化路径便于脚本处理
- ✅ 遵循官方规范：与 Anthropic 官方示例一致

### 替代方案（传统项目结构）

如果你的项目已有固定目录结构，也可以使用传统路径：

```
project-root/
├── database/
│   ├── schema-design.md
│   ├── schema.sql
│   └── er-diagram.json
├── design/
│   ├── ui-specification.md
│   └── wireframes/
├── docs/
│   ├── prd.md
│   ├── api-documentation.md
│   └── technical-specs.md
└── architecture/
    ├── system-architecture.md
    └── deployment-plan.md
```

**适用场景：**
- 现有项目已有固定目录结构
- 需要与现有代码库集成
- 团队已有既定的文件组织规范

### 文件命名约定

- 使用短横线命名法（kebab-case）：`user-authentication-flow.md`
- 包含版本或日期（可选）：`schema-design-v1.0.md` 或 `prd-2024-12-10.md`
- 使用描述性名称：`e-commerce-database-schema.sql`
- 双语文档指定语言：`technical-analysis-zh.md`、`technical-analysis-en.md`

## 可扩展性

### 添加新技能

1. 创建插件目录结构
2. 编写包含清晰说明的 skill.md
3. 定义触发模式
4. 记录使用示例
5. 使用各种输入进行测试

### 创建自定义代理

1. 识别工作流模式
2. 映射所需技能
3. 定义决策逻辑
4. 实现协调策略
5. 测试端到端工作流

### 贡献技能

要贡献新技能：

1. Fork 仓库
2. 按照结构指南创建插件
3. 添加全面的文档
4. 包含使用示例
5. 提交拉取请求

## 性能考虑

### Token 效率

- 技能使用简洁、专注的提示
- 避免冗余说明
- 为常见模式使用模板

### 上下文窗口管理

- 仅在需要时加载技能
- 大型说明被适当分块
- 历史上下文被高效管理

### 缓存策略

- 技能定义可缓存
- 生成的输出引用缓存内容
- 模板减少冗余生成

## 安全考虑

### 输入验证

技能应验证：
- 用户输入参数
- 文件路径目标
- 外部资源引用

### 输出净化

生成的输出应：
- 在 SQL 中转义特殊字符
- 验证文件路径
- 净化用户提供的内容

### 安全默认值

- 保守的权限
- 安全的配置示例
- 最佳实践推荐

## 测试策略

### 技能测试

1. **单元测试：** 单个技能激活
2. **集成测试：** 技能组合
3. **回归测试：** 更新间的一致性

### 代理测试

1. **工作流测试：** 完整的代理流程
2. **边缘情况测试：** 不寻常的请求
3. **性能测试：** 大规模操作

## 未来增强

### 计划功能

1. **交互式代理：** 多轮对话
2. **可自定义模板：** 用户定义的输出格式
3. **技能市场：** 社区贡献的技能
4. **版本管理：** 技能版本控制和兼容性

### 潜在集成

1. **外部工具：** 与设计工具、数据库集成
2. **CI/CD 流水线：** 自动文档生成
3. **项目模板：** 初始化项目结构

## 命令命名约定

### 单技能插件
单个插件使用完整的插件名称作为其命令:
- `/database-designer` - 数据库设计器插件
- `/product-manager` - 产品经理插件
- `/ui-designer` - UI设计师插件
- `/solution-architect` - 解决方案架构师插件
- `/academic-writing` - 学术写作插件

### 套件插件
套件插件使用 `spw-` 前缀(单人工作流):
- `/spw-db` - 数据库设计(来自 product-development-suite)
- `/spw-prd` - 产品需求(来自 product-development-suite)
- `/spw-ui` - UI设计(来自 product-development-suite)
- `/spw-arch` - 架构设计(来自 product-development-suite)
- `/spw-writing` - 学术写作(来自 product-development-suite)

### 工作流插件
工作流插件使用描述性的工作流名称:
- `/build-dev-workflow` - 完整的产品开发工作流

## 架构故障排除

### 常见问题

**技能未激活(自然语言):**
- 检查触发模式是否匹配
- 验证 SKILL.md 格式是否正确
- 确保插件已安装
- **解决方案**: 使用斜杠命令以保证激活

**斜杠命令未找到:**
- 验证插件安装: `claude plugin list`
- 检查 `commands/` 目录中是否存在命令
- 确保命令文件具有正确的前置信息
- 如需要,重启 Claude Code 会话

**代理协调失败：**
- 审查工作流逻辑
- 检查技能依赖关系
- 验证上下文传递

**输出格式问题：**
- 验证模板结构
- 检查文件路径权限
- 验证输出格式化

## 技术规范

### 支持的格式

- **输入：** 自然语言、Markdown、JSON
- **输出：** Markdown、SQL、JSON、DBML、PlantUML
- **文档：** GitHub 风格的 Markdown

### 依赖

- Claude Code CLI v1.0+
- Git（用于安装）
- Node.js（用于某些生成的输出）

### 兼容性

- **操作系统：** Windows、macOS、Linux
- **Claude 模型：** 所有当前模型
- **Claude Code 版本：** 最新稳定版本

## 开发者最佳实践

### 技能开发

1. 从清晰的用例开始
2. 定义狭窄的范围
3. 编写全面的说明
4. 包含多样化的示例
5. 使用真实场景进行测试

### 代理开发

1. 映射完整的工作流
2. 识别技能依赖关系
3. 处理边缘情况
4. 提供清晰的进度反馈
5. 验证最终输出

### 文档

1. 为初学者编写
2. 包含实际示例
3. 展示常见模式
4. 解释决策理由
5. 保持更新

## 结论

单人工作流市场为构建专门的 Claude Code 能力提供了灵活、可扩展的架构。通过遵循模块化设计原则和清晰的约定，它使独立开发者能够访问专业级工具，进行完整的产品开发。

有关实施细节，请参阅[用户指南](user-guide.md)。有关安装说明，请参阅[安装指南](installation.md)。
