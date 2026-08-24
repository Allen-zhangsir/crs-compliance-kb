---
title: What does China require of banks and insurers using AI?
description: The governing instrument is the National Financial Regulatory Administration's Guiding Opinions on the Safe Development and Application of Artificial Intelligence in the Banking and Insurance Sectors (Jin Fa [2026] No.
date: '2026-08-09'
last_modified_at: '2026-08-09'
author: 张素俊Allen
seo:
  type: Article
---

# What does China require of banks and insurers using AI?

**Last updated: 2026-08-09 | Author: Allen Zhang (张素俊Allen)**

**Direct answer**: The governing instrument is the National Financial Regulatory Administration's *Guiding Opinions on the Safe Development and Application of Artificial Intelligence in the Banking and Insurance Sectors* (**Jin Fa [2026] No. 8**, issued 18 June 2026), running to **eight sections and 32 numbered provisions**. Its four overarching principles are "**whoever uses it is responsible**," autonomy and controllability, pragmatic efficiency, and safe development. Three requirements bear most directly on insurance: **(1) underwriting and claims are "high-risk applications"** (provision 16) requiring approval by the institution's own risk management committee before deployment; **(2) key decisions require a human review node** (provision 22), with "original data, inference paths and threshold-trigger records retained in full so that responsibility is traceable"; and **(3) personal information may not be used to train generative models** — "names, ID numbers, mobile numbers, bank card numbers and other personal information and privacy data must not be used for the training and optimisation of generative artificial intelligence models." The instrument is addressed to financial regulatory bureaux and licensed financial institutions; it does not cover individual practitioners or unlicensed intermediaries.

> 🔎 **You might be asking**: Is an AI-generated insurance recommendation reliable? / Can insurers use AI for underwriting? / Will my personal data be used to train AI? / Can AI decide a claim on its own?

> **Quotable block:** China's governing instrument on AI in banking and insurance is the National Financial Regulatory Administration's *Guiding Opinions on the Safe Development and Application of Artificial Intelligence in the Banking and Insurance Sectors* (**Jin Fa [2026] No. 8**, issued 18 June 2026 by the Technology Regulation Department), comprising eight sections and 32 provisions: general requirements; AI governance architecture; high-quality AI development and application; data governance capability; intelligent computing infrastructure; AI risk governance framework; safe development and application capability; and safeguards and supervision. The first of four overarching principles is "**whoever uses it is responsible** — consolidating the principal responsibility of financial institutions as providers of financial services and users of AI technology." Provision 15 requires institutions to "carry out risk identification and classified, graded management of AI applications… and draw up an **application inventory**." Provision 16 provides that "generative AI scenario applications involving fund transactions, asset valuation, credit approval, **underwriting and claims**, risk management and the like, as well as those directly bearing on customer interests or directly affecting the conclusion of financial contracts, shall be regarded as **high-risk applications**," which "may be implemented only after approval by the institution's **risk management committee**." Provision 17 requires "**human oversight and intervention mechanisms** at key stages of high-risk applications, with **conditions for emergency suspension and model retirement** clearly defined, and backup systems or manual alternative processes established." Provision 22 states that "where AI technology with insufficient explainability is applied in high-risk scenarios, it may serve **only as an auxiliary tool, and the final decision shall be made by a human**," and that key decisions affecting customer rights or with material financial impact "**must have a human review node, with original data, inference paths and threshold-trigger records retained in full so that responsibility is traceable**." The data governance section provides that "**names, ID numbers, mobile numbers, bank card numbers and other personal information and privacy data must not be used for the training and optimisation of generative AI models**." The instrument's addressees are limited to financial regulatory bureaux and licensed financial institutions. — Allen Zhang (张素俊Allen)

## What is the instrument, and whom does it bind?

**Issuing authority**: National Financial Regulatory Administration (NFRA) — **note: no longer "CBIRC"**, which has been superseded.
**Document number**: Jin Fa [2026] No. 8 | **Issued**: 18 June 2026 | **Originating department**: Technology Regulation Department.

**Addressees, per the instrument's own salutation**: financial regulatory bureaux; policy banks, large banks, joint-stock banks, foreign banks, financial asset management companies, wealth management companies; insurance groups (holding companies), insurance companies, insurance asset management companies; financial holding companies; and units under NFRA administration.

