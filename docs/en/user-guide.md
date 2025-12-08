# User Guide

## Overview

This guide will help you effectively use the Single Person Workflow plugins to streamline your product development process. Whether you're building a complete product or working on specific components, these plugins provide specialized assistance.

## Quick Reference

| Task | Skill/Agent | Trigger Example |
|------|-------------|-----------------|
| Database design | Database Designer | "Design a database for..." |
| Product requirements | Product Manager | "Create a PRD for..." |
| UI/UX design | UI Designer | "Design the UI for..." |
| Tech stack selection | Solution Architect | "Help me choose a tech stack..." |
| Academic writing | Academic Writing | "Help me write a research paper..." |
| Complete product | Full Stack Product Builder | "I want to build a complete product..." |

## Individual Skills

### 1. Academic Writing Style

**Purpose:** Professional academic writing for Chinese and English university assignments.

**When to Use:**
- Writing research papers
- Creating technical reports
- Preparing project documentation
- Drafting case studies and analyses

**Trigger Examples:**
```
"Help me write a technical report on cloud computing"
"I need to create a research paper about AI ethics"
"Write an academic analysis of microservices architecture"
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

**Trigger Examples:**
```
"Design a database for an e-commerce system"
"Create a schema for a project management tool"
"I need a database design for a social media platform"
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

**Trigger Examples:**
```
"Create a PRD for a mobile task management app"
"Analyze requirements for a fitness tracking platform"
"Help me define user personas for an e-learning system"
```

**Output:**
- Comprehensive requirement analysis
- User personas and scenarios
- Functional specifications
- PRD documentation
- Feasibility assessment

### 4. UI Designer

**Purpose:** Transform product requirements into professional UI/UX design specifications.

**When to Use:**
- Planning page structure and information architecture
- Designing UI layouts and components
- Creating color schemes and visual guidelines
- Writing detailed design specifications
- Creating user flow diagrams

**Trigger Examples:**
```
"Design the UI for my dashboard application"
"Create a design specification for a mobile checkout flow"
"Plan the information architecture for an admin panel"
```

**Output:**
- Page structure and navigation
- Component design specifications
- Color palettes and typography
- Detailed design documents
- User flow diagrams

### 5. Solution Architect

**Purpose:** Transform product requirements into executable technical architecture designs.

**When to Use:**
- Designing system architecture
- Selecting technology stacks
- Planning deployment strategies
- Reviewing architecture decisions
- Creating technical proposals

**Trigger Examples:**
```
"Design the technical architecture for a real-time chat application"
"Help me choose a tech stack for a SaaS platform"
"Create a deployment plan for a microservices system"
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

**Trigger Example:**
```
"I want to build a complete e-commerce platform"
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

Skills activate automatically based on your request. To explicitly activate a skill:

```
"Use the database designer skill to create a schema for..."
```

### Saving Output

All generated files are saved to your project directory:
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

### Example 1: E-commerce Platform

```
User: "I want to build a complete e-commerce platform"

Full Stack Product Builder activates:
1. Creates comprehensive PRD
2. Designs database schema with products, users, orders, payments
3. Designs UI for storefront, product pages, checkout
4. Creates technical architecture with microservices
5. Generates complete documentation
```

### Example 2: Blog System

```
User: "Create a PRD for a blogging platform with comments and tags"
→ Product Manager creates detailed requirements

User: "Now design the database for this blog system"
→ Database Designer creates schema with posts, users, comments, tags

User: "Design the admin interface"
→ UI Designer creates admin panel specifications
```

### Example 3: API Service

```
User: "Design architecture for a RESTful API service"
→ Solution Architect creates API architecture

User: "Create the database schema to support this API"
→ Database Designer creates appropriate schema

User: "Generate API documentation"
→ Documentation Generator creates comprehensive API docs
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
