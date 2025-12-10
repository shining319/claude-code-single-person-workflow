# Architecture Documentation

## Overview

The Single Person Workflow Marketplace is designed as a modular, extensible plugin system for Claude Code. This document explains the architecture, design decisions, and how the components work together.

## System Architecture

```
Claude Code CLI
    │
    ├─── Single Person Workflow Marketplace (Root)
    │       │
    │       ├─── Individual Skills
    │       │     ├─── academic-writing
    │       │     ├─── database-designer
    │       │     ├─── product-manager
    │       │     ├─── ui-designer
    │       │     └─── solution-architect
    │       │
    │       ├─── Skill Suites
    │       │     └─── product-development-suite
    │       │           (bundles all 5 skills)
    │       │
    │       └─── Workflow Agents
    │             └─── product-workflow-agents
    │                   ├─── Full Stack Product Builder
    │                   ├─── Product Requirements Analyzer
    │                   ├─── Database Architecture Planner
    │                   ├─── UI/UX Design Coordinator
    │                   ├─── Technical Solution Designer
    │                   └─── Documentation Generator
```

## Core Concepts

### 1. Skills

**Definition:** A skill is a specialized capability that Claude Code can invoke to perform specific tasks.

**Characteristics:**
- Single responsibility (one skill, one purpose)
- Triggered by natural language or slash commands
- Produces specific output formats
- Stateless (each invocation is independent)

**Activation Methods:**
1. **Natural Language**: Automatic detection based on user intent
   - Example: "Design a database for my app" → Database Designer activates
2. **Slash Commands**: Explicit activation via command
   - Example: `/database-designer "e-commerce system"` → Direct activation

**Implementation:**
```
plugins/
  └─── skill-name/
       ├─── skill.md          # Skill prompt and instructions
       └─── examples/         # Usage examples (optional)
```

### 2. Skill Suites

**Definition:** A collection of related skills bundled together for convenience.

**Benefits:**
- Single installation for multiple skills
- Logical grouping of capabilities
- Reduced installation complexity

**Implementation:**
```
plugins/
  └─── suite-name/
       ├─── skill.md          # Suite metadata
       └─── skills/           # Bundled individual skills
            ├─── skill-1/
            ├─── skill-2/
            └─── skill-3/
```

### 3. Workflow Agents

**Definition:** Intelligent agents that orchestrate multiple skills and tasks to accomplish complex workflows.

**Capabilities:**
- Multi-step task coordination
- Automatic skill selection
- Context management across steps
- Decision-making and planning

**Implementation:**
```
plugins/
  └─── workflow-agents/
       ├─── agent.md          # Agent configuration
       └─── agents/
            ├─── agent-1/
            ├─── agent-2/
            └─── agent-3/
```

## Plugin Structure

### Minimal Plugin

```
plugin-name/
├─── .claude-plugin/
│    └─── plugin.json      # Plugin metadata
├─── skills/               # Skill definitions
│    └─── skill-name/
│         └─── SKILL.md
└─── README.md             # Optional: Documentation
```

### Full Plugin with Slash Commands

```
plugin-name/
├─── .claude-plugin/
│    └─── plugin.json      # Plugin metadata
├─── skills/               # Skill definitions
│    └─── skill-name/
│         ├─── SKILL.md
│         └─── references/ # Reference materials
├─── commands/             # Slash commands
│    ├─── command-1.md
│    └─── command-2.md
├─── README.md             # Documentation
└─── LICENSE.txt           # License
```

### Slash Command Structure

Each slash command is a Markdown file in the `commands/` directory:

```markdown
---
description: Brief command description
argument-hint: "[parameter hint]"
---

Use the SKILL_NAME skill. User input: $ARGUMENTS
```

**Example:** `/database-designer` command file:
```markdown
---
description: Complete database schema design with ER diagrams
argument-hint: "[business domain or requirements]"
---

Use the database-designer skill. User input: $ARGUMENTS
```

