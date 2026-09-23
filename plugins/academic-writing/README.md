# Academic Writing Assistant / 学术写作助手

[English](#english) | [中文](#中文)

## English

### Overview

Professional academic writing assistant for Chinese and English university assignments. Produces natural, flowing prose that avoids typical AI markers like bullet points, rigid structures, and formulaic transitions.

### Features

- **Three Modes**: Write new drafts, revise/polish existing drafts, or learn your style from past writing samples
- **Plain Language**: Short sentences and everyday words in every document, in both languages
- **Bilingual Support**: Chinese and English writing
- **Natural Writing Style**: Checks drafts against a Chinese/English list of common AI words and patterns
- **Academic Quality**: Professional yet accessible language
- **Structured Content**: Clear chapter divisions with descriptive headings
- **Specific Examples**: Concrete details rather than generic statements

### Installation

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/academic-writing
```

### Usage

Use this plugin when you need help with:
- Academic reports and essays
- Project documentation
- Technical analyses
- Research reviews
- Case studies

### Example

```
User: Help me write a technical analysis report about cloud computing adoption
Assistant: [Shows an outline for confirmation, then writes the report chapter by chapter]

User: Polish this draft and make it sound less like AI: <draft>
Assistant: [Lists the problems found, then saves a revised version with a short change summary]

User: Here are two essays I wrote before. Write the new report in my style.
Assistant: [Builds style-profile.md from the samples and uses it for the new report]
```

### Output File Locations

All academic writing outputs are saved to `outputs/<project-name>/writing/`:

```
outputs/
└── <project-name>/
    └── writing/
        ├── technical-analysis.md
        ├── research-review.md
        ├── case-study.md
        ├── <original-name>-revised.md   # Revised draft
        └── style-profile.md             # Your style profile
```

**File Naming Convention:**
- Use kebab-case: `cloud-computing-analysis.md`
- Include version/date when needed: `research-review-v1.0.md`
- Specify language if bilingual: `technical-analysis-en.md`

**Alternative:** Traditional project structure using `./docs/` directory.

---

## 中文

### 概述

专业的中英文学术写作助手，适用于大学作业。生成自然流畅的文章，避免典型的AI特征，如项目符号、僵化结构和公式化过渡。

### 功能特性

- **三种模式**: 新写、润色改写已有稿件、从你以前的文章中学习文风
- **行文朴素**: 所有文章都用短句和平实的用词，中英文都一样
- **双语支持**: 中文和英文写作
- **自然写作风格**: 对照中英文 AI 高频词和句式清单检查稿件
- **学术质量**: 专业且易读的语言
- **结构化内容**: 清晰的章节划分和描述性标题
- **具体示例**: 具体细节而非泛泛而谈

### 安装

```bash
claude plugin install github:shining319/claude-code-single-person-workflow/plugins/academic-writing
```

### 使用场景

当您需要以下帮助时使用此插件：
- 学术报告和论文
- 项目文档
- 技术分析
- 研究综述
- 案例分析

### 示例

```
用户: 帮我写一篇关于云计算采用的技术分析报告
助手: [先给出大纲请你确认，再按章节写完报告]

用户: 帮我润色这篇稿子，降低AI痕迹：<稿件>
助手: [先列出发现的问题，再保存修改后的版本，并附简短的修改说明]

用户: 这是我以前写的两篇文章，按我的文风写这篇新报告
助手: [根据样本生成 style-profile.md，并按它写新报告]
```

### 文件输出位置

所有学术写作输出保存到 `outputs/<project-name>/writing/` 目录：

```
outputs/
└── <project-name>/
    └── writing/
        ├── technical-analysis.md
        ├── research-review.md
        ├── case-study.md
        ├── <原文件名>-revised.md        # 润色后的稿件
        └── style-profile.md             # 你的风格档案
```

**文件命名规范：**
- 使用短横线命名法：`cloud-computing-analysis.md`
- 需要时包含版本/日期：`research-review-v1.0.md`
- 双语文档指定语言：`technical-analysis-zh.md`

**替代方案：** 传统项目结构使用 `./docs/` 目录。

## License

MIT License - See LICENSE.txt for details