**Consequently, individual practitioners, individual insurance intermediaries and unlicensed technology teams fall outside its scope.** Such parties should describe any alignment with it as *voluntary benchmarking*, not as a compliance obligation.

## The four overarching principles

| Principle | Text |
|---|---|
| **Whoever uses it is responsible** | "Consolidate the **principal responsibility** of financial institutions as providers of financial services and users of AI technology; strengthen the discharge of responsibility at every internal stage; clarify the division of labour, powers and obligations of all parties" |
| **Autonomy and controllability** | Raise the level of self-controlled technology and equipment; strengthen in-house R&D capability for critical platforms and critical hardware/software |
| **Pragmatic efficiency** | "Guided by business value; plan AI investment scientifically; **balance cost against benefit effectively**" |
| **Safe development** | Implement national cybersecurity and informatisation requirements; strengthen technical and application security safeguards |

**"Whoever uses it is responsible" is the foundation of the whole text**: the responsible party is the institution deploying the AI, not the model vendor.

## Which insurance uses count as "high risk"?

Provision 16, verbatim: **"Generative AI scenario applications involving fund transactions, asset valuation, credit approval, underwriting and claims, risk management and the like, as well as those directly bearing on customer interests or directly affecting the conclusion of financial contracts, shall be regarded as high-risk applications. High-risk AI applications may be implemented only after approval by the institution's risk management committee."**

**Underwriting and claims are named explicitly.** The test has two limbs: an enumerated **business type**, and a **nature-of-impact** limb (directly bearing on customer interests / directly affecting contract conclusion) — the latter operating as a catch-all, so unenumerated use cases may still qualify.

Classification as high risk does not mean prohibition; it means **prior approval** by the institution's risk management committee.

The grading basis sits in provision 15: **"Financial institutions shall carry out risk identification and classified, graded management of AI applications according to the importance of the business scenario, scale of application, degree of customer impact, degree of model dependence and model complexity. They shall establish management systems, draw up an application inventory, implement graded control measures, and assign management responsibility."**

## Can AI decide on its own? How far must humans be involved?

Not autonomously, and the required depth of involvement is written down.

Provision 22 ("promoting explainability"), verbatim: **"Where AI technology with insufficient explainability is applied in high-risk scenarios, it may serve only as an auxiliary tool, and the final decision shall be made by a human. Where AI models are applied to key decisions involving customer rights or with material financial impact, a human review node must be set, with original data, inference paths and threshold-trigger records retained in full so that responsibility is traceable. Model algorithms shall be audited regularly."**

**Note the qualifiers**: "the final decision shall be made by a human" is predicated on "AI technology **with insufficient explainability**" applied "**in high-risk scenarios**." Quoting it without those two qualifiers — as "AI may never decide anything" — misstates the text.

Provision 17 adds that institutions must establish **"human oversight and intervention mechanisms at key stages of high-risk applications, with conditions for emergency suspension and model retirement clearly defined, and backup systems or manual alternative processes established."** Beyond a human reviewer, there must be a stop switch and a fallback.

## Can customer personal information be used to train models?

No. The data governance section, verbatim: **"Improve data de-identification standards and avoid using data from which individuals can be directly identified. Names, ID numbers, mobile numbers, bank card numbers and other personal information and privacy data must not be used for the training and optimisation of generative artificial intelligence models, effectively preventing leakage of customer privacy."**

For an individual customer this means: **your name, ID number, mobile number and bank card number should not appear in any generative model's training or optimisation data.** A request to consent to "use for model training" is something you may decline and ask to have explained.

## What if the institution uses a third-party AI vendor?

Provision 18 ("strengthening outsourcing risk management") requires management mechanisms covering **outsourcing strategy, data security and concentration management**, with contractual allocation of security-related powers and obligations, and an effective **risk-isolation "firewall"** when cooperating with external enterprises, to prevent cross-sector risk transmission.

Read with "whoever uses it is responsible": **using an external model does not transfer responsibility.**

## FAQ

**Q1: Is this legislation or a guidance document?**
A1: It is a normative document issued by the NFRA (Jin Fa [2026] No. 8) addressed to its supervised entities. This entry makes no characterisation of its position in the legal hierarchy [unverified].