## Skill Definition Format

### Basic Structure (skill.md)

```markdown
---
name: skill-name
description: Brief description of what this skill does
triggers:
  - keyword1
  - keyword2
  - phrase pattern
---

# Skill Instructions

Detailed instructions for Claude on how to perform this skill.

## Input

Expected input format and parameters.

## Processing

Steps to process the input.

## Output

Expected output format and structure.
```

### Example: Database Designer

```markdown
---
name: database-designer
description: Complete database schema design with ER diagrams
triggers:
  - database design
  - schema design
  - ER diagram
  - data model
---

# Database Designer Skill

You are a database design expert...

[Detailed instructions follow]
```

## Command Usage Patterns

### Overview

This marketplace follows standardized command naming conventions to ensure consistency and discoverability across all plugins.

### Naming Conventions

#### 1. Individual Skill Plugins

**Pattern:** `/plugin-name`

**Examples:**
- `/database-designer` - Database schema design
- `/product-manager` - Product requirements and PRD
- `/ui-designer` - UI/UX design specifications
- `/solution-architect` - Technical architecture design
- `/academic-writing` - Academic writing assistance

**Usage:** Direct activation of a single skill

#### 2. Suite Plugins

**Pattern:** `/spw-*` (spw = single-person workflow)

**Examples:**
- `/spw-db` - Database design (from product-development-suite)
- `/spw-prd` - Product requirements (from product-development-suite)
- `/spw-ui` - UI design (from product-development-suite)
- `/spw-arch` - Architecture design (from product-development-suite)
- `/spw-writing` - Academic writing (from product-development-suite)

**Usage:** Quick access to skills within the product-development-suite package

#### 3. Workflow Plugins

**Pattern:** Descriptive workflow names

**Example:**
- `/build-dev-workflow` - Complete product development workflow

**Usage:** Orchestrate multiple skills in a complete end-to-end workflow

### Command Frontmatter Specifications

Commands are defined in `plugins/*/commands/*.md` files with YAML frontmatter.

#### Allowed Fields

- `description` - English description of the command
- `argument-hint` - Hint text for command arguments (shown in CLI)
- `allowed-tools` - Tools the command can use (optional)
- `model` - Model configuration (typically `inherit`)

#### Important Notes

- **`description_zh` is NOT supported** in command frontmatter
- Chinese descriptions should be maintained in README files and documentation
- Keep command definitions minimal and focused on skill activation
- Use `$ARGUMENTS` variable to pass user input to skills

#### Example Command File

```markdown
---
description: "Design database schema with ER diagrams"
argument-hint: "[requirements]"
model: inherit
---

Activate the database-designer skill with the provided requirements: $ARGUMENTS
```

### Command Discovery

Users can discover available commands through:
1. **Auto-completion** in Claude Code CLI
2. **Documentation** in README files and user guides
3. **Natural language** - Commands are also discoverable through conversational requests

## Model Configuration Strategy

### Overview

This marketplace uses an inheritance-based model configuration strategy to maintain flexibility while providing sensible defaults.

### Configuration Hierarchy

#### 1. Skills (No model field)

**Behavior:**
- Skills do **not** specify a `model` field in their frontmatter
- They inherit the model from their invocation context
- This allows the same skill to run with different models based on how it's invoked

**Rationale:**
- Maximum flexibility for users
- Skills remain model-agnostic
- Users can choose the best model for their use case

#### 2. Agents (Default: `model: inherit`)

**Behavior:**
- Workflow agents typically use `model: inherit` in their frontmatter
- This allows the agent to use the model specified by the user or system
- Override only when a specific model is required for the agent's task

**Example:**
```yaml
---
name: product-manager
description: Product requirements analysis and PRD creation
model: inherit
---
```

#### 3. Commands (Default: `model: inherit`)

**Behavior:**
- Slash commands typically use `model: inherit`
- This respects the user's model preference
- Override only when the command requires specific model capabilities

