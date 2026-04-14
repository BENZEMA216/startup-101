# Shared Rules (_shared.md)

> 本文件定义 startup-101 的全局规则、7 阶段定义、disclaimer 文案。所有 stage 和 mode 文件 MUST 加载此文件。

## Disclaimer（每个阶段入口必须展示）

> ⚠️ startup-101 不是律师 / 会计师 / 税务师意见。
> 所有具体决策必须由专业机构二次确认。
> 政策变化快（尤其 AI 合规、跨境数据、EU AI Act），请交叉验证最新信息。

## 7 阶段定义

| Stage | 名称 | 进入条件 | 核心交付物 |
|---|---|---|---|
| 1 | Pre-incorporation | 还没注册公司 | 联创协议 / 股权初分 / 架构选择 |
| 2 | Incorporation | 决定架构，准备注册 | 执照 + 章程 + 公章 + 开户 |
| 3 | Day-30 | 刚拿到执照 | 税务登记 / 代账 / 发票规范 / 社保 |
| 4 | Hiring & Equity | 要招人、发期权 | ESOP 文件 / 劳动合同 / IP Assignment |
| 5 | AI 产品上线前 | 产品将 go-live | 算法备案 / GDPR / AI Act / PIPL 出境 |
| 6 | Fundraising | 准备融资 | BP / Termsheet 审阅 / SAFE / 条款红线 |
| 7 | Ongoing | 已融完 | 月/季/年报 / 审计 / 转让定价 / GPAI 年检 |

## 3 档 Archetype

| Archetype | 判定 | 推荐路径 |
|---|---|---|
| A. 纯内资 | ≥70% 中国用户 + 不融美元 + 非订阅出海 | 内资有限 → 国内合规 → 人民币基金 |
| B. 双层出海（默认） | 研发在中国 + 用户全球或美元融资 | Cayman/SG + WFOE / Delaware + HK / 37号文 + ODI |
| C. 创始人已出海 | 创始人已在海外 + 研发分布式 | 纯 Delaware C-corp / SG Pte Ltd / Mercury / QSBS |

## 6 条红旗清单（跨阶段主动扫描）

1. **37 号文未办** — 中国居民境外 SPV 持境内权益未登记 → 分红/退出汇不回
2. **IP Assignment 未指向海外主体** — 融资 DD 爆雷
3. **个人 PayPal/微信收订阅规模化** — >$50k/年 涉嫌非法结汇
4. **Llama Community License 违规** — 月活 7 亿上限 / 不得改进其他 LLM
5. **AGPL 污染** — 传染 SaaS 闭源代码
6. **EU 无 Art. 27 代表** — 欧盟用户 >0 必须有欧盟代表

## Skill 路由原则

- 每次调用先读 `_profile.md`（用户当前目录）
- 未完成 profile → 跳 stage-0-profile.md
- 已完成 → 根据 `current_stage` 字段或用户选择进入对应 stage
- 每个 stage 结束后 append 结果到 profile，询问是否继续

## 引用策略

- 内置全文仅限 License 清楚的资源（见 references/README.md）
- 其他一律通过 references/index/ 做摘要 + URL
- 用户本地 clip（如 Obsidian）通过环境变量 `$OBSIDIAN_CLIPPINGS` 引用，开源版剔除
