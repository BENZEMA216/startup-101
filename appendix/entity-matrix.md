# Entity Matrix — 公司架构决策表

> 用于 Stage 1 (前置选择) 和 Stage 2 (注册执行) 参考。

## 六种主流架构

| 架构 | 适用场景 | 设立成本 | 设立时间 | 年维护成本 | 主要红旗 |
|---|---|---|---|---|---|
| **Cayman + HK + WFOE (VIE)** | 计划美元融资 + 中国团队 + 数据/资质敏感行业 | $15k-30k | 4-8 周 | $10k+ | VIE 2021 后灰区 / 37 号文必办 |
| **Cayman + HK + WFOE (非 VIE 红筹)** | 计划美元融资 + 中国团队 + 业务无外资限制 | $10k-20k | 3-6 周 | $8k+ | ODI 审批 / 37 号文 |
| **Delaware C-corp + HK/SG 子公司** | 目标 US VC + 产品在美 | $1k-3k（主体）+ 子公司另算 | 1-2 周（主体） | $3k-5k | C-corp 双重征税 / 可用 QSBS 对冲 |
| **Singapore Pte Ltd** | 东南亚 + 全球用户 + 税务效率 | SGD 3k-5k | 1-2 周 | SGD 3k+ | EP 工签门槛高 / Nominee Director 非长久 |
| **Hong Kong Ltd** | CNH/USD 收款 + 靠近内地 + 优才高才通 | HKD 10k-20k | 2-4 周 | HKD 10k+ | 银行开户 2023 后极严 |
| **纯内资有限公司** | 工具类 / 买断制 / B2B（无订阅收款） | ¥0-500 | 1-2 周 | ¥3-10k（代账） | 不能直连 Stripe / 出海规模化卡死 |
| **BVI 纯控股 SPV** | 股东层隔离 | <$2k | 1-2 周 | $1-2k | 被列入 EU 灰名单 / 部分银行拒接 |

## Archetype → 推荐架构

| Archetype | 首选 | 备选 |
|---|---|---|
| A（纯内资） | 纯内资有限公司 | — |
| B（双层出海） | Cayman + HK + WFOE（非 VIE） | Delaware + HK + WFOE |
| C（创始人已出海） | Delaware C-corp | Singapore Pte Ltd |

## 2024-2026 真实案例

| 公司 | 主实体 | 收款 | 备注 |
|---|---|---|---|
| Manus (Butterfly Effect) | Singapore Pte Ltd | Stripe SG | Benchmark $75M |
| HeyGen | Delaware C-corp | Stripe US | 2023 从深圳迁 LA |
| Opus Clip | Delaware C-corp | Stripe US | a16z 投资 |
| Pika Labs | Delaware C-corp | Stripe US | 斯坦福背景 |
| Dreamina 海外版 | ByteDance Cayman → SG | 字节内部通道 | 走 TikTok 同款 |

**规律：** 2024 后新做的 AI 出海默认 **Delaware 或 Singapore**，新 VIE 越来越少（除非触碰内容/支付牌照）。

## 决策树

```
融美元？
├─ 是 → 研发在中国？
│       ├─ 是 → Cayman + HK + WFOE（非 VIE）
│       └─ 否 → Delaware C-corp 或 SG Pte Ltd
└─ 否 → 订阅制 / 海外用户 >30%？
        ├─ 是 → HK Ltd + Paddle MoR / SG Pte Ltd
        └─ 否 → 纯内资有限公司
```

## 关键决策点的细节

### Cayman vs Delaware（美元路径二选一）

| 维度 | Cayman + WFOE | Delaware C-corp |
|---|---|---|
| 税 | Cayman 0% 公司税，但分红层层抽成 | 联邦 21% + 州税，**QSBS 5 年持有豁免最高 $10M 资本利得** |
| 融资 | 美元基金主流接受 | 美元基金原生路径 |
| 上市 | 香港 / 美股灵活 | 美股最顺 |
| 中国团队 | WFOE 下一层容易 | 需要单独搭 WFOE |
| 监管 | CFIUS 审查压力（2024-2026 加剧）| 同样 CFIUS，但结构简单些 |
| 成本 | 高 | 低 |

### SG vs HK（东南亚/全球枢纽二选一）

| 维度 | Singapore Pte Ltd | Hong Kong Ltd |
|---|---|---|
| 税 | 17% + Startup Tax Exemption 前三年大幅减免 | 两级 8.25% / 16.5% |
| 开户 | EP 工签门槛高（COMPASS SGD 5.6k+）| 亲赴 + 业务证明，2023 后极严 |
| 基金偏好 | Antler / 东南亚系基金 | 内地美元基金 |
| 人才 | EP 困难 | 优才/高才通 + 7 年永居 |

## 翻红筹成本

从内资 → 红筹（Cayman 架构）重组：
- 时间：6-12 个月
- 费用：5-15% 的估值（税 + 律师费 + 会计师费）
- 关键阻力：ODI 审批、37 号文、国资/外资关联交易

**结论：** 如果预计融美元，**搭架构前置** 永远比融资后翻红筹便宜。

## 引用

- [The Information — Manus Raising $75M](https://www.theinformation.com/articles/manus-ai-raising-75-million-funding-round-benchmark)
- [YC SAFE Documents](https://www.ycombinator.com/documents)
- [Stripe Atlas Guides](https://stripe.com/atlas/guides)
- [IRC §1202 QSBS（美国国税局）](https://www.irs.gov/)
- 石头《融资指南》§11「中国 AI 公司出海的常用架构」
