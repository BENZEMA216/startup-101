# References: AI Tech — AI 技术

## Tier 1

### a16z — Emerging Architectures for LLM Applications

- **作者/来源：** Andreessen Horowitz
- **发布：** 2023-06（持续更新版本）
- **URL：** https://a16z.com/emerging-architectures-for-llm-applications/
- **适用阶段：** 产品架构设计 / Stage 5 上线前
- **一句话价值：** LLM 应用参考架构事实标准图 — data pipeline / embedding / vector DB / orchestration / observability
- **核心要点：**
  1. Data Preprocessing → Embedding Model → Vector DB → LLM APIs → Orchestration → Logging
  2. "In-context learning" 是主要范式
  3. 推荐组件：Pinecone / Weaviate / Pgvector（向量） / LangChain / LlamaIndex（编排） / LangSmith / Langfuse（观测）

---

### a16z — AI Canon

- **作者/来源：** a16z
- **URL：** https://a16z.com/ai-canon/
- **一句话价值：** AI 必读论文 + 博客清单（持续更新） — Attention Is All You Need / GPT-3 原论文 / Chinchilla / RAG paper 等
- **适用阶段：** 整个职业生涯
- **特别推荐：**
  - "Software 2.0" (Karpathy)
  - "State of GPT" (Karpathy)
  - "Chain of Thought Prompting" (Wei et al.)
  - Simon Willison 系列

---

### Ben Horowitz — 16 Startup Metrics

- **作者/来源：** Jeff Jordan, Anu Hariharan, Preethi Kasireddy (a16z team)
- **发布：** 2015-08（常看常新）
- **URL：** https://a16z.com/16-startup-metrics/
- **适用阶段：** Stage 7 Ongoing 投后汇报 / Stage 6 融资 BP
- **一句话价值：** 创业公司 metrics 入门权威清单
- **16 条：**
  1. Bookings vs. Revenue
  2. Recurring Revenue vs. Total Revenue
  3. Gross Profit
  4. Total Contract Value vs. Annual Contract Value
  5. Lifetime Value (LTV)
  6. Gross Merchandise Value vs. Revenue
  7. Unearned or Deferred Revenue (for SaaS)
  8. Churn
  9. Customer Acquisition Cost (CAC)
  10. Active Users (DAU/MAU)
  11. Month-on-Month Growth
  12. Cumulative Charts
  13. Charts Tricks (Don't Cheat with Axes)
  14. Net Burn vs. Gross Burn
  15. Runway
  16. Cash Flow ≠ Revenue

---

### Karpathy — Intro to Large Language Models

- **作者/来源：** Andrej Karpathy (OpenAI / Tesla)
- **发布：** 2023-11
- **URL：** https://www.youtube.com/watch?v=zjkBMFhNj_g
- **文字稿：** https://karpathy.ai/stateofgpt.html（相关版本）
- **License：** YouTube 公开 + 幻灯片 MIT（若 Karpathy GitHub 发布）
- **一句话价值：** 1 小时理解 LLM 全部 — pretraining / instruction tuning / RLHF / 工具使用 / 安全
- **v0.3 计划：** 若 Karpathy 明确 CC 授权，内置 markdown 到 `bundled/`

---

### Simon Willison — Prompt Injection 系列

- **作者/来源：** Simon Willison（Django 联创）
- **URL：** https://simonwillison.net/tags/promptinjection/
- **License：** CC-BY 4.0（博客首页注明）
- **一句话价值：** Prompt Injection 这个威胁类的命名者 + 最持续更新者
- **必读单篇：**
  - [Prompt injection: What's the worst that can happen?](https://simonwillison.net/2023/Apr/14/worst-that-can-happen/)
  - [The dual LLM pattern for building AI assistants that can resist prompt injection](https://simonwillison.net/2023/Apr/25/dual-llm-pattern/)
- **AI 创业者启发：** Agent 上线前必读，避免 Indirect Prompt Injection 事故

---

### Sonya Huang — Generative AI 三部曲

- **作者/来源：** Sonya Huang（Sequoia）+ David Cahn 第三篇
- **发布：**
  - 2022-09 [Generative AI: A Creative New World](https://www.sequoiacap.com/article/generative-ai-a-creative-new-world/)
  - 2023-09 [Generative AI Act Two](https://www.sequoiacap.com/article/generative-ai-act-two/)
  - 2024-06 [AI's $600B Question](https://www.sequoiacap.com/article/ais-600b-question/)
- **适用阶段：** Stage 6 讲资本故事 / Stage 7 业务 positioning
- **一句话价值：** Sequoia 视角的 AI 市场演变三幕剧

---

## Tier 2

- **Bessemer — State of the Cloud** — https://www.bvp.com/atlas/state-of-the-cloud — 年度 SaaS 数据
- **Lightspeed — State of AI** — 年度 AI 投资观察
- **a16z — Top 100 GenAI Consumer Apps** — 季度榜单
- **Hugging Face Blog** — 最前沿开源模型动态
- **Ethan Mollick — One Useful Thing** — Substack，AI 实用主义视角
- **Chip Huyen — AI 博客** — ML Engineering 实战
- **Latent Space Podcast** — https://www.latent.space/ — AI 工程师必听
- **Nathan Lambert — Interconnects** — 开源模型分析

---

## 常见问题快查

| 场景 | 推荐 |
|---|---|
| 我要做 RAG，架构怎么选？ | a16z Emerging Architectures |
| Agent 上线前安全检查？ | Simon Willison Prompt Injection 系列 |
| 怎么给投资人讲 AI 赛道故事？ | Sonya Huang 三部曲 + $600B |
| Board Deck 该看哪些指标？ | 16 Startup Metrics |
| 想入行 AI 工程？ | Karpathy + a16z Canon |

---

## 本 index 在 skill 中的角色

- Stage 5（AI 上线前）— Simon Willison / Emerging Architectures 是技术护栏
- Stage 6 BP 写作 — Sonya Huang 提供叙事框架
- Stage 7 汇报 — 16 Metrics 是 board update 骨架
