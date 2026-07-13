<!-- 本页由私库自动同步发布 -->
> **发布说明**：本中译本由 **张素俊Allen 组织并主导需求、AI 辅助完成翻译**，人工做了排版与校对组织，公开分享以方便中文读者研读 GEO 开山论文。原论文以 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 发布于 [arXiv:2311.09735v3](https://arxiv.org/abs/2311.09735v3)（正式版见 KDD 2024，DOI: [10.1145/3637528.3671900](https://doi.org/10.1145/3637528.3671900)）；原作者拥有原作全部权利，本译本为中文改编，不代表原作者或其机构的背书。译文如与原文有出入，以英文原文为准；发现误译请提 Issue，我们公开更正。
> 配套阅读：[什么是GEO（导读）](qa/what-is-generative-engine-optimization.md) ｜ [GEO 公开实验室（本站实测数据）](geo-lab.md)

# GEO：生成式引擎优化

**GEO: Generative Engine Optimization**

中文全译版｜依据 arXiv v3（2024年6月28日修订）与 KDD 2024 正式版本校译

---

## 校译说明

1. 本译本完整覆盖论文的题名、作者与机构、摘要、正文、公式、图表及图注、致谢、参考文献和附录。参考文献保留英文题名与书目信息，以免影响检索准确性。
2. 术语统一如下：Generative Engine 译为“生成式引擎”；Generative Engine Optimization 译为“生成式引擎优化”；visibility 译为“可见度”；impression 译为“展示度”；Position-Adjusted Word Count 译为“位置调整词数”；Subjective Impression 译为“主观展示度”。
3. 原文存在少量拼写、标点及语法疏漏，译文依照上下文还原作者本意，不改变任何公式、数值、实验设置或论证结论。
4. 论文图内的英文文字在原图之后逐项给出中文对照；表格数据按原文保留。
5. 本译本基于采用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 的 [arXiv:2311.09735v3](https://arxiv.org/abs/2311.09735v3) 制作，属于中文改编。原作者拥有原作权利；译本不代表原作者或其所在机构对译者及使用者的背书。

---

## 作者与机构

**Pranjal Aggarwal<sup>*</sup>**  
印度理工学院德里分校，印度新德里  
pranjal2041@gmail.com

**Vishvak Murahari<sup>*</sup>**  
普林斯顿大学，美国新泽西州普林斯顿  
murahari@cs.princeton.edu

**Tanmay Rajpurohit**  
独立研究者，美国西雅图  
tanmay.rajpurohit@gmail.com

**Ashwin Kalyan**  
独立研究者，美国西雅图  
asaavashwin@gmail.com

**Karthik Narasimhan**  
普林斯顿大学，美国新泽西州普林斯顿  
karthikn@princeton.edu

**Ameet Deshpande**  
普林斯顿大学，美国新泽西州普林斯顿  
asd@princeton.edu

<sup>*</sup> 同等贡献。

## 出版信息

- 会议：第30届 ACM SIGKDD 知识发现与数据挖掘国际会议（KDD ’24）
- 时间与地点：2024年8月25日至29日，西班牙巴塞罗那
- 页码：5–16，共12页
- DOI：[10.1145/3637528.3671900](https://doi.org/10.1145/3637528.3671900)
- arXiv：[2311.09735v3](https://arxiv.org/abs/2311.09735v3)

**ACM 推荐引用格式：**  
Pranjal Aggarwal, Vishvak Murahari, Tanmay Rajpurohit, Ashwin Kalyan, Karthik Narasimhan, and Ameet Deshpande. 2024. GEO: Generative Engine Optimization. In *Proceedings of the 30th ACM SIGKDD Conference on Knowledge Discovery and Data Mining (KDD ’24)*, August 25–29, 2024, Barcelona, Spain. ACM, New York, NY, USA, 12 pages. https://doi.org/10.1145/3637528.3671900

**ACM 版本所载许可说明（译文）：**  
允许为个人使用或课堂使用而免费制作本作品全部或部分内容的数字版或纸质版副本，前提是这些副本并非出于营利或商业优势而制作或分发，并且副本首页须载明本声明及完整引用信息。对于本作品中版权不属于作者的组成部分，其版权必须得到尊重。允许在注明出处的情况下制作摘要。若以其他方式复制、再版、发布到服务器或重新分发到邮件列表，则须事先获得明确许可和／或支付费用。许可申请请联系 permissions@acm.org。

## 计算机分类体系（CCS）概念

- 计算方法学 → 自然语言处理
- 计算方法学 → 机器学习
- 信息系统 → 网络搜索与信息发现

## 关键词

生成模型；搜索引擎；数据集与基准

---

## 摘要

大语言模型（Large Language Models，LLMs）的出现，催生了一种新的搜索引擎范式：使用生成模型收集并总结信息，以回答用户查询。我们将这一新兴技术统一形式化为“生成式引擎”（Generative Engines，GEs）框架。它能够生成准确且个性化的回答，并正在迅速取代 Google、Bing 等传统搜索引擎。

生成式引擎通常会综合多个来源的信息，再使用大语言模型加以总结，从而满足用户查询。虽然这一转变显著提高了用户效用，也增加了生成式搜索引擎的流量，但它给第三类利益相关者——网站与内容创作者——带来了巨大挑战。由于生成式引擎具有黑箱性且变化迅速，内容创作者几乎无法控制自己的内容将在何时、以何种方式被呈现。

生成式引擎已然成为长期存在的事物，因此我们必须确保创作者经济不会因此处于不利地位。为此，我们提出“生成式引擎优化”（Generative Engine Optimization，GEO）。这是首个帮助内容创作者提升其内容在生成式引擎回答中可见度的新范式：它通过一个灵活的黑箱优化框架，定义并优化可见度指标。

为了对这一范式进行系统评估，我们提出 GEO-bench——一个大规模基准，其中包含来自多个领域的多样化用户查询，以及回答这些查询所需的相关网络来源。通过严格评估，我们证明 GEO 能使内容在生成式引擎回答中的可见度提高多达 40%。此外，我们还发现，不同策略的有效性会因领域而异，这凸显了领域特定优化方法的必要性。

我们的工作为信息发现系统开辟了一个新的前沿，对生成式引擎开发者和内容创作者都具有深远影响。<sup>1</sup>

<sup>1</sup> 代码与数据见：https://generative-engines.com/GEO/

---

# 1 引言

三十年前，传统搜索引擎的发明彻底改变了全球信息获取和传播的方式 [4]。这些搜索引擎虽然功能强大，并催生了学术研究、电子商务等众多应用，但它们只能针对用户查询提供一份相关网站列表。

然而，大语言模型近年来取得的成功 [5, 21]，为 BingChat、Google 的 SGE 和 Perplexity.ai 等更先进的系统铺平了道路。这些系统将传统搜索引擎的能力与生成模型结合起来。我们将它们称为“生成式引擎”（Generative Engines，GE），因为它们既会搜索信息，也会利用多个来源综合生成多模态回答。从技术角度看，生成式引擎（见图2）会从数据库（如互联网）中检索相关文档，再使用大型神经模型生成以这些来源为依据的回答，从而既能标明出处，也能为用户提供核验信息的途径。

生成式引擎对开发者和用户的价值显而易见：用户可以更快、更准确地获取信息；开发者则可以制作精确且个性化的回答，从而提高用户满意度和收入。然而，生成式引擎却使第三类利益相关者——网站与内容创作者——处于不利地位。

与传统搜索引擎不同，生成式引擎会直接给出精确而全面的回答，不再要求用户跳转到网站。这可能减少网站的自然流量并影响其可见度 [16]。数以百万计的小企业和个人依靠网络流量与可见度维持生计，因此生成式引擎将显著重塑创作者经济。此外，生成式引擎具有黑箱性和专有性，使内容创作者难以控制和理解自己的内容如何被吸收、又如何被呈现。

在本研究中，我们提出首个面向创作者、用于优化生成式引擎内容的一般性框架，并将其命名为“生成式引擎优化”（Generative Engine Optimization，GEO），旨在帮助内容创作者更有信心地应对这一新的搜索范式。

GEO 是一个灵活的黑箱优化框架，用于在专有、闭源的生成式引擎中优化网络内容的可见度（见图1）。GEO 接收一个来源网站作为输入，通过调整和校准其呈现方式、文本风格与内容，输出优化后的网站版本，从而提高该网站在生成式引擎中的可见度。

*【图1：GEO 方法示意图（原论文图）——原图请见 arXiv:2311.09735 原文；图内文字中文对照见下方】*

**图1：** 我们提出的生成式引擎优化（GEO）方法会优化网站，以提高其在生成式引擎回答中的可见度。图中的披萨网站原本可见度很低；借助 GEO 的黑箱优化框架，网站所有者可以对其网站进行优化，提高它在生成式引擎中的可见度。此外，GEO 的一般框架允许内容创作者自行定义并优化定制化可见度指标，使他们在这一新兴范式中获得更大的控制权。

**图1内部文字中文对照：**

- Query: Things to do in NY? → 查询：在纽约可以做什么？
- GE generates response based on sources → 生成式引擎依据来源生成回答。
- Low Visibility. Use GEO! → 可见度低。使用 GEO！
- Objective: Optimize Pizza Website → 目标：优化披萨网站。
- Response Before GEO → 使用 GEO 前的回答。
- Response After GEO → 使用 GEO 后的回答。
- 使用 GEO 前：“下午，在中央公园悠闲漫步，远离城市的喧嚣 [1]。然后前往标志性的自由女神像 [2]。也别忘了品尝纽约风格披萨 [3]。”
- 使用 GEO 后：“首先品尝这座城市著名的纽约风格披萨作为早餐。这是一场为全天定下基调的美食体验 [3]。然后游览中央公园 [1]，接着前往自由女神像 [2]。”

此外，GEO 还提出了一个灵活框架，用于定义专门适配生成式引擎的可见度指标，因为生成式引擎中的“可见度”概念比传统搜索引擎更细腻、更多维（见图3）。传统搜索引擎以线性网站列表呈现结果，因此结果页上的平均排名可以很好地衡量可见度；但这一指标并不适用于生成式引擎。

生成式引擎会提供内容丰富、结构化程度很高的回答，并把网站作为行内引文嵌入回答中；不同网站被引用的篇幅、位置和样式往往各不相同。因此，我们需要专门为生成式引擎设计可见度指标，从客观和主观两个角度，在多个维度上衡量已署名来源的可见度，例如引文与查询的相关性，以及引文对回答的影响力。

为了对 GEO 方法进行可靠而广泛的评估，我们提出 GEO-bench。该基准由 10,000 条来自不同领域和不同来源、并经过生成式引擎适配的查询组成。

通过系统评估，我们证明，所提出的生成式引擎优化方法能在多样化查询上将可见度提高多达 40%，从而为内容创作者提供有益策略，帮助他们提高可见度。其中，我们发现，在内容中加入引文、相关来源的直接引语以及统计数据，能够显著提高来源可见度；在各种查询中，增幅可超过 40%。我们还在真实世界的生成式引擎 Perplexity.ai 上验证了生成式引擎优化的有效性，可见度提升最高达到 37%。

概括而言，我们的贡献有三点：

1. 我们提出生成式引擎优化，这是首个帮助网站所有者针对生成式引擎优化网站的一般性优化框架。对于广泛的查询、领域和真实世界黑箱生成式引擎，生成式引擎优化可以将网站可见度提高多达 40%。
2. 我们的框架提出了一套专为生成式引擎设计的综合可见度指标，并允许内容创作者通过定制化可见度指标，灵活优化自己的内容。
3. 为推动在生成式引擎环境中可靠评估 GEO 方法，我们提出首个大规模基准。它包含来自广泛领域和数据集的多样化搜索查询，并专门针对生成式引擎进行了适配。

---

# 2 形式化定义与方法

## 2.1 生成式引擎的形式化定义

尽管众多生成式引擎已经部署并服务于数以百万计的用户，但目前尚无标准框架。我们给出一种形式化定义，使其能够容纳生成式引擎设计中的各种模块化组件。

我们所描述的生成式引擎包含若干后端生成模型，以及一个用于检索来源的搜索引擎。生成式引擎（GE）接收用户查询 $q_u$，返回自然语言回答 $r$；其中，$P_U$ 表示个性化用户信息。生成式引擎可以表示为如下函数：

$$
f_{GE} := (q_u, P_U) \rightarrow r \tag{1}
$$

生成式引擎包含两个关键组成部分：

1. 一组生成模型 $G=\{G_1,G_2,\ldots,G_n\}$，每个模型承担查询改写、摘要等特定任务；
2. 一个搜索引擎 $SE$，它在给定查询 $q$ 后返回一组来源 $S=\{s_1,s_2,\ldots,s_m\}$。

图2给出了一个具有代表性的工作流程；在本文撰写时，它与 BingChat 的设计高度相似。该流程先把输入查询分解为一组更简单、更容易交由搜索引擎处理的查询。给定一个查询后，查询改写生成模型 $G_1=G_{qr}$ 会生成查询集合 $Q^1=\{q_1,q_2,\ldots,q_n\}$，然后将这些查询传给搜索引擎 $SE$，以检索一组经过排序的来源 $S=\{s_1,s_2,\ldots,s_m\}$。

来源集合 $S$ 随后被传给摘要模型 $G_2=G_{sum}$。该模型为 $S$ 中的每个来源生成摘要 $Sum_j$，形成摘要集合 $Sum=\{Sum_1,Sum_2,\ldots,Sum_m\}$。接着，摘要集合被传给回答生成模型 $G_3=G_{resp}$，后者生成一个以来源 $S$ 为依据的综合回答 $r$。

本文聚焦单轮生成式引擎，但这一形式化定义可以扩展到多轮对话式生成式引擎（见附录A）。

*【图2：生成式引擎概览（原论文图）——原图请见 arXiv:2311.09735 原文；图内文字中文对照见下方】*

**图2：** 生成式引擎概览。生成式引擎主要由一组生成模型和一个检索相关文档的搜索引擎组成。生成式引擎接收用户查询，通过一系列步骤生成最终回答；该回答以检索到的来源为依据，并在全文中嵌入行内出处标注。

**图2内部文字中文对照：**

- Query → 查询
- Query Reformulating Model → 查询改写模型
- Reformulated Queries → 改写后的查询
- Search Engine → 搜索引擎
- Summarizing Model → 摘要模型
- Response Model → 回答模型
- Output → 输出
- Generative Engine → 生成式引擎

回答 $r$ 通常是嵌入了引文的结构化文本。鉴于大语言模型容易产生幻觉，引用尤为重要 [10]。具体而言，设回答 $r$ 由句子集合 $\{l_1,l_2,\ldots,l_o\}$ 构成。每个句子都可能由一组引文提供支撑，这组引文属于检索到的文档集合，即 $C_i\subset S$。

理想的生成式引擎应当确保：回答中的所有陈述都有相关引文支持，即引文召回率高；所有引文都能准确支持与其关联的陈述，即引文精确率高 [14]。图3给出了一个具有代表性的生成式引擎回答。

## 2.2 生成式引擎优化

搜索引擎的出现催生了搜索引擎优化（Search Engine Optimization，SEO）。SEO 是帮助网站创建者优化内容、提高搜索引擎排名的过程。排名越高，通常意味着可见度和网站流量越高。

然而，传统 SEO 方法不能直接应用于生成式引擎。原因在于：不同于传统搜索引擎，生成式引擎中的生成模型并不局限于关键词匹配；语言模型在读取来源文档和生成回答时，能够更细致地理解文本与用户查询。随着生成式引擎迅速成为主要的信息传递范式，而 SEO 又无法直接适用，我们需要新的技术。

为此，我们提出生成式引擎优化这一新范式。在该范式下，内容创作者的目标是提高自己在生成式引擎回答中的可见度（或展示度）。我们用函数 $Imp(c_i,r)$ 定义网站——亦即引文 $c_i$——在带有引文的回答 $r$ 中的可见度；网站创建者希望将其最大化。

从生成式引擎的角度看，其目标是最大化与用户查询最相关的引文的可见度，即最大化：

$$
\sum_i f\bigl(Imp(c_i,r),Rel(c_i,q,r)\bigr)
$$

其中，$Rel(c_i,q,r)$ 衡量在回答 $r$ 的语境中，引文 $c_i$ 与查询 $q$ 的相关性；函数 $f$ 由生成式引擎的具体算法设计决定，对终端用户而言是一个黑箱函数。此外，$Imp$ 与 $Rel$ 这两个函数都带有主观性，在生成式引擎场景中尚未得到清晰定义。下文将对其作出定义。

*【图3：传统搜索引擎与生成式引擎中的排名和可见度（原论文图）——原图请见 arXiv:2311.09735 原文；图内文字中文对照见下方】*

**图3：** 在传统搜索引擎中，排名和可见度指标较为直接：网站来源按排名顺序排列，并原样展示内容。生成式引擎则会生成内容丰富、结构化的回答，经常把多个引文交错嵌入同一个文本块中，因此“排名”和“可见度”变得细腻而多维。此外，与已有大量提高网站可见度研究的搜索引擎不同，如何优化内容在生成式引擎回答中的可见度仍不明确。为应对这些挑战，我们的黑箱优化框架提出了一系列精心设计的展示度指标，供创作者衡量并优化网站表现，同时也允许创作者自行定义展示度指标。

**图3内部文字中文对照：**

- Rank → 排名
- Query: Things to do in NY? → 查询：在纽约可以做什么？
- Search Engine → 搜索引擎
- Do creators know…? → 创作者是否知道……？
- How to measure visibility? → 如何衡量可见度？
- How to improve visibility? → 如何提高可见度？
- How is my content being portrayed? → 我的内容正在以怎样的方式被呈现？
- Generative Engine → 生成式引擎
- 传统搜索结果1：“纽约中央公园：在城市中心的中央公园悠闲漫步，远离城市的喧嚣。”
- 传统搜索结果2：“自由女神像：前往标志性的自由女神像。它不仅是一座纪念碑，更是希望与自由的象征。”
- 传统搜索结果3：“纽约风格披萨：品尝著名的纽约风格披萨。这是一场在世界其他地方都无可比拟的美食体验。”
- 生成式回答：“在中央公园周边别致的小餐馆里品尝标志性的纽约风格披萨，把美食享受与风景体验结合起来 [1, 3]。欣赏自由女神像所承载的历史 [2]；多元的披萨配料也映照出这座城市的文化交汇，深受当地人与游客喜爱 [2, 3]。当白昼渐入黄昏，漫步中央公园，就像在一顿风味浓烈的美餐之后感受宁静 [3, 1]。”

### 2.2.1 生成式引擎的展示度

在 SEO 中，网站的展示度（或可见度）由它在一系列查询中的平均排名决定。然而，生成式引擎的输出形态要求我们采用不同的展示度指标。与搜索引擎不同，生成式引擎会在同一个回答中整合多个来源的信息。因此，引用网站内容的篇幅、独特性和呈现方式等因素，共同决定一条引文的真实可见度。

如图3所示，结果页上的简单排名可以有效衡量传统搜索引擎中的展示度与可见度，却不能用于生成式引擎回答。

为应对这一挑战，我们提出一组展示度指标，并在设计时遵循三项关键原则：

1. 指标应当与创作者切身相关；
2. 指标应当具备可解释性；
3. 广大内容创作者应当能够轻松理解这些指标。

第一项指标是“词数”（Word Count），即与某一引文相关的句子所包含的归一化词数。其数学定义如下：

$$
Imp_{wc}(c_i,r)=\frac{\sum_{s\in S_{c_i}}|s|}{\sum_{s\in S_r}|s|} \tag{2}
$$

其中，$S_{c_i}$ 是引用 $c_i$ 的句子集合，$S_r$ 是回答中的句子集合，$|s|$ 是句子 $s$ 的词数。如果一个句子引用了多个来源，我们会在这些引文之间平均分配该句的词数。

直观而言，词数越高，说明该来源在回答中发挥的作用越重要，用户接触该来源的程度也就越高。然而，“词数”并不受引文排名或出现位置影响——例如，它不会因为某条引文最先出现而发生变化。因此，我们提出“位置调整词数”，按照引文位置的指数衰减函数降低权重：

$$
Imp_{pwc}(c_i,r)=\frac{\sum_{s\in S_{c_i}}|s|\cdot e^{-\frac{pos(s)}{|S|}}}{\sum_{s\in S_r}|s|} \tag{3}
$$

直观地说，回答中较早出现的句子更有可能被用户阅读，因此，$Imp_{pwc}$ 定义中的指数项会给予这些引文更高权重。于是，位于回答开头的网站，即使对应词数较少，也可能比位于回答中部或末尾、词数更多的网站获得更高展示度。

之所以选择指数衰减函数，是因为多项研究表明，搜索引擎中的点击率会随着排名呈幂律变化 [7, 8]。

上述展示度指标是客观且有充分依据的，但它们忽略了引文影响用户注意力时的主观因素。为此，我们提出“主观展示度”（Subjective Impression）指标。它包含以下维度：被引材料与用户查询的相关性；引文的影响力；引文所呈现材料的独特性；主观位置；主观数量；用户点击引文的概率；以及所呈现材料的多样性。我们使用 G-Eval [15] 衡量各项子指标；G-Eval 是当时使用大语言模型进行评估的最先进方法。

### 2.2.2 面向网站的生成式引擎优化方法

为了提高展示度指标，内容创作者必须修改网站内容。我们提出若干不依赖特定生成式引擎的策略，并将其称为生成式引擎优化方法（GEO）。从数学上看，每一种 GEO 方法都是一个函数 $f:W\rightarrow W'_i$，其中 $W$ 是初始网络内容，$W'$ 是应用 GEO 方法后的修改内容。修改可以小到简单的文体调整，也可以扩展到以结构化形式加入新内容。

设计良好的 GEO 相当于一种黑箱优化方法：它无需了解生成式引擎的具体算法设计，就能提高网站可见度，并且能够独立于具体查询，对 $W$ 实施文本修改。

在实验中，我们使用大语言模型对网站内容应用 GEO 方法，并通过提示词要求模型对网站执行特定的文体和内容修改。具体而言，每一种 GEO 方法都会规定一组期望特征，来源内容再据此进行修改。我们提出并评估了以下方法：

1. **权威化（Authoritative）：** 调整来源内容的文本风格，使其更具说服力和权威感。
2. **添加统计数据（Statistics Addition）：** 在可能的情况下，用定量统计数据取代定性讨论。
3. **关键词堆砌（Keyword Stuffing）：** 在内容中加入更多来自查询的关键词，这也是传统 SEO 优化中常见的做法。
4. **引用来源（Cite Sources）：** 加入来自可信来源的相关出处。
5. **添加引语（Quotation Addition）：** 加入来自可信来源的相关直接引语。
6. **易于理解（Easy-to-Understand）：** 简化网站语言。
7. **流畅度优化（Fluency Optimization）：** 提高网站文本的流畅度。
8. **独特词汇（Unique Words）：** 在可能的地方加入独特词汇。
9. **专业术语（Technical Terms）：** 在可能的地方加入专业术语。

这些方法覆盖了多种通用策略，网站所有者可以快速实施，也可以不受具体网站内容限制地使用。除方法3、4、5外，其余方法无需加入额外内容，而是通过改善现有内容的呈现方式，使其更具说服力或对生成式引擎更具吸引力。方法3、4、5则可能需要添加某种形式的新内容。

为了分析各方法带来的性能增益，对于每一条输入用户查询，我们随机选择一个来源网站作为优化对象，并分别在同一来源上应用每一种 GEO 方法。有关 GEO 方法的更多细节，请参见附录B.4。

---

# 3 实验设置

## 3.1 被评估的生成式引擎

依照既有研究 [14]，我们采用两阶段生成式引擎设计。第一阶段为输入查询检索相关来源；第二阶段由大语言模型依据检索到的来源生成回答。与既有研究类似，我们不执行摘要，而是为每个来源提供完整文本。

由于 Transformer 模型存在上下文长度限制，而且计算成本会随上下文规模呈二次增长，因此，对于每条查询，我们只从 Google 搜索引擎中获取排名前5的来源。该设置与既有研究的工作流程以及 You.com、Perplexity.ai 等商业生成式引擎的一般设计高度相似。

随后，我们使用 gpt-3.5-turbo 模型 [20]，按照既有研究 [14] 所采用的同一提示词生成答案。为了减少统计偏差，我们将温度设为 0.7，并为每条查询采样5个不同回答。

此外，在第6节及附录C.1中，我们还会在商业化部署的生成式引擎 Perplexity.ai 上评估同一组 GEO 方法，以检验所提出方法的可泛化性。

## 3.2 基准：GEO-bench

目前没有公开可用、专门包含生成式引擎相关查询的数据集。因此，我们整理了 **GEO-bench**：它包含来自多个来源、经重新利用以适配生成式引擎的 10,000 条查询，同时也包含合成生成的查询。

该基准中的查询来自九个不同来源，并进一步按照目标领域、难度、查询意图及其他维度进行分类。

### 数据集

**1. MS MARCO；2. ORCAS-I；3. Natural Questions [13, 1, 6]。** 这些数据集包含来自 Bing 和 Google 搜索引擎的真实匿名用户查询。三者共同构成搜索引擎研究中常用的一组数据集。

然而，生成式引擎还会面对难度更高、更具体的查询；这些查询的目的并非简单地搜索答案，而是要求系统综合多个来源形成回答。为此，我们重新利用了另外若干公开数据集：

**4. AllSouls。** 该数据集包含牛津大学万灵学院的论文题。要回答这些查询，生成式引擎必须进行适当推理，并聚合多个来源的信息。

**5. LIMA [25]。** 该数据集包含高难度问题，要求生成式引擎不仅聚合信息，还要进行适当推理才能作答，例如写一首短诗或编写 Python 代码。

**6. Davinci-Debate [14]。** 该数据集包含为测试生成式引擎而生成的辩论题。

**7. Perplexity.ai Discover。** 这些查询取自 Perplexity.ai 的 Discover 栏目，该栏目会持续更新平台上的热门查询。<sup>2</sup>

**8. ELI5。** 该数据集包含 Reddit 的 ELI5 社区中的问题；用户会提出复杂问题，并期待得到简单、通俗的回答。<sup>3</sup>

**9. GPT-4 生成的查询。** 为提高查询分布的多样性，我们提示 GPT-4 [21] 生成不同领域（如科学、历史）、不同查询意图（如导航型、交易型）、不同难度和不同回答范围（如开放式、事实型）的查询。

<sup>2</sup> https://www.perplexity.ai/discover  
<sup>3</sup> https://huggingface.co/datasets/eli5_category

GEO-bench 共包含 10,000 条查询，按 8,000／1,000／1,000 划分为训练集、验证集和测试集。我们保留了真实世界的查询分布：80% 为信息型查询，交易型和导航型查询各占 10%。对于每条查询，我们还加入了 Google 搜索引擎前5个搜索结果经清洗后的文本内容。

### 标签

网站内容优化往往需要根据任务领域作出有针对性的修改。此外，GEO 用户可能只需针对一部分查询确定适当的方法，而这一选择需要综合考虑领域、用户意图和查询性质等多个因素。为此，我们从七类标签中为每条查询进行标注。标注由 GPT-4 完成，并由人工在测试集上核验其高召回率与高精确率。

总体而言，GEO-bench 包含艺术、健康、游戏等25个不同领域的查询；查询难度从简单到多层面不等；包含信息型、交易型等9种不同查询类型；并涵盖7种不同分类维度。

凭借专门设计的高度多样性、较大的规模以及真实世界属性，GEO-bench 构成了一个综合性的生成式引擎评估基准，也为本文及未来研究在多种用途下评估生成式引擎提供了标准测试平台。有关 GEO-bench 的更多细节见附录B.2。

### 表1：GEO 方法在 GEO-bench 上的绝对展示度指标

下表使用两类指标及其子指标衡量性能。与基线相比，SEO 中传统使用的关键词堆砌等简单方法表现不佳；而添加统计数据、添加引语等方法，在所有指标上均表现出明显提升。最佳方法在“位置调整词数”和“主观展示度”上分别比基线提高 41% 和 28%。为便于阅读，主观展示度得分相对于位置调整词数进行了归一化，因此两者的基线得分相近。

| 方法 | 词数 | 位置 | 位置调整词数·总体 | 相关性 | 影响力 | 独特性 | 多样性 | 后续点击／追问 | 主观位置 | 主观数量 | 主观展示度·平均 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **未实施 GEO** ||||||||||||
| 无优化 | 19.5 | 19.3 | 19.3 | 19.3 | 19.3 | 19.3 | 19.3 | 19.3 | 19.3 | 19.3 | 19.3 |
| **表现不佳的 GEO 方法** ||||||||||||
| 关键词堆砌 | 17.8 | 17.7 | 17.7 | 19.8 | 19.1 | 20.5 | 20.4 | 20.3 | 20.5 | 20.4 | 20.2 |
| 独特词汇 | 20.7 | 20.5 | 20.5 | 20.5 | 20.1 | 19.9 | 20.4 | 20.2 | 20.7 | 20.2 | 20.4 |
| **表现优异的 GEO 方法** ||||||||||||
| 易于理解 | 22.2 | 22.4 | 22.0 | 20.2 | 21.0 | 20.0 | 20.1 | 20.1 | 20.9 | 19.9 | 20.5 |
| 权威化 | 21.8 | 21.3 | 21.3 | 22.3 | 22.1 | 22.4 | 23.1 | 22.2 | 23.1 | 22.7 | 22.9 |
| 专业术语 | 23.1 | 22.7 | 22.7 | 20.9 | 21.7 | 20.5 | 21.2 | 20.8 | 21.9 | 20.8 | 21.4 |
| 流畅度优化 | 25.1 | 24.6 | 24.7 | 21.1 | 22.9 | 20.4 | 21.6 | 21.0 | 22.4 | 21.1 | 21.9 |
| 引用来源 | 24.9 | 24.5 | 24.6 | 21.4 | 22.5 | 21.0 | 21.6 | 21.2 | 22.2 | 20.7 | 21.9 |
| 添加引语 | 27.8 | 27.3 | **27.2** | 23.8 | 25.4 | 23.9 | 24.4 | 22.9 | 24.9 | 23.2 | **24.7** |
| 添加统计数据 | 25.9 | 25.4 | 25.2 | 22.5 | 24.5 | 23.0 | 23.3 | 21.6 | 24.2 | 23.0 | 23.7 |

## 3.3 GEO 方法

我们评估了第2.2.2节所述的9种 GEO 方法，并将其与基线进行比较。基线衡量的是未经修改的网站来源的展示度指标。所有方法都在 GEO-bench 的完整测试集上进行评估。为了降低结果方差，我们还使用5个不同的随机种子重复实验，并报告其平均值。

## 3.4 评估指标

我们使用第2.2.1节所定义的展示度指标，具体包括两类：

1. **位置调整词数（Position-Adjusted Word Count）。** 该指标结合了词数与位置计数。为了分析各组成部分的单独作用，我们也分别报告这两个子指标的得分。
2. **主观展示度（Subjective Impression）。** 该主观指标涵盖七个不同方面：① 被引句子与用户查询的相关性；② 引文影响力，即生成回答在多大程度上依赖该引文；③ 引文所呈现材料的独特性；④ 主观位置，即从用户视角衡量来源所处位置的显著程度；⑤ 主观数量，即用户阅读引文时主观感知到的、来自该引文的内容量；⑥ 用户点击该引文的可能性；⑦ 所呈现材料的多样性。

这些子指标覆盖多个不同方面，内容创作者可以据此有针对性地改善其中一个或多个方面。我们按照与 G-Eval [15] 类似的方法，使用 GPT-3.5 评估每一项子指标。在 G-Eval 中，研究者向语言模型提供基于表单的评估模板，以及生成式引擎生成且带有引文的回答；模型再为每条引文输出一个分数，该分数通过多次采样计算得到。

然而，由于 G-Eval 得分的校准较差，为实现公平且有意义的比较，我们对其进行归一化，使其均值和方差与位置调整词数相同。所使用的具体模板见附录B.3。

此外，所有展示度指标都会乘以一个常数因子进行归一化，使一条回答中所有引文的展示度之和等于1。在分析中，我们通过计算展示度的相对提升来比较不同方法。设初始回答 $r$ 由来源 $S_i\in\{s_1,\ldots,s_m\}$ 生成，修改后的回答为 $r'$，则每个来源 $s_i$ 的展示度相对提升定义为：

$$
Improvement_{s_i}=\frac{Imp_{s_i}(r')-Imp_{s_i}(r)}{Imp_{s_i}(r)}\times100 \tag{4}
$$

修改后的回答 $r'$ 由以下方式产生：对来源之一 $s_i$ 应用正在评估的 GEO 方法。待优化来源 $s_i$ 随机选取；但对于某一特定查询，在所有 GEO 方法下都保持不变。

---

# 4 结果

我们评估了多种 GEO 方法。这些方法旨在优化网站内容，使其在生成式引擎回答中获得更高可见度；比较基线则是不进行任何优化。评估使用 GEO-bench，其中包含来自多个领域和多种设置的多样化用户查询。

性能通过两项指标衡量：位置调整词数和主观展示度。前者同时考虑生成式引擎回答中的词数和引文位置；后者综合多个主观因素，计算整体展示度得分。

表1详细列出了不同方法在多项指标上的绝对展示度。结果显示，在 GEO-bench 上，我们的 GEO 方法在所有指标上都持续优于基线。这说明，尽管查询具有多样性，这些方法仍然能够产生显著提升，对不同查询表现出较强稳健性。

具体而言，表现最好的方法——引用来源、添加引语和添加统计数据——在位置调整词数指标上相对提高了 30%–40%，在主观展示度指标上相对提高了 15%–30%。

这些方法分别在网站内容中加入相关统计数据、可信引语以及可靠来源的出处。它们只需要对原有内容进行很少修改，却能显著提高网站在生成式引擎回答中的可见度，同时提升内容的可信度和信息丰富度。

### 表2：不同搜索排名来源使用 GEO 后的可见度变化

| 方法 | 排名第1 | 排名第2 | 排名第3 | 排名第4 | 排名第5 |
|---|---:|---:|---:|---:|---:|
| 权威化 | -6.0% | 4.1% | -0.6% | 12.6% | 6.1% |
| 流畅度优化 | -2.0% | 5.2% | 3.6% | -4.4% | 2.2% |
| 引用来源 | -30.3% | 2.5% | 20.4% | 15.5% | 115.1% |
| 添加引语 | -22.9% | -7.0% | 3.5% | 25.1% | 99.7% |
| 添加统计数据 | -20.6% | -3.9% | 8.1% | 10.0% | 97.9% |

**表2说明：** 表中数值为可见度相对提升。GEO 对搜索引擎中排名较低的网站尤其有帮助。

### 表3：各 GEO 方法表现最好的类别

| 方法 | 第1类别 | 第2类别 | 第3类别 |
|---|---|---|---|
| 权威化 | 辩论 | 历史 | 科学 |
| 流畅度优化 | 商业 | 科学 | 健康 |
| 引用来源 | 陈述 | 事实 | 法律与政府 |
| 添加引语 | 人与社会 | 解释 | 历史 |
| 添加统计数据 | 法律与政府 | 辩论 | 观点 |

**表3说明：** 上表列出每一种 GEO 方法表现最好的类别。网站所有者可以根据自己的目标领域选择相应的 GEO 策略。

值得注意的是，改善来源文本流畅度和可读性的文体调整——即流畅度优化和易于理解——也使可见度显著提高了 15%–30%。这表明，生成式引擎看重的不只是内容本身，也看重信息的呈现方式。

此外，生成式引擎所使用的生成模型通常被设计为遵循指令，因此人们或许会预期：网站内容若采用更有说服力、更具权威感的语气，便能提高可见度。然而，我们没有发现显著提升，这表明生成式引擎对这类变化已经具备一定稳健性。因此，网站所有者更应把重点放在改善内容呈现和提高可信度上。

最后，我们评估了关键词堆砌，即在网站内容中加入更多相关关键词。尽管这一技术广泛用于搜索引擎优化，但我们发现，它对生成式引擎回答几乎没有改善，甚至完全没有改善。这说明，网站所有者必须重新思考面向生成式引擎的优化策略：在传统搜索引擎中有效的技术，不一定能在这一新范式中取得成功。

---

# 5 分析

## 5.1 领域特定的生成式引擎优化

第4节呈现了 GEO 在整个 GEO-bench 基准上的提升。但在真实世界的 SEO 场景中，网站通常会采用领域特定优化。鉴于 GEO-bench 为每条查询都提供了分类标签，我们进一步分析各种 GEO 方法在不同类别上的表现。

表3详细列出了 GEO 方法最有效的类别。对结果进行仔细分析，可以得到若干有趣观察。例如，“权威化”能显著改善辩论型问题以及历史领域查询的表现。这与我们的直觉一致：更具说服力的写作方式，在辩论语境中很可能更有价值。

类似地，“引用来源”对事实型问题尤其有益。这可能是因为引文可以为所陈述的事实提供核验来源，从而提高回答的可信度。

不同 GEO 方法的有效性会因领域而异。例如，表3第5行显示，“法律与政府”等领域以及“观点”类问题，会从网站内容中添加相关统计数据这一做法中显著获益。这表明，在某些特定语境中，以数据为依据的证据可以提高网站可见度。

“添加引语”在“人与社会”“解释”和“历史”领域最有效。这可能是因为，这些领域往往涉及个人叙事或历史事件，直接引语能够为内容增添真实性与深度。

总体而言，我们的分析表明，网站所有者若想获得更高可见度，应当针对网站所属领域进行有针对性的调整。

## 5.2 多个网站同时优化

随着生成式引擎不断发展，GEO 方法很可能会被广泛采用，届时所有来源内容都可能经过 GEO 优化。为了理解这一情形的影响，我们同时优化全部来源内容，并对 GEO 方法进行评估。结果见表2。

一项关键观察是：GEO 对网站的影响会因网站在搜索引擎结果页（Search Engine Results Pages，SERP）中的排名而异。尤其值得注意的是，通常难以获得可见度的低排名网站，从 GEO 中获得的收益显著高于高排名网站。

这是因为，传统搜索引擎依赖反向链接数量、域名影响力等多个因素，而小型创作者很难具备这些条件。生成式引擎则使用以网站内容为条件的生成模型，因此，建立反向链接等因素不应再使小型创作者处于不利地位。表2所列可见度相对提升印证了这一点。例如，“引用来源”使 SERP 排名第5的网站可见度大幅提高 115.1%；与此同时，排名第1的网站平均可见度下降了 30.3%。

这一发现凸显了 GEO 作为数字空间民主化工具的潜力。许多低排名网站由小型内容创作者或独立企业创建；在传统搜索引擎结果中，他们很难与占据头部排名的大型公司竞争。生成式引擎的出现，起初可能看起来对这些小型主体不利。

然而，应用 GEO 方法为这些内容创作者提供了一个显著提高其在生成式引擎回答中可见度的机会。借助 GEO 改善内容，他们可以触达更广泛的受众，从而拉平竞争环境，更有效地与大型公司竞争。

## 5.3 GEO 策略组合

虽然单独的 GEO 策略已在不同领域展现出显著提升，但在实践中，网站所有者很可能会组合使用多种策略。为了研究组合 GEO 策略所产生的性能提升，我们考察了表现最好的4种 GEO 方法两两组合的所有情况：引用来源、流畅度优化、添加统计数据和添加引语。

*【图4：GEO 策略组合的相对提升热力图（原论文图）——原图请见 arXiv:2311.09735 原文；图内文字中文对照见下方】*

**图4：** 组合使用 GEO 策略所产生的相对提升。将流畅度优化与添加统计数据结合，可获得最高性能。最右侧一列显示，流畅度优化与其他策略搭配时最有益。

**图4数据中文对照：**

| 行／列策略 | 流畅度优化 | 添加统计数据 | 引用来源 | 添加引语 | 平均提升 |
|---|---:|---:|---:|---:|---:|
| 流畅度优化 | 22.4% | 35.8% | 34.4% | 33.0% | 31.4% |
| 添加统计数据 | 35.8% | 27.0% | 30.3% | 35.4% | **32.1%** |
| 引用来源 | 34.4% | 30.3% | 19.1% | 20.1% | 26.0% |
| 添加引语 | 33.0% | 35.4% | 20.1% | 30.3% | 29.7% |

图4展示了组合不同 GEO 策略后，在位置调整词数可见度指标上取得的相对提升。分析表明，组合 GEO 方法可以进一步改善性能；最佳组合——流畅度优化加添加统计数据——比任何一种单独 GEO 策略高出 5.5 个百分点以上。<sup>4</sup>

此外，虽然“引用来源”单独使用时效果相对较弱——比“添加引语”低8个百分点——但它与其他方法结合时能显著提升性能，平均提升达到 31.4%。这些发现凸显了研究 GEO 方法组合的重要性，因为真实世界的内容创作者很可能会组合使用这些方法。

<sup>4</sup> 受成本限制，该分析只在测试集的200个样本子集上进行，因此这里的数值与表1不同。

## 5.4 定性分析

表4给出了 GEO 方法的定性分析，其中包含若干代表性示例：GEO 方法只对来源作少量修改，便提高了来源可见度。每种方法都通过适当增删文字来优化一个来源。

第一个示例表明，只需在文本中加入一项陈述的来源，就能显著提高该来源在最终回答中的可见度，而内容创作者几乎不需付出额外努力。第二个示例表明，在适当位置加入相关统计数据，可确保来源在最终生成式引擎回答中的可见度得到提高。第三个示例则说明，仅仅强调文本中的部分内容，并采用更具说服力的文风，也能带来可观的可见度提升。

### 表4：GEO 优化来源网站的代表性示例

表中**粗体**表示新增内容，~~删除线~~表示删除内容。

| 方法 | GEO 优化内容 | 相对提升 |
|---|---|---:|
| 引用来源 | **查询：瑞士巧克力的秘诀是什么？** 瑞士人年均巧克力消费量为11至12公斤，位居全球最爱吃巧克力的人群之列。**（根据国际巧克力消费研究小组开展的一项调查 [1]）** | 132.4% |
| 添加统计数据 | **查询：机器人是否应当取代劳动力中的人类？** 来源：不是这里，也不是现在——至少直到最近都不是。最大的区别在于，机器人的到来不是为了摧毁我们的生活，而是为了扰乱我们的工作；**过去十年，机器人参与度惊人地增长了70%。** | 65.5% |
| 权威化 | **查询：杰克逊维尔美洲虎队是否曾打进超级碗？** 来源：**必须指出，**美洲虎队从未~~出现~~**亮相**于超级碗。**不过，**他们曾~~获得4个分区冠军头衔。~~**取得一项令人印象深刻的成就：拿下4个分区冠军；这证明了他们的实力与决心。** | 89.1% |

**表4说明：** 这些示例展示 GEO 方法如何优化来源网站。新增内容在原论文中以绿色标示，删除内容以红色标示。即使不加入任何实质性新信息，GEO 方法也能显著提高来源内容的可见度。

---

# 6 真实世界中的 GEO：在已部署生成式引擎上的实验

### 表5：以 Perplexity.ai 为生成式引擎时，GEO 方法在 GEO-bench 上的绝对展示度

| 方法 | 位置调整词数 | 主观展示度 |
|---|---:|---:|
| 无优化 | 24.1 | 24.7 |
| 关键词堆砌 | 21.9 | 28.1 |
| 添加引语 | **29.1** | 32.1 |
| 添加统计数据 | 26.2 | **33.9** |

**表5说明：** 关键词堆砌等 SEO 方法表现不佳；我们提出的 GEO 方法则可以泛化到多个生成式引擎，并显著提高内容可见度。

为了进一步验证所提出 GEO 方法的有效性，我们在 Perplexity.ai 上对其进行评估。Perplexity.ai 是一个拥有庞大用户群、已经实际部署的生成式引擎。结果见表5。

与我们构建的生成式引擎相似，“添加引语”在位置调整词数指标上表现最佳，比基线提高 22%。在我们构建的生成式引擎中表现良好的“引用来源”和“添加统计数据”，在两项指标上分别实现最高 9% 和 37% 的提升。

我们先前的其他观察也得到进一步印证。例如，关键词堆砌等传统 SEO 方法缺乏有效性：它的表现比基线低 10%。

这些结果之所以重要，有三点原因：

1. 它们凸显了开发不同 GEO 方法、使内容创作者受益的重要性；
2. 它们表明，我们提出的 GEO 方法可以泛化到不同生成式引擎；
3. 它们证明，内容创作者可以直接使用这些易于实施的 GEO 方法，因此本研究具有很高的真实世界影响力。

更多细节见附录C.1。

---

# 7 相关工作

**基于证据的答案生成。** 既有研究已经采用多种技术生成有来源支持的答案。Nakano 等人 [19] 训练 GPT-3 在网络环境中进行浏览，从而生成由来源支撑的答案。类似地，其他方法 [17, 23, 24] 会通过搜索引擎获取来源，再据此生成答案。我们的工作统一了这些方法，并提供一个通用基准，以便未来进一步改进这些系统。

Kumar 和 Lakkaraju 在一份近期工作论文 [11] 中表明，策略性文本序列可以操纵大语言模型的推荐结果，从而提高产品在生成式引擎中的可见度。他们的方法着眼于通过对抗性文本提高产品可见度；与之不同，我们的方法提出非对抗性策略，用于优化任意网站内容，使其在生成式引擎搜索结果中获得更高可见度。

**检索增强语言模型。** 近期多项研究通过从知识库获取相关来源来完成任务，从而解决语言模型记忆有限的问题 [3, 18, 9]。然而，生成式引擎不仅需要生成答案，还必须在整个答案中提供出处标注。

此外，生成式引擎的输入和输出都不限于单一文本模态。生成式引擎框架也不只负责获取相关来源，还包含查询改写、来源选择，以及决定何时、以何种方式执行这些任务等多个环节。

**搜索引擎优化。** 过去近25年间，大量研究致力于为搜索引擎优化网络内容 [2, 12, 22]。这些方法可以分为两类：站内 SEO，通过改善内容与用户体验进行优化；站外 SEO，通过建立链接提高网站权威度。

相比之下，GEO 面对的是一个更复杂的环境，其中包含多模态与对话式设置。GEO 的优化对象是生成模型，而生成模型并不局限于简单的关键词匹配，因此，传统 SEO 策略不适用于生成式引擎场景；这正凸显了 GEO 的必要性。

---

# 8 结论

在本研究中，我们对由生成模型增强的搜索引擎作出形式化定义，并将其称为“生成式引擎”。我们提出生成式引擎优化（GEO），帮助内容创作者在生成式引擎环境下优化自己的内容。

我们为生成式引擎定义了展示度指标，并提出、发布了 GEO-bench。该基准涵盖来自多个领域和多种设置的多样化用户查询，以及回答这些查询所需的相关来源。

我们提出多种面向生成式引擎的内容优化方法，并证明这些方法能使来源在生成式引擎回答中的可见度提高多达 40%。其中一项重要发现是，加入引文、来自相关来源的直接引语以及统计数据，可以显著提高来源可见度。

此外，我们发现 GEO 方法的有效性取决于查询所属领域，多种 GEO 策略组合使用也具有潜力。我们还在一个拥有数百万活跃用户、已经商业化部署的生成式引擎上取得了有前景的结果，展示了本研究的真实世界影响力。

总而言之，我们的工作首次对重要且正当其时的 GEO 范式作出形式化定义，并发布算法与基础设施——包括基准、数据集和指标——以推动研究社区在生成式引擎领域快速进展。这是理解生成式引擎如何影响数字空间，以及 GEO 在这一搜索引擎新范式中发挥何种作用的第一步。

---

# 9 局限性

尽管我们在两个生成式引擎上严格测试了所提出的方法——其中一个可公开使用——但随着生成式引擎不断演进，这些方法可能也需要随时间调整，就像 SEO 的演进历程一样。

此外，尽管我们努力确保 GEO-bench 中的查询与真实世界查询高度相似，但查询的性质可能随时间变化，因此基准需要持续更新。

由于搜索引擎算法具有黑箱性质，我们没有评估 GEO 方法会如何影响搜索排名。不过需要指出，GEO 方法所作的是有针对性的文本内容修改，与 SEO 方法有一定相似之处；它们不会影响域名、反向链接等其他元数据，因此不太可能影响搜索引擎排名。

此外，随着大语言模型支持更长上下文的经济成本下降，未来的生成模型预计能够读取更多来源，从而减弱搜索排名的影响。

最后，虽然我们对 GEO-bench 中的每一条查询都进行了标签标注和人工检查，但由于主观解释不同或标注错误，数据中仍可能存在不一致。

---

# 10 致谢

本研究所依据的工作得到美国国家科学基金会第2107048号资助。本文所表达的任何观点、研究发现、结论或建议均属于作者本人，并不必然代表美国国家科学基金会的立场。

---

# 参考文献

> 参考文献的作者、题名、期刊／会议、年份及链接按英文原文保留，以确保检索与引用准确。

[1] Daria Alexander, Wojciech Kusa, and Arjen P. de Vries. 2022. ORCAS-I: Queries Annotated with Intent using Weak Supervision. *Proceedings of the 45th International ACM SIGIR Conference on Research and Development in Information Retrieval* (2022). <https://api.semanticscholar.org/CorpusID:248495926>

[2] Prashant Ankalkoti. 2017. Survey on Search Engine Optimization Tools & Techniques. *Imperial journal of interdisciplinary research* 3 (2017). <https://api.semanticscholar.org/CorpusID:116487363>

[3] Akari Asai, Xinyan Velocity Yu, Jungo Kasai, and Hannaneh Hajishirzi. 2021. One Question Answering Model for Many Languages with Cross-lingual Dense Passage Retrieval. In *Neural Information Processing Systems*. <https://api.semanticscholar.org/CorpusID:236428949>

[4] Sergey Brin and Lawrence Page. 1998. The Anatomy of a Large-Scale Hypertextual Web Search Engine. *Comput. Networks* 30 (1998), 107–117. <https://api.semanticscholar.org/CorpusID:7587743>

[5] Tom Brown, Benjamin Mann, Nick Ryder, Melanie Subbiah, Jared D Kaplan, Prafulla Dhariwal, Arvind Neelakantan, Pranav Shyam, Girish Sastry, Amanda Askell, Sandhini Agarwal, Ariel Herbert-Voss, Gretchen Krueger, Tom Henighan, Rewon Child, Aditya Ramesh, Daniel Ziegler, Jeffrey Wu, Clemens Winter, Chris Hesse, Mark Chen, Eric Sigler, Mateusz Litwin, Scott Gray, Benjamin Chess, Jack Clark, Christopher Berner, Sam McCandlish, Alec Radford, Ilya Sutskever, and Dario Amodei. 2020. Language Models are Few-Shot Learners. In *Advances in Neural Information Processing Systems*, H. Larochelle, M. Ranzato, R. Hadsell, M.F. Balcan, and H. Lin (Eds.), Vol. 33. Curran Associates, Inc., 1877–1901. <https://proceedings.neurips.cc/paper_files/paper/2020/file/1457c0d6bfcb4967418bfb8ac142f64a-Paper.pdf>

[6] Nick Craswell, Bhaskar Mitra, Emine Yilmaz, Daniel Fernando Campos, and Jimmy J. Lin. 2021. MS MARCO: Benchmarking Ranking Models in the Large-Data Regime. *Proceedings of the 44th International ACM SIGIR Conference on Research and Development in Information Retrieval* (2021). <https://api.semanticscholar.org/CorpusID:234336491>

[7] Brian Dean. 2023. We Analyzed 4 Million Google Search Results. Here’s What We Learned About Organic Click Through Rate. <https://backlinko.com/google-ctr-stats> Accessed: 2024-06-08.

[8] Danny Goodwin. 2011. Top Google Result Gets 36.4% of Clicks \[Study\]. <https://www.searchenginewatch.com/2011/04/21/top-google-result-gets-36-4-of-clicks-study/>

[9] Kelvin Guu, Kenton Lee, Zora Tung, Panupong Pasupat, and Ming-Wei Chang. 2020. REALM: Retrieval-Augmented Language Model Pre-Training. *ArXiv* abs/2002.08909 (2020). <https://api.semanticscholar.org/CorpusID:211204736>

[10] Ziwei Ji, Nayeon Lee, Rita Frieske, Tiezheng Yu, Dan Su, Yan Xu, Etsuko Ishii, Ye Jin Bang, Andrea Madotto, and Pascale Fung. 2023. Survey of hallucination in natural language generation. *Comput. Surveys* 55, 12 (2023), 1–38.

[11] Aounon Kumar and Himabindu Lakkaraju. 2024. Manipulating Large Language Models to Increase Product Visibility. arXiv:2404.07981 \[cs.IR\]

[12] R.Anil Kumar, Zaiduddin Shaik, and Mohammed Furqan. 2019. A Survey on Search Engine Optimization Techniques. *International Journal of P2P Network Trends and Technology* (2019). <https://doi.org/10.14445/22492615/IJPTT-V9I1P402>

[13] Tom Kwiatkowski, Jennimaria Palomaki, Olivia Redfield, Michael Collins, Ankur P. Parikh, Chris Alberti, Danielle Epstein, Illia Polosukhin, Jacob Devlin, Kenton Lee, Kristina Toutanova, Llion Jones, Matthew Kelcey, Ming-Wei Chang, Andrew M. Dai, Jakob Uszkoreit, Quoc V. Le, and Slav Petrov. 2019. Natural Questions: A Benchmark for Question Answering Research. *Transactions of the Association for Computational Linguistics* 7 (2019), 453–466. <https://api.semanticscholar.org/CorpusID:86611921>

[14] Nelson F. Liu, Tianyi Zhang, and Percy Liang. 2023b. Evaluating Verifiability in Generative Search Engines. *ArXiv* abs/2304.09848 (2023). <https://api.semanticscholar.org/CorpusID:258212854>

[15] Yang Liu, Dan Iter, Yichong Xu, Shuo Wang, Ruochen Xu, and Chenguang Zhu. 2023a. G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment. *ArXiv* abs/2303.16634 (2023). <https://api.semanticscholar.org/CorpusID:257804696>

[16] G. D. Maayan. 2023. How Google SGE will impact your traffic – and 3 SGE recovery case studies. *Search Engine Land* (5 Sep 2023). <https://searchengineland.com/how-google-sge-will-impact-your-traffic-and-3-sge-recovery-case-studies-431430>

[17] Jacob Menick, Maja Trebacz, Vladimir Mikulik, John Aslanides, Francis Song, Martin Chadwick, Mia Glaese, Susannah Young, Lucy Campbell-Gillingham, Geoffrey Irving, and Nathan McAleese. 2022. Teaching language models to support answers with verified quotes. *ArXiv* abs/2203.11147 (2022). <https://api.semanticscholar.org/CorpusID:247594830>

[18] Grégoire Mialon, Roberto Dessì, Maria Lomeli, Christoforos Nalmpantis, Ramakanth Pasunuru, Roberta Raileanu, Baptiste Rozière, Timo Schick, Jane Dwivedi-Yu, Asli Celikyilmaz, Edouard Grave, Yann LeCun, and Thomas Scialom. 2023. Augmented Language Models: a Survey. *ArXiv* abs/2302.07842 (2023). <https://api.semanticscholar.org/CorpusID:256868474>

[19] Reiichiro Nakano, Jacob Hilton, S. Arun Balaji, Jeff Wu, Ouyang Long, Christina Kim, Christopher Hesse, Shantanu Jain, Vineet Kosaraju, William Saunders, Xu Jiang, Karl Cobbe, Tyna Eloundou, Gretchen Krueger, Kevin Button, Matthew Knight, Benjamin Chess, and John Schulman. 2021. WebGPT: Browser-assisted question-answering with human feedback. *ArXiv* abs/2112.09332 (2021). [Semantic Scholar CorpusID:245329531](https://api.semanticscholar.org/CorpusID:245329531)

[20] OpenAI. 2022. Introducing ChatGPT. <https://openai.com/index/chatgpt/>

[21] OpenAI, Josh Achiam, Steven Adler, Sandhini Agarwal, Lama Ahmad, Ilge Akkaya, Florencia Leoni Aleman, Diogo Almeida, Janko Altenschmidt, Sam Altman, Shyamal Anadkat, Red Avila, Igor Babuschkin, Suchir Balaji, Valerie Balcom, Paul Baltescu, Haiming Bao, Mohammad Bavarian, Jeff Belgum, Irwan Bello, Jake Berdine, Gabriel Bernadett-Shapiro, Christopher Berner, Lenny Bogdonoff, Oleg Boiko, Madelaine Boyd, Anna-Luisa Brakman, Greg Brockman, Tim Brooks, Miles Brundage, Kevin Button, Trevor Cai, Rosie Campbell, Andrew Cann, Brittany Carey, Chelsea Carlson, Rory Carmichael, Brooke Chan, Che Chang, Fotis Chantzis, Derek Chen, Sully Chen, Ruby Chen, Jason Chen, Mark Chen, Ben Chess, Chester Cho, Casey Chu, Hyung Won Chung, Dave Cummings, Jeremiah Currier, Yunxing Dai, Cory Decareaux, Thomas Degry, Noah Deutsch, Damien Deville, Arka Dhar, David Dohan, Steve Dowling, Sheila Dunning, Adrien Ecoffet, Atty Eleti, Tyna Eloundou, David Farhi, Liam Fedus, Niko Felix, Simón Posada Fishman, Juston Forte, Isabella Fulford, Leo Gao, Elie Georges, Christian Gibson, Vik Goel, Tarun Gogineni, Gabriel Goh, Rapha Gontijo-Lopes, Jonathan Gordon, Morgan Grafstein, Scott Gray, Ryan Greene, Joshua Gross, Shixiang Shane Gu, Yufei Guo, Chris Hallacy, Jesse Han, Jeff Harris, Yuchen He, Mike Heaton, Johannes Heidecke, Chris Hesse, Alan Hickey, Wade Hickey, Peter Hoeschele, Brandon Houghton, Kenny Hsu, Shengli Hu, Xin Hu, Joost Huizinga, Shantanu Jain, Shawn Jain, Joanne Jang, Angela Jiang, Roger Jiang, Haozhun Jin, Denny Jin, Shino Jomoto, Billie Jonn, Heewoo Jun, Tomer Kaftan, Łukasz Kaiser, Ali Kamali, Ingmar Kanitscheider, Nitish Shirish Keskar, Tabarak Khan, Logan Kilpatrick, Jong Wook Kim, Christina Kim, Yongjik Kim, Jan Hendrik Kirchner, Jamie Kiros, Matt Knight, Daniel Kokotajlo, Łukasz Kondraciuk, Andrew Kondrich, Aris Konstantinidis, Kyle Kosic, Gretchen Krueger, Vishal Kuo, Michael Lampe, Ikai Lan, Teddy Lee, Jan Leike, Jade Leung, Daniel Levy, Chak Ming Li, Rachel Lim, Molly Lin, Stephanie Lin, Mateusz Litwin, Theresa Lopez, Ryan Lowe, Patricia Lue, Anna Makanju, Kim Malfacini, Sam Manning, Todor Markov, Yaniv Markovski, Bianca Martin, Katie Mayer, Andrew Mayne, Bob McGrew, Scott Mayer McKinney, Christine McLeavey, Paul McMillan, Jake McNeil, David Medina, Aalok Mehta, Jacob Menick, Luke Metz, Andrey Mishchenko, Pamela Mishkin, Vinnie Monaco, Evan Morikawa, Daniel Mossing, Tong Mu, Mira Murati, Oleg Murk, David Mély, Ashvin Nair, Reiichiro Nakano, Rajeev Nayak, Arvind Neelakantan, Richard Ngo, Hyeonwoo Noh, Long Ouyang, Cullen O’Keefe, Jakub Pachocki, Alex Paino, Joe Palermo, Ashley Pantuliano, Giambattista Parascandolo, Joel Parish, Emy Parparita, Alex Passos, Mikhail Pavlov, Andrew Peng, Adam Perelman, Filipe de Avila Belbute Peres, Michael Petrov, Henrique Ponde de Oliveira Pinto, Michael, Pokorny, Michelle Pokrass, Vitchyr H. Pong, Tolly Powell, Alethea Power, Boris Power, Elizabeth Proehl, Raul Puri, Alec Radford, Jack Rae, Aditya Ramesh, Cameron Raymond, Francis Real, Kendra Rimbach, Carl Ross, Bob Rotsted, Henri Roussez, Nick Ryder, Mario Saltarelli, Ted Sanders, Shibani Santurkar, Girish Sastry, Heather Schmidt, David Schnurr, John Schulman, Daniel Selsam, Kyla Sheppard, Toki Sherbakov, Jessica Shieh, Sarah Shoker, Pranav Shyam, Szymon Sidor, Eric Sigler, Maddie Simens, Jordan Sitkin, Katarina Slama, Ian Sohl, Benjamin Sokolowsky, Yang Song, Natalie Staudacher, Felipe Petroski Such, Natalie Summers, Ilya Sutskever, Jie Tang, Nikolas Tezak, Madeleine B. Thompson, Phil Tillet, Amin Tootoonchian, Elizabeth Tseng, Preston Tuggle, Nick Turley, Jerry Tworek, Juan Felipe Cerón Uribe, Andrea Vallone, Arun Vijayvergiya, Chelsea Voss, Carroll Wainwright, Justin Jay Wang, Alvin Wang, Ben Wang, Jonathan Ward, Jason Wei, CJ Weinmann, Akila Welihinda, Peter Welinder, Jiayi Weng, Lilian Weng, Matt Wiethoff, Dave Willner, Clemens Winter, Samuel Wolrich, Hannah Wong, Lauren Workman, Sherwin Wu, Jeff Wu, Michael Wu, Kai Xiao, Tao Xu, Sarah Yoo, Kevin Yu, Qiming Yuan, Wojciech Zaremba, Rowan Zellers, Chong Zhang, Marvin Zhang, Shengjia Zhao, Tianhao Zheng, Juntang Zhuang, William Zhuk, and Barret Zoph. 2024. GPT-4 Technical Report. arXiv:2303.08774 \[cs.CL\]

[22] A. Shahzad, Deden Witarsyah Jacob, Nazri M. Nawi, Hairulnizam Bin Mahdin, and Marheni Eka Saputri. 2020. The new trend for search engine optimization, tools and techniques. *Indonesian Journal of Electrical Engineering and Computer Science* 18 (2020), 1568. <https://api.semanticscholar.org/CorpusID:213123106>

[23] Kurt Shuster, Jing Xu, Mojtaba Komeili, Da Ju, Eric Michael Smith, Stephen Roller, Megan Ung, Moya Chen, Kushal Arora, Joshua Lane, Morteza Behrooz, W.K.F. Ngan, Spencer Poff, Naman Goyal, Arthur Szlam, Y-Lan Boureau, Melanie Kambadur, and Jason Weston. 2022. BlenderBot 3: a deployed conversational agent that continually learns to responsibly engage. *ArXiv* abs/2208.03188 (2022). <https://api.semanticscholar.org/CorpusID:251371589>

[24] Romal Thoppilan, Daniel De Freitas, Jamie Hall, Noam Shazeer, Apoorv Kulshreshtha, Heng-Tze Cheng, Alicia Jin, Taylor Bos, Leslie Baker, Yu Du, YaGuang Li, Hongrae Lee, Huaixiu Steven Zheng, Amin Ghafouri, Marcelo Menegali, Yanping Huang, Maxim Krikun, Dmitry Lepikhin, James Qin, Dehao Chen, Yuanzhong Xu, Zhifeng Chen, Adam Roberts, Maarten Bosma, Vincent Zhao, Yanqi Zhou, Chung-Ching Chang, Igor Krivokon, Will Rusch, Marc Pickett, Pranesh Srinivasan, Laichee Man, Kathleen Meier-Hellstern, Meredith Ringel Morris, Tulsee Doshi, Renelito Delos Santos, Toju Duke, Johnny Soraker, Ben Zevenbergen, Vinodkumar Prabhakaran, Mark Diaz, Ben Hutchinson, Kristen Olson, Alejandra Molina, Erin Hoffman-John, Josh Lee, Lora Aroyo, Ravi Rajakumar, Alena Butryna, Matthew Lamm, Viktoriya Kuzmina, Joe Fenton, Aaron Cohen, Rachel Bernstein, Ray Kurzweil, Blaise Aguera-Arcas, Claire Cui, Marian Croak, Ed Chi, and Quoc Le. 2022. LaMDA: Language Models for Dialog Applications. arXiv:2201.08239 \[cs.CL\]

[25] Chunting Zhou, Pengfei Liu, Puxin Xu, Srini Iyer, Jiao Sun, Yuning Mao, Xuezhe Ma, Avia Efrat, Ping Yu, L. Yu, Susan Zhang, Gargi Ghosh, Mike Lewis, Luke Zettlemoyer, and Omer Levy. 2023. LIMA: Less Is More for Alignment. *ArXiv* abs/2305.11206 (2023). <https://api.semanticscholar.org/CorpusID:258822910>

---

# 附录A 对话式生成式引擎

第2.1节讨论的是单轮生成式引擎：给定一条用户查询后，它输出一个回答。然而，未来生成式引擎的一项优势，是能够与用户展开主动、来回往复的对话。

对话使用户可以对自己的查询或生成式引擎的回答作出澄清，也可以提出后续问题。具体而言，在公式（1）中，输入不再是单一查询 $q_u$，而被建模为由 $(q_u^t,r^t)$ 对组成的对话历史 $H$。回答 $r^{t+1}$ 定义如下：

$$
GE:=f_{LE}(H,P_U)\rightarrow r^{t+1} \tag{5}
$$

其中，$t$ 表示对话轮次。

此外，为了让用户继续参与对话，单独的大语言模型 $L_{follow}$ 或 $L_{resp}$ 可以依据 $H$、$P_U$ 和 $r^{t+1}$ 生成建议的后续查询。这些建议查询通常以最大化用户参与概率为目标。

这不仅能通过增加用户互动使生成式引擎提供商受益，也能通过提高网站可见度使网站所有者受益。此外，这些后续查询还可以帮助用户获得更详细的信息。

---

# 附录B 实验设置

## B.1 被评估的生成式引擎

实验中使用的确切提示词见清单1。

### 清单1：生成式引擎所使用的提示词

生成式引擎以查询和5个来源为输入，输出以这些来源为依据的查询回答。

```text
请仅使用所提供的网络搜索结果摘要，为给定的用户问题写出准确而简洁的答案。
答案应当正确、优质，并由专家以无偏见的新闻写作语气撰写。
应当使用用户选择的语言，例如英语、法语、西班牙语、德语，或[原文此处缺词]。
答案应当信息充分、有趣且具有吸引力。
答案的逻辑与推理应当严谨、经得起辩护。

答案中的每一个句子之后，都必须立即跟随对搜索结果的行内引用。
被引用的搜索结果应当完整支持该句中的全部信息。
搜索结果须使用 [索引号] 的格式引用。
引用多个搜索结果时，请使用 [1][2][3]，而不要使用 [1, 2, 3]。
你可以使用多个搜索结果给出全面回答，同时避免使用无关的搜索结果。

问题：{query}

搜索结果：
{source_text}
```

## B.2 基准

GEO-bench 包含来自九个数据集的查询。清单2展示了每个数据集中的代表性查询。此外，我们会从七个不同类别中为每条查询打标签。标签由 GPT-4 模型生成，我们再通过人工核验，确认标注具有较高召回率和精确率。

不过，由于标注由自动化系统完成，标签中可能存在噪声，因此解读时应保持谨慎。各类标签的细节列于清单2之后。

### 清单2：GEO-bench 九个数据集中的代表性查询

```text
### ORCAS
- “全球化”是什么意思？
- 葡萄酒配餐清单

### AllSouls
- 开放获取期刊会成为学术出版的未来吗？
- 在英国，学习非西方哲学是否应当成为哲学学位的必修要求？

### Davinci-Debate
- 是否应向所有公民发放基本收入？
- 政府是否应当推广无神论？

### ELI5
- 我的猫玩玩具时为什么会用后腿踢它？
- 咖啡因究竟会对肌肉产生什么作用，尤其是在锻炼方面？

### GPT-4
- 生酮饮食有哪些益处？
- 文艺复兴时期对现代社会产生了哪些最深远的影响？

### LIMA
- 影响消费者行为的主要因素有哪些？
- 谋杀悬疑故事可以采用什么精彩反转？我想要有创意的构思，而不是重炒旧套路。

### MS-MARCO
- “monogamous（一夫一妻制的／单配偶的）”是什么意思？
- 儿童空腹血糖的正常范围是多少？

### Natural Questions
- “bee line（直线前往／径直而去）”这个短语源自哪里？
- 《圣经》中的“波斯王子”指什么？

### Perplexity.ai
- 如何在 LinkedIn 上获得更多关注者？
- 为什么餐后血糖会升高？
```

### 七类标签

1. **难度等级：** 查询的复杂程度，从简单到复杂。
2. **查询性质：** 查询所寻求的信息类型，例如事实、观点或比较。
3. **领域：** 查询所属类别或领域，例如艺术与娱乐、金融或科学。
4. **具体主题：** 查询所涉及的具体学科，例如物理学、经济学或计算机科学。
5. **敏感性：** 查询是否涉及敏感主题。
6. **用户意图：** 用户发起查询的目的，例如研究、购买或娱乐。
7. **回答类型：** 查询所寻求的回答格式，例如事实、观点或列表。

## B.3 评估指标

我们使用7种不同的主观展示度指标。相关提示词发布在公开代码库：https://github.com/GEO-optim/GEO 。

## B.4 GEO 方法

我们提出9种不同的生成式引擎优化方法，用于针对生成式引擎优化网站内容。所有方法都在完整的 GEO-bench 测试集上进行评估。为降低结果方差，我们使用5个不同的随机种子重复实验，并报告平均值。

## B.5 GEO 方法所用提示词

全部提示词发布在公开代码库：https://github.com/GEO-optim/GEO 。所有实验均使用 GPT-3.5 Turbo。

### 表6：五个随机种子下，GEO 方法在 GEO-bench 上的绝对展示度指标

括号内为统计偏差。

| 方法 | 词数 | 位置 | 位置调整词数·总体 | 相关性 | 影响力 | 独特性 | 多样性 | 后续点击／追问 | 主观位置 | 主观数量 | 主观展示度·平均 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **未实施 GEO** ||||||||||||
| 无优化 | 19.7 (±0.7) | 19.6 (±0.5) | 19.8 (±0.6) | 19.8 (±0.9) | 19.8 (±1.6) | 19.8 (±0.6) | 19.8 (±1.1) | 19.8 (±1.0) | 19.8 (±1.0) | 19.8 (±0.9) | 19.8 (±0.9) |
| **表现不佳的 GEO 方法** ||||||||||||
| 关键词堆砌 | 19.6 (±0.5) | 19.5 (±0.6) | 19.8 (±0.5) | 20.8 (±0.8) | 19.8 (±1.0) | 20.4 (±0.5) | 20.6 (±0.9) | 19.9 (±0.9) | 21.1 (±1.0) | 21.0 (±0.9) | 20.6 (±0.7) |
| 独特词汇 | 20.6 (±0.6) | 20.5 (±0.7) | 20.7 (±0.5) | 20.8 (±0.7) | 20.3 (±1.3) | 20.5 (±0.3) | 20.9 (±0.3) | 20.4 (±0.7) | 21.5 (±0.6) | 21.2 (±0.4) | 20.9 (±0.4) |
| **表现优异的 GEO 方法** ||||||||||||
| 易于理解 | 21.5 (±0.7) | 22.0 (±0.8) | 21.5 (±0.6) | 21.0 (±1.1) | 21.1 (±1.8) | 21.2 (±0.9) | 20.9 (±1.1) | 20.6 (±1.0) | 21.9 (±1.1) | 21.4 (±0.9) | 21.3 (±1.0) |
| 权威化 | 21.3 (±0.7) | 21.2 (±0.9) | 21.1 (±0.8) | 22.3 (±0.8) | 22.9 (±0.8) | 22.1 (±0.9) | 23.2 (±0.7) | 21.9 (±0.4) | 23.9 (±1.2) | 23.0 (±1.1) | 23.1 (±0.7) |
| 专业术语 | 22.5 (±0.6) | 22.4 (±0.6) | 22.5 (±0.6) | 21.2 (±0.7) | 21.8 (±0.8) | 20.5 (±0.5) | 21.1 (±0.6) | 20.5 (±0.6) | 22.1 (±0.6) | 21.2 (±0.2) | 21.4 (±0.4) |
| 流畅度优化 | 24.4 (±0.8) | 24.4 (±0.6) | 24.4 (±0.8) | 21.3 (±0.9) | 23.2 (±1.5) | 21.2 (±1.0) | 21.4 (±1.4) | 20.8 (±1.3) | 23.2 (±1.8) | 21.5 (±1.3) | 22.1 (±1.2) |
| 引用来源 | 25.5 (±0.7) | 25.3 (±0.6) | 25.3 (±0.6) | 22.8 (±0.9) | 24.2 (±0.7) | 21.7 (±0.3) | 22.3 (±0.8) | 21.3 (±0.9) | 23.5 (±0.4) | 21.7 (±0.6) | 22.9 (±0.5) |
| 添加引语 | 27.5 (±0.8) | 27.6 (±0.8) | 27.1 (±0.6) | 24.4 (±1.0) | 26.7 (±1.1) | 24.6 (±0.7) | 24.9 (±0.9) | 23.2 (±0.9) | 26.4 (±1.0) | 24.1 (±1.2) | 25.5 (±0.9) |
| 添加统计数据 | 25.8 (±1.2) | 26.0 (±0.8) | 25.5 (±1.2) | 23.1 (±1.4) | 26.1 (±0.9) | 23.6 (±0.9) | 24.5 (±1.2) | 22.4 (±1.2) | 26.1 (±1.2) | 23.8 (±1.2) | 24.8 (±1.1) |

**表6说明：** 与基线相比，SEO 中传统使用的关键词堆砌等简单方法表现不佳；添加统计数据和添加引语等方法则在所有指标上表现出明显提升。最佳方法在位置调整词数和主观展示度上分别比基线提高 41% 和 28%。

---

# 附录C 结果

我们使用5个随机种子进行实验，并在表6中呈现带有统计偏差的结果。

## C.1 真实世界中的 GEO：在已部署生成式引擎上的实验

我们还在真实世界中已经部署的生成式引擎 Perplexity.ai 上评估了所提出的 GEO 方法。由于 Perplexity.ai 不允许用户指定来源网址，我们改为把来源文本作为文件上传至 Perplexity.ai，同时确保所有回答都只使用所提供文件中的来源生成。

我们在测试集的200个样本子集上评估全部方法。Perplexity.ai 的完整结果见表7。

### 表7：以 Perplexity.ai 为生成式引擎时，GEO 方法在 GEO-bench 上的完整结果

| 方法 | 词数 | 位置 | 位置调整词数·总体 | 相关性 | 影响力 | 独特性 | 多样性 | 后续点击／追问 | 主观位置 | 主观数量 | 主观展示度·平均 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **未实施 GEO** ||||||||||||
| 无优化 | 24.0 | 24.4 | 24.1 | 24.7 | 24.7 | 24.7 | 24.7 | 24.7 | 24.7 | 24.7 | 24.7 |
| **表现不佳的 GEO 方法** ||||||||||||
| 关键词堆砌 | 21.9 | 21.4 | 21.9 | 26.3 | 27.2 | 27.2 | 30.2 | 27.9 | 28.2 | 26.9 | 28.1 |
| 独特词汇 | 24.0 | 23.7 | 23.6 | 24.9 | 25.1 | 24.7 | 24.4 | 23.0 | 23.6 | 23.9 | 24.1 |
| **表现优异的 GEO 方法** ||||||||||||
| 权威化 | 25.6 | 25.7 | 25.9 | 28.9 | 30.9 | 31.2 | 31.7 | 31.5 | 26.9 | 29.5 | 30.6 |
| 流畅度优化 | 25.8 | 26.2 | 26.0 | 28.9 | 29.4 | 29.8 | 30.6 | 30.1 | 29.6 | 29.6 | 30.0 |
| 引用来源 | 26.6 | 26.9 | 26.8 | 19.8 | 20.7 | 19.5 | 18.9 | 20.0 | 18.5 | 18.9 | 19.0 |
| 添加引语 | 28.8 | 28.7 | **29.1** | 31.4 | 31.9 | 31.9 | 32.3 | 31.4 | 31.7 | 30.9 | 32.1 |
| 添加统计数据 | 25.8 | 26.6 | 26.2 | 31.6 | 33.4 | 34.0 | 33.7 | 34.0 | 33.3 | 33.1 | **33.9** |

**表7说明：** 与基线相比，SEO 中传统使用的关键词堆砌等简单方法往往表现更差；添加统计数据和添加引语等方法则在各项指标上表现出明显提升。表现最好的方法，在位置调整词数上比基线提高 22%，在主观展示度上比基线提高 37%。

---

## 原作与译本署名

- 原作：Pranjal Aggarwal, Vishvak Murahari, Tanmay Rajpurohit, Ashwin Kalyan, Karthik Narasimhan, Ameet Deshpande, “GEO: Generative Engine Optimization,” arXiv:2311.09735v3 / KDD 2024。
- 原作链接：https://arxiv.org/abs/2311.09735v3
- 正式出版版本：https://doi.org/10.1145/3637528.3671900
- 原作许可：Creative Commons Attribution 4.0 International（CC BY 4.0）。
- 改编说明：本文为中文翻译与版式重排，未改变原论文的公式、数据、实验结论和参考文献指向。
