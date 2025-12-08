# Installation Guide

## Prerequisites

Before installing the Single Person Workflow plugins, ensure you have:

- **Claude Code CLI** installed and configured
- **Git** installed on your system
- An active **Claude API key** configured with Claude Code

## Installation Methods

### Method 1: Install Entire Marketplace (Recommended for New Users)

Install all plugins at once for the complete experience:

```bash
claude plugin install github:shining319/claude-code-single-person-workflow
```

This will install:
- All 5 specialized skills
- The product development suite
- All 6 workflow agents

### Method 2: Install Product Development Suite

Get all skills in one package without the workflow agents:

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-development-suite
```

**Includes:**
- Academic Writing
- Database Designer
- Product Manager
- UI Designer
- Solution Architect

### Method 3: Install Workflow Agents Only

If you only need intelligent workflow orchestration:

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-workflow-agents
```

**Includes 6 agents:**
- Full Stack Product Builder
- Product Requirements Analyzer
- Database Architecture Planner
- UI/UX Design Coordinator
- Technical Solution Designer
- Documentation Generator

### Method 4: Install Individual Plugins

Install only specific skills you need:

#### Academic Writing
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/academic-writing
```

#### Database Designer
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

#### Product Manager
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/product-manager
```

#### UI Designer
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/ui-designer
```

#### Solution Architect
```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/solution-architect
```

## Verification

After installation, verify the plugins are available:

```bash
claude plugin list
```

You should see your installed plugins listed. To verify a specific skill is working:

```bash
claude skill list
```

## Updating Plugins

To update all installed plugins to the latest version:

```bash
claude plugin update
```

To update a specific plugin:

```bash
claude plugin update github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

## Uninstalling

To remove a specific plugin:

```bash
claude plugin uninstall github:shining319/claude-code-single-person-workflow/plugins/database-designer
```

To remove all plugins from this marketplace:

```bash
claude plugin uninstall github:shining319/claude-code-single-person-workflow
```

## Troubleshooting

### Plugin Not Found

If you get a "plugin not found" error:

1. Check your internet connection
2. Verify the repository URL is correct
3. Ensure you have the latest version of Claude Code CLI

### Skill Not Activating

If a skill doesn't activate when you expect it to:

1. Check that the plugin is installed: `claude plugin list`
2. Verify the skill is available: `claude skill list`
3. Try using more specific trigger words (see [User Guide](user-guide.md))
4. Restart your Claude Code session

### Permission Issues

If you encounter permission errors:

- On Linux/macOS: You may need to use `sudo` or adjust file permissions
- On Windows: Run your terminal as Administrator

### Getting Help

If you encounter issues not covered here:

1. Check the [User Guide](user-guide.md) for usage tips
2. Review the [Architecture](architecture.md) documentation
3. Open an issue on the [GitHub repository](https://github.com/shining319/claude-code-single-person-workflow/issues)

## Next Steps

Once installed, proceed to the [User Guide](user-guide.md) to learn how to use the plugins effectively.
