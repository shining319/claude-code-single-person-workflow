# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2025-12-08

### Added

#### Slash Commands
- **16 minimal slash commands** for quick access to skills and workflows
  - **5 single-skill plugin commands**: Use full plugin names for clarity
    - `/academic-writing` - Academic writing assistant
    - `/database-designer` - Database schema design
    - `/product-manager` - PRD creation
    - `/ui-designer` - UI/UX design
    - `/solution-architect` - Technical architecture
  - **5 product-development-suite commands**: Use `spw-` prefix (single-person workflow)
    - `/spw-db` - Database design
    - `/spw-ui` - UI design
    - `/spw-prd` - Product management
    - `/spw-arch` - Architecture design
    - `/spw-writing` - Academic writing
  - **6 product-workflow-agents commands**: Suite commands + workflow orchestration
    - All 5 `spw-*` commands from suite
    - `/build-dev-workflow` - Complete product development workflow

#### Command Features
- Follow Claude Code official specification
- Minimal frontmatter (4-6 lines per command)
- Support for `$ARGUMENTS` parameter passing
- Only official fields: `description`, `argument-hint`, `allowed-tools`, `model`
- No `description_zh` field (not supported by Claude Code)

### Changed

#### Documentation
- **CLAUDE.md**: Added comprehensive "Slash Commands" chapter
  - Command structure explanation
  - Complete command reference tables
  - Usage examples
  - Creating new commands guide
- **Plugin Structure**: Enhanced diagram to include `.claude/commands/` directory
- **File Naming Conventions**: Added command file naming rules (`kebab-case.md`)

### Technical Details
- **Command files location**: `plugins/*/.claude/commands/*.md`
- **Template structure**:
  ```markdown
  ---
  description: Command description
  argument-hint: "[parameter hint]"
  ---

  Use the SKILL_NAME skill. User input: $ARGUMENTS
  ```
- **Total commands**: 16 (5 + 5 + 6)
- **Average file size**: 4-6 lines
- **Compliance**: Claude Code official specification

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

[1.1.0]: https://github.com/shining319/claude-code-single-person-workflow/releases/tag/v1.1.0
[1.0.0]: https://github.com/shining319/claude-code-single-person-workflow/releases/tag/v1.0.0
