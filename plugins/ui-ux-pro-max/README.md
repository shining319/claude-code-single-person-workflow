# UI/UX Pro Max - Design Intelligence

[English](#english) | [中文](#中文)

## English

### Overview

Data-driven UI/UX design intelligence with a searchable knowledge base of 50+ styles, 21 color palettes, 50 font pairings, and framework-specific guidelines for 9 tech stacks.

### Features

- **Searchable Design Database**: BM25-powered search across styles, colors, typography, and UX guidelines
- **Multi-Framework Support**: React, Next.js, Vue, Svelte, SwiftUI, React Native, Flutter, Tailwind, shadcn/ui
- **Design System Data**: Comprehensive CSV-based design knowledge
- **Stack-Specific Guidelines**: Do's and don'ts for each framework
- **Professional UI Checklists**: Pre-delivery quality checks

### Installation

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/ui-ux-pro-max
```

### Prerequisites

Python 3.x is required for the search functionality:

```bash
# Check if Python is installed
python3 --version || python --version
```

### Usage

Use this plugin when you need to:
- Get style recommendations for specific product types
- Find color palettes for industries (SaaS, e-commerce, healthcare)
- Get typography pairings with Google Fonts imports
- Learn framework-specific best practices
- Review UI against professional checklists

### Slash Command

```bash
/ui-ux-pro-max "design a dashboard for SaaS analytics"
```

### Search Domains

| Domain | Use For | Example Keywords |
|--------|---------|------------------|
| `product` | Product type recommendations | SaaS, e-commerce, portfolio |
| `style` | UI styles, effects | glassmorphism, minimalism, dark mode |
| `typography` | Font pairings | elegant, playful, professional |
| `color` | Color palettes | saas, healthcare, fintech |
| `landing` | Page structures | hero, testimonial, pricing |
| `chart` | Chart recommendations | trend, comparison, funnel |
| `ux` | Best practices | animation, accessibility |

### Supported Stacks

- `html-tailwind` (default)
- `react`
- `nextjs`
- `vue`
- `svelte`
- `swiftui`
- `react-native`
- `flutter`
- `shadcn`

---

## 中文

### 概述

数据驱动的 UI/UX 设计智能，拥有可搜索的设计知识库，包含 50+ 种风格、21 种配色方案、50 种字体配对，以及 9 种技术栈的框架指南。

### 功能特性

- **可搜索设计数据库**: BM25 算法驱动的风格、配色、字体和 UX 指南搜索
- **多框架支持**: React、Next.js、Vue、Svelte、SwiftUI、React Native、Flutter、Tailwind、shadcn/ui
- **设计系统数据**: 基于 CSV 的全面设计知识
- **框架特定指南**: 每种框架的最佳实践和注意事项
- **专业 UI 检查清单**: 交付前质量检查

### 安装

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/ui-ux-pro-max
```

### 前置要求

搜索功能需要 Python 3.x：

```bash
# 检查 Python 是否已安装
python3 --version || python --version
```

### 使用场景

当您需要以下帮助时使用此插件：
- 获取特定产品类型的风格推荐
- 查找行业配色方案（SaaS、电商、医疗）
- 获取 Google Fonts 字体配对
- 学习框架特定最佳实践
- 根据专业检查清单审查 UI

### Slash 命令

```bash
/ui-ux-pro-max "为 SaaS 分析仪表盘设计界面"
```

### 搜索域

| 域 | 用途 | 示例关键词 |
|----|------|-----------|
| `product` | 产品类型推荐 | SaaS、电商、作品集 |
| `style` | UI 风格、效果 | 玻璃拟态、极简、暗黑模式 |
| `typography` | 字体配对 | 优雅、活泼、专业 |
| `color` | 配色方案 | saas、医疗、金融科技 |
| `landing` | 页面结构 | hero、推荐语、定价 |
| `chart` | 图表推荐 | 趋势、对比、漏斗 |
| `ux` | 最佳实践 | 动画、无障碍 |

### 支持的技术栈

- `html-tailwind`（默认）
- `react`
- `nextjs`
- `vue`
- `svelte`
- `swiftui`
- `react-native`
- `flutter`
- `shadcn`

## License

MIT License
