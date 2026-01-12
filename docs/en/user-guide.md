# User Guide

## Overview

This guide will help you effectively use the Single Person Workflow plugins to streamline your product development process. Whether you're building a complete product or working on specific components, these plugins provide specialized assistance.

## Quick Reference

| Task | Skill/Agent | Natural Language Trigger | Slash Command |
|------|-------------|-------------------------|---------------|
| Database design | Database Designer | "Design a database for..." | `/database-designer` or `/spw-db` |
| Product requirements | Product Manager | "Create a PRD for..." | `/product-manager` or `/spw-prd` |
| UI/UX design | UI Designer | "Design the UI for..." | `/ui-designer` or `/spw-ui` |
| Tech stack selection | Solution Architect | "Help me choose a tech stack..." | `/solution-architect` or `/spw-arch` |
| Academic writing | Academic Writing | "Help me write a research paper..." | `/academic-writing` or `/spw-writing` |
| Complete product | Full Stack Product Builder | "I want to build a complete product..." | `/build-dev-workflow` |

## Using Skills: Two Methods

All skills in this marketplace can be activated in two ways:

### Method 1: Natural Language (Automatic)
Simply describe what you want in natural language. Claude Code will automatically detect and activate the appropriate skill based on your request.

**Example:**
```
"Design a database for an e-commerce system"
→ Automatically activates Database Designer skill
```

### Method 2: Slash Commands (Explicit)
Use slash commands for direct, explicit skill activation. This is faster and guarantees the exact skill you want.

**Available Slash Commands:**

#### Single-Skill Plugin Commands
- `/academic-writing [assignment type and topic]` - Academic writing assistant
- `/database-designer [business domain or requirements]` - Complete database schema design
- `/product-manager [product idea or requirements]` - Product management and PRD creation
- `/ui-designer [page or feature to design]` - UI/UX design with specifications
- `/solution-architect [system or application requirements]` - Technical architecture design

#### Suite Plugin Commands (spw = single-person workflow)
If you installed the product-development-suite or full marketplace:
- `/spw-db [requirements]` - Database schema design
- `/spw-ui [page or feature]` - UI/UX interface design
- `/spw-prd [product idea]` - Product management and PRD
- `/spw-arch [system requirements]` - Technical architecture
- `/spw-writing [assignment topic]` - Academic writing

#### Workflow Command
- `/build-dev-workflow [product description]` - Complete product development workflow

**Example:**
```
/database-designer "design a blog system database with users, posts, comments"
```

## Individual Skills

### 1. Academic Writing Style

**Purpose:** Professional academic writing for Chinese and English university assignments.

**When to Use:**
- Writing research papers
- Creating technical reports
- Preparing project documentation
- Drafting case studies and analyses

**Slash Commands:**
- `/academic-writing [assignment type and topic]`
- `/spw-writing [assignment type and topic]` (if using suite)

**Natural Language Triggers:**
```
"Help me write a technical report on cloud computing"
"I need to create a research paper about AI ethics"
"Write an academic analysis of microservices architecture"
```

**Slash Command Examples:**
```
/academic-writing "technical report on cloud computing security"
/spw-writing "research paper about AI ethics in healthcare"
```

**Output:**
- Natural, flowing prose
- Proper academic structure
- Clear chapter divisions
- Professional yet accessible language

### 2. Database Designer

**Purpose:** Complete database schema design with ER diagrams and SQL scripts.

**When to Use:**
- Designing new database schemas
- Creating data models for applications
- Generating ER diagrams
- Writing migration scripts

**Slash Commands:**
- `/database-designer [business domain or requirements]`
- `/spw-db [requirements]` (if using suite)

**Natural Language Triggers:**
```
"Design a database for an e-commerce system"
"Create a schema for a project management tool"
"I need a database design for a social media platform"
```

**Slash Command Examples:**
```
/database-designer "e-commerce system with products, users, orders, payments"
/spw-db "project management tool with tasks, teams, milestones"
```

**Output:**
- Detailed Markdown design document
- Executable SQL scripts (MySQL, PostgreSQL, SQL Server)
- DrawDB-compatible JSON/DBML files
- ER diagram specifications

**Features:**
- Logical relationships without physical foreign keys
- Realistic field sizes
- Optimized indexes
- Mandatory comments on all objects

### 3. Product Manager

**Purpose:** Transform ideas into professional product requirements documents (PRD).

**When to Use:**
- Analyzing product requirements
- Creating user personas
- Writing PRDs
- Planning MVP features
- Defining user stories