**Example:**
```yaml
---
description: "Design database schema with ER diagrams"
argument-hint: "[requirements]"
model: inherit
---
```

#### 4. Plugin Configurations (No model field)

**Behavior:**
- `plugin.json` files do **not** configure models
- Model selection is handled at the skill/agent/command level
- This keeps plugin metadata focused on structural information

### When to Override

Use explicit model values (`opus`, `haiku`, `sonnet`) **only** when:

1. **Specific Capabilities Required**
   - The task requires complex reasoning that only `opus` can handle
   - Example: Multi-step architectural decision-making

2. **Performance Optimization**
   - Simple tasks that can use `haiku` for faster response
   - Example: Quick format conversions or simple validations

3. **Quality Differences**
   - Testing has shown significant quality differences between models
   - Document the reasoning in comments or documentation

### Supported Model Values

- `inherit` - Use the model from invocation context (recommended default)
- `opus` - Claude Opus (highest capability, slower, more expensive)
- `haiku` - Claude Haiku (fast, efficient, lower cost)
- `sonnet` - Claude Sonnet (balanced capability and performance)

### Best Practices

1. **Start with `inherit`** for all new agents and commands
2. **Document reasoning** if you override to a specific model
3. **Test with different models** to verify the override is necessary
4. **Refer to `.claude/CLAUDE.md`** for detailed model configuration guidelines
5. **Consider user preferences** - users may have cost or performance constraints

### Configuration Examples

**Good - Using inherit (recommended):**
```yaml
---
name: database-architect
description: Database schema design workflow
model: inherit
---
```

**Acceptable - Justified override:**
```yaml
---
name: complex-architecture-planner
description: Multi-system architecture design requiring deep reasoning
model: opus  # Requires opus for complex multi-step reasoning
---
```

**Avoid - Unnecessary override:**
```yaml
---
name: simple-formatter
description: Format text output
model: opus  # ❌ Unnecessary - haiku or inherit would work fine
---
```

## Agent Architecture

### Agent Types

1. **Orchestrator Agents**
   - Coordinate multiple skills
   - Example: Full Stack Product Builder

2. **Specialist Agents**
   - Deep expertise in one domain
   - Example: Database Architecture Planner

3. **Utility Agents**
   - Support and auxiliary functions
   - Example: Documentation Generator

### Agent Decision Flow

```
User Request
    │
    ├─── Agent Analyzes Request
    │       │
    │       ├─── Determines Required Skills
    │       ├─── Plans Execution Sequence
    │       └─── Allocates Resources
    │
    ├─── Agent Executes Steps
    │       │
    │       ├─── Step 1: Activate Skill A
    │       ├─── Step 2: Activate Skill B
    │       └─── Step N: Activate Skill N
    │
    └─── Agent Delivers Result
            │
            ├─── Combines Outputs
            ├─── Validates Completeness
            └─── Presents to User
```

## Integration with Claude Code

### Skill Activation

Skills can be activated through two pathways:

#### **Method 1: Natural Language Activation**
1. **User Input:** User types natural language request
2. **Pattern Matching:** Claude Code matches request to skill triggers
3. **Skill Loading:** Corresponding SKILL.md is loaded
4. **Context Injection:** Skill instructions are injected into context
5. **Execution:** Claude processes request using skill instructions
6. **Output:** Result is formatted and presented

#### **Method 2: Slash Command Activation**
1. **User Input:** User types slash command (e.g., `/database-designer "requirements"`)
2. **Command Parsing:** Claude Code parses command and arguments
3. **Direct Skill Loading:** Corresponding skill is directly activated
4. **Context Injection:** Command expands to skill invocation
5. **Execution:** Claude processes with skill instructions
6. **Output:** Result is formatted and presented

**Advantages of Slash Commands:**
- Guaranteed skill activation (no ambiguity)
- Faster execution (no pattern matching needed)
- Explicit intent declaration
- Better for automation and scripting

