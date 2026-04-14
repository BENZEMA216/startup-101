# YC Post-Money SAFE — Cap and Discount（组合变体）

> Source: https://www.ycombinator.com/documents （基础模板：Cap-Only）
> Variant: "Post-money Safe: Cap + Discount"（组合结构，目前 YC 不再单独发布独立 DOCX，需要在 Cap-Only 基础上加 Discount 条款）
> License note: YC 允许任何人免费使用 + 不承担后果；务必请律师审阅

## 一句话定位

投资人同时享有 **Cap**（下行保护）和 **Discount**（定价折扣），转股时按 **min(Cap 对应价, 下一轮定价 × Discount Rate)** 取更低价，对投资人最友好。

## YC 官网状态（2026-04 核对）

2026-04 访问 ycombinator.com/documents 时，YC 页面仅主推 **Cap-Only / Discount-Only / MFN-Only** 三种独立模板。**Cap+Discount 组合**历史上是第四个变体，目前常见做法：
- 从 **Cap-Only** DOCX 作为底稿
- 手工 / 律师加入 **Discount Rate** 条款（修改 "Conversion Price" 定义）
- 或使用律所（如 Cooley）自有的组合模板

## 结构要点（合并自 Cap / Discount）

| Section | 要点 |
|---|---|
| **Purchase Amount** | 本轮投资金额 |
| **Post-Money Valuation Cap** | 上限估值 |
| **Discount Rate** | 折扣率（典型 80-85%）|
| **Conversion Price** | **min(Cap Price, 下一轮 Price × Discount Rate)** |
| 其他 | 同 Cap-Only |

## 何时选这个变体

- 投资人要求"既要 Cap 也要 Discount"
- 创业者愿意多让一点以换快速 Closing
- AI 赛道 2024-2026 种子期常见（投资人对估值上限不确定时既要 Cap 兜底又要 Discount 对冲）

## 红旗

- 🚩 **Cap 低 + Discount 大**：等于两层稀释叠加，创始人吃亏
- 🚩 **手工拼接条款未经律师审阅**：Conversion Price 定义错位 → 未来转股争议
- 🚩 **对方拿"Pre-money Cap + Discount"当 Post-money 签**：务必核对 Cap 的口径

## Skill 交叉引用

- Stage 6 决策 3 + 决策 4
- post-money-cap.md / post-money-discount.md（阅读前置）

## 使用建议

因为这是"组合"变体且 YC 不提供官方单模板，**必须找律师起草**。不建议创业者自己拼接。