**Slash Commands:**
- `/product-manager [product idea or requirements]`
- `/spw-prd [product idea]` (if using suite)

**Natural Language Triggers:**
```
"Create a PRD for a mobile task management app"
"Analyze requirements for a fitness tracking platform"
"Help me define user personas for an e-learning system"
```

**Slash Command Examples:**
```
/product-manager "mobile task management app with team collaboration"
/spw-prd "fitness tracking platform with social features"
```

**Output:**
- Comprehensive requirement analysis
- User personas and scenarios
- Functional specifications
- PRD documentation
- Feasibility assessment

### 4. UI Designer

**Purpose:** Transform product requirements into professional UI/UX solutions—either as production-ready frontend code or comprehensive design specifications.

**When to Use:**
- Planning page structure and information architecture
- Designing UI layouts and components
- Creating color schemes and visual guidelines
- Generating production-ready frontend code with distinctive aesthetics
- Writing detailed design specifications for developers

**Slash Commands:**
- `/ui-designer [page or feature to design]`
- `/spw-ui [page or feature]` (if using suite)

**Natural Language Triggers:**
```
"Design the UI for my dashboard application"
"Create a design specification for a mobile checkout flow"
"Implement a landing page with modern aesthetics"
```

**Slash Command Examples:**
```
/ui-designer "user dashboard with analytics widgets and charts"
/spw-ui "mobile checkout flow with payment options"
```

**Workflow:**
1. **Requirements Gathering** - Answer 5 questions about your product (target users, features, platform, etc.)
2. **Page Structure Planning** - Receive page structure and user flow planning
3. **Output Mode Selection** - Choose between:
   - **Code Implementation** - Production-ready frontend code (HTML/CSS/JS or React/Vue)
   - **Design Documentation** - Comprehensive UI specification document

**Code Implementation Mode:**

When you select code implementation, the skill applies:
- **Design Thinking Framework** - Strategic decisions on aesthetic direction (minimal vs. maximalist, retro-futuristic vs. organic, etc.)
- **Frontend Aesthetics Guidelines** - Distinctive typography, cohesive color themes, thoughtful animations, creative spatial composition
- Focus on creating memorable, context-appropriate designs that avoid generic AI aesthetics

Output: Production-grade code with complete styles, animations, and interactions. Files placed flexibly based on your project structure.

**Design Documentation Mode:**

Generates a comprehensive `ui-specification.md` file containing:
- Page overview and design concept
- Layout specifications (grid system, spacing, responsive breakpoints)
- Color and typography standards
- Component inventory (table format)
- Interaction and animation guidelines

Output location: `outputs/<project-name>/design/ui-specification.md`

**Key Features:**
- **Dual-Mode Flexibility** - Choose code or documentation based on your needs
- **Design Thinking Integration** - Strategic aesthetic direction before implementation
- **Quality Aesthetics** - Avoids overused fonts (Inter, Roboto), cliched color schemes, predictable layouts
- **Streamlined Workflow** - 3-step process from requirements to output

### 5. Solution Architect

**Purpose:** Transform product requirements into executable technical architecture designs.

**When to Use:**
- Designing system architecture
- Selecting technology stacks
- Planning deployment strategies
- Reviewing architecture decisions
- Creating technical proposals

**Slash Commands:**
- `/solution-architect [system or application requirements]`
- `/spw-arch [system requirements]` (if using suite)

**Natural Language Triggers:**
```
"Design the technical architecture for a real-time chat application"
"Help me choose a tech stack for a SaaS platform"
"Create a deployment plan for a microservices system"
```

**Slash Command Examples:**
```
/solution-architect "real-time chat application with WebSocket support"
/spw-arch "SaaS platform with multi-tenant architecture"
```

**Output:**
- Complete architecture designs
- Technology stack recommendations
- Deployment strategies
- Infrastructure planning
- Architecture review reports

## Workflow Agents

### 1. Full Stack Product Builder

**Purpose:** Orchestrates the entire product development process from concept to deployment.

**When to Use:**
- Building a complete product from scratch
- Need end-to-end workflow coordination
- Want automatic task orchestration

**Slash Command:**
- `/build-dev-workflow [product description]`

**Natural Language Trigger:**
```
"I want to build a complete e-commerce platform"
```

**Slash Command Example:**
```
/build-dev-workflow "e-commerce platform with product catalog, shopping cart, and payment processing"
```

