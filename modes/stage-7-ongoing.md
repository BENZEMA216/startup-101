# Stage 7: Ongoing — 持续义务

> last_policy_review: 2026-04-15

## 读取前置状态

从 `_profile.md` 读取：
- `stage_2_output.chosen_path` — 决定要维护哪套实体的持续义务
- `stage_2_output.wfoe_formed` / `hk_entity_formed` / `delaware_entity_formed` 等 — 各实体年报 / 审计日历
- `stage_3_output.transfer_pricing_framework_drafted` — 若 no，本阶段要补
- `stage_5_output.eu_ai_act_gpai_trigger` — 若 yes，需加入 GPAI 年检日历
- `stage_6_output.closed` + `amount_raised` — 决定 FBAR / Form 5472 / 对赌对接节奏
- `founders_tax_residency` — FBAR / 个税汇算口径

## 何时进入

- 融资完成（Stage 6 完成）或 产品稳定运营 6+ 个月
- 公司运营进入"稳态"，但合规义务按月/季/年持续

## Disclaimer

> ⚠️ 本阶段义务繁琐但**错过任何一项都可能引发重大问题**（罚款 / 信用 / 融资下一轮阻碍）。
> 一次性建立 **合规日历**（月/季/年）是最有效的投入。

## Ongoing 日历概览

| 周期 | 国内 | 海外（Archetype B/C） |
|---|---|---|
| **月** | 增值税 / 附加税申报 / 发票 / 社保公积金 | US：州 payroll tax（如 CA） |
| **季** | 企业所得税预缴 / 个税申报 | US：Estimated tax / SG GST |
| **半年** | 金税期末核对 | — |
| **年** | 企业所得税汇算清缴 / 个税汇算 / 工商年报 / 统计 / 审计 | 年度审计 / 年报 / GPAI 训练摘要更新 / 转让定价文档 |
| **不定期** | 算法备案 / 大模型备案重大变更 | FBAR / CFIUS 后续披露 / AI Act 事件报告 |

---

## 1. 月度义务（国内）

### 税
- 增值税 + 附加税：次月 15 日前申报（按月 或 按季，取决于小规模/一般纳税人）
- 企业所得税按季预缴 → 详见"季度"
- 个税代扣：次月 15 日前

### 发票
- 当月开票数据与销项税核对
- 进项发票认证（一般纳税人）

### 社保 + 公积金
- 当月缴费

### 工具
- 代账公司通常覆盖全部流程
- 自用：金税盘 / 税控盘

---

## 2. 季度义务

### 国内
- 企业所得税预缴（季度末次月 15 日前）
- 小微企业优惠：年利润 ≤300 万部分按 5% 优惠
- 统计 / 行业季报（如适用）

### 海外（US）
- Delaware franchise tax（年度 3 月 1 日，非季度，但提前规划）
- Estimated tax payments（4 次 / 年：Q1 Q2 Q3 Q4）

### SG GST
- 年营业额 >SGD 1M 须登记 GST，按季申报

---

## 3. 年度义务（最重）

### 国内

#### 企业所得税汇算清缴
- 次年 5 月 31 日前
- 大修项：纳税调增 / 调减 / 应纳税所得额重计

#### 个税汇算清缴
- 次年 3-6 月
- 创始人 / 高管综合所得

#### 工商年报
- 次年 **6 月 30 日** 前网上申报
- 漏报 → 经营异常名录 → 影响融资 DD

#### 外资企业年检 / 联合年报（WFOE）
- 工商 + 外汇 + 商务 + 统计 + 海关（如涉）五合一
- 每年 6 月 30 日前

#### 审计（WFOE）
- 外资企业必须年度审计（本土会计师事务所）
- 出具审计报告附工商年报

### Hong Kong

#### Profits Tax Return
- 年度，通常每年 4-5 月发出
- 需附审计报告（HK 法定审计）

#### Annual Return (NAR1)
- 周年日后 42 天内
- 公司秘书办理

### Singapore

#### Annual Return
- ACRA，财年结束后 7 个月内

#### Corporate Tax Return (Form C-S/C)
- 每年 11 月 30 日前
- **Small Company 审计豁免条件**（满足 2 项）：
  1. 总营收 ≤SGD 10M
  2. 总资产 ≤SGD 10M
  3. 员工 ≤50 人
- 不满足 → 法定审计

### Cayman

