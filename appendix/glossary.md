# Glossary — 术语表

> last_policy_review: 2026-04-15

## 架构 & 实体

**VIE（Variable Interest Entity）** — 可变利益实体。境外上市主体通过协议控制境内运营主体的架构。2021 后新设 VIE 灰区，多数 AI 公司选择"非 VIE 红筹"。

**红筹架构（Red-Chip）** — 中国业务 + 境外控股公司 + 境外上市。"非 VIE 红筹"指境外主体经 WFOE 股权直接控股境内业务，不依赖协议控制。

**Cayman 三明治** — 典型红筹层级：Cayman 母公司 → BVI 中间层 → HK 中间层 → WFOE 境内。

**WFOE（Wholly Foreign-Owned Enterprise）** — 外商独资企业。境外公司 100% 持股的中国境内子公司。

**SPV（Special Purpose Vehicle）** — 特殊目的公司。股东层持股 / 投融资专用壳公司，常在 BVI / Cayman 设立。

**ODI（Outbound Direct Investment）** — 境外直接投资备案。中国主体对外投资需发改委 + 商务部 + 外管局三件套。2024 后 AI 行业 ODI 审批趋严。

**BVI** — British Virgin Islands，英属维京群岛。典型股东层 SPV 设立地，税率 0、保密度高。2024 年起部分被列入欧盟灰名单。

**C-corp / S-corp / LLC** — 美国公司三种形态。**Delaware C-corp** 是创业融资事实标准（QSBS 仅限 C-corp）。

**Pte Ltd** — Private Limited。Singapore 标准公司形态。

**Nominee Director** — 挂名董事。Singapore 公司无本地居民董事时临时使用，非长久方案。

---

## 合规 & 监管

**37 号文** — 《国家外汇管理局关于境内居民通过特殊目的公司境外投融资及返程投资外汇管理有关问题的通知》（汇发〔2014〕37 号）。中国居民设立境外 SPV 持境内权益前必办外汇登记。不办 → 分红 / 退出汇不回。

**PIPL（Personal Information Protection Law）** — 《个人信息保护法》2021。中国版 GDPR。

**DSL（Data Security Law）** — 《数据安全法》2021。重要数据 / 核心数据定义基础。

**CSL（Cybersecurity Law）** — 《网络安全法》2017，2026-01-01 修订生效，新增 AI 治理条款（第 20 条）。

**PIPL 出境** — PI 出境需走 "安全评估 / SCC 备案 / 认证" 三选一（2024-03 CAC 新规）。阈值见 compliance-matrix.md。

**SCC（Standard Contractual Clauses）** — 标准合同条款。中国 / 欧盟都有各自版本，用于跨境数据传输合规。

**GDPR（General Data Protection Regulation）** — 欧盟数据保护通用条例。2018 生效。

**Art. 27** — GDPR 第 27 条。非欧盟公司处理欧盟用户 PI 必须指定欧盟代表。

**Art. 50（EU AI Act）** — AI 系统透明度义务。AI 生成内容标识、用户知情 AI 交互。2026-08-02 生效。

**GPAI（General-Purpose AI）** — 通用目的 AI 模型。EU AI Act 定义的基础模型类别，Provider 有额外义务（训练数据摘要 + 版权政策 + 下游披露）。2025-08-02 起生效。

**Code of Practice（AI Act）** — 非强制但可作为 GPAI Provider 的 compliance pathway。签约 → 推定符合。

**算法备案** — 互联网信息服务算法备案。向网信办报告算法情况并公示。

**大模型备案** — 自研生成式 AI 模型面向公众服务需进行的备案（含专家评审）。

**大模型登记** — 调 API 非自研的轻型备案变体。

**深度合成备案** — 人脸 / 语音 / 数字人等独立算法备案轨道。

**CFIUS（Committee on Foreign Investment in the United States）** — 美国外资投资委员会。中国背景创业者 + AI + US VC → 三要素常触发 CFIUS 审查。

**CCPA / CPRA** — 加州消费者隐私法 / 加州隐私权法。2023-01 CPRA 扩展 B2B + 员工数据保护。

**Colorado AI Act** — 美国首部通用 AI 法（SB24-205）。生效延至 **2026-06-30**。核心是"consequential decision" AI 系统的 impact assessment。

**SB-53 (TFAIA)** — California Transparency in Frontier AI Act，2026-01-01 生效。frontier 大模型方需公示 AI framework + 年度更新 + 事件报告。

---

## 融资 & 股权

**SAFE（Simple Agreement for Future Equity）** — YC 发明，简单未来股权协议。种子 / 天使标准工具。

**YC Post-Money SAFE** — 2018 更新版。稀释计算对创始人更友好。

**Valuation Cap** — 估值上限。SAFE 两种定价机制之一。

**Discount（SAFE）** — 下轮估值折扣，SAFE 另一种定价机制（或与 Cap 并用）。

**MFN（Most Favored Nation）** — 最惠国待遇条款。SAFE 中允许后来者更优条款传导至先到的 SAFE 投资人。

