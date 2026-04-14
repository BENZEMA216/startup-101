# YC Post-Money SAFE — Discount Only

> Source: https://www.ycombinator.com/documents
> Variant: "Post-money Safe: Discount Only"
> License note: YC 允许任何人免费使用 + 不承担后果；务必请律师审阅

## 一句话定位

投资人以 **Discount Rate（折扣率）** 为保护，未来下一轮定价时按折扣价转股。**不设 Cap**，所以上涨空间归创始人；但投资人得到的只是下一轮价格的 N%。

## 结构要点

| Section | 要点 |
|---|---|
| **Purchase Amount** | 本轮投资金额 |
| **Discount Rate** | 下一轮转股价格的折扣率（典型 80-85%）|
| **Conversion Price** | 下一轮 Price × Discount Rate |
| **其他** | 与 Cap-Only 变体一致（Liquidity / Dissolution / Amendment）|

## 关键参数

- **Discount Rate**：典型 80% (= 20% discount) 或 85% (= 15% discount)
  - **低于 80%** 对创始人不友好，需警惕
  - **高于 90%**（即 discount < 10%）对投资人吸引力低，少见

## 何时用 Discount-Only 而非 Cap-Only

- 公司早期**估值很难定**，创始人不想锚定 Cap
- 预期下一轮会很快（<12 个月）到来，Cap 谈不拢
- 投资人相对 "friendly"，接受纯折扣换早期风险

**业界现实**：Cap-Only 和 Cap+Discount 更常见。纯 Discount-Only 少见，因为投资人通常坚持 Cap 来锁定上限。

## 红旗

- 🚩 **Discount < 80%**：严重偏向投资人
- 🚩 **叠加过多 Discount-Only SAFE**：下一轮会出现"无限上升空间"错觉但折扣堆砌会让下一轮投资人惊讶
- 🚩 **与 Cap-Only SAFE 混签**：稀释计算更复杂，每张 SAFE 取 min(Cap 转换价, Discount 转换价)

## Skill 交叉引用

- Stage 6 决策 3
- post-money-cap.md（通常 A/B 组对比阅读）

## 下载与使用

1. https://www.ycombinator.com/documents → "Post-money Safe: Discount Only"
2. 下载 `.docx`，律师审阅
3. 填写参数：Purchase Amount / Discount Rate
