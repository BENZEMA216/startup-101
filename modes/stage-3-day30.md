# Stage 3: Day-30 — 拿到执照后的前 30 天

> last_policy_review: 2026-04-15

## 读取前置状态

从 `_profile.md` 读取：
- `stage_2_output.chosen_path` — 决定本阶段走哪套流程（内资 / WFOE+Cayman+HK / Delaware 单主体…）
- `stage_2_output.wfoe_formed`, `domestic_entity_formed`, `delaware_entity_formed` 等 — 已有哪些实体就对应开户 / 登记
- `stage_2_output.bank_accounts_opened` — 若 partial / no，本阶段决策 1 需深入
- `city` — 决定社保 / 公积金基数 + 代账推荐方向

## 何时进入

- Stage 2 完成：营业执照 / Certificate of Incorporation 已到手
- 章程 / 公章 / 基本文件齐全
- 但银行 / 代账 / 税务登记 / 发票还没跑

## Disclaimer

> ⚠️ 本阶段涉及 **税务登记逾期罚款**、**首次税种核定**、**跨境银行开户合规**。
> 错过时间窗口的代价：滞纳金 / 补缴 / 额度收紧。所有具体申报由会计师 / 代账公司执行，skill 只给清单。

## 按 Archetype 分流

| Archetype | 本阶段重点 |
|---|---|
| A（纯内资） | 国内税务登记 / 代账 / 发票 / 社保 / 税种核定 |
| B（双层出海） | **国内 + 海外两套并行** — WFOE 税务 + Cayman 年维护 + Transfer Pricing 初设 |
| C（创始人已出海） | Delaware / SG 税务 + Mercury / Stripe 开通 + US Payroll |

---

## 决策 1：银行开户

### Archetype A（内资）
- 对公基本户（国内任一银行，推荐招行 / 工行 / 中行）
- 对公一般户（如有其他结算需求）
- 1-3 周
- **必备：** 营业执照 / 公章财务章 / 法人身份证 / 章程

### Archetype B（WFOE + Cayman + HK）
- **WFOE：** 对公人民币户 + 对公美元户（用于接收 HK 汇入的资金）
- **HK Ltd：** Airwallex HK（在线，多币种，可连 Stripe）/ ZA Bank（虚拟银行）/ HSBC Sprint（传统，严）
- **Cayman：** 一般不在 Cayman 开户，直接由 HK 层操作资金
- **注意：** 2023-2026 HK 银行对大陆实控人审查极严。Airwallex / ZA Bank 是新创业者首选

### Archetype C（Delaware C-corp）
- **Mercury**（首选，完全在线，1-3 天）
  - 2024 后对中国实控人加审但仍是主流
  - 被拒怎么办：转 **Brex / Wise Business / Rho / Relay**
- Stripe 账户（收款）
- **若 Mercury 拒：** 准备完整商业证明 — 联创身份 / 业务目标 / 中国研发 subsidiary（如有）解释清楚，重试 2-3 次或转 Wise
- 参考 `appendix/payment-matrix.md`

### 红旗

- 🚩 内资公司拿到执照 30+ 天还没开对公户 → 税务登记逾期风险
- 🚩 Mercury 被拒后硬刚不换备选 → 直接丢 1-2 周 runway

---

## 决策 2：税务登记（内资 + WFOE）

### 时间窗口

**领取营业执照之日起 30 日内** 必须办税务登记。**逾期滞纳金 + 罚款 + 影响企业信用**。

### 材料

- [ ] 营业执照正副本
- [ ] 公章 / 财务章
- [ ] 法人身份证
- [ ] 章程
- [ ] 办公场所证明（租赁合同 / 房产证）
- [ ] 财务负责人任命 + 资格（会计证 or 代账合同）
- [ ] 开户许可证 / 基本户信息

### 一般纳税人 vs 小规模纳税人

| 维度 | 小规模纳税人 | 一般纳税人 |
|---|---|---|
| 增值税率 | 1%（2026 延续 2023 小微优惠）| 6%（服务业） |
| 进项抵扣 | 不能 | 能 |
| 开票 | 普票（小规模也可开专票给一般纳税人） | 专票 |
| 适用 | 年营收 ≤500 万 + 客户多为 C 端 / 小微 | 年营收 >500 万 或 客户要求专票 |

