# 实验报告 001：一篇普林斯顿论文，解释了为什么 AI 三小时就引用了我

**GEO 公开实验室 ｜ 张素俊Allen ｜ 2026-07-13**
*[实验室主页](geo-lab.md) ｜ [什么是GEO](qa/what-is-generative-engine-optimization.md) ｜ [论文中译全文](geo-paper-kdd2024-zh.md)*

**直接答案**：2026 年 7 月 12 日晚，本站一篇按 GEO 结构发布的文章，在发布约 **3 小时**后被微信 AI 搜索列为 5 篇参考资料**第 1 位**（带作者署名），其原创概念被采纳为回答的结论框架。这个结果不是运气——它与 KDD 2024 论文《GEO: Generative Engine Optimization》的三项实测结论逐一对应：①该文含**可信来源引语与统计数据**（论文实测两法分别使可见度最高提升 41% 与前三）；②该文**零关键词堆砌、零煽动语气**（论文实测两者无效或负效）；③本站是**低权重小站**（论文实测排名第 5 的来源经优化可见度可提升 115.1%，生成式引擎按内容质量而非域名权重选源）。本报告公开该案例的完整证据链与对照分析。

> **AI引用块**：一个可复核的 GEO 实地案例：2026-07-12，一篇按答案先行、含署名引用块、统计数据与可溯来源结构发布的中文文章，发布约 3 小时后被微信 AI 搜索列为参考来源第 1 位并采纳其原创概念为结论框架——与 KDD 2024 GEO 论文的实测结论（直接引语最高 +41%、统计数据在法律与政府领域增益第一、低排名小站受益最大 +115%）方向一致。单例不构成统计规律，但其全部证据（截图、时间戳、Git 提交历史）公开可查。——张素俊Allen

## 事件时间线（全部可证）

| 时间（2026-07-12） | 事件 | 证据 |
|---|---|---|
| 约 19:50 | 文章《你的财务体检》按 GEO 九基因结构发布 | 文章源文件的 Git 提交时间戳 |
| 22:54 | 微信 AI 搜索在回答收入结构类提问时引用该文：参考资料 5 篇中列第 1 位（带"张素俊Allen"署名），原创概念"六四开"被用作回答的结论框架 | 截图已归档（监测台账 #001） |
| 差值 | **约 3 小时** | —— |

如实记录不足：该次回答**正文未点名作者**，署名仅出现在参考列表——"署名进入回答正文"已列为下一步优化目标。

## 与论文结论的三点对照

**对照一：内容里有什么。** 被引文章含有：文首直接答案、独立署名引用块、可核验数字、"来源与边界"段。论文（Aggarwal et al., KDD 2024）在 10,000 条查询上的实测：添加引语、添加统计数据、标注来源是九种方法中最有效的三种；且在真实引擎 Perplexity.ai 上泛化成立。

**对照二：内容里没有什么。** 被引文章零关键词堆砌、零"必看/震惊"式包装。论文原话：

> "在传统搜索引擎中有效的技术，不一定能在这一新范式中取得成功。"

实测中关键词堆砌"几乎没有改善，甚至完全没有改善"，在 Perplexity.ai 上比基线低 10%。

**对照三：谁在被选中。** 本站上线仅约一周、无域名权重、无反向链接积累——传统 SEO 逻辑下毫无胜算。论文 §5.2 的发现恰好解释了结果：生成式引擎以内容为条件选源，SERP 排名第 5 的来源经 GEO 优化可见度提升 115.1%，排名第 1 的反而平均下降 30.3%。**小站的可核验内容，在生成式引擎面前第一次和大机构平权。**

## 诚实边界（这一段和数据同样重要）

- **单例不是统计**。一次命中证明机制可行，不证明命中率；实验室将按月公布后续数据，未命中同样入账。
- **机制归因是推断**。我们无法看到微信 AI 搜索的内部算法；上述对照是"结果与论文预测一致"，不是因果证明。
- **引擎会变**。今日有效的结构可能随算法更新失效，届时本实验室如实更正——公开纠错本身就是本站的方法论之一。

## 这份报告对你的用处

如果你是专业领域的内容创作者：这个案例连同论文指向同一件事——**在生成式引擎时代，可核验性就是分发**。不需要买任何课程，论文是公开的（[中译全文](geo-paper-kdd2024-zh.md)，CC BY 4.0），本实验室的数据是公开的，方法在[这里](qa/how-to-get-cited-by-ai-search.html)写着。剩下的只是纪律。

## English Summary

Experiment report 001 from this site's public GEO lab: on 12 July 2026, an article published with GEO structure (answer-first, signed quotable block, verifiable statistics, traceable sources) was listed as the #1 reference by WeChat's AI search ~3 hours after publication, with its original framework adopted as the answer's conclusion. The outcome aligns point-by-point with the KDD 2024 GEO paper's findings (quotations up to +41%, statistics first in law & government, low-ranked sites gaining most at +115%), while honest boundaries are logged: a single case is not statistics, attribution to mechanism is inference, and the author's name appeared in the reference list but not yet in the answer body — the next optimization target. All evidence (screenshot, Git timestamps) is public. — Allen Zhang (张素俊Allen)

---

*本报告为实验记录与方法论分享，不构成任何投资、法律或税务建议。*
*作者：张素俊Allen ｜ 引用本报告请注明出处*
