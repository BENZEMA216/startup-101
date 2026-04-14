# Payment Matrix — 出海收款方案决策表

> 用于 Stage 3 (Day-30) 参考。v0.1 版本，Stage 3 文件 v0.2 补。

## 收款方案对比

| 方案 | 主体要求 | 手续费 | 放款速度 | 难度 | 适用 |
|---|---|---|---|---|---|
| **Stripe US** | Delaware C-corp + US 银行 | 2.9% + $0.3 | T+2 | 低 | Archetype C 首选 |
| **Stripe SG/HK** | SG Pte Ltd / HK Ltd | 同上 | T+2/3 | 中 | Archetype B 首选 |
| **Paddle (MoR)** | 任何主体（含内资）| 5% + $0.5 | T+15 左右 | 低 | 内资出海 SaaS 事实标准 |
| **Lemon Squeezy (MoR)** | 任何主体 | 5% + $0.5 | T+30 | 低 | 小规模替代 |
| **支付宝国际 / 微信 HK** | HK/SG 主体 | 2-3% | 较快 | 中 | 华人 C 端 / 覆盖差 |

## 中国内资公司能否收美元订阅？

**能，但必须走 MoR：**
- Paddle / Lemon Squeezy 作为 Merchant of Record 替你接收全球付款 + 处理 VAT / sales tax
- 汇至你内资公司的对公美元户
- 银行结汇入人民币账户
- 手续费比 Stripe 贵 ~1.5x，换取合规

**不能直接：**
- 纯内资公司无法通过 Stripe 审核
- 个人 PayPal 归集 → **红旗 3**

## 银行开户决策

### Delaware C-corp 首选

| 银行 | 特点 | 中国实控人审核 |
|---|---|---|
| **Mercury** | 创业者首选，完全在线 | 2024 后收紧但仍主流 |
| **Brex** | 偏 US 本地化 | 严 |
| **Wise Business** | 多币种 | 相对宽松 |

### 香港公司首选

| 银行 | 特点 |
|---|---|
| **Airwallex** | 在线开户，多币种，可连 Stripe |
| **ZA Bank** | 虚拟银行，2024 后对初创友好 |
| **HSBC Sprint** | 传统严格 |

### 新加坡公司首选

| 银行 | 特点 |
|---|---|
| **Aspire** | 在线，创业友好 |
| **Wise Business SG** | 多币种 |
| **DBS** | 传统，需线下 |

## 跨境薪资方案

| 场景 | 方案 |
|---|---|
| WFOE 给中国员工发工资 | 标准：WFOE 人民币账户 → 员工社保 + 个税代扣 |
| Cayman / Delaware 给海外员工 | **Deel / Remote.com** EOR（雇主替代）服务，$500-700/月/人 |
| 创始人自己从海外主体拿钱 | 顾问费 / 分红 / 工资三种方式，税负差异大，需咨询税务师 |

## 资金回流路径

```
Cayman → HK → WFOE 分红：
  - HK-Mainland 税收协定：5% 预提税
  - Cayman → HK 无税
  - HK → 股东个人：利得税 0%（HK 公司派息免税）
  - 最终股东在中国：20% 个税（分红回中国个人）

Cayman → HK → WFOE 贷款：
  - HK 贷款给 WFOE，WFOE 还本付息
  - 利息受中国预提税 10%
  - 避免分红双重征税
```

## 红旗对照

- 纯内资 + 目标订阅制 + 无 Paddle → **Red Flag 3**
- 已有海外主体但未开 Stripe/Airwallex → 提示 Stage 3 处理
- 月流水 >$50k 仍靠个人 PayPal → 立即中止，搭架构

## 引用

- [Airwallex HK](https://www.airwallex.com/hk)
- [Mercury](https://mercury.com/)
- [Paddle](https://www.paddle.com/)
- [Deel](https://www.deel.com/)
- Stripe Atlas International Expansion Guide