### Context Management

```
Session Context
    │
    ├─── User Request History
    ├─── Active Skill Context
    ├─── Generated Outputs
    └─── Workflow State (for agents)
```

## Design Principles

### 1. Modularity

Each skill is independent and can be installed/uninstalled separately.

**Benefits:**
- Users install only what they need
- Easy to maintain and update
- Clear separation of concerns

### 2. Composability

Skills and agents can be combined to create complex workflows.

**Examples:**
- Product Manager → Database Designer → UI Designer
- Solution Architect ← Database Designer → UI Designer

### 3. Discoverability

Skills can be discovered and activated in multiple ways.

**Implementation:**
- **Natural Language Triggers**: Broad patterns for flexibility
  - Overlapping triggers for related skills
  - Contextual activation based on conversation
- **Slash Commands**: Direct command discovery
  - Auto-completion in Claude Code interface
  - Help documentation listing all commands
  - Argument hints for proper usage

### 4. Consistency

All skills follow similar patterns for predictable user experience.

**Standards:**
- Consistent output formats
- Predictable file locations
- Uniform documentation structure

## File Output Conventions

### Recommended Approach (Following Claude Code Official Standards)

All generated files are saved to `outputs/<project-name>/` directory, organized by type:

```
outputs/
└── <project-name>/              # Project name (e.g., task-management-app)
    ├── docs/                    # Product documentation (product-manager)
    │   ├── prd.md
    │   ├── user-personas.md
    │   └── requirements.md
    ├── architecture/            # Technical architecture (solution-architect)
    │   ├── system-architecture.md
    │   ├── tech-stack.md
    │   └── deployment-plan.md
    ├── database/                # Database design (database-designer)
    │   ├── schema-design.md
    │   ├── schema.sql
    │   ├── drawdb-schema.json
    │   └── drawdb-schema.dbml
    ├── design/                  # UI/UX design (ui-designer)
    │   ├── ui-specification.md
    │   ├── design-system.md
    │   └── user-flows.md
    └── writing/                 # Academic/technical writing (academic-writing)
        ├── technical-analysis.md
        └── project-documentation.md
```

**Example:**
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

**Advantages:**
- ✅ Good isolation: Each project has its own directory
- ✅ Easy cleanup: Delete entire project directory
- ✅ Automation-friendly: Standardized paths for scripting
- ✅ Official standard: Consistent with Anthropic official examples

### Alternative Approach (Traditional Project Structure)

If your project has an existing directory structure, you can also use traditional paths:

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

**Use Cases:**
- Existing projects with established directory structure
- Need to integrate with existing codebase
- Team has established file organization standards

### File Naming Conventions

- Use kebab-case: `user-authentication-flow.md`
- Include version or date (optional): `schema-design-v1.0.md` or `prd-2024-12-10.md`
- Use descriptive names: `e-commerce-database-schema.sql`
- Specify language for bilingual docs: `technical-analysis-en.md`, `technical-analysis-zh.md`

## Extensibility

### Adding New Skills

1. Create plugin directory structure
2. Write skill.md with clear instructions
3. Define trigger patterns
4. Document usage examples
5. Test with various inputs

### Creating Custom Agents

1. Identify workflow pattern
2. Map required skills
3. Define decision logic
4. Implement coordination strategy
5. Test end-to-end workflow

### Contributing Skills

To contribute a new skill:

1. Fork the repository
2. Create plugin following structure guidelines
3. Add comprehensive documentation
4. Include usage examples
5. Submit pull request

## Performance Considerations

### Token Efficiency

- Skills use concise, focused prompts
- Avoid redundant instructions
- Use templates for common patterns

### Context Window Management

- Skills are loaded only when needed
- Large instructions are chunked appropriately
- Historical context is managed efficiently

### Caching Strategy

- Skill definitions are cacheable
- Generated outputs reference cached content
- Templates reduce redundant generation