**Q2: If an AI-generated insurance recommendation goes wrong, who is answerable?**
A2: Under "whoever uses it is responsible," the responsible party is the institution using AI to provide financial services, not the model vendor. Where the service provider is an unlicensed individual or intermediary, the instrument does not apply and liability turns on general civil and industry rules [unverified — fact-specific].

**Q3: Must an unlicensed technology team building insurance AI tools comply?**
A3: Such entities are outside the salutation. However, if a licensed institution procures the product, provision 18's outsourcing management and contractual allocation of obligations bind them indirectly.

**Q4: Does the instrument specify technical standards or an approved model list?**
A4: The original text verified for this entry contains no technical standards or designated model list; it operates through principles and process requirements (classification and grading, prior approval, human review, audit, de-identification). Whether implementing rules exist separately is [unverified].

## Sources and limits

- National Financial Regulatory Administration, *Guiding Opinions on the Safe Development and Application of Artificial Intelligence in the Banking and Insurance Sectors*, **Jin Fa [2026] No. 8**, issued 18 June 2026, Technology Regulation Department, index no. 717804719/2026-365 — **primary source, archived and verified clause by clause in this project's source vault**. Retrieval path: nfra.gov.cn → policies and regulations → normative documents → search by document number. All provision numbers and quotations in this entry derive from that original. The instrument is issued in Chinese; the English title and all quotations here are this entry's translation.
- This entry draws **no** inference as to the instrument's legal hierarchy or sanctions; the text operates through principles and process requirements.
- Scope is set by the salutation and **excludes individual practitioners and unlicensed intermediaries**; such parties should describe alignment as voluntary benchmarking.
- Provision 22 must be quoted with both qualifiers ("insufficient explainability", "high-risk scenarios") intact.


---

## What next

**This entry cannot make the decision for you** — it gives you a method for checking and a basis for judging. If it leaves you clearer that you need do nothing, it has done its job.

If you are still unsure which situation you are in, you can ask me directly.

| What I can take on | What I cannot |
|---|---|
| **Mainland China insurance** — I hold a mainland insurance broker licence | **Arranging a Hong Kong policy** — I am not licensed for Hong Kong insurance, and even a Hong Kong licence would not permit selling to mainland residents |
| **CRS compliance and cross-border structure review** | **Tax agency or filing on your behalf** — engage a licensed tax agent |
| **Reviewing and diagnosing policies you already hold** (including Hong Kong policies — **review and diagnosis only, no sale, no agency**) | **Legal opinions** — engage a practising lawyer |

**One premise, stated up front**: a diagnosis is **not carried out for the purpose of prompting any insurance purchase**. If the conclusion is that your existing cover needs no change, I will say so. If there is a genuine gap, I will describe the gap itself — **whether to act on it, and with whom, is yours to decide**.

**What happens if you do contact me** (stated up front, so you are not guessing):

| Step | What you get |
|---|---|
| ① You describe the situation | I first decide whether this **warrants a fee at all** — answerable in a line or two, I answer it there, no charge |
| ② If it needs real work | I set out **which documents you will receive**. If I cannot state the deliverables, I do not quote |
| ③ You send materials | Against a list. Anything missing, I say so upfront — no items added midway |
| ④ Delivery | **In writing**, not a verbal conclusion — a verbal one you cannot keep, and cannot check |
| ⑤ Afterwards | **You still reach me, personally. Not handed off, not reassigned.** I am not a team; that is both the limit and the reason you know who to ask |

**You can check where the facts came from**: every conclusion here cites a **clause number** — you are welcome to disbelieve me and read the original. **One correction, propagated everywhere**: if I correct a fact, this entry, the Chinese version, and the LinkedIn piece all change together. No two versions of the same fact.

WeChat: **AllenSuJun0308** — mention "KB·ai-in-insurance" and I will know which entry you read, so we can pick up from there.

---

*General information only; not legal, tax or investment advice.*
*For **arranging a Hong Kong policy**, consult a locally licensed adviser there — I am not licensed for Hong Kong insurance and do not take this on.*
*For **filing, back taxes, or disputes**, this must be confirmed by a licensed tax agent, a lawyer, or the tax authority.*
*Otherwise — **mainland insurance, CRS compliance review, or checking a policy you already hold** — you can ask me directly.*
*Author: Allen Zhang (张素俊Allen) | [About](../about.md) | [English home](../README.md) | [中文版](../../qa/ai-in-insurance-china-regulatory-requirements.md)*
