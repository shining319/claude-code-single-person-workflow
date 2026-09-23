# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.7.0] - 2026-09-23

### Added

#### product-manager Skill
- **Two fixed deliverables**: `prd.md` (PRD) and `task-backlog.md` (Task Backlog). The structure follows the user's reference examples
- **PRD template** (`references/prd-template.md`), 11 sections: overview, personas, epics and user stories with acceptance criteria and story points, priority matrix, NFRs, technical architecture, sprint planning, definition of done, risks. New compared with the reference example:
  - 1.4 Out of Scope & Assumptions
  - a Core flow for every P0 epic
  - 5.5 Accessibility & Privacy
  - Section 10 Open Questions
  - Section 11 Next Steps: Task Backlog
  - a status line under the title
  - an EN/ZH heading table
- **Technical architecture placeholders**: with no architecture document and no stated stack, PRD Section 6 is written as `[TBD — pending architecture design]` under a pending notice. No technology is guessed
- **Backlog prerequisites**: the Task Backlog is generated only when an architecture document, a database design and a completed PRD all exist. Otherwise the skill lists what is missing and the commands to run. The chat reply, PRD Section 11 and the docs all state this order
- **Backlog template** (`references/backlog-template.md`):
  - backend (B*) and frontend (F*) tasks per story, each with acceptance criteria, hours and dependencies
  - breakdown rules: 0.5–5 hour tasks, a unit test task for every backend story, dependencies only on the same or earlier sprints
  - sprint summaries and an API endpoint list
  - **Critical Path & Start Order** for each sprint: tasks that can start now, cross-role blockers with earliest unblock hour and a workaround, and the critical path with its total hours
- **Quality checklist** (`references/quality-checklist.md`) to run before delivery:
  - epic points equal the sum of their stories; sprint and hour totals add up
  - section numbering is continuous
  - backlog frameworks match PRD Section 6; tables and APIs match the database and architecture documents
  - dependency IDs exist, with no cycles
  - every acceptance criterion is covered by a task
- **Mode routing**: PRD (default), Backlog, PRD + Backlog, Blocked (a prerequisite is missing), Quick consult

### Changed

#### product-manager Skill
- `SKILL.md` rewritten in English: 7-step workflow, prerequisite check, mode routing, reference map, hard rules. Output language follows the user
- `user-persona-templates.md` now uses the four persona blocks from the reference PRD (basic information, goals & motivations, pain points & challenges, behavioral traits)
- Template example stack checked as of 2026-09:
  - MySQL 8.0 reached EOL in April 2026, so the example uses MySQL 8.4 LTS
  - Spring Boot 4.x
  - Vue 3 + Pinia + Element Plus used consistently; the reference example's "React.js 3" and its React/Vue mix are fixed

#### Agents, Commands and Configuration
- **product-manager agent**: prerequisite check, modes, five-phase workflow; tells the user the next steps when only the PRD is produced
- **full-stack-product-builder agent**:
  - Phase 1 produces the PRD only
  - new Phase 4 Task Backlog runs after architecture and database design and fills PRD Section 6
  - UI/UX and documentation move to Phases 5 and 6
  - output tree now `docs/prd.md` + `docs/task-backlog.md`
- **Commands** `/product-manager` and `/spw-prd` (both suites): bilingual descriptions and argument hints
- **Versions**:
  - product-manager plugin.json: bilingual description, new keywords, 1.0.0 → 1.1.0
  - product-development-suite and product-workflow-agents: 1.2.0 → 1.3.0
  - marketplace.json: 1.6.0 → 1.7.0

#### Documentation
- README.md, docs/en|zh/user-guide.md and the product-manager README describe the recommended order (PRD → architecture → database → PRD again for the backlog) and the three prerequisites
- Output trees in README, architecture and installation guides, plugin READMEs and CLAUDE.md command table updated

### Removed

#### product-manager Skill
- The Task Dependency Diagrams and the Suggested Development Timeline in the backlog, replaced by Critical Path & Start Order
- `references/document-templates.md` and `references/design-workflow.md`, replaced by the new templates and the workflow in `SKILL.md`
- The scattered output files `user-personas.md`, `feature-specs.md`, `user-stories.md`, `mvp-plan.md` and `requirements-analysis.md`

## [1.6.0] - 2026-09-23

### Added

#### solution-architect Skill
- **7-step workflow**: requirements clarification (10 dimensions) → NFR quantification → capacity estimate (formulas and single-instance ceilings) → pattern and stack line → per-layer selection → deployment → design doc and ADRs
- **Mode routing**: full design, design with assumptions, concept only, selection only, deployment only, architecture review
- **10 hard rules**: modular monolith and PostgreSQL by default; every design covers auth, backups, observability, CI/CD and secrets; idempotency for money flows; GDPR / ICP flags; evolution path; explicit trade-offs; "needs verification" for versions and prices
- **New references** (Chinese, from the system architecture handbook):
  - `architecture-patterns.md`: backend/rendering/frontend patterns, main stack decision tree, trade-off table
  - `tech-stack-java.md`: Line A (React/Vue + Spring Boot, Spring Cloud / Alibaba / K8s-native)
  - `tech-stack-typescript.md`: Line B (Next.js, Nuxt, TanStack Start, React Router, Hono, NestJS, ORM, queues, monorepo)
  - `tech-selection-matrix.md`: cross-cutting layers from mobile to observability
  - `data-architecture.md`: database choice, caching, consistency, multi-tenancy, scaling path, backups
  - `nfr-security-compliance.md`: performance, reliability, OWASP, GDPR/PIPL/PCI/HIPAA, cost tiers
  - `reference-architectures.md`: 10 reference architectures (A–J) with Mermaid diagrams
  - `output-templates.md`: 15-section design doc, ADR, launch checklist, anti-patterns, review checklist
