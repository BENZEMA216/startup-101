---
name: check-cross-border-payment
description: 跨境收款路径选择 — 根据主体架构 + 币种 + 业务模型，给出 Stripe / Paddle / Airwallex / MoR 等路径的对比 + 首推方案 + 红旗扫描
argument-hint: '[--currency <USD|EUR|JPY|...>] [--model <subscription|one-time|b2b|marketplace>] [--urgency <high|normal>]'
trigger: /startup-101 check cross-border-payment
source_appendix:
  - appendix/payment-matrix.md
  - modes/red-flags.md  # Red Flag 3
profile_fields_used:
  - stage_0_output.archetype
  - stage_2_output.chosen_path
  - stage_2_output.cayman_entity_formed
  - stage_2_output.delaware_entity_formed
  - stage_2_output.sg_entity_formed
  - stage_2_output.hk_entity_formed
  - stage_3_output.bank_account_status
  - payment_model
  - target_currency
profile_fields_written:
  - stage_3_output.payment_path_chosen
  - stage_3_output.payment_setup_deadline
last_policy_review: 2026-04-15
---

# Check: 跨境收款路径选择

> 📎 完整矩阵见 [`appendix/payment-matrix.md`](../../appendix/payment-matrix.md)。
> 本命令只做"**给定你的架构 + 业务模型，选哪条收款路径 + 为什么**"的判定，不复述所有可选项细节。

## 何时用这个命令

- 准备开收款账户前（Stage 3 Day-30 黄金窗口）
- 目标币种 ≠ RMB（出海 SaaS、AI API、开源付费、App Store 等）
- 已经在用个人 PayPal / 微信 / 支付宝归集境外订阅款（🚩 Red Flag 3 高危）
- 订阅制 + 每月 >$4000 的流水开始规模化
- 融资 DD 要求规范收款流水

## 输入

从 `./_profile.md` 读取：

| 字段 | 作用 |
|---|---|
| `stage_0_output.archetype` | A / B / C 决定哪些方案是闭门 |
| `stage_2_output.*_entity_formed` | 各海外主体是否已注册 |
| `stage_3_output.bank_account_status` | 各银行开户进度 |
| `payment_model` | `subscription` / `one-time` / `b2b_invoice` / `marketplace` |
| `target_currency` | 决定 MoR 手续费对冲 |

若字段缺失，一次问一个：

1. 你的主体架构？ `[A 纯内资 / B 双层(Cayman+HK+WFOE) / C 纯海外(Delaware/SG) / 其他]`
2. 业务模型？ `[a] 订阅制 SaaS` `[b] 一次性付费` `[c] To B 开票` `[d] Marketplace 分成` `[e] 混合`
3. 主要目标币种？ `[USD / EUR / JPY / GBP / 多币种]`
4. 预期 12 个月 GMV 量级？ `[<$10k / $10-100k / $100k-1M / >$1M]`
5. 收款紧迫度？ `[立刻能收 / 1-3 个月内 / 架构搭完再说]`
6. 当前是否已用**个人 PayPal / 微信 / 支付宝**收过境外款？ `[Y/N]` 若 Y → 月流水多少？

## 决策逻辑

### 第一层：架构决定可选方案

```
archetype == A (纯内资)
├─ 订阅制 / 一次性 → 【首选 Paddle MoR】
├─ To B 开票为主 → 境内对公美元户直接收（汇款方承担手续费）
└─ ❌ 无法：Stripe US / Stripe SG 审核过不了

archetype == B (Cayman + HK + WFOE)
├─ 订阅制 → 【首选 Stripe HK / Stripe SG】+ Airwallex 收款
├─ 一次性 → 同上
├─ To B 开票 → HK 对公 USD 户（Airwallex / ZA Bank）
└─ 备选：Paddle MoR（若 Stripe 延迟开通）

archetype == C (Delaware)
├─ 订阅制 → 【首选 Stripe US】+ Mercury 银行
├─ 一次性 → 同上
├─ To B 开票 → Mercury USD / Wise Business
└─ 备选：Brex 银行 + Stripe（若 Mercury 不过）
```

### 第二层：业务模型修正

| 模型 | 首选 | 为什么 |
|---|---|---|
| Subscription SaaS | Stripe（Archetype B/C）/ Paddle（A） | 自动续订 + failed payment retry |
| One-time payment | Stripe + Link / Apple/Google Pay | 前端体验最好 |
| B2B invoice | 对公 USD 户 + wire | 手续费结构不同，Stripe 不划算 |
| Marketplace / Connect | Stripe Connect（B/C） | 分账 + 1099/K 自动化（US） |
| App Store / Google Play | 平台本身 MoR，落到主体银行 | 平台已经做 MoR 扣税 |
| 混合 | Stripe + Paddle 双通道 | Stripe 主渠 + Paddle 作为"无主体国家"兜底 |

### 第三层：紧迫度修正