**Workflow:**
1. Requirements gathering → Product Manager
2. Database design → Database Designer
3. UI/UX design → UI Designer
4. Technical architecture → Solution Architect
5. Documentation → Academic Writing
6. Implementation coordination

### 2. Product Requirements Analyzer

**Purpose:** Deep analysis of product requirements and feasibility.

**When to Use:**
- Evaluating new product ideas
- Analyzing market fit
- Assessing technical feasibility

### 3. Database Architecture Planner

**Purpose:** Comprehensive database planning and optimization.

**When to Use:**
- Complex database design projects
- Performance optimization needed
- Scaling considerations

### 4. UI/UX Design Coordinator

**Purpose:** Coordinates complete UI/UX design processes.

**When to Use:**
- Large-scale design projects
- Multiple page/component designs
- Design system creation

### 5. Technical Solution Designer

**Purpose:** Advanced technical architecture and system design.

**When to Use:**
- Complex system architectures
- Microservices design
- Cloud-native applications

### 6. Documentation Generator

**Purpose:** Automated generation of comprehensive project documentation.

**When to Use:**
- Creating technical documentation
- API documentation
- User manuals and guides

## Best Practices

### 1. Be Specific

Instead of:
```
"Design a database"
```

Use:
```
"Design a database for an e-commerce system with products, users, orders, and inventory management"
```

### 2. Provide Context

Include relevant information:
- Target audience
- Scale requirements
- Technology preferences
- Constraints or requirements

### 3. Iterate

Start with initial output and refine:
```
"Update the database design to include a ratings and reviews system"
"Add social login to the authentication flow"
```

### 4. Combine Skills

You can request multiple skills in sequence:
```
"First create a PRD for a blog platform, then design the database schema"
```

### 5. Use Workflow Agents for Complex Projects

For complete products, let the Full Stack Product Builder coordinate:
```
"I want to build a complete project management tool with team collaboration features"
```

## Common Workflows

### Workflow 1: New Product Development

1. **Requirements** → Product Manager
   ```
   "Create a PRD for a task management application"
   ```

2. **Database** → Database Designer
   ```
   "Design a database based on the PRD above"
   ```

3. **UI Design** → UI Designer
   ```
   "Design the UI for the task management application"
   ```

4. **Architecture** → Solution Architect
   ```
   "Create the technical architecture for this system"
   ```

### Workflow 2: Feature Addition

1. **Requirements** → Product Manager
   ```
   "Analyze requirements for adding real-time collaboration features"
   ```

2. **Database** → Database Designer
   ```
   "Update the database schema to support real-time collaboration"
   ```

3. **Architecture** → Solution Architect
   ```
   "Design the technical solution for real-time features"
   ```

### Workflow 3: Documentation

1. **Technical Docs** → Academic Writing
   ```
   "Create technical documentation for the authentication system"
   ```

2. **API Docs** → Documentation Generator
   ```
   "Generate API documentation for the REST endpoints"
   ```

## Tips and Tricks

### Switching Between Skills

Skills activate automatically based on your request. You have three ways to activate a specific skill:

**Method 1: Natural language (automatic detection)**
```
"Design a database for an e-commerce system"
```

**Method 2: Explicit skill mention**
```
"Use the database designer skill to create a schema for..."
```

**Method 3: Slash commands (recommended for precision)**
```
/database-designer "e-commerce system"
```

### Slash Command Best Practices

1. **Be specific with your arguments**
   ```
   Good: /database-designer "blog system with users, posts, comments, tags"
   Poor: /database-designer "blog"
   ```

2. **Use quotes for multi-word arguments**
   ```
   /spw-prd "task management app with team collaboration features"
   ```

3. **Combine with natural follow-ups**
   ```
   /database-designer "e-commerce system"
   [After output] "Add a wishlist feature to the database"
   ```

4. **Choose the right command variant**
   - Single plugin: `/database-designer` (if you installed individual plugin)
   - Suite plugin: `/spw-db` (if you installed product-development-suite)
   - Both work the same way, use whichever you have installed

### Saving Output

**Recommended Approach (Following Claude Code Official Standards):**

All generated files are saved to `outputs/<project-name>/` directory, organized by type:

```
outputs/
└── <project-name>/              # Project name (e.g., task-management-app)
    ├── docs/                    # Product documentation
    ├── architecture/            # Technical architecture
    ├── database/                # Database design
    ├── design/                  # UI/UX design
    └── writing/                 # Academic/technical writing
```

