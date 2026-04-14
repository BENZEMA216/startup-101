# Stage 2: Incorporation — 注册执行

> last_policy_review: 2026-04-15

## 何时进入

- Stage 1 完成：架构路径已定
- 准备执行注册

## Disclaimer

> ⚠️ 本阶段涉及多司法管辖区注册、章程起草、37 号文等硬合规动作。
> **必须找跨境律所执行，不要自己跑代办。**

## 五条架构分支

选你的路径：

- [Path A] 纯内资有限公司
- [Path B1] Cayman + HK + WFOE（非 VIE 红筹）— Archetype B 首选
- [Path B2] Delaware C-corp + HK/SG 子公司 + WFOE — Archetype B 备选
- [Path C1] Delaware C-corp 单主体 — Archetype C 首选
- [Path C2] Singapore Pte Ltd 单主体 — Archetype C 备选

---

## Path A：纯内资有限公司

### 必查清单

- [ ] 核名通过（建议备 5 个名字，避免重复）
- [ ] 注册地址
  - 实际办公地址（商用办公楼最佳，能开租金发票）
  - 不要贪税收洼地，运营地注册即可（2024 后洼地压缩中）
  - 住宅地址需备案并交租赁税
- [ ] 注册资本（认缴制，建议 10-100 万 RMB，不要过高）
- [ ] 经营范围
  - **必含 AI 相关**：技术开发、技术服务、软件开发、人工智能算法研发等
  - 不含需要牌照的（增值电信 / 金融 / 医疗等）除非你有牌照
- [ ] 股东 + 法人 + 监事配置（一人有限的风险见下文）
- [ ] 章程
- [ ] 公章 / 财务章 / 发票章 / 合同章 / 法人章（**不要自己保管全部章**，分权）
- [ ] 营业执照

### 关键决策

**一人有限 vs 多股东有限：**
- 一人有限股东在公司破产清算时**承担无限连带责任**（个人资产被追索）
- 多股东有限（哪怕只持 1%）就没这个风险
- **强烈建议找一个信任的人持 1-5%**

### 时间线

- 核名：1-3 天
- 工商注册：3-7 天
- 刻章：1-2 天
- 银行开户：见 Stage 3

### 红旗

- 🚩 一人有限（无限连带）
- 🚩 经营范围漏 AI 类目（影响后续算法备案主体适格）
- 🚩 住宅地址不备案（查得越来越严）

---

## Path B1：Cayman + HK + WFOE（红筹）

### 架构图

```
创始人（中国）
   ↓ 持股
Cayman 母公司（融资 / 上市主体）
   ↓ 100% 持股
HK Ltd（中间层，享 HK-中国税收协定）
   ↓ 100% 持股
WFOE（深圳/上海/北京，承担中国研发 + 员工）
```

### 必查清单

- [ ] **注册律所选型**（跨境经验必备）
- [ ] Cayman 公司设立
  - Registered Office + Registered Agent
  - 授权股本（通常 50,000 股）
  - 章程 + 董事（至少 1 名，可以是创始人）
  - 预计费用 $5-10k + 年维护 $3-5k
- [ ] **37 号文登记**（⚠️ 红旗 1）
  - 创始人作为中国居民持有 Cayman 股份前必办
  - 登记主体：户籍地外管局
  - 时间：通常 1-3 个月
- [ ] HK Ltd 设立
  - 1 名董事（可以是创始人）
  - 公司秘书（必须 HK 居民，可外包）
  - 注册地址（可外包）
  - 预计费用 HKD 10-20k
- [ ] **ODI 备案**（Cayman/HK 如何投资 WFOE）
  - 发改委 + 商务部 + 外管局三件套
  - 2024 后 AI 行业审批偏紧，2-6 个月
- [ ] WFOE 设立
  - 由 HK Ltd 100% 持股
  - 内资有限公司流程 + 外资登记
  - 时间 1-3 个月（含 ODI）
- [ ] **股份权证 + 股东协议**（在 Cayman 层）
- [ ] 章程 / 董事会决议模板

### 关键决策

**创始人 Cayman 持股方式：**
- 直接持股 → 退出交易结构简单，但个人税负高
- SPV（BVI）持股 → 保护 + 隔离，但多一层结构
- 推荐：早期直接持股，B 轮后再做 SPV

