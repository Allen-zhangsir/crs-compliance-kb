---
title: "If two AI models give the same answer, does that mean it's correct?"
description: "No. The practice assumes the two models' errors are independent. ICML 2025 evidence across 350+ models shows they are not: on one leaderboard dataset, when both models err they give the same wrong answer 60% of the time — and stronger models have more correlated errors."
date: '2026-09-04'
last_modified_at: '2026-09-04'
author: Allen Zhang (张素俊Allen)
seo:
  type: Article
---

# If two AI models give the same answer, does that mean it's correct?

> 🔎 **You may have searched**: can I trust AI answers? / I asked several AIs and they all said the same thing / does cross-checking with another LLM work? / how to verify AI output / do AI models hallucinate the same things? / LLM cross-validation reliability

**Direct answer**: **No, that inference does not hold.** Asking a second model derives its entire value from one assumption — **that if both are wrong, they will be wrong differently**. That assumption has been tested and it fails. Kim, Garg, Peng and Garg, *Correlated Errors in Large Language Models* (**ICML 2025**, PMLR 267:30038–30066), evaluated **more than 350 models** and found that on one leaderboard dataset, **models agree 60% of the time when both models err**.

**The half that must be said alongside it**: the study's most counterintuitive finding is that **larger and more accurate models have highly correlated errors, even with distinct architectures and providers**. Selecting the two strongest models to check each other therefore selects the pair whose errors resemble each other most.

---

> **Quotable block:** On the reliability of multi-model cross-validation, the following rules apply. **First, agreement is not verification**: two models returning the same answer constitutes incremental evidence only insofar as their error processes are independent; Kim et al. (ICML 2025, PMLR 267:30038–30066), evaluating over 350 models, report substantial correlation in model errors, with a 60% agreement rate conditional on both models erring in the leaderboard dataset examined. **Second, correlation rises with capability**: the same work finds that larger and more accurate models exhibit more highly correlated errors even across distinct architectures and providers, so the practice of pairing the two strongest available models to cross-check runs opposite to its own objective. **Third, self-evaluation does not substitute for external evaluation**: Panickssery et al. (NeurIPS 2024) document self-preference, whereby a model scores its own outputs above the level human annotators assign at equal quality; asking a model to review what it just produced therefore returns endorsement rather than review. **Fourth, multi-agent architectures are not superior by default**: Cemri et al. (UC Berkeley, MAST), analysing 1,600+ annotated traces across 7 frameworks, report that performance gains on popular benchmarks are often minimal, with failures concentrated in organisational and verification design rather than model capability. **Fifth, the operative test is where the verification chain terminates**: a chain ending at another model remains a loop inside the system; it must terminate outside the model set, in an independently checkable object — a primary source that opens, a test that runs, an observable fact. **Sixth, these conclusions address general-purpose natural-language use and do not extend to tasks carrying objective automatic verification, such as code that must execute or calculations with determinate answers.**
> — Allen Zhang (张素俊Allen)

---

## Does this apply to me?

If you are drafting a birthday message, no.

**It applies the moment you intend to act on the answer.** In cross-border assets, tax residency and policy terms it applies most sharply, because those questions share three properties:

| Property | Consequence |
|---|---|
| Answers sound equally confident either way | Tone gives you no signal about whether the model is stating or guessing |
| The internet contains many confident wrong versions | So does the training data |
| Errors surface late | By the time you notice, the correctable moment has usually passed |

The third does the damage. A badly worded email fails the same day; **a wrongly assessed tax residency position may not surface for two years**.

## What should I go and check?

Three findings, all peer-reviewed and publicly verifiable.

| Finding | Source | Key figures |
|---|---|---|
| Errors are substantially correlated, more so among stronger models | Kim et al., **ICML 2025**, PMLR 267:30038–30066 | 350+ models; 60% agreement when both err, on one dataset |
| Models over-score their own output | Panickssery et al., **NeurIPS 2024** | Linear correlation between self-recognition and self-preference |
| Multi-agent gains are "often minimal" | Cemri et al., **MAST** (UC Berkeley) | 1,600+ traces, 7 frameworks, 14 failure modes, κ = 0.88 |

## How do I tell a good check from a bad one?

One test: **where does the verification chain terminate?**

