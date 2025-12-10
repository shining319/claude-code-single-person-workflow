# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2025-12-10

### Added

#### Development Standards & Workflow Rules

- **Slash Commands & Command Usage Guidelines**
  - Standardized command naming conventions
    - Individual plugins: `/plugin-name` (e.g., `/database-designer`)
    - Suite plugins: `/spw-*` prefix (e.g., `/spw-db`, `/spw-ui`)
    - Workflow plugins: Descriptive names (e.g., `/build-dev-workflow`)
  - Command frontmatter field restrictions
    - Allowed fields: `description`, `argument-hint`, `allowed-tools`, `model`
    - Removed `description_zh` from command frontmatter
    - Chinese descriptions now maintained in docs/READMEs only

- **Model Configuration Strategy**
  - Introduced inherit-first model configuration approach
  - Agents and commands default to `model: inherit`
  - Skills inherit model from invocation context (no `model` field in skills)
  - Plugin configurations (`plugin.json`) do not specify models
  - Explicit model override (`opus`, `haiku`, `sonnet`) only when strongly justified

### Changed

#### Documentation Updates
- **`.claude/CLAUDE.md`**: Added comprehensive workflow guidelines (Slash Commands, Model Configuration, Planning Process)
- **`.augment/rules/auggie-workflow.md`**: Synchronized with CLAUDE.md workflow rules for Augment Agent
- **`docs/en/architecture.md`** & **`docs/zh/architecture.md`**: Added command usage patterns and model configuration strategy sections
- **`IMPLEMENTATION_SUMMARY.md`**: Updated architecture capabilities to reflect new development standards

## [1.1.0] - 2025-12-08

### Added

#### Slash Commands
- **11 slash commands** for quick access to skills and workflows
  - **5 single-skill plugin commands**: Individual plugin activation
    - `/academic-writing [topic]` - Academic writing assistant
    - `/database-designer [requirements]` - Database schema design
    - `/product-manager [idea]` - Product requirements and PRD creation
    - `/ui-designer [page/feature]` - UI/UX design specifications
    - `/solution-architect [system]` - Technical architecture design
  - **5 suite plugin commands**: Product-development-suite shortcuts (spw = single-person workflow)
    - `/spw-db [requirements]` - Database design
    - `/spw-ui [page/feature]` - UI design
    - `/spw-prd [idea]` - Product requirements
    - `/spw-arch [system]` - Architecture design
    - `/spw-writing [topic]` - Academic writing
  - **1 workflow command**: Complete development workflow orchestration
    - `/build-dev-workflow [product description]` - End-to-end product development

#### Command Features
- Follows Claude Code official specification
- Minimal frontmatter with only supported fields
- Dynamic parameter passing via `$ARGUMENTS`
- Auto-completion support in Claude Code CLI
- Argument hints for better user experience

### Changed

#### Documentation Updates (All Files)
- **README.md**:
  - Added dual activation methods (Natural Language vs Slash Commands)
  - Added Quick Command Reference table
  - Included slash command examples for all plugin types
- **docs/en/user-guide.md** & **docs/zh/user-guide.md**:
  - Added "Using Skills: Two Methods" comprehensive section
  - Updated Quick Reference table with slash command column
  - Added slash command examples for all 5 skills and workflow agents
  - Added "Slash Command Best Practices" section
  - Enhanced all usage examples to show both activation methods
- **docs/en/installation.md** & **docs/zh/installation.md**:
  - Added "Testing Slash Commands" section
  - Organized test commands by plugin type
  - Enhanced troubleshooting with slash command solutions
- **docs/en/architecture.md** & **docs/zh/architecture.md**:
  - Updated plugin structure to include `commands/` directory
  - Added slash command activation pathway documentation
  - Added "Command Naming Conventions" section
  - Enhanced skill activation flow with dual methods
  - Updated troubleshooting for slash command issues

### Technical Details
- **Command files location**: `plugins/*/commands/*.md`
- **Command structure**: Markdown files with YAML frontmatter
- **Total commands**: 11 unique slash commands
- **Command naming**:
  - Individual plugins: Full plugin name (`/database-designer`)
  - Suite plugins: `spw-` prefix (`/spw-db`)
  - Workflow: Descriptive name (`/build-dev-workflow`)
- **Compliance**: Claude Code official plugin specification

## [1.0.0] - 2025-12-07

### Added

#### Skills
- **academic-writing-style** - Personalized academic writing assistant for Chinese and English
- **database-designer** - Comprehensive database design with ER diagrams (MySQL, PostgreSQL, SQL Server)
- **product-manager** - Product management from requirements analysis to PRD creation
- **ui-designer** - UI/UX design with detailed specifications and user flows
- **solution-architect** - Technical architecture design and technology selection

#### Plugins
- **academic-writing** - Individual skill plugin for academic writing
- **database-designer** - Individual skill plugin for database design
- **product-manager** - Individual skill plugin for product management
- **ui-designer** - Individual skill plugin for UI/UX design
- **solution-architect** - Individual skill plugin for solution architecture
- **product-development-suite** - All-in-one package with all 5 skills
- **product-workflow-agents** - Intelligent workflow orchestration with 6 specialized agents

#### Workflow Agents
- **Product Manager Agent** - Requirements analysis and PRD creation workflow
- **Solution Architect Agent** - Technical architecture and deployment planning workflow
- **Database Architect Agent** - Database schema design workflow
- **UI/UX Designer Agent** - Interface design and specifications workflow
- **Technical Writer Agent** - Documentation and technical writing workflow
- **Full Stack Product Builder Agent** - End-to-end product development orchestrator

#### Documentation
- Bilingual documentation (English and Chinese)
- Installation guides
- User guides
- Architecture documentation
- Individual plugin READMEs

#### Features
- Complete marketplace structure
- Modular plugin architecture
- Skill reusability across plugins
- Agent-based workflow orchestration
- Production-ready best practices
- DrawDB format support for database design
- Comprehensive Chinese comments for all database schemas

### Technical Details

- **Total Plugins**: 7 (5 skills + 1 suite + 1 agents)
- **Total Skills**: 5 unique specialized skills
- **Total Agents**: 6 intelligent workflow agents
- **Supported Languages**: Chinese, English
- **License**: MIT

---

[1.2.0]: https://github.com/shining319/claude-code-single-person-workflow/releases/tag/v1.2.0
[1.1.0]: https://github.com/shining319/claude-code-single-person-workflow/releases/tag/v1.1.0
[1.0.0]: https://github.com/shining319/claude-code-single-person-workflow/releases/tag/v1.0.0
