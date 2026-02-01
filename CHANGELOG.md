# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.4.0] - 2025-01-12

### Added

#### New Skill & Plugin
- **ui-ux-pro-max**: Data-driven UI/UX design intelligence plugin
  - **Searchable Design Knowledge Base**: BM25-powered search across 50+ styles, 21 color palettes, 50 font pairings
  - **Multi-Framework Support**: Guidelines for React, Next.js, Vue, Svelte, SwiftUI, React Native, Flutter, Tailwind, shadcn/ui
  - **Design System Data**: Comprehensive CSV-based design knowledge (styles, colors, typography, UX guidelines, framework-specific best practices)
  - **Professional UI Checklists**: Pre-delivery quality checks for production-ready designs
  - **Python-Powered Search**: Pure Python implementation with no external dependencies
  - **Independent Plugin**: Available at `/plugins/ui-ux-pro-max/`
  - **Suite Integration**: Added to both `product-development-suite` and `product-workflow-agents`

#### New Agent
- **ui-ux-pro-max agent**: Workflow orchestration for data-driven design recommendations
  - Four-phase workflow: Requirements Analysis → Design Intelligence Search → Framework-Specific Guidance → Design Recommendations
  - Automatic activation patterns for design-related queries
  - Comprehensive deliverables: design recommendations, implementation guides, design tokens, resource links

#### New Commands
- `/ui-ux-pro-max` - Independent plugin command
- `/spw-ui-pro-max` - Suite command for product-development-suite and product-workflow-agents

### Changed

#### Configuration Updates
- **marketplace.json**: Added ui-ux-pro-max plugin entry (total plugins: 7 → 8)
- **sync-skills.js**: Updated skill synchronization logic to include ui-ux-pro-max
- **CLAUDE.md**: Updated statistics (6 skills, 7 agents), command tables, and usage examples
- **README files**: Updated suite plugin READMEs to include ui-ux-pro-max in available skills/agents

#### Documentation
- Updated all relevant documentation to reflect new plugin (IMPLEMENTATION_SUMMARY.md, CLAUDE.md, README.md)
- Added comprehensive bilingual README for ui-ux-pro-max plugin

### Fixed

#### Commands
- **spw-ui-pro-max**: Corrected command to invoke `ui-ux-pro-max agent` instead of skill
  - **Issue**: Command was calling skill directly, causing conflicts with `/ui-ux-pro-max` command from ui-ux-pro-max plugin
  - **Resolution**: Updated to call agent for workflow orchestration (Requirements Analysis → Design Intelligence → Framework Guidance → Recommendations)
  - **Impact**: `/spw-ui-pro-max` now properly invokes the multi-phase agent workflow instead of the lightweight skill

## [1.3.0] - 2025-01-11

### Changed

#### Skills

- **ui-designer**: Optimized workflow from 5 steps to streamlined 3-step process
  - **Workflow Simplification**: Reduced from 5-step interaction (需求收集 → 页面规划 → /设计 → /下一步 → /流程图) to 3-step flow (需求收集 → 页面规划 → 模式选择 → 输出)
  - **Removed Interactive Commands**: Eliminated `/设计`, `/下一步`, `/流程图` slash commands for cleaner user experience
  - **Dual-Mode Output**: Added choice between code implementation and design documentation
    - **Code Implementation Mode**: Generates production-ready frontend code (HTML/CSS/JS or React/Vue) with integrated Design Thinking and Frontend Aesthetics Guidelines
    - **Design Documentation Mode**: Produces comprehensive single-file UI specification (`ui-specification.md`)
  - **Design Quality Enhancement**:
    - Integrated Design Thinking framework for strategic design decisions
    - Added Frontend Aesthetics Guidelines to avoid generic AI aesthetics
    - Emphasis on distinctive, memorable designs with intentional aesthetic direction
  - **File Output Clarification**: `design/` directory now exclusively stores design documentation; code files placed flexibly based on project structure
  - **Documentation Updated**: Updated user guides and README to reflect new capabilities
  - Line count reduced from 286 to 232 (19% reduction) while adding significant functionality

## [1.2.1] - 2025-12-11

### Fixed

#### Command Agent Invocation
- **Fixed 5 slash commands to correctly invoke agents instead of skills**
  - `spw-prd.md`: Now correctly invokes `product-manager agent` (was: `product-manager skill`)
  - `spw-db.md`: Now correctly invokes `database-architect agent` (was: `database-designer skill`)
  - `spw-ui.md`: Now correctly invokes `ui-ux-designer agent` (was: `ui-designer skill`)
  - `spw-arch.md`: Now correctly invokes `solution-architect agent` (was: `solution-architect skill`)
  - `spw-writing.md`: Now correctly invokes `technical-writer agent` (was: `academic-writing-style skill`)
  - **Impact**: Commands now properly delegate to specialized agents with independent context windows
  - **Compliance**: Aligns with Claude Code official documentation on agent invocation patterns

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

- **File Output Conventions**
  - Standardized output directory structure: `outputs/<project-name>/`
  - Organized by type: `docs/`, `architecture/`, `database/`, `design/`, `writing/`
  - Follows Anthropic's official Claude Code standards
  - Alternative traditional structure supported: `./docs/`, `./database/`, etc.
  - File naming conventions: kebab-case with optional version/date stamps
  - Bilingual file naming support: `technical-analysis-en.md`, `technical-analysis-zh.md`

- **Comprehensive Documentation Updates**
  - Updated all 5 source skills with detailed output convention sections
  - Synced 15 plugin skill files via `npm run sync`
  - Updated all 6 workflow agents with output file locations
  - Updated all 7 plugin READMEs with bilingual output location sections
  - Updated architecture docs (Chinese & English)
  - Updated user guides (Chinese & English)
  - **Total: 37 files updated** for consistent output conventions across the entire marketplace

### Changed

#### Documentation Updates
- **`.claude/CLAUDE.md`**: Added comprehensive workflow guidelines (Slash Commands, Model Configuration, Planning Process)
- **`.augment/rules/auggie-workflow.md`**: Synchronized with CLAUDE.md workflow rules for Augment Agent
- **`docs/en/architecture.md`** & **`docs/zh/architecture.md`**: Added command usage patterns, model configuration strategy, and updated file output conventions
- **`docs/en/user-guide.md`** & **`docs/zh/user-guide.md`**: Updated "Saving Output" sections with new output conventions
- **`IMPLEMENTATION_SUMMARY.md`**: Updated architecture capabilities to reflect new development standards

#### Skills & Agents
- **All 5 Source Skills**:
  - Added comprehensive "File Output Convention" sections with directory structure, naming conventions, and examples
  - Updated `description` to bilingual format (English | Chinese) for better skill discovery and Claude's autonomous skill invocation
- **All 6 Workflow Agents**:
  - Added "Output File Locations" sections with complete deliverable organization
  - **Removed `description_zh` field** (non-compliant with Claude Code official specification)
  - **Merged Chinese content into `description` field** using bilingual format (English | Chinese)
  - Now fully compliant with Claude Code agent frontmatter specification
- **All 7 Plugin READMEs**: Added bilingual output location documentation for user discoverability

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