**Advantages:**
- ✅ Each project has its own directory for good isolation
- ✅ Easy to cleanup and manage
- ✅ Automation-friendly for scripting
- ✅ Follows Anthropic official standards

**Alternative Approach (Traditional Project Structure):**

If your project has an existing directory structure, you can also use:
- Database designs: `./database/`
- Design specs: `./design/`
- Documentation: `./docs/`
- Architecture: `./architecture/`

### Version Control

Generated files are plain text (Markdown, SQL, JSON), making them perfect for Git:

```bash
git add docs/database-design.md
git commit -m "Add initial database design"
```

### Working with Teams

Share generated documents with your team:
- PRDs for product discussions
- Database schemas for backend developers
- UI specs for frontend developers
- Architecture docs for infrastructure teams

## Customization

### Database Preferences

Specify your preferred database:
```
"Design a PostgreSQL database for..."
"Create a MongoDB schema for..."
```

### Design Style

Guide the UI Designer:
```
"Design a minimalist UI for..."
"Create a modern, colorful design for..."
```

### Architecture Preferences

Specify technology preferences:
```
"Design architecture using Node.js and React"
"Create a Python-based microservices architecture"
```

## Troubleshooting

### Skill Not Activating

If the wrong skill activates or no skill activates:

1. Be more specific with your request
2. Use explicit skill names
3. Check that the plugin is installed

### Output Not Meeting Expectations

If the output isn't what you expected:

1. Provide more context and details
2. Iterate with refinement requests
3. Use examples to guide the output

### Multiple Skills Needed

For complex requests needing multiple skills:

1. Use workflow agents for automatic coordination
2. Break down into sequential requests
3. Reference previous outputs in new requests

## Examples

### Example 1: E-commerce Platform (Using Workflow Command)

**Natural Language:**
```
User: "I want to build a complete e-commerce platform"

Full Stack Product Builder activates:
1. Creates comprehensive PRD
2. Designs database schema with products, users, orders, payments
3. Designs UI for storefront, product pages, checkout
4. Creates technical architecture with microservices
5. Generates complete documentation
```

**Using Slash Command:**
```
/build-dev-workflow "e-commerce platform with product catalog, shopping cart, checkout, and payment integration"
```

### Example 2: Blog System (Using Individual Commands)

**Natural Language:**
```
User: "Create a PRD for a blogging platform with comments and tags"
→ Product Manager creates detailed requirements

User: "Now design the database for this blog system"
→ Database Designer creates schema with posts, users, comments, tags

User: "Design the admin interface"
→ UI Designer creates admin panel specifications
```

**Using Slash Commands:**
```
/product-manager "blogging platform with comments, tags, and user management"
[Review output]

/database-designer "blog system based on above PRD with posts, users, comments, tags, categories"
[Review output]

/ui-designer "admin interface for blog management with post editor and analytics"
```

### Example 3: API Service (Using Suite Commands)

**Natural Language:**
```
User: "Design architecture for a RESTful API service"
→ Solution Architect creates API architecture

User: "Create the database schema to support this API"
→ Database Designer creates appropriate schema

User: "Generate API documentation"
→ Documentation Generator creates comprehensive API docs
```

**Using Slash Commands:**
```
/spw-arch "RESTful API service with authentication, rate limiting, and caching"
[Review output]

/spw-db "database schema to support the API with users, sessions, and audit logs"
[Review output]

/spw-writing "API documentation covering all endpoints, authentication, and error handling"
```

## Advanced Usage

### Chaining Requests

Build complex outputs by chaining requests:

```
1. "Create a PRD for a chat application"
2. "Design a scalable database for 1M+ users"
3. "Design architecture with WebSocket support"
4. "Create UI design for mobile and web"
```

### Refinement Loop

Iterate until perfect:

```
1. "Design a database for user management"
2. "Add support for OAuth and social login"
3. "Include audit logging for all user actions"
4. "Optimize for read-heavy workloads"
```

### Template Creation

Create reusable patterns:

```
"Create a database design template for multi-tenant SaaS applications"
```

## Getting Help

- Review the [Installation Guide](installation.md) for setup issues
- Check the [Architecture](architecture.md) for understanding plugin structure
- Open issues on [GitHub](https://github.com/shining319/claude-code-single-person-workflow/issues)

## Next Steps

- Explore the [Architecture Documentation](architecture.md) to understand how plugins work
- Start with simple requests and gradually tackle more complex projects
- Share feedback and contribute to the community
