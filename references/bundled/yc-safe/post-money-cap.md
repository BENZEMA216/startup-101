# YC Post-Money SAFE — Valuation Cap Only

> Source: https://www.ycombinator.com/documents
> Variant: "Post-money Safe: Valuation Cap Only"
> License note: YC 允许任何人免费使用 + 不承担后果；务必请律师审阅

## 一句话定位

**最常见**的种子期融资工具：投资人以 **Cap（估值上限）** 为保护，未来下一轮定价时以 min(Cap, 下一轮估值) 折算股份。没有折扣率、没有到期日、没有利息。

## 结构要点

| Section | 要点 |
|---|---|
| **Purchase Amount** | 本轮投资金额 |
| **Post-Money Valuation Cap** | 上限估值（Post-Money 口径，含本轮 SAFE 稀释） |
| **Conversion on Equity Financing** | 下一轮 Priced Round 时按 min(Cap, 本轮定价) 转股 |
| **Liquidity Event** | IPO / 并购时：按 Cap 或 Purchase Amount 返还（取较高）|
| **Dissolution Event** | 清算时按 Purchase Amount 返还（senior to 普通股，subordinate to 债权人）|
| **Most Favored Nation（隐含）** | Post-money 版本**不含** MFN 条款（与 Pre-money 版本区别之一）|
| **Amendments** | 需 SAFE 持有人 majority 同意 |

## 关键参数（谈判点）

- **Post-Money Valuation Cap** — 最关键。Post-money 意味着 Cap 里已"装了"本轮 SAFE，因此创始人稀释更明确。
  - 2024-2026 AI 种子期典型 Cap 区间：$10M – $30M（大 Cap 要有叙事支撑）
- **Purchase Amount** — 单个投资人本轮出资额

## 与 Pre-money SAFE 的区别（必知）

| 维度 | Pre-money SAFE（旧）| Post-money SAFE（2018+ 推荐）|
|---|---|---|
| Cap 口径 | 不含 SAFE 的估值 | 含本轮全部 SAFE 的估值 |
| 稀释可预测性 | 差（多个 SAFE 叠加会让创始人多稀释）| 好（Cap 即 Post-money） |
| MFN | 内置 | 单独 MFN-only SAFE |
| 业界现状 | 基本弃用 | 当前默认 |

**Skill 硬建议**：种子期**只用 Post-money SAFE**。如果对方递 Pre-money SAFE → 换。

## 触发转换的"Equity Financing"定义

下一轮 Priced Round（通常 A 轮）发行 Preferred Stock 且金额超过门槛（常见 $1M min）→ SAFE 自动转为该轮价格对应的 Preferred Stock（Safe Preferred，和 A 轮同等级优先股）。

## 红旗（谈判中注意）

- 🚩 **Cap 过低**：用户拿到低得离谱的 Cap（相对同行）→ 下一轮稀释过重
- 🚩 **"Side letter" 魔改**：有些投资人附加 side letter（回购 / board / veto）→ 签前律师核
- 🚩 **混用 Pre/Post SAFE**：同轮混用会造成稀释计算极难，坚持全部 Post

## Skill 交叉引用

- Stage 6 决策 3：SAFE / 可转债 / 股权直投的选择
- Stage 6 决策 4：Termsheet 五大类条款（SAFE 本身不涉及 control，但下一轮 Priced Round 会）

## 下载与使用

1. 访问 https://www.ycombinator.com/documents
2. 点击 "Post-money Safe: Valuation Cap Only"，下载 `.docx`
3. 填写：Company Name / Investor / Purchase Amount / Valuation Cap / Date / 签字
4. 律师审阅
5. 双方签字 + 投资人打款 + 公司出具 counter-signed SAFE

## 参考阅读

- YC 原版 blog 解释：https://www.ycombinator.com/blog/announcing-the-safe-a-replacement-for-convertible-notes
- 石头《融资指南》§10.1 — 经济类条款