## Security Considerations

### Input Validation

Skills should validate:
- User input parameters
- File path destinations
- External resource references

### Output Sanitization

Generated outputs should:
- Escape special characters in SQL
- Validate file paths
- Sanitize user-provided content

### Safe Defaults

- Conservative permissions
- Secure configuration examples
- Best practice recommendations

## Testing Strategy

### Skill Testing

1. **Unit Testing:** Individual skill activation
2. **Integration Testing:** Skill combinations
3. **Regression Testing:** Consistency across updates

### Agent Testing

1. **Workflow Testing:** Complete agent flows
2. **Edge Case Testing:** Unusual requests
3. **Performance Testing:** Large-scale operations

## Future Enhancements

### Planned Features

1. **Interactive Agents:** Multi-turn conversations
2. **Customizable Templates:** User-defined output formats
3. **Skill Marketplace:** Community-contributed skills
4. **Version Management:** Skill versioning and compatibility

### Potential Integrations

1. **External Tools:** Integration with design tools, databases
2. **CI/CD Pipelines:** Automated documentation generation
3. **Project Templates:** Initialized project structures

## Command Naming Conventions

### Single-Skill Plugins
Individual plugins use the full plugin name as their command:
- `/database-designer` - Database Designer plugin
- `/product-manager` - Product Manager plugin
- `/ui-designer` - UI Designer plugin
- `/solution-architect` - Solution Architect plugin
- `/academic-writing` - Academic Writing plugin

### Suite Plugins
Suite plugins use the `spw-` prefix (single-person workflow):
- `/spw-db` - Database design (from product-development-suite)
- `/spw-prd` - Product requirements (from product-development-suite)
- `/spw-ui` - UI design (from product-development-suite)
- `/spw-arch` - Architecture design (from product-development-suite)
- `/spw-writing` - Academic writing (from product-development-suite)

### Workflow Plugins
Workflow plugins use descriptive workflow names:
- `/build-dev-workflow` - Complete product development workflow

## Troubleshooting Architecture

### Common Issues

**Skill Not Activating (Natural Language):**
- Check trigger pattern matches
- Verify SKILL.md is properly formatted
- Ensure plugin is installed
- **Solution**: Use slash commands for guaranteed activation

**Slash Command Not Found:**
- Verify plugin installation: `claude plugin list`
- Check command exists in `commands/` directory
- Ensure command file has proper frontmatter
- Restart Claude Code session if needed

**Agent Coordination Failures:**
- Review workflow logic
- Check skill dependencies
- Validate context passing

**Output Format Issues:**
- Verify template structure
- Check file path permissions
- Validate output formatting

## Technical Specifications

### Supported Formats

- **Input:** Natural language, Markdown, JSON
- **Output:** Markdown, SQL, JSON, DBML, PlantUML
- **Documentation:** GitHub-flavored Markdown

### Dependencies

- Claude Code CLI v1.0+
- Git (for installation)
- Node.js (for some generated outputs)

### Compatibility

- **Operating Systems:** Windows, macOS, Linux
- **Claude Models:** All current models
- **Claude Code Versions:** Latest stable release

## Best Practices for Developers

### Skill Development

1. Start with clear use case
2. Define narrow scope
3. Write comprehensive instructions
4. Include diverse examples
5. Test with real scenarios

### Agent Development

1. Map complete workflow
2. Identify skill dependencies
3. Handle edge cases
4. Provide clear progress feedback
5. Validate final outputs

### Documentation

1. Write for beginners
2. Include practical examples
3. Show common patterns
4. Explain decision rationale
5. Keep updated with changes

## Conclusion

The Single Person Workflow Marketplace provides a flexible, extensible architecture for building specialized Claude Code capabilities. By following modular design principles and clear conventions, it enables solo developers to access professional-grade tools for complete product development.

For implementation details, see the [User Guide](user-guide.md). For installation instructions, see the [Installation Guide](installation.md).