**决策树：**
```
主要客户类型？
├─ ToC / 小微 ToB → 小规模起步 + 享 1% 优惠
├─ 大 ToB（需专票抵扣）→ 一般纳税人
└─ 出海 + 零增值税出口 → 一般纳税人（出口退税要资格）
```

**切换：** 小规模 → 一般纳税人可主动申请或自动（超阈值 12 个月）。反向极难。

### 发票抬头规范

- 不要让员工随便写"某某有限公司" — 必须完整工商登记名称 + 税号 + 地址 + 电话 + 开户行账号
- 一开始就用电子发票（节省邮寄 + 存档自动化）
- **红旗：** 员工经常丢失发票 → 每月对账压力 → 要明确"差旅发票模板"

---

## 决策 3：代账 vs 自记（Archetype A / B 的 WFOE 侧）

### 代账优势
- 月费 300-800 RMB / 月（一线城市）
- 包：月度记账 + 报税 + 年度汇算清缴初稿 + 发票管理
- **早期创业（<10 人）强烈推荐代账**

### 自记优势
- 更懂自己业务
- 更贵（全职会计 10k+/月）
- **10+ 人 + 多实体 + 跨境转让定价** → 考虑自记 + 外部审计

### 推荐类型
- 代账公司（百万选 / 本地小而美 / 猪八戒 / 税务师事务所个人）
- **必问：** 能否处理 WFOE 跨境结汇 / Transfer Pricing / VAT 退税
- **不要贪便宜** — 199/月的代账多数是串号假账风险

---

## 决策 4：Multi-entity accounting（Archetype B 重点）

### WFOE 向 Cayman/HK 的资金流逻辑

```
Cayman（融资 / 持股）
  ↓（股东借款 or 增资）
HK Ltd（中间层）
  ↓（借款 or 服务费付款）
WFOE（国内研发 / 员工）
```

### Transfer Pricing 原则

**WFOE 不是"利润中心"，是"成本中心 + 研发服务中心"。**

常见模式：
- **Cost-plus Service Agreement**：Cayman 委托 WFOE 做研发，WFOE 按"总成本 + 5-15% markup"向 Cayman 开发票
- 这笔服务费通过 HK 层汇入 WFOE 人民币账户 → 结汇
- WFOE 按该收入交 6% 增值税 + 25% 企业所得税（减去人员成本后的净利润）

### 初设 Transfer Pricing 合同要点

- [ ] 服务范围（必须具体：研发 / 测试 / 客服等）
- [ ] 定价方法（Cost+markup 最常见，markup 通常 8-12%）
- [ ] 结算周期（按月 / 按季）
- [ ] 合同币种（推荐 USD，结汇记汇率差）
- [ ] 适用法律（推荐 HK 法）
- [ ] 签署双方：HK Ltd + WFOE，不是 Cayman + WFOE（HK 层便于税收协定）

**2024 后金税四期加码：** 转让定价审查趋严，markup 低于 5% 或高于 20% 都容易被税局关注。**建议 8-12% 为基准带，请税务师定期 benchmark**。

---

## 决策 5：社保 & 公积金（Archetype A / B 的 WFOE 侧）

### 开户时点

- 营业执照后 30 日内
- 与税务登记同步做效率最高

### 险种
- 五险一金：养老 / 医疗 / 失业 / 工伤 / 生育 + 公积金
- 全国各地比例略不同；北京 / 上海 / 深圳为主要运营地参考
- **成本：** 员工月薪的 **约 40-45%**（公司端）+ 员工 ~20% 代扣

### 争议点

- 早期工资可否只交最低基数？
  - **合规答案：** 不行，按实际工资交
  - **现实：** 很多小公司按最低基数申报 → 面临追溯风险 + 员工维权压力
  - **建议：** 尊重法规，成本列入预算；或用"高薪低基 + 奖金"结构折中（灰区，需咨询律师）

---

