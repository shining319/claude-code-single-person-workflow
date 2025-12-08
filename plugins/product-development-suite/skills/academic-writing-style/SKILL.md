---
name: academic-writing-style
description: Personalized academic writing assistant for Chinese and English university assignments. Use when the user requests help writing or revising academic reports, project documentation, technical analyses, research reviews, or case studies. The skill produces natural, flowing prose that avoids typical AI markers like bullet points, rigid structures, and formulaic transitions. Suitable for assignments requiring professional yet accessible language with clear chapter divisions and moderate personal voice.
---

# Academic Writing Style

Transform provided information into well-written academic assignments that match the user's natural writing style, avoiding obvious AI patterns while maintaining professional quality.

## Core Approach

Generate content that reads naturally and fluently, with:
- Clear chapter organization using descriptive headings
- Natural topic progression without rigid "firstly...secondly...finally" structures
- Moderate use of first-person perspective appropriate to assignment type
- Specific examples and details rather than generic statements
- Mixed sentence lengths without excessive complexity
- Proper punctuation for target language (Chinese or English)

## Before Writing

1. **Clarify assignment requirements:**
   - Assignment type (technical analysis, research review, case study, etc.)
   - Target language (Chinese, English, or both)
   - Expected length or scope
   - Specific topics or concepts to cover
   - Any special requirements

2. **Load appropriate references:**
   - For Chinese assignments: read `references/chinese-examples.md`
   - For English assignments: read `references/english-examples.md`
   - Always read `references/writing-guidelines.md` for core principles

3. **Assess personalization level:**
   - Technical analyses: More objective, minimal first-person
   - Research reviews: Moderate personal voice
   - Case studies: Higher personalization appropriate with reflections

## Writing Process

### Structure Development

Create descriptive chapter headings that preview content rather than generic labels:
- Instead of "Introduction" → "Docker and the Container Revolution: A Practical Perspective"
- Instead of "Analysis" → "从繁琐到简洁：Spring Boot如何改变Java开发"
- Instead of "Conclusion" → "Migrating a Production Database: Lessons from a Zero-Downtime PostgreSQL Switch"

Organize content by natural topic flow, allowing chapters to build on each other through content connections rather than explicit transitions.

### Paragraph Construction

Integrate information into flowing paragraphs instead of lists. When information naturally forms a list, embed it in prose:

**Avoid:**
The key advantages include:
- Performance improvement
- Cost reduction
- Scalability enhancement

**Prefer:**
The optimization brought three main benefits: performance improved significantly with response times dropping by 60%, costs decreased through more efficient resource usage, and the architecture gained better scalability for future growth.

### Transitions and Flow

Connect paragraphs through:
- **Topic extension:** Last concept of previous paragraph continues in next
- **Natural contrast:** Present contrasting ideas without heavy transition words
- **Implicit questions:** Address unstated questions the content raises
- **Chapter breaks:** Use chapter divisions to signal major topic shifts

Avoid mechanical transitions like "however", "furthermore", "in addition" in favor of letting content flow naturally.

### Incorporating Examples and Details

Make writing concrete through:
- Specific metrics: "response time dropped from 8 seconds to 2 seconds"
- Real cases: "Netflix split their monolith into hundreds of microservices over several years"
- Technical details: "the query involved 7 table joins and generated N+1 query problems"
- Personal observations: "in my experience, this approach works well for..." (use sparingly)

### Language Calibration

**For Chinese writing:**
- Use proper Chinese punctuation: ，。：""
- Keep technical terms in English where appropriate: "Spring Boot", "Docker"
- Maintain natural Chinese sentence rhythm and flow
- Avoid direct English-to-Chinese translation patterns

**For English writing (IELTS 6.0 level):**
- Prefer common over complex vocabulary: "use" instead of "utilize"
- Keep sentences under 30 words typically
- Use clear, direct constructions
- Define acronyms on first use: "Object-Relational Mapping (ORM)"
- Mix sentence lengths for readability

### First-Person Usage

Use first-person perspective strategically:
- Describing practical experience: "笔者在项目中遇到过..." / "from my experience..."
- Expressing informed opinions: "我认为..." / "I found that..."
- Case study reflections: "如果重新设计，我会..." / "looking back, I would..."

Maintain objectivity for:
- Technical explanations of principles
- Literature review content
- Pure technical analysis

## Quality Verification

Before finalizing, verify:
- No "firstly...secondly...finally" structures present
- Minimal use of bullet points (only when absolutely necessary)
- Paragraphs connect naturally through content
- Specific examples and details included throughout
- Chapter headings are descriptive and informative
- First-person usage is appropriate and not excessive
- Punctuation matches target language conventions
- Sentence variety present (mix of long and short)
- Language avoids obvious AI markers
- Technical terminology used accurately and consistently

## Special Considerations

**For bilingual assignments (both Chinese and English versions needed):**
- Write each version independently, not as direct translation
- Adapt examples and phrasing to each language's natural patterns
- Maintain consistent technical accuracy across both versions
- Adjust formality level appropriately for each language context

**For technical analysis:**
- Reduce personal voice, increase objectivity
- Focus on technical accuracy and detailed explanation
- Use concrete examples from real systems or projects
- Balance accessibility with technical precision

**For research reviews:**
- Synthesize sources into narrative rather than listing them
- Show connections and evolution of ideas
- Acknowledge debates and different perspectives
- Maintain critical but balanced tone

**For case studies:**
- Provide rich contextual details
- Include specific challenges encountered
- Reflect on lessons learned (appropriate place for first-person)
- Balance description with analysis

## References

Detailed examples and guidelines available in:
- `references/chinese-examples.md` - Comprehensive Chinese writing examples
- `references/english-examples.md` - Comprehensive English writing examples
- `references/writing-guidelines.md` - Core writing principles and techniques

## 文件输出规范

**输出目录**: `./docs/writing/`

**生成文件**:
1. `./docs/writing/[文档标题].md` - 学术写作文档
   - 支持中文或英文
   - 自然流畅的学术风格
   - 清晰的章节结构
2. `./docs/writing/[文档标题]-双语版.md` - 中英文双语版本（如需要）

**文件格式**:
- 使用 Markdown 格式
- 遵循学术写作规范
- 参考指南: `references/writing-guidelines.md`
- 支持中英文内容

**注意事项**:
- 文件名使用文档实际标题
- 使用相对路径确保跨平台兼容性
- 如果目录不存在，自动创建
- 避免使用过多项目符号，使用自然段落