**期权池：**
- 在 Cayman 层设立（不是 WFOE）
- 典型 10-15%
- Vesting 条款写进 Cayman 章程
- **中国员工期权：间接持股 SPV + 37 号文**（见 Stage 4）

### 时间线

- Cayman + HK：4-8 周
- 37 号文：1-3 个月（并行）
- ODI：2-6 个月
- WFOE：1-3 个月（在 ODI 后）
- **总计：3-6 个月**

### 红旗

- 🚩 **Red Flag 1: 37 号文未办** — 本阶段最关键动作
- 🚩 ODI 未备案直接注资 WFOE — 外管局违规
- 🚩 Cayman 选用模板章程不改反稀释条款 — 后续融资吃亏

---

## Path B2：Delaware C-corp + HK/SG + WFOE

类似 B1 但顶层换成 Delaware C-corp。

### 差异要点

- Delaware 本身成本低（~$500 + Stripe Atlas $500，1 周）
- **但整体结构比 Cayman 复杂**：Delaware → HK → WFOE 需走 ODI
- 用 Delaware 作顶层通常意味着瞄准美股上市 + 有美国股东
- QSBS 豁免需要创始人持股 Delaware 主体 5 年 + 资产 ≤$50M

### 何时选 B2 而非 B1

- 核心投资人已锁定 a16z / Sequoia US 等 US VC
- 目标美股上市
- 创始人有美国税籍考虑

---

## Path C1：Delaware C-corp 单主体

### 必查清单

- [ ] 用 **Stripe Atlas** 或 Clerky 注册（$500-1000，1-2 周）
- [ ] 获得 EIN（雇主识别号，注册即免费）
- [ ] 开 Mercury 银行账户
- [ ] 注册 Stripe（收款）
- [ ] 股权发行 + **83(b) 选举 30 天内必做**（否则 vesting 期每年按 market value 交税）
- [ ] 章程（Certificate of Incorporation）+ Bylaws + Stockholders Agreement（Cooley GO 模板）
- [ ] 首次董事会决议

### 关键决策

**83(b) 选举：**
- 创始人拿到 restricted stock 30 天内必须向 IRS 提交 83(b)
- 否则后续 vesting 期每次 vest 按 market value 交个税
- **漏了就是百万美元级损失**

**QSBS 资格：**
- IRC §1202：持股 5 年 + 公司资产 ≤$50M → 资本利得豁免最高 $10M
- Delaware C-corp 是唯一资格（LLC/S-corp 不行）

### 时间线

- Stripe Atlas 注册：1-2 周
- EIN：即时到 1 周
- Mercury 开户：1-3 天
- 整体：**2 周内**

---

## Path C2：Singapore Pte Ltd 单主体

### 必查清单

- [ ] 至少 1 名新加坡居民董事（PR 或 EP 持有人或 Nominee Director）
- [ ] 注册资本（$1 起，建议 S$1000-10000）
- [ ] 章程（ACRA 提供模板）
- [ ] 公司秘书（6 个月内必须有，可外包）
- [ ] 开 Aspire / Wise Business SG 账户
- [ ] 考虑：Startup Tax Exemption（前 3 年大幅减免）

### 关键决策

**Nominee Director：**
- 不是长久之计：每年 SGD 2-3k，隐形风险（Nominee 可以做很多损害公司的事）
- 长久方案：创始人自己申 EP（2024 后门槛 COMPASS SGD 5.6k+ 起，难度上升）

### 时间线

- 1-2 周

---

## 红旗扫描（本阶段）

调用 `modes/red-flags.md`，重点：
- Red Flag 1（37 号文）— Path B 必扫
- 经营范围漏 AI 类目（Path A 特有）

## 推荐阅读

- `appendix/entity-matrix.md`
- `references/index/02-incorporation.md`
  - Stripe Atlas Incorporation Guide
  - Cooley GO Starter Documents
  - Index Ventures Founder Handbook
- 石头《融资指南》§11 出海架构章节

## 本阶段结束状态

用户持有：
1. 营业执照 / Certificate of Incorporation
2. 章程（中英）
3. 股东协议（联创 vesting + IP）
4. 公司所有公章（Path A）/ 公司印鉴（Path B/C）
5. 37 号文登记证明（Path B）
6. ODI 备案证明（Path B）
7. 银行开户预约或已开户

确认后进入 Stage 3 Day-30。
