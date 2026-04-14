# Case Studies — 2024-2026 中国 AI 出海真实案例

> last_policy_review: 2026-04-15
> **信息均来自公开报道，仅作教育参考。创业者决策请以最新信息 + 律师尽调为准。**

## 导读

本 appendix 6 个案例覆盖 Archetype B / C 的主要变体：

| 案例 | Archetype | 主体 | 主要学习点 |
|---|---|---|---|
| [Manus](#1-manus--butterfly-effect) | C | Singapore | 搬家 Singapore / Benchmark / CFIUS |
| [HeyGen](#2-heygen) | C | Delaware | 深圳→LA 搬家 / 视频生成合规 |
| [Opus Clip](#3-opus-clip) | C | Delaware | YC 路径 / 创始人税籍 |
| [Pika Labs](#4-pika-labs) | C | Delaware | 学术背景 / 视频模型 |
| [Dreamina 海外版](#5-dreamina-海外版) | B（大厂内嵌） | 字节 Cayman | 大厂通道 / 品牌切割 |
| [DeepSeek 海外触达](#6-deepseek-海外触达) | 特殊 | 纯内资 + 开源模型 | 不出海的"被动出海"模式 |

---

## 1. Manus / Butterfly Effect

**所在公司：** Butterfly Effect Pte Ltd（Singapore）
**核心产品：** Manus 通用 Agent
**关键节点：** 2025-03 爆红；2025-05 Benchmark 领投 $75M（据 The Information）；估值 $500M 级

### 架构

- **Singapore Pte Ltd** 作主体 — 避 Cayman 复杂 + 贴近 Benchmark
- 创始人团队部分搬至 Singapore，部分仍在国内
- 国内侧一度为 WFOE，后 Singapore 化进程中重组

### 收款 / 融资

- Stripe SG
- 美元基金 Benchmark 领投

### 注意与教训

- **据多方报道，Manus 轮次经历 CFIUS 延期**（中国创始人背景 + AI 关键技术 + US VC 投资 → CFIUS 触发三要素）
- **品牌策略：** "从 Butterfly Effect 到 Manus" 的品牌与主体分离是刻意的海外化
- **在 Stage 1 的启发：** 如果核心目标是 Benchmark / a16z 这类顶级 US VC 的"Global AI"赛道，**Singapore 比 Cayman 更友好 + 比 Delaware 更低 CFIUS 风险**

### 引用

- [The Information — Manus Raising $75M](https://www.theinformation.com/articles/manus-ai-raising-75-million-funding-round-benchmark)

---

## 2. HeyGen

**核心产品：** 数字人 / 视频生成
**关键节点：** 2023 从深圳搬 Los Angeles；2024 ARR $35M；Benchmark + Conviction + Sequoia 投资

### 架构

- **Delaware C-corp** 单主体
- 创始人搬至 US（持 O-1 或绿卡路径）
- 训练 / 研发搬 US

### 教训

- **彻底搬家路径**：需要创始人个人身份迁移、数据迁移、模型 IP 搬运（训练日志 / weights / 合同统统迁移）
- 早期曾有 VIE 架构思路，中途放弃转 Delaware 纯海外
- **2024 后几乎所有以视频 / 图像为核心的出海 AI，倾向 HeyGen 模式**（彻底 Delaware）— 降低 PIPL + EU AI Act GPAI 层面风险

### 启发

- 训练数据 / 用户数据从一开始就留海外，**避免后续 PIPL 出境合规难题**
- QSBS 可得（5 年 + $50M 资产门槛）

---

## 3. Opus Clip

**核心产品：** AI 长视频剪短 C 端工具
**关键节点：** 2023 YC + a16z 种子；2024 A 轮

### 架构

- **Delaware C-corp** 单主体
- 创始人（young，纯技术背景）走 YC 路径

### 教训

- **YC 路径优点：** Delaware 注册 + SAFE 模板 + Stripe Atlas 一站式
- **YC 路径陷阱（创始人税籍）：** 如果仍是中国税务居民 → 退出时中国 20% 个税 + 美国资本利得税可能叠加
- **建议：** 进 YC 前就处理创始人身份（O-1 → 绿卡路径常见）

---

## 4. Pika Labs

**核心产品：** 文生视频
**关键节点：** 2023 Stanford 背景；Lightspeed / Spark 投资；2024 估值 $500M+

### 架构

- **Delaware C-corp**
- 创始人斯坦福 CS PhD 背景，美国身份

### 教训

- **纯 Archetype C**：创始人已在美 → 无 37 号文 / ODI / WFOE 痛点
- QSBS 优势最大化（持股 5 年 + 公司资产 ≤$50M 退出）
- **训练数据合规**：采用 Shutterstock 等授权数据 + 公开数据 + 合成数据，未来 AI Act 训练数据摘要披露压力较低

### 启发

- 学术背景 + 美国身份的创始人：Delaware 单主体永远是最优
- 不要强行为了"中国 AI"叙事搭红筹

---

## 5. Dreamina 海外版

**核心产品：** 字节跳动旗下 AI 绘画 / 视频（国内叫"即梦"，海外以"Dreamina"）
**关键节点：** 2024 全球发布；走 TikTok 同款合规通道

### 架构

- ByteDance Cayman 顶层下，海外产品经 **Singapore 实体** 出海
- 与国内主体切割数据流：海外版不回传国内
- 训练主要依赖国内 WFOE + 海外合作数据

### 教训

- **大厂通道优势：** 品牌切割 + 数据切割 + 合规切割三板斧
- 小创业者难以复制，但可以学：**国内 + 海外版本数据 & 模型权重分离**，避免跨境合规
- 海外版采用独立品牌（"Dreamina" vs "即梦"），避免国内品牌风险传导

### 启发

- 纯内资公司也可"被动出海"— 通过海外合作伙伴 / 独立海外子品牌
- 但：创业者不是大厂，**数据隔离成本** 对小团队难以承受。**仍建议 Archetype B**（Cayman/SG 顶层）作为长期架构。

---

## 6. DeepSeek 海外触达

**核心公司：** 杭州深度求索（关联私募幻方量化）
**核心产品：** DeepSeek V3 / R1 等开源大模型
**关键节点：** 2025-01 R1 发布全球爆火；纯内资架构

### 架构

- **纯内资有限公司**（Archetype A 变体）
- 模型开源（MIT）→ 海外用户直接用开源权重 / 第三方 API
- 官方 chat.deepseek.com 有海外访问但无美元收款主体

### 教训

- **开源模型作为出海手段**（不是出海，是"全球都能用"）
- 纯内资 + 开源 → **没有 PIPL 出境 / EU AI Act GPAI 难题**（用户自己部署自己合规）
- 商业变现靠国内 API / 私有部署 / 战略合作

### 启发

- **如果你做开源基础模型**：纯内资可行，靠开源声誉传播
- 但 C 端订阅 / API 海外变现 → 仍需 Archetype B/C 架构
- R1 发布后 OpenAI / Anthropic 对中国创业 AI 友好度 **整体下降**（赛道敏感度上升），这影响后来者的 CFIUS 风险

---

## 跨案例规律

| 规律 | 说明 |
|---|---|
| **2024 后新出海默认 Delaware 或 Singapore** | VIE / Cayman+VIE 几乎消失（除非特定牌照行业） |
| **视频 / 图像 / 数字人类产品尤其倾向彻底搬家** | 训练数据 + 用户数据的 PIPL 压力最大 |
| **创始人身份是硬约束** | 身份没迁移，架构迁移效果减半（FBAR / 全球征税 / 37 号文） |
| **CFIUS 是 US VC 路径的常客** | 中国创始人 + AI + US 资本三要素 → 提前预审 |
| **品牌切割** | 大厂案例共性：国内品牌 ≠ 海外品牌（避免舆论传染） |
| **开源作为出海路径** | DeepSeek / Qwen 的模式值得研究，但不适合 C 端订阅 |

## 本 appendix 在 skill 流程中的角色

- Stage 1 决策 3（架构前置判断）— 给用户具体参考
- Stage 5（AI 上线）— 看别人怎么处理跨境数据 + 模型 IP
- Stage 6（融资）— 看别人怎么应对 CFIUS / 估值 / 架构错配

## 引用

- [The Information — Manus $75M](https://www.theinformation.com/articles/manus-ai-raising-75-million-funding-round-benchmark)
- HeyGen 公开融资信息（Crunchbase / PitchBook）
- Opus Clip YC S23
- Pika Labs 公开投资方披露
- Dreamina：字节跳动官方产品页
- DeepSeek：https://www.deepseek.com/ 及开源 repo