```
紧迫度 == 立刻能收
├─ archetype A + 订阅制 → Paddle（最快，1-3 天接入）
├─ archetype C + 有 Mercury 预账 → Stripe US（3-7 天）
├─ archetype B 但 HK 公司未注册完 → 先走 Paddle，后迁 Stripe
└─ 无海外主体 → ❌ 停，先开公司，不走"个人 PayPal 归集"（Red Flag 3）

紧迫度 == 1-3 个月
├─ 可以等 Stripe 审批 / 银行开户 → 走首选方案
└─ 并行开两条通道（Stripe + Paddle）增加冗余

紧迫度 == 架构搭完再说
└─ 不单独走本命令，回到 Stage 2/3 主线
```

### 第四层：成本建模（建议呈现）

| GMV/年 | Paddle 5% | Stripe 2.9% | Airwallex 2-3% |
|---|---|---|---|
| $50k | $2500 | $1450 | $1000-1500 |
| $200k | $10k | $5800 | $4000-6000 |
| $1M | $50k | $29k | $20-30k |

> 若年 GMV ≥ $200k 且在 Archetype A → **考虑加急翻红筹到 B 架构 + 换 Stripe**，手续费差额足够覆盖架构搭建成本。

## 输出 schema

```markdown
# 🎯 跨境收款路径推荐

**首推方案**：<Stripe HK / Stripe US / Paddle MoR / ...>
**为什么**：<1-2 句话理由>
**备选方案**：<second choice>
**不推荐**：<with reason>

## 搭建清单（按首推方案）
- [ ] 主体银行开户：<bank name>（预计 <N> 天）
- [ ] 收单账户审核：<Stripe/Paddle/...>（预计 <N> 天）
- [ ] 税务自动化配置：<Stripe Tax / Paddle 自动处理 / 自建>
- [ ] 账单 / 发票模板：<PDF 模板 / 平台自带>
- [ ] 财务记账对接：<手动 / Xero / QuickBooks>

## 💰 成本对照（按你的 GMV 预期 $<X>/年）
| 方案 | 年手续费 | 放款速度 | 合规负担 |
|---|---|---|---|
| 首推 | $<X> | T+<N> | <低/中/高> |
| 备选 | $<X> | T+<N> | <低/中/高> |

## 🚩 红旗（主动触发）
1. <具体红旗 1>
2. <具体红旗 2>

## 下一步
- [ ] 写回 _profile.md (stage_3_output.payment_path_chosen)
- [ ] 若紧迫度高：同步跑 Stage 3 银行开户子流程
- [ ] 若已有个人 PayPal 历史流水：咨询税务师是否需要补申报（Red Flag 3）

## 深入阅读
- 完整矩阵：appendix/payment-matrix.md
- Red Flag 3：modes/red-flags.md
- Stripe Atlas International Guide（官方）
```

## 关键红旗

| # | 红旗 | 判定条件 | 后果 |
|---|---|---|---|
| 1 | **个人 PayPal / 微信归集境外款 + 月流水 > $4k** | Red Flag 3 命中 | 非法结汇 / 逃汇，外管局 5 年追溯，罚 30-50% 涉案金额 |
| 2 | **Archetype A 试图开 Stripe US** | 内资直开海外收单 | 审核必拒，浪费 2-3 周 |
| 3 | **无海外主体但已在跑海外订阅** | 架构滞后于业务 | 立即中止，7 天内搭 MoR 过渡 |
| 4 | **Archetype B 但 HK 公司未开银行就对接 Stripe** | 顺序错 | Stripe 审批卡在"请提供银行证明" |
| 5 | **仅开单通道无冗余** | 订阅制 + 规模 > $1M/年 | Stripe 冻结 = 业务停摆，应双通道 |
| 6 | **To B 开票走 Stripe** | 手续费 2.9% vs wire 固定费 | 每笔亏 2-3% |
| 7 | **MoR 用了但税务未对账** | Paddle 处理 VAT，但国内记账未拉 MoR 报表 | 年底税务口径对不上 |
| 8 | **创始人个人户跑公司钱** | 创始人用个人卡 / PayPal 收公司款 | 个税 + 外管局双风险 |

## 写回 profile

```yaml
stage_3_output:
  payment_path_chosen:
    primary: stripe_hk | stripe_us | paddle | airwallex | ...
    secondary: paddle | null
    rationale: "..."
    estimated_annual_fee_usd: 5800
  payment_setup_deadline: 2026-05-15
  payment_red_flags: [personal_paypal_historical_usage]
  payment_scan_date: 2026-04-21
```

## 限界

- **本命令不代申请 Stripe / 银行账户** — 只做方案选择
- **不覆盖加密货币收款**（USDC / USDT 合规另一套逻辑，建议单独咨询）
- **不判定 VAT / sales tax 税号注册**（欧盟 VAT MOSS / 加州 sales tax 另行处理）
- **不覆盖跨境分账 / 佣金场景的详细结构**（Stripe Connect / Adyen 需专项方案）
