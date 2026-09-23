# 用户画像模板

PRD 第 2 章使用这个结构。四个小节的标题和 `Example_PRD` 一致；中文输出时标题分别为：基本信息 / 目标与动机 / 痛点与挑战 / 行为特征。

## 结构

```markdown
### 2.1 Primary User: <角色名>

**Basic information:**

- Age: <年龄段>
- Occupation: <职业 / 身份>
- Technical proficiency: <Low / Average / High>（<一句说明，例如 "familiar with cash register systems">）
- Usage context: <可选：在哪里、用什么设备、多久用一次>

**Goals & motivations:**

- <主要目标>
- <次要目标>
- <深层动机，可选>

**Pain points & challenges:**

- <当前做法的不足>
- <核心痛点>
- <情感诉求，可选>

**Behavioral traits:**

- <会直接影响设计的行为习惯>
```

## 写作要点

- 每个小节 3–5 条，写具体行为，不写空泛的形容词
- Behavioral traits 要能推导出设计决策，例如：
  - "Easily interrupted" → 操作可以随时中断，已填内容不丢失
  - "Afraid of making mistakes" → 危险操作要二次确认，并提供撤销
  - "Prefers large buttons and clear text" → 写进 5.3 易用性和 5.5 无障碍
- 有两类以上用户时，只给主要用户写完整画像；次要用户（2.2）可以只写目标和痛点
- 画像里提到的痛点，都应该能在第 3 章找到对应的 Story

## 示例：银发族用户

```markdown
### 2.1 Primary User: Senior Resident

**Basic information:**

- Age: 60–75
- Occupation: Retired
- Technical proficiency: Low (uses a smartphone mainly for messaging)
- Usage context: At home, on a phone, a few times a month

**Goals & motivations:**

- Complete basic tasks such as paying bills and shopping
- Stay in touch with their children
- Stay independent and avoid bothering family

**Pain points & challenges:**

- Small text, complex steps and jargon
- Afraid of making irreversible mistakes
- Cannot remember multi-step flows

**Behavioral traits:**

- Values simplicity over features
- Learns from family recommendations and community events
- Needs patient, step-by-step guidance
```

## 特殊群体考量清单

写画像和 5.5 Accessibility & Privacy 时逐项检查，相关的写进文档：

- [ ] 视觉障碍用户
- [ ] 听觉障碍用户
- [ ] 运动功能受限用户
- [ ] 认知障碍用户
- [ ] 数字素养较低的用户
- [ ] 隐私敏感用户