#### Annual Return + Government Fee
- 1 月底前，$800-1000 级
- 通常不做法定审计（除非 fund 架构 / 上市准备）

### Delaware

#### Annual Report + Franchise Tax
- 每年 3 月 1 日前
- Franchise tax 计算复杂（授权股本法 或 资产法，取低者）
- 典型 $400-8000（早期创业公司通常 $400-800）

#### Federal Corporate Tax Return (Form 1120)
- 每年 4 月 15 日前
- 亏损可结转

---

## 4. 转让定价年度（Archetype B 关键）

### 合同维护
- WFOE ↔ HK Ltd Cost+markup 服务协议每年续签或 reaffirm
- Markup benchmark 年度复核（推荐 8-12%，行业基准）

### 同期资料 Master File / Local File
- 关联交易年度 >4000 万 或 合计 >2 亿 RMB → 准备同期资料
- 金税四期 2024+ 加码，要求电子化提交
- 税务师出具

### 红旗
- 🚩 markup <5% 或 >20% 长期保持
- 🚩 服务内容描述泛化（"综合服务"）→ 税局不认

---

## 5. FBAR / FATCA（Archetype C / 美国税籍创始人）

### FBAR（FinCEN Form 114）

- US Person（公民 / 绿卡 / 税务居民）
- 海外账户合计 >$10k 任意时点
- 每年 4 月 15 日前（自动延至 10 月 15 日）
- **独立于报税，不申报 FinCEN 处罚 $10k-100k/次**

### Form 8938 (FATCA)
- 与报税同交
- 海外金融资产阈值（单身 $50k / 联合 $100k）

### 场景
- 公司是 Delaware 但创始人在新加坡持有 Aspire + Cayman 持有 BVI → FBAR + 8938 并用
- 创始人拿绿卡未申报 → 放弃时一次性 exit tax 风险

---

## 6. AI 相关持续义务

### 算法备案 / 大模型备案重大变更

**触发：** 算法机制重大变化 / 应用场景扩展 / 模型主版本升级 / 数据来源重大变化 / 主体变更

**动作：** 30 日内提交变更申报。审核周期同初次。

### EU AI Act GPAI 年度义务（自研模型）

- **训练数据摘要** 至少年度更新（新增训练 / 重要 fine-tune）
- **下游 Incident Reporting** — 严重 incident 必须按规定窗口上报（days-to-weeks）
- Code of Practice 签约方：按 Code 频率做 safety review

### Art. 50 运营合规（2026-08 起）
- 标识水印持续嵌入
- 用户交互界面 AI 告知语 UI 审阅

### PIPL 出境有效期维护
- 安评 / SCC 备案：3 年有效
- 到期前 3 个月开始重新申报

### 网络安全法修订（2026-01-01 生效）
- AI 伦理 / 风险评估成为法定责任
- 定期风险监测 + 事件上报机制建立

---

## 7. 投后关系管理（融完的下一步）

### 参考石头《融资指南》§12

- 月度 / 季度 update email（模板：KPIs + 重大事件 + ask）
- 董事会会议（通常季度 1 次）
- 财务数据披露（按 SPA 条款）
- **关键：主动沟通比 VC 追着问好得多**

### a16z 16 Startup Metrics（推荐看板）

- Bookings / Revenue / ARR / MRR
- GM / Contribution Margin
- CAC / LTV / Payback Period
- Churn / NRR / GRR
- Burn / Runway
- Active Users (DAU/MAU)
- Engagement
- TCV

`references/index/04-ai-tech.md` 有详细摘要。

---

## 必查清单

### Archetype A
- [ ] 月度税务 / 发票 / 社保（代账）
- [ ] 季度所得税预缴
- [ ] 年度汇算清缴（次年 5-31）
- [ ] 工商年报（次年 6-30）
- [ ] 算法备案变更（如有）

### Archetype B（增量）
- [ ] WFOE 年度审计 + 联合年报
- [ ] HK Profits Tax + Annual Return
- [ ] Cayman Annual Return + Government Fee
- [ ] 转让定价同期资料（若超阈值）
- [ ] 37 号文变更登记（若股权 / SPV 结构变化）
- [ ] GPAI 训练摘要年度更新 + 下游事件上报
- [ ] PIPL 出境有效期追踪

### Archetype C（增量）
- [ ] Delaware Annual Report + Franchise Tax
- [ ] Form 1120 + 州 tax return
- [ ] FBAR（个人） + Form 8938
- [ ] SG / HK 子公司相应年报
- [ ] SB-53 Frontier AI Framework 年度更新（若触发）

