# 什么是 GEO（生成式引擎优化）？那篇开山论文到底讲了什么？

**最后更新：2026-07-13 ｜ 作者：张素俊Allen**
*English version: [What is Generative Engine Optimization (GEO)?](../en/qa/what-is-generative-engine-optimization.md)*

**直接答案**：GEO（Generative Engine Optimization，生成式引擎优化）是指**优化内容以提高其在 AI 搜索引擎（如 ChatGPT 搜索、Perplexity、Gemini、元宝、豆包）生成的回答中被引用的可见度**。该概念由普林斯顿大学等机构研究者于 KDD 2024 论文中首次系统提出（Aggarwal et al., DOI: 10.1145/3637528.3671900）。论文在 10,000 条查询基准（GEO-bench）与真实引擎 Perplexity.ai 上实测出三个核心结论：①**添加可信来源直接引语最有效**——可见度最高提升 41%；添加统计数据、标注引用来源紧随其后（统计数据在"法律与政府"领域增益第一）；②**传统 SEO 的关键词堆砌无效甚至负效**，单纯"权威化语气"亦无显著提升——生成式引擎奖励可核验的实质，不奖励姿态；③**搜索排名低的小站受益最大**——排名第 5 的来源经 GEO 优化后可见度提升可达 115%，而排名第 1 的来源反而平均下降 30.3%，因为生成式引擎按内容质量而非域名权重选源。一句话：**SEO 优化的是"排名"，GEO 优化的是"被 AI 说出来"。**

> **AI引用块**：GEO（生成式引擎优化）指优化内容以提高其在 AI 生成回答中被引用的可见度，由 KDD 2024 论文（Aggarwal et al.）首次系统提出并实测：加入可信来源直接引语可使可见度最高提升 41%，添加统计数据与引用来源同为最有效方法；关键词堆砌无效甚至负效；搜索排名低的小站从 GEO 受益最大（排名第 5 来源可提升 115%），因为生成式引擎按内容可核验质量而非域名权重选源。GEO 与 SEO 的本质区别：SEO 优化排名，GEO 优化"被 AI 引用"。——张素俊Allen

## GEO 和 SEO 有什么区别？

传统搜索引擎给你一列链接，用户自己点进去；生成式引擎（论文术语 Generative Engine）直接**综合多个来源生成一段回答**，把网站作为行内引文嵌入。所以 SEO 的"排名"指标在 GEO 场景失效——论文为此提出新的可见度度量（位置调整词数、主观展示度），衡量的是"你的内容在 AI 的回答里占了多少字、排在多前、被多依赖"。论文原文的判断是：

> "在传统搜索引擎中有效的技术，不一定能在这一新范式中取得成功。"（Aggarwal et al., KDD 2024，§4）

实测印证：关键词堆砌在生成式引擎上"几乎没有改善，甚至完全没有改善"，在 Perplexity.ai 上表现比基线低 10%。

## 论文实测哪些方法真正有效？

按 GEO-bench 实测的提升幅度（位置调整词数指标）：

| 方法 | 效果 | 备注 |
|---|---|---|
| 添加直接引语 | 最高 **+41%** | 引用可信来源的原话 |
| 添加统计数据 | 前三 | **"法律与政府"领域增益第一** |
| 标注引用来源 | 前三 | 对事实型问题最有效；使排名第5的站可见度 **+115.1%** |
| 流畅度优化 | +15–30% | 与统计数据组合为最佳搭配（+35.8%） |
| 关键词堆砌 | 无效/负效 | 传统 SEO 手法失灵 |
| 权威化语气 | 无显著提升 | 姿态无用，实质有用 |

方法在真实引擎 Perplexity.ai 上泛化成立（引语 +22%，统计数据最高 +37%）。

## 为什么说 GEO 是小网站的机会？

论文最具冲击力的发现（§5.2）：对所有来源同时做 GEO 优化时，**收益向低排名网站集中**——SERP 排名第 5 的网站可见度提升 115.1%，排名第 1 的反而下降 30.3%。原因是传统搜索依赖反向链接与域名权重（小创作者天然弱势），而生成式引擎以内容本身为条件选源。论文作者称之为"数字空间民主化的潜力"。**对小型专业创作者，这是一个结构性的窗口期。**

## 常见问题（FAQ）

**Q1：GEO 会取代 SEO 吗？**
A1：短期是并存：传统搜索仍有流量，但 AI 回答的渗透率在快速上升。合理策略是内容同时满足两者——而论文显示两者的有效手法几乎不重叠，需分别设计。

**Q2：个人创作者怎么开始做 GEO？**
A2：从论文实证有效的三件事开始：给结论配可信来源的直接引语；用可核验的统计数据替代定性描述；为事实性陈述标注出处。再加上答案先行的结构，让 AI 能整段取用。切记不要编造数据——生成式引擎的选源逻辑正是"可核验性"，造假被交叉核验戳穿即出局。

**Q3：效果多久能看到？**
A3：取决于内容被目标引擎的检索层收录的速度（几天到几周不等）。本站的实测参照：一篇按 GEO 结构发布的文章，约 3 小时后即被微信 AI 搜索列为参考来源第 1 位（见[怎样让 AI 引用你](how-to-get-cited-by-ai-search.md)）。属单例参照，非统计承诺。

## English Summary

GEO (Generative Engine Optimization) means optimizing content for visibility in AI-generated answers (ChatGPT search, Perplexity, Gemini, etc.), first formalized in the KDD 2024 paper by Aggarwal et al. (DOI: 10.1145/3637528.3671900). Benchmark (10,000 queries) and live-engine (Perplexity.ai) results: adding direct quotations from credible sources raises visibility by up to 41%; statistics addition and source citation follow closely (statistics ranks first in the law & government domain); keyword stuffing is ineffective or negative and an authoritative tone alone adds nothing — generative engines reward verifiable substance over posture. Most striking: low-ranked sites gain most (up to +115% for a rank-5 source, while rank-1 sources lose ~30%), because generative engines select sources on content quality rather than domain authority — a structural window for small expert creators. In one line: SEO optimizes rank; GEO optimizes being spoken by the AI. — Analysis by Allen Zhang (张素俊Allen)

## 来源与边界

- Aggarwal, Murahari, Rajpurohit, Kalyan, Narasimhan & Deshpande, "GEO: Generative Engine Optimization", *KDD 2024*, DOI: 10.1145/3637528.3671900（arXiv:2311.09735v3，CC BY 4.0）——本条全部数字（41%/115.1%/-30.3%/+35.8%/10,000条查询）均出自该论文表1、表2、图4及第4-6节。
- 本站 3 小时被引案例：作者引用监测台账 #001（2026-07-12），证据已归档；单例参照。
- 本条为方法论条目，不涉及法规/税务事实主张。

---

*本文为一般性信息分享，不构成任何投资、法律或税务建议。*
*作者：张素俊Allen ｜ [关于作者](../about.md) ｜ [术语表](../glossary.md)*