- **Architecture review mode** with a per-item pass / risk / fail report

### Changed

#### solution-architect Skill
- `SKILL.md` rewritten around the 7-step workflow, reference map, hard rules, output files and review mode; description adds capacity planning, ADR and review triggers
- `deployment-guide.md` replaced with hosting models, VPS topology, containers, CI/CD, release strategy, IaC, secrets, regions, plus a platform migration section
- Versions and service status checked against sources as of 2026-09: Java 25 LTS, Spring Boot 4.x, Spring AI 2.x, Node.js 24 LTS, Next.js 16, Nuxt 4, Tailwind CSS v4, Prisma 7 (no Rust engine), Drizzle 1.0 still beta; Auth.js now maintained by the Better Auth team; Lucia is a learning resource; Lemon Squeezy still operating alongside Stripe Managed Payments; Redis 8 AGPLv3 option vs Valkey; Eureka still maintained
- Output: `system-architecture.md` and `architecture-decisions.md` always; `tech-stack.md`, `deployment-plan.md`, `cost-estimate.md` when relevant

#### Agents, Commands and Configuration
- **solution-architect agent**: mode selection, 7-step workflow, hard rules, new deliverables and handoff to database-architect
- **full-stack-product-builder agent**: Phase 2 now covers NFRs, capacity, reference architecture and ADRs; hands data-architecture decisions to Phase 3; architecture output tree adds ADR and deployment files
- **Commands** `/solution-architect`, `/spw-arch` (both suites): bilingual descriptions and argument hints
- **solution-architect plugin.json**: bilingual description, new keywords, version 1.0.0 → 1.1.0
- **marketplace.json**: version 1.5.0 → 1.6.0; solution-architect entry updated; product-development-suite and product-workflow-agents → 1.2.0

#### Documentation
- Updated README.md, docs/en|zh/user-guide.md, and the solution-architect, product-development-suite and product-workflow-agents READMEs

### Removed

#### solution-architect Skill
- `references/tech-stacks.md`, including the Go / Rust / Python stacks and the list of seven Java data-access options. The skill now covers only the Java and TypeScript lines
- Outdated statements from the old deployment guide (e.g. "D1 still in beta", "Workers cannot hold WebSocket connections", fixed platform prices)

## [1.5.0] - 2026-09-23

### Added

#### academic-writing-style Skill
- **Three writing modes**: write new (mode A), revise/polish existing drafts (mode B), learn the user's style from samples (mode C)
  - Mode A: outline confirmation for 1500+ Chinese characters / 1000+ English words; long documents written chapter by chapter
  - Mode B: diagnosis report first, then rewrite that keeps facts, data, citations and opinions; outputs `<name>-revised.md` with a change summary; light polish by default, deep rewrite on request
  - Mode C: 7-dimension style analysis saved as reusable `style-profile.md`
- **Plain-writing hard rule**: applies to every document type, mode and language. Chinese sentences mostly under 40 characters (split over 60); English average 15–20 words (rarely over 25), at most one subordinate clause
- **`references/ai-markers.md`**: Chinese and English AI-marker checklist (long sentences, high-frequency words, sentence patterns, structural issues) with replacements and a 4-step self-check
- **`references/revision-and-style.md`**: detailed steps for modes B and C

### Changed

#### academic-writing-style Skill
- `SKILL.md`: added mode routing, rule priority (school format > plain writing > style profile > defaults), outline and section-by-section writing, self-check against ai-markers; description adds revise/polish/style triggers
- `writing-guidelines.md`: plain writing is now principle 1; English sentence limit tightened from 30 to 25 words; transition words like "however / 然而" changed from banned to "use sparingly"; the 5-row replacement table now points to `ai-markers.md`
- `chinese-examples.md` / `english-examples.md`: "expected style" passages rewritten in plain language (Chinese average sentence length 39.9 → 24.2 characters; no sentences over the limits; dashes and "however / crucial / demonstrate / 此外" removed)

#### Agents, Commands and Configuration
- **technical-writer agent**: mode selection, outline confirmation, plain-writing rule, ai-markers self-check, revision/style triggers and outputs
- **Commands** `/academic-writing`, `/spw-writing` (both suites): bilingual descriptions and new argument hints covering the three modes
- **academic-writing plugin.json**: bilingual description, new keywords, version 1.0.0 → 1.1.0
- **marketplace.json**: version 1.4.0 → 1.5.0; academic-writing entry description updated; academic-writing, product-development-suite and product-workflow-agents versions → 1.1.0

#### Documentation
- Updated README.md, docs/en|zh/user-guide.md, and the academic-writing, product-development-suite and product-workflow-agents READMEs

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