## 决策 6：US Payroll / International Payroll（Archetype B / C）

### Delaware / SG / HK 主体雇员工

- **Deel / Remote.com / Oyster** = EOR（Employer of Record）
  - $500-700/月/人
  - 无需在目标国开子公司
  - 处理当地工资 + 社保 + 税
- **Deel Engage / Rippling** 可同步 HR + 股权管理

### 自家 Delaware C-corp 雇 US 员工

- **Gusto / Rippling** Payroll
- $40-80/月 + 每雇员 $6-12/月
- 处理 W-2 / 401k / 税务代扣

### 创始人自己从海外主体拿钱

- **顾问费（1099）**：中国税务居民需申报劳务报酬
- **工资（W-2 / 海外 payroll）**：需要当地工签或远程合规
- **分红**：累积到退出时一次性

**建议：** 早期不提工资，融资后再从海外主体 payroll，税务师先 benchmark。

---

## 必查清单

### Archetype A
- [ ] 对公银行账户开通
- [ ] 税务登记（30 日内）
- [ ] 税种核定（一般 vs 小规模）
- [ ] 发票模板 + 领票
- [ ] 代账 / 会计配置
- [ ] 社保公积金开户
- [ ] 首月报税预演

### Archetype B（增量）
- [ ] WFOE 对公美元户
- [ ] HK Ltd Airwallex / ZA Bank
- [ ] Cayman 年维护合约
- [ ] Transfer Pricing 合同（HK ↔ WFOE）
- [ ] 首笔 Cayman → HK → WFOE 资金流打通
- [ ] 37 号文登记证明归档（来自 Stage 2）

### Archetype C
- [ ] Mercury / Brex 开户
- [ ] Stripe 账户
- [ ] EIN（Stage 2 已拿 / 未拿补办）
- [ ] Gusto / Rippling Payroll（如有 US 雇员）
- [ ] 首次季度预估税预估（US 联邦 + 州）
- [ ] QuickBooks / Xero 会计软件

---

## 典型避坑场景

**场景 1：税务登记逾期 60 天**
某 AI 工具小团队拿到执照后忙产品迭代，60 天后才办税务登记。滞纳金 + 罚款合计 2.3 万，信用记录影响未来一般纳税人升级。

**场景 2：一人有限在 Mercury 被拒后硬开**
创始人单人持股 100% WFOE 实控 Delaware C-corp，Mercury 审核拒。**坚持用同一份材料申请 Brex / Rho / Wise，全部被拒，6 周 runway 烧掉。** 最终补一个联创 1% 持股改 HK 层后重试 Wise 通过。

**场景 3：Transfer Pricing markup 0%**
某出海 AI 公司 WFOE 按"零利润"向 Cayman 开票，金税四期大数据预警。税务稽查追溯 3 年补税 + 滞纳金 200 万+，律师费另算。

---

## 红旗扫描（本阶段）

调用 `modes/red-flags.md`，重点：
- Red Flag 3（个人 PayPal 收订阅）— 本阶段必解决
- **新增：逾期税务登记**（未进主红旗清单，但本阶段扫）
- **新增：Transfer Pricing markup 偏离**（Archetype B）

## 推荐阅读

- `appendix/payment-matrix.md` — 银行 / 收款全景
- `appendix/glossary.md` — EOR / MoR / Transfer Pricing
- `references/index/02-incorporation.md` — Stripe Atlas 文档
- Stripe Atlas *International Expansion Guide*

## 本阶段输出（写入 _profile.md）

```yaml
stage_3_output:
  completed_at: <YYYY-MM-DD>
  tax_registration_done: <yes | no | not_applicable>
  bookkeeping_provider: <代账 | 自记 | 混合>
  invoice_setup_done: <yes | no | not_applicable>
  vat_taxpayer_type: <一般纳税人 | 小规模纳税人 | not_applicable>
  social_insurance_setup: <yes | no | not_applicable>
  transfer_pricing_framework_drafted: <yes | no | not_applicable>
```

并在 `completed_stages` 追加 `3`。确认后进入 Stage 4 Hiring & Equity。