**Convertible Note** — 可转债。有到期日 + 利息 + 转股触发。

**Priced Round** — 股权直投轮。A 轮及之后常见，需明确估值 + Term Sheet + SPA。

**Term Sheet（TS）** — 投资条款清单。非完全 binding 但实质决定最终条款。

**SPA（Share Purchase Agreement）** — 股权购买协议。TS 之后的正式文件。

**DD（Due Diligence）** — 尽职调查。法律 DD / 财务 DD / 业务 DD 三路并行。

**IC（Investment Committee）** — 基金投委会。TS 之前最后决策环节。

**Vesting** — 股权成熟机制。典型 4 年 + 1 年 cliff。

**Cliff** — 悬崖期。通常 1 年。1 年内离开 = 0 股权。

**Single-trigger Acceleration** — 单触发加速。并购/控制权变更时 vesting 自动全部到期。

**Double-trigger Acceleration** — 双触发加速。并购 + 离职 两项同时触发才加速。**双触发更中性，对投资人更友好**。

**Good Leaver / Bad Leaver** — 好离开 / 坏离开。影响已 vest 股权的回购 / 保留。

**Liquidation Preference** — 优先清算权。投资人在退出时优先拿回本金或其倍数。**1x non-participating 是标配**。

**Participating Preferred** — 参与分配型优先股。拿完优先清算后仍按股比参与剩余分配（"两吃"）。对创始人不利。

**Pari Passu** — 同顺位。多轮投资人清算顺序平等（而非后进先出）。

**Protective Provisions** — 保护性条款 / 一票否决权。范围必须精确限定。

**Drag-along** — 拖售权。多数股东可强制少数跟随卖公司。需设触发阈值 + 最低估值。

**Tag-along** — 共售权。少数股东可跟创始人 / 大股东一起卖。

**Full Ratchet** — 完全棘轮反稀释。对创始人最不利。🚩 坚决拒。

**Weighted Average（Narrow / Broad-based）** — 加权平均反稀释。**Broad-based 是业界 65% 采用的健康区**。

**Redemption** — 回购。2021-2024 中国 AI 公司的重灾区。**创始人个人连带回购 = 死刑条款**。

**Drop-away** — 失效条款。回购 / 对赌可设公司达到某里程碑后自动失效。

**Basket（回购条款）** — 篮子条款。需一定比例投资人同时触发才生效。

---

## 税 & 跨境

**QSBS（Qualified Small Business Stock）** — IRC §1202。Delaware C-corp 持股 5 年 + 公司资产 ≤$50M → 资本利得豁免最高 $10M。**C-corp 独享**。

**83(b) Election** — IRS 选举。Restricted stock 发行 30 天内必提交，锁定按授予时 market value 计税，避免每次 vest 都计税。**漏了 = 百万美元级损失**。

**FBAR（FinCEN Form 114）** — Foreign Bank Account Report。US Person（公民 / 绿卡 / 税务居民）海外账户合计 >$10k 需年度申报。**漏报单次罚款 $10k-100k，故意漏报更重**。

**FATCA** — 美国海外账户税务合规法案。非美金融机构对美国人账户披露。

**MoR（Merchant of Record）** — 商户代表。Paddle / Lemon Squeezy 替你处理全球付款 + VAT + sales tax。纯内资公司出海收款事实标准。

**EOR（Employer of Record）** — 雇主代表。Deel / Remote.com 替你雇海外员工（无需当地主体）。

**Transfer Pricing（转让定价）** — 跨境关联交易定价。Cayman ↔ WFOE 间的服务费 / 特许权使用费需符合独立交易原则，Cost+markup 典型 8-15%。

**Exit Tax** — 美国公民 / 绿卡放弃身份时的一次性清算税。创始人融资后才放绿卡 → 可能触发。

---

## AI 技术术语（skill 场景需）

**Llama Community License** — Meta 发布的自定义许可。核心限制：**7 亿月活上限** + **不得用 Llama 输出训练改进其他 LLM**。

**Apache 2.0** — 商业友好开源许可。Qwen / DeepSeek / Mistral 部分版本采用。无月活上限。

**AGPL** — Affero GPL。**SaaS 闭源杀手**：通过网络提供服务也视为"分发"，需开源。

**Prompt Injection** — 提示词注入。Simon Willison 命名。LLM 安全首要威胁类。

**Red Team** — 红队测试。大模型备案 / Frontier AI 常见义务。

**RAG** — Retrieval-Augmented Generation。

**System Prompt** — 系统提示词。合规中常作为 safety guardrail 载体。

---

## Misc

**Archetype A / B / C** — 本 skill 自定义创业者分流：A 纯内资 / B 双层出海 / C 创始人已出海。

**Disclaimer** — 免责声明。本 skill 每个 stage 入口必展示。

**第三方代表（Article 27 rep）** — 非欧盟公司委托的欧盟代表实体。Prighter / VeraSafe / EDPO 是典型服务商。

**国密算法 / 商密等级保护** — 中国本土网络安全等级保护标准（等保 2.0）。大模型备案常要求 3 级。
