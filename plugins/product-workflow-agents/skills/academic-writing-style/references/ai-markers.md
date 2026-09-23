# AI 痕迹清单与替换策略

成稿后按本清单逐项扫描，命中的地方改写。润色模式（模式 B）的诊断也用这份清单。

使用原则：清单里的词不是绝对禁用，而是不能成为习惯。同一个词全文出现一两次问题不大，反复出现、出现在段落开头或结尾才是 AI 痕迹。

---

## 一、长难句与辞藻堆砌（最高优先级）

朴素行文是本 skill 的硬约束，这一类问题优先处理。

| 问题 | 判断标准 | 改法 |
| --- | --- | --- |
| 中文长句 | 一句超过 60 字 | 拆成两三句，一句只讲一件事 |
| 中文流水句 | 一句里有 5 个以上逗号 | 在意思转换处改用句号 |
| 多层定语 | 一句里“的”超过 3 个 | 把长定语拆成独立的一句 |
| 英文长句 | 一句超过 25 词 | 先写主干，再用新句子补细节 |
| 英文嵌套从句 | 一句有两个以上从句 | 每句最多保留一个从句 |
| 名词化 | make a decision、进行优化 | 改用动词：decide、优化 |
| 堆砌四字词 | 连续三四个四字短语 | 保留最有信息量的一个，其余换成具体描述 |
| 华丽比喻 | “数字化浪潮”“技术的灯塔” | 直接说事实 |
| 宏大开头 | “随着科技的飞速发展……” | 从具体问题或具体事实开始写 |

**拆句示例（中文）**

- 原句：随着微服务架构在大型互联网企业中的广泛应用以及容器化技术的不断成熟，如何在保证系统高可用性的前提下有效降低服务之间的通信延迟已经成为业界普遍关注的重要问题。
- 改为：微服务在大型互联网公司里已经很常见，容器技术也越来越成熟。服务拆多了以后，服务之间的通信延迟成了新问题。难点在于，降低延迟的同时还要保证系统可用。

**拆句示例（英文）**

- Before: The implementation of a caching layer, which was designed to reduce the load on the database that had been experiencing significant performance degradation during peak hours, resulted in a substantial improvement.
- After: The database slowed down badly during peak hours. The team added a caching layer to reduce its load. Response times improved a lot.

---

## 二、中文高频词

| 避免 | 问题 | 替换策略 |
| --- | --- | --- |
| 首先……其次……最后 | 机械的结构标记 | 按话题、时间或因果顺序自然展开 |
| 综上所述、总而言之、总的来说 | 套话式总结 | 删掉，或写“从这些情况看” |
| 值得注意的是、需要指出的是 | 空洞的强调 | 删掉，直接说要注意的内容 |
| 至关重要、不可或缺、举足轻重 | 空泛的形容 | 说明具体影响，如“缺少索引时查询要 8 秒” |
| 深入探讨、深入分析、全面剖析 | 自我拔高 | 删掉，直接写分析内容 |
| 赋能、助力、打造、构建……生态 | 宣传腔 | 用普通动词：支持、帮助、做出 |
| 全方位、多维度、多层次 | 空泛的修饰 | 列出具体是哪几个方面 |
| 日益、愈发、不断 | 泛泛的趋势描述 | 给出时间和数据 |
| 随着……的不断发展 | 宏大开头 | 从具体事实写起 |
| 在……的背景下 | 套话开头 | 删掉，或换成具体的时间和场景 |
| 如上所述、如前所述 | 多余的回指 | 直接重述要点，或删掉 |
| 该技术、本文、上述方法 | 指代模糊 | 用具体名称：Docker、这次优化 |
| 具有以下特点： | 冒号后接列表 | 把特点写进段落 |
| 起到了重要作用 | 空洞的评价 | 说清楚具体起了什么作用 |

## 三、中文句式

| 句式 | 问题 | 改法 |
| --- | --- | --- |
| 不仅……而且……更…… | 层层递进，显得刻意 | 拆成两句平铺直叙 |
| 三项排比（“提升了效率、降低了成本、优化了体验”） | 凡事凑三点 | 只写真正有依据的一两点，并给出数据 |
| 段尾拔高总结（“这充分体现了……的重要意义”） | 每段都升华 | 段落在最后一个事实处结束 |
| 对称句（“既要……又要……”“一方面……另一方面……”反复出现） | 句式单调 | 全文少用，换成普通陈述 |
| 破折号频繁出现 | AI 常见标点习惯 | 改用逗号、句号或括号，全文少量使用 |
| 设问开头（“那么，……呢？”） | 刻意制造悬念 | 直接陈述 |

---

## 四、英文高频词

| Avoid | Problem | Use instead |
| --- | --- | --- |
| delve into | AI 高频词 | look at, examine |
| crucial, pivotal, vital | 空泛的强调 | important, or state the actual effect |
| landscape, realm, tapestry | 华丽比喻 | field, area, or name it directly |
| leverage, utilize | 书面腔 | use |
| robust, seamless | 空泛的赞美 | describe what actually works |
| it is worth noting that | 空洞的强调 | delete it and state the point |
| plays a vital role in | 空洞的评价 | say what it does |
| in today's fast-paced world | 宏大开头 | start with a specific fact |
| moreover, furthermore, additionally | 机械衔接（经常出现在段首时） | let the content connect, or use "also" |
| in conclusion, to sum up | 套话式总结 | end with the last real point |
| demonstrate, facilitate | 书面腔 | show, help |
| a myriad of, a plethora of | 华丽表达 | many |
| navigate the complexities of | 空洞的动词短语 | deal with |
| ever-evolving, cutting-edge | 宣传腔 | new, recent, or give a date |

## 五、英文句式

| Pattern | Problem | Fix |
| --- | --- | --- |
| not only … but also … | 刻意的递进 | two plain sentences |
| rule of three ("faster, cheaper, and more reliable") | 凡事凑三点 | keep only the points with evidence |
| em-dash used often (—) | AI 常见标点习惯 | use commas, periods or parentheses |
| "This highlights the importance of …" at paragraph end | 段尾拔高总结 | end on the last fact |
| "While X, Y" opening many sentences | 句式单调 | vary the sentence openings |

---

## 六、结构层面

| 问题 | 判断标准 | 改法 |
| --- | --- | --- |
| 段落长度一样 | 每段都是 4–5 句 | 让段落长短随内容变化，短段可以只有两句 |
| 每节以总结句结尾 | 每一节的最后一句都在复述本节内容 | 删掉复述，让下一节自己开始 |
| 加粗过多 | 一段里有多处加粗 | 正文基本不加粗 |
| 过度模糊（hedging） | “在一定程度上”“可能会”“或许”反复出现 | 有依据的结论直接说，没有依据的就不写 |
| 列表过多 | 正文里频繁出现项目符号 | 写成段落 |
| 空泛标题 | 引言、分析、结论 | 用描述内容的标题 |

---

## 自查流程

1. **句长**：逐段检查，按本清单第一部分的标准拆分长句。
2. **高频词**：搜索第二部分和第四部分的词，数一数出现次数。反复出现或出现在段首、段尾的，改写。
3. **句式和结构**：通读全文，对照第三、五、六部分检查。
4. **重读**：改完后再读一遍，确认意思没有变，事实和数据没有丢。