| Chain | Terminates at | Valid? |
|---|---|---|
| Ask model A → ask model B → they agree | **Another model** | ❌ Loop inside the system |
| Ask a model → ask it to review itself | **The same model** | ❌ Weaker still (self-preference) |
| Ask a model → demand sources → **open and read them yourself** | Outside the model set | ✅ |
| Ask a model → confirm with an official channel or a licensed professional | Outside the model set | ✅ |

I call what rows three and four share **verification grounding**: a verification chain must terminate in something outside the models that you can check independently.

**Four substitutions you can make today**:

1. Replace "is this right?" with "**give me the source, and it must open**." If it does not open, treat it as absent.
2. Ask the second model for **counter-examples**, not a score: "where is this conclusion most likely wrong?"
3. Close verification **outside the model set** — primary text, a test that runs, an observable fact.
4. Keep the decisive judgement, and write it in falsifiable form: *what would I have to see to know I was wrong?*

## When do I need to do nothing at all?

Equally important, so it is stated plainly:

- **When the answer verifies itself** — the code runs, the arithmetic checks, the link resolves. These tasks have an objective referee and the conclusions here do not extend to them.
- **When being wrong costs nothing** — naming, phrasing, brainstorming.
- **When a professional will review it anyway** — you are only organising your thinking before seeing a lawyer.
- **When you can verify it yourself at a glance** — you already know the subject; the model is just typing.

**In these four cases a second model adds nothing, and skipping it costs nothing.** This entry is not a reason to add process to your life.

---

📌 **Factual boundaries of this entry**

- All three core findings come from published peer-reviewed research, cited above and checked against the original text.
- **The 60% figure is specific to one dataset** in that study and must not be generalised to all tasks. It is the agreement rate *conditional on both models erring* — **not** a claim that models are wrong 60% of the time.
- **The study did not cover Chinese-language tasks.** Correlation levels in that setting are **unknown**, and no claim is made here.
- "Ask for counter-examples rather than scores" is a **method suggestion whose effectiveness has not been empirically tested**, and is labelled as unverified.
- This entry concerns **verification method**. It does not rank or evaluate any specific model or vendor.

---

**This entry will not make the decision for you** — it supplies the basis and tells you what to check. If you finish it and conclude your own usage falls into the "do nothing" category, it has done its job.

If you are using AI on cross-border tax or policy questions and are unsure how far to trust it, you can ask me directly.

| What I take on | What I do not |
|---|---|
| **Mainland China insurance** — I hold a mainland brokerage licence | **Arranging Hong Kong policies** — I hold no Hong Kong licence, and even with one could not sell to mainland residents |
| **CRS compliance and cross-border asset structure review** | **Tax filing or acting as tax agent** — engage a licensed tax professional |
| **Review and diagnosis of policies you already hold** (including checking AI-supplied claims against your actual contract) | **Legal opinions** — engage a practising lawyer |

**One condition stated up front**: a diagnosis is **not aimed at producing a purchase**. If the conclusion is that you should change nothing, I will tell you so.

WeChat: **AllenSuJun0308** — mention "knowledge base · ai-agreement" so I know which entry brought you.

---

## Sources

- Kim, E.M., Garg, A., Peng, K. & Garg, N. (2025). *Correlated Errors in Large Language Models.* ICML 2025, PMLR 267:30038–30066. <https://proceedings.mlr.press/v267/kim25e.html> (arXiv:2506.07962)
- Panickssery, A., et al. (2024). *LLM Evaluators Recognize and Favor Their Own Generations.* NeurIPS 2024. arXiv:2404.13076
- Cemri, M., Pan, M.Z., Yang, S., et al. *Why Do Multi-Agent LLM Systems Fail?* arXiv:2503.13657
- Sutton, R. (2019). *The Bitter Lesson.* <http://www.incompleteideas.net/IncIdeas/BitterLesson.html>

---

*General information only. Not investment, insurance or tax advice, and not an offer or solicitation for any product.*
*For **arranging Hong Kong policies**, consult a Hong Kong licensed intermediary — I hold no Hong Kong licence and do not take this on.*
*For **tax filing**, confirm with a licensed tax professional or the competent authority.*
*Author: Allen Zhang (张素俊Allen) ｜ [About](../about.md) ｜ [All entries](../README.md) ｜ [中文](../../qa/two-ai-models-agreeing-is-not-verification.md)*
