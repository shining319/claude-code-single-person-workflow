# UI/UX Designer / UI/UX设计师

[English](#english) | [中文](#中文)

## English

### Overview

UI/UX design specialist for interface design, specifications, and user flows. Transform product requirements into professional design specifications with detailed component documentation.

### Features

- **Dual-Mode Output**: Choose between production-ready code or design documentation
- **Design Thinking Integration**: Strategic aesthetic direction framework
- **Frontend Aesthetics Guidelines**: High-quality, distinctive design implementation
- **Information Architecture**: Page structure and navigation planning
- **Code Implementation**: Production-grade frontend code (HTML/CSS/JS, React, Vue)
- **Design Documentation**: Comprehensive single-file UI specifications

### Installation

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/ui-designer
```

### Usage

Use this plugin when you need to:
- Design UI interfaces
- Create page layouts
- Develop design specifications
- Generate user flow diagrams
- Plan information architecture

### Deliverables

**Code Implementation Mode:**
- Production-ready frontend code (HTML/CSS/JS or React/Vue)
- Complete styles with animations and interactions
- Design rationale and implementation notes

**Design Documentation Mode:**
- Comprehensive UI specification document (`ui-specification.md`)
- Layout specifications (grid system, spacing, responsive breakpoints)
- Color and typography standards
- Component inventory with detailed specifications
- Interaction and animation guidelines

### Output File Locations

**Design Documentation Mode:**

Design documents are saved to `outputs/<project-name>/design/`:

```
outputs/
└── <project-name>/
    └── design/
        └── ui-specification.md
```

**Note:** The `design/` directory stores **design documentation only**. Code files are placed flexibly based on your project structure.

**Code Implementation Mode:**

Code files are placed according to your project structure:
- Can be in project root
- Can be in `src/` directory
- Can be in framework-specific directories
- Skill will ask about your project structure or auto-detect appropriate location

---

## 中文

### 概述

UI/UX设计专家，负责界面设计、规格说明和用户流程。将产品需求转化为专业的设计规格，包含详细的组件文档。

### 功能特性

- **双模式输出**: 在生产级代码和设计文档之间选择
- **Design Thinking 集成**: 战略性审美方向框架
- **前端美学指南**: 高质量、独特的设计实现
- **信息架构**: 页面结构和导航规划
- **代码实现**: 生产级前端代码（HTML/CSS/JS、React、Vue）
- **设计文档**: 全面的单文件 UI 规格

### 安装

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/ui-designer
```

### 使用场景

当您需要以下帮助时使用此插件：
- 设计UI界面
- 创建页面布局
- 开发设计规格
- 生成用户流程图
- 规划信息架构

### 交付物

**代码实现模式：**
- 生产级前端代码（HTML/CSS/JS 或 React/Vue）
- 包含动画和交互的完整样式
- 设计理念和实现说明

**设计文档模式：**
- 全面的 UI 规格文档（`ui-specification.md`）
- 布局规格（栅格系统、间距、响应式断点）
- 色彩和字体标准
- 详细组件清单
- 交互和动画指南

### 文件输出位置

**设计文档模式：**

设计文档保存到 `outputs/<project-name>/design/` 目录：

```
outputs/
└── <project-name>/
    └── design/
        └── ui-specification.md
```

**注意：** `design/` 目录**仅存放设计文档**。代码文件根据项目结构灵活放置。

**代码实现模式：**

代码文件根据项目结构放置：
- 可以在项目根目录
- 可以在 `src/` 目录
- 可以在框架特定的目录
- Skill 会询问您的项目结构或自动检测合适的位置

## License

MIT License
