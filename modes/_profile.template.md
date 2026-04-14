# Startup Profile

> 此文件由 startup-101 skill 运行时生成，保存在你的项目目录。
> 不要提交到 skill repo。

```yaml
profile_schema_version: 0.3   # v0.3 新增：版本号。旧 profile 无此字段会触发迁移提示。

# === 基本信息 ===
team_size: null          # 1 | 2-5 | 6-15
roles: []                # [founder, co-founder, engineer, ...]
city: null               # 深圳 | 北京 | 上海 | 杭州 | 其他
founder_background: []   # [技术 / 产品 / 运营 / 学术]

# === 产品画像 ===
ai_track: null           # LLM 应用 | Agent | AIGC | 基础模型 | 具身 | 科学计算 | 其他
self_trained_model: null # yes | no
public_facing: null      # yes | no
generates_content: null  # yes | no

# === 目标市场 ===
user_geography: null     # >=70% 海外 | >=70% 中国 | 均衡
target_currency: null    # USD | CNY | 双币种
payment_model: null      # 订阅制 | 买断 | 按次 | 免费/广告 | ToB 定制

# === 融资预期 ===
fundraising_intent: null # 不融 | 天使/种子 | A轮+ | 战略
target_investors: null   # 美元基金 | 人民币基金 | 混合

# === 团队地理 ===
rnd_location: null       # 中国 | 海外 | 分布式
founders_tax_residency: null  # 中国 | 香港 | 新加坡 | 美国 | 其他

# === 阶段标记（skill 自动填充）===
current_stage: null      # 1-7
completed_stages: []
archetype: null          # A | B | C

# === 红旗扫描结果（skill 自动填充）===
red_flags_triggered: []
```

---

## 阶段结构化输出（v0.3 新增）

> 每完成一个 stage，skill 会把关键结论以 yaml-ish 键值对 append 到对应 section。
> 下一个 stage 进入前会读取这些 section 汇总呈现，保证阶段之间的上下文不丢。

### stage_0_output
```yaml
completed_at: null           # YYYY-MM-DD
archetype: null              # A | B | C
primary_ambiguity: null      # 若 profile 有歧义点，在此记录
```

### stage_1_output
```yaml
completed_at: null
founder_count: null          # 1 | 2 | 3 | 4+
founder_agreement_signed: null     # yes | no | not_applicable
vesting_structure: null      # "4+1" | "3+1" | "other:..." | none
equity_split_decided: null   # yes | no
esop_pool_reserved_pct: null # 0-20
arch_path_shortlist: null    # A | B1 | B2 | C1 | C2
personal_tax_residency_plan: null  # 不动 | 迁港 | 迁新 | 迁美 | 其他
counsel_shortlisted: null    # yes | no
```

### stage_2_output
```yaml
completed_at: null
chosen_path: null            # A | B1 | B2 | C1 | C2
cayman_entity_formed: null   # yes | no | not_applicable
delaware_entity_formed: null # yes | no | not_applicable
singapore_entity_formed: null # yes | no | not_applicable
hk_entity_formed: null       # yes | no | not_applicable
wfoe_formed: null            # yes | no | not_applicable
domestic_entity_formed: null # yes | no | not_applicable
37_wen_registered: null      # yes | no | not_applicable | in_progress
odi_filed: null              # yes | no | not_applicable | in_progress
bank_accounts_opened: null   # yes | partial | no
```

### stage_3_output
```yaml
completed_at: null
tax_registration_done: null  # yes | no | not_applicable
bookkeeping_provider: null   # 代账 | 自记 | 混合
invoice_setup_done: null     # yes | no | not_applicable
vat_taxpayer_type: null      # 一般纳税人 | 小规模纳税人 | not_applicable
social_insurance_setup: null # yes | no | not_applicable
transfer_pricing_framework_drafted: null # yes | no | not_applicable
```

### stage_4_output
```yaml
completed_at: null
labor_contract_template_ready: null  # yes | no
esop_cayman_established: null        # yes | no | not_applicable
esop_delaware_established: null      # yes | no | not_applicable
ip_assignment_executed_to: null      # cayman | delaware | sg | wfoe | 个人 | null
employee_37_wen_count: null          # 0+ integer; employees who hold Cayman options and are CN tax residents
pending_37_wen_employees: null       # integer
```

### stage_5_output
```yaml
completed_at: null
domestic_filing_tracks:      # 三轨中已走哪几条
  algorithm_filing: null     # done | in_progress | not_applicable
  large_model_filing: null   # done | in_progress | not_applicable
  registration_only: null    # done | in_progress | not_applicable
overseas_corpus_pct: null    # 0-100 — TC260-003 ≤30%
content_labeling_ready: null # yes | no
gdpr_representative_appointed: null  # yes | no | not_applicable
gdpr_dpa_in_place: null              # yes | no | not_applicable
eu_ai_act_gpai_trigger: null         # yes | no
eu_ai_act_gpai_obligations_tracked: null  # yes | no | not_applicable
pipl_outbound_route: null    # 免评估 | 标准合同 | 安全评估 | 认证 | not_applicable
software_copyright_route: null  # 自主申报 | 不申报 | 走第三方
```

### stage_6_output
```yaml
completed_at: null
raise_or_not: null           # raise | skip
route: null                  # usd | rmb | dual | not_applicable
instrument: null             # safe | note | priced | not_applicable
termsheet_reviewed_by_counsel: null  # yes | no | not_applicable
redemption_personal_liability: null  # none | company_only | founder_personal (🚩 硬红线)
antidilution: null           # weighted_avg | full_ratchet (🚩) | none
board_seats_founder: null    # integer
cfius_prescreen_done: null   # yes | no | not_applicable
closed: null                 # yes | no | in_progress
amount_raised: null          # e.g. "$5M seed" | null
```

### stage_7_output
```yaml
completed_at: null
monthly_cadence_set: null    # yes | no
quarterly_cadence_set: null  # yes | no
annual_filings_done:         # 按年度勾选
  cit_settlement: null       # yes | no | not_applicable
  iit_settlement: null       # yes | no | not_applicable
  annual_report_aic: null    # yes | no | not_applicable
  wfoe_joint_annual: null    # yes | no | not_applicable
  wfoe_audit: null           # yes | no | not_applicable
  hk_audit: null             # yes | no | not_applicable
  sg_acra_ar: null           # yes | no | not_applicable
  delaware_franchise_tax: null # yes | no | not_applicable
  form_5472: null            # yes | no | not_applicable
  fbar: null                 # yes | no | not_applicable
transfer_pricing_doc: null   # yes | no | not_applicable
gpai_annual_review: null     # yes | no | not_applicable
```

---

## 日志
<!-- skill 在这里 append 每个阶段的自由文本结论、红旗触发记录、下一步提醒 -->
