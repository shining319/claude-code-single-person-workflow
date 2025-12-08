# 安装指南

## 前置要求

在安装单人工作流插件之前，请确保您已具备：

- 已安装并配置 **Claude Code CLI**
- 系统已安装 **Git**
- 已配置有效的 **Claude API 密钥**

## 安装方式

### 方式一：安装完整市场（推荐新用户）

一次性安装所有插件以获得完整体验：

```bash
claude plugin install github:shining319/claude-code-single-person-workflow
```

这将安装：
- 全部 5 个专业技能
- 产品开发套件
- 全部 6 个工作流代理

### 方式二：安装产品开发套件

在一个包中获取所有技能，不包含工作流代理：

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-development-suite
```

**包含内容：**
- 学术写作
- 数据库设计器
- 产品经理
- UI设计师
- 解决方案架构师

### 方式三：仅安装工作流代理

如果您只需要智能工作流编排：

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-workflow-agents
```

**包含 6 个代理：**
- 全栈产品构建者
- 产品需求分析师
- 数据库架构规划师
- UI/UX设计协调员
- 技术解决方案设计师
- 文档生成器

### 方式四：安装单个插件

仅安装您需要的特定技能：

#### 学术写作
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/academic-writing
```

#### 数据库设计器
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

#### 产品经理
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-manager
```

#### UI设计师
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/ui-designer
```

#### 解决方案架构师
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/solution-architect
```

## 验证安装

安装后，验证插件是否可用：

```bash
claude plugin list
```

您应该能看到已安装的插件列表。要验证特定技能是否正常工作：

```bash
claude skill list
```

## 更新插件

更新所有已安装的插件到最新版本：

```bash
claude plugin update
```

更新特定插件：

```bash
claude plugin update github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

## 卸载

卸载特定插件：

```bash
claude plugin uninstall github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

卸载此市场的所有插件：

```bash
claude plugin uninstall github:shining319/claude-code-single-person-workflow
```

## 故障排除

### 插件未找到

如果遇到"插件未找到"错误：

1. 检查您的网络连接
2. 验证仓库 URL 是否正确
3. 确保您使用的是最新版本的 Claude Code CLI

### 技能未激活

如果技能没有按预期激活：

1. 检查插件是否已安装：`claude plugin list`
2. 验证技能是否可用：`claude skill list`
3. 尝试使用更具体的触发词（参见[用户指南](user-guide.md)）
4. 重启您的 Claude Code 会话

### 权限问题

如果遇到权限错误：

- 在 Linux/macOS：可能需要使用 `sudo` 或调整文件权限
- 在 Windows：以管理员身份运行终端

### 获取帮助

如果遇到此处未涵盖的问题：

1. 查看[用户指南](user-guide.md)获取使用技巧
2. 查阅[架构文档](architecture.md)了解插件结构
3. 在 [GitHub 仓库](https://github.com/shining319/claude-code-single-person-workflow/issues)中提交问题

## 下一步

安装完成后，请查看[用户指南](user-guide.md)学习如何有效使用插件。