---

## 典型避坑场景

**场景 1：工商年报漏报进经营异常名录**
某 AI 公司 2024 年中想融 A 轮，DD 时发现 2023 年 WFOE 工商年报漏报 → 经营异常名录 3 个月。VC 要求先恢复再打款。

**场景 2：转让定价 markup 0% 被金税四期预警**
某出海 AI 公司 WFOE 常年"零利润"服务开票。2025 金税四期大数据预警 → 3 年追溯补税 200 万+。

**场景 3：创始人 FBAR 漏报**
某 Delaware C-corp 创始人是绿卡持有人，2021-2024 四年 FBAR 漏报。IRS 追溯 → 每年 $10k 单次罚款 × 4 年 = $40k + 律师费。

**场景 4：GPAI 训练数据摘要未更新**
某中国基模出海后 2026 做了一次大 fine-tune 但未更新 AI Act 训练摘要 → 欧盟投诉举报 → 处理周期 3 个月 + 欧洲客户流失。

---

## 红旗扫描（本阶段）

调用 `modes/red-flags.md`，但本阶段新增持续义务红旗（未入 6 条主清单）：

- 🚩 工商年报漏报（经营异常名录）
- 🚩 转让定价 markup 长期偏离
- 🚩 FBAR 漏报（US Person）
- 🚩 GPAI 训练数据摘要未年度更新
- 🚩 算法备案重大变更未 30 日内报

## 推荐阅读

- `references/index/04-ai-tech.md` — a16z 16 metrics / Bessemer State of Cloud
- `references/index/07-cross-border.md` — EU AI Act Incident Reporting
- 石头《融资指南》§12 投后关系管理
- [Bessemer State of the Cloud](https://www.bvp.com/atlas/state-of-the-cloud)
- [a16z 16 Startup Metrics](https://a16z.com/16-startup-metrics/)

## 合规日历模板（建议创建）

用户目录下生成 `startup-compliance-calendar.md`：

```markdown
# 合规日历 — YYYY

## 月度
- [ ] 每月 15 日：增值税 / 附加税申报（上月）
- [ ] 每月 15 日：个税代扣申报
- [ ] 每月 20 日：社保 + 公积金

## 季度
- [ ] 季度末次月 15 日：企业所得税预缴

## 年度
- [ ] 3-31：HK Profits Tax Filing（如适用）
- [ ] 3-31：Delaware Annual Report & Franchise Tax
- [ ] 4-15：US Federal Tax Return
- [ ] 5-31：企业所得税汇算清缴
- [ ] 6-30：工商年报（WFOE 联合年报）
- [ ] 10-15：FBAR 延期截止
- [ ] 11-30：SG Form C-S

## 不定期
- [ ] 算法备案重大变更 → 30 日内申报
- [ ] GPAI 下游严重事件 → 按规定窗口上报
- [ ] PIPL 出境 3 年到期前 3 个月复核
```

## 本阶段输出（写入 _profile.md）

Stage 7 没有一次性"结束"— 建议每年度末运行一次本 stage，更新如下 section：

```yaml
stage_7_output:
  completed_at: <YYYY-MM-DD>   # 本轮更新时间
  monthly_cadence_set: <yes | no>
  quarterly_cadence_set: <yes | no>
  annual_filings_done:
    cit_settlement: <yes | no | not_applicable>
    iit_settlement: <yes | no | not_applicable>
    annual_report_aic: <yes | no | not_applicable>
    wfoe_joint_annual: <yes | no | not_applicable>
    wfoe_audit: <yes | no | not_applicable>
    hk_audit: <yes | no | not_applicable>
    sg_acra_ar: <yes | no | not_applicable>
    delaware_franchise_tax: <yes | no | not_applicable>
    form_5472: <yes | no | not_applicable>
    fbar: <yes | no | not_applicable>
  transfer_pricing_doc: <yes | no | not_applicable>
  gpai_annual_review: <yes | no | not_applicable>
```

`completed_stages` 第一次追加 `7`（后续只更新 `completed_at` 和内部字段）。

**目标是把合规从"紧急事件驱动"转为"日历驱动"。**

Skill 完成使命，推荐：
- 每半年运行一次 `/startup-101 redflags` 全扫
- 重大产品 / 架构变更时重走相应 stage
- 政策窗口（EU AI Act / PIPL 新规）更新时查对应 appendix
