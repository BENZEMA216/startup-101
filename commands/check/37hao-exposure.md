---
name: check-37hao-exposure
description: 扫描 37 号文（外管局境外投资/境外持股登记）暴露面 — 创始人 + 员工两侧全查，输出必办清单 + 补救路径 + 融资 DD 爆雷风险评分
argument-hint: '[--founders-only] [--employees-only] [--as-of <YYYY-MM-DD>]'
trigger: /startup-101 check 37hao-exposure
source_appendix:
  - modes/stage-4-hiring-equity.md
  - modes/red-flags.md  # Red Flag 1
  - references/index/02-incorporation.md
profile_fields_used:
  - stage_0_output.archetype
  - stage_2_output.chosen_path
  - stage_2_output.cayman_entity_formed
  - stage_2_output.37_wen_registered
  - stage_4_output.employee_37_wen_count
  - stage_4_output.pending_37_wen_employees
  - stage_4_output.next_funding_dd_date
  - founders_tax_residency
profile_fields_written:
  - stage_4_output.37hao_exposure_snapshot
  - stage_4_output.37hao_action_deadline
  - stage_4_output.37hao_followup_commands
last_policy_review: 2026-04-15
---

# Check: 37 号文暴露扫描

> 37 号文 = 《国家外汇管理局关于境内居民通过特殊目的公司境外投融资及返程投资外汇管理有关问题的通知》（汇发〔2014〕37 号）。
> 📎 政策 + 补救详见 [`modes/red-flags.md#red-flag-1-37-号文未办`](../../modes/red-flags.md) 和 [`references/index/02-incorporation.md`](../../references/index/02-incorporation.md)。

## 何时用这个命令

- 创始人是**中国税务居民**，且已有（或计划）Cayman / BVI / SG / Delaware 母公司
- 准备给**中国员工发境外母公司期权**（Cayman option）
- 融资 DD / A 轮 / B 轮启动前（境外律所必查的第一件事）
- 已知架构搭了一半，但不确定"登记"到底办了没、办得对不对

## 输入

从 `./_profile.md` 读取（若存在）：

| 字段 | 作用 |
|---|---|
| `stage_0_output.archetype` | A（内资）= 大多数情况免 37；B / C = 必查 |
| `stage_2_output.chosen_path` | 决定 SPV 持股层级 |
| `stage_2_output.37_wen_registered` | 创始人侧登记状态（`yes` / `no` / `in_progress` / `unknown`） |
| `stage_4_output.employee_37_wen_count` | 员工侧已登记数 |
| `stage_4_output.pending_37_wen_employees` | 员工侧待登记数（持境外 option 但未登记）|
| `founders_tax_residency` | 判定谁命中 37 号文适用主体 |

若 profile 不存在或字段为空，一次问一个：

1. 你是中国税务居民吗？（过去 183 天在中国累计 ≥183 天 / 户籍 / 家庭中心） `[Y/N/不确定]`
2. 公司当前是否有境外母公司（Cayman / BVI / SG / Delaware / HK）？ `[Y/N]`
3. 你是否以**个人**身份直接或通过境外信托 / SPV 持有该母公司股份？ `[Y/N]`
4. 已有 / 计划给**中国籍员工**发境外母公司 option？ `[Y/N]` 若 Y → 多少人？ 已行权多少人？
5. 上次外管局 37 号文办理 / 更新日期？ `[YYYY-MM-DD / 从未办 / 不确定]`
6. **下一个融资 DD / 关键业务里程碑的目标日期？（用于计算绝对 deadline）** `YYYY-MM-DD / 暂无`

## 决策逻辑

### 第一层：是否落入适用范围

```
archetype == A (纯内资)
├─ 创始人未持境外股权 → ✅ 免适用
└─ 创始人持任何境外 SPV → 仍需登记（即使公司是内资）

archetype == B (Cayman + WFOE)
└─ 强命中：创始人 + 员工两侧全查

archetype == C (Delaware C-corp)
├─ 创始人已转非中国税务居民 + 家庭中心海外 → 条件免（但要有证据）
└─ 创始人仍是中国税务居民 → 强命中
```

### 第二层：创始人侧状态表

| 状态 | 判定 | 动作 |
|---|---|---|
| `unknown` | 不确定是否办过 | 🚩 立即找跨境律所做 37 号文历史核查（1-2 周） |
| `no` | 未办 | 🚩🚩 **Red Flag 1 命中** — 补登记 2-6 个月 + ~5-10 万 RMB |
| `in_progress` | 办理中 | ⚠️ 确认律所跟进节奏，融资前必须完成 |
| `yes, >1 年未更新` | 登记过但股权变动后未变更 | ⚠️ 重大变更（增发 / 股权转让 / 架构调整）需办变更登记 |
| `yes, <1 年且股权无变动` | ✅ | 仍建议每半年复核 |

### 第三层：员工侧状态表

```
员工侧暴露分数 = pending_37_wen_employees / (employee_37_wen_count + pending_37_wen_employees)
```

| 分数 | 判定 | 动作 |
|---|---|---|
| 0（全员已办）| ✅ OK | 每次新员工入职时走标准流程 |
| 0 < x < 0.3 | ⚠️ 个别遗漏 | 30 天内清零待办 |
| 0.3 - 0.7 | 🚩 系统性缺失 | 启动批量补登记 + 暂停新 option 授予 |
| ≥ 0.7 | 🚩🚩 爆雷风险极高 | 融资 DD 必被发现，立即找跨境律所统筹 |

### 第四层：融资 DD 爆雷风险评分

按下表加权（满分 10）：

| 条件 | 分数 |
|---|---|
| 创始人 37 号文未办 / unknown | +4 |
| 员工侧待办数 > 0 | +2 |
| 员工侧待办率 ≥ 0.5 | 额外 +2 |
| 已行权但未登记的员工 ≥ 1 | +2 |
| 已发生跨境股权转让（退出 / 回购）未登记 | +3 |
| 创始人有多个境外 SPV 架构（Trust / 多层持股） | +1 |

- **0-2 分**：DD 基本无事
- **3-5 分**：DD 会问，给出合理方案即可
- **6-8 分**：估值打折 5-15% 风险
- **≥ 9 分**：交易可能延期 / 破裂，立即停一切融资动作先做合规

### 第五层：绝对 deadline 计算

以 Q6 的 `next_funding_dd_date`（或下一个业务里程碑）为锚点：

| 动作 | 最晚完成 |
|---|---|
| 创始人侧补登记启动 | `dd_date - 120 days`（补登记需 2-6 个月） |
| 员工侧批量补登记启动 | `dd_date - 90 days` |
| 重大股权变动变更登记 | 变动后 30 日内 |

若任何 deadline < 今天 → 🚩 **立即触发最高级告警**：暂停一切新 option 授予、新股权转让、对外融资接触，直到合规窗口恢复。

### 第六层：自动 follow-up 命令注入

```
创始人侧未登记 OR 风险评分 ≥ 6？
└─ 注入：/startup-101 redflags  # 触发 6 条主红旗完整扫描，确认是否还有联动雷

员工侧待登记 ≥ 1 + 已行权？
└─ 注入：/startup-101 review term-sheet  # （v0.5 补）融资前条款 DD 配套

存在员工期权 + 创始人/员工流水可能走个人账户？
└─ 注入：/startup-101 check cross-border-payment  # 排查 RF3 联动

每次主扫描结束？
└─ 建议：/startup-101 redflags  # 作为体检闭环
```

## 输出 schema（呈现给用户）

```markdown
# 🎯 你的 37 号文暴露扫描结果

**适用范围**：<是 / 否 / 条件免>
**创始人侧状态**：<状态 + 动作>
**员工侧状态**：<分数 + 动作>
**融资 DD 爆雷风险评分**：X / 10

## 绝对 deadline 表（基于下一个 DD / 里程碑日期）
| 动作 | 最晚完成 | 状态 |
|---|---|---|
| 创始人侧补登记启动 | YYYY-MM-DD | ✅ 还有 N 天 / 🚩 已晚 X 天 |
| 员工侧批量补登记启动 | YYYY-MM-DD | ✅ / 🚩 |
| 重大变动变更登记 | 变动后 30 日 | 常态化 |

## 🚩 必须在 N 天内完成的动作
1. <具体动作 1，带绝对日期>
2. <具体动作 2>
3. <具体动作 3>

## 必须跑的 follow-up 命令（自动生成）
- [ ] `/startup-101 redflags`（命中条件：创始人未登记 OR 风险评分 ≥ 6）
- [ ] `/startup-101 check cross-border-payment`（命中条件：员工期权发放 + 疑似个人账户流水）

## 推荐跨境律所类型（非背书）
- 汉坤 / 方达 / 君合 / 通商 — 老牌跨境登记流程熟
- 费用区间：创始人侧 5-10 万 RMB，员工侧 1-3 万 RMB/人

## 下一步
- [ ] 将本扫描结论写入 _profile.md (stage_4_output.37hao_exposure_snapshot)
- [ ] 若风险评分 ≥ 6，暂停新 option 授予直到创始人侧补登记完成
- [ ] 若准备融资，把本扫描结果作为 DD 自查清单的第一项

## 深入阅读
- 补救流程：modes/red-flags.md § Red Flag 1
- 员工侧专项：modes/stage-4-hiring-equity.md § ESOP + 37 号文员工篇
- 法规原文：汇发〔2014〕37 号 + 外管局相关问答
```

## 关键红旗（主动触发）

| # | 红旗 | 判定条件 | 后果 |
|---|---|---|---|
| 1 | 创始人 Cayman/BVI 架构已搭但**未办任何 37 号文** | cayman_entity_formed=yes + 37_wen_registered ∈ {no, unknown} | 退出时对价无法合法汇回中国 + 50-100 万罚款 |
| 2 | 员工**已行权**但未登记 | pending 中含 "已行权" 员工 | 员工自己面临外汇处罚 + 公司 DD 爆雷 |
| 3 | 股权**增发 / 转让 / 回购**后未办**变更登记** | 日志中出现股权变动 | 视同未登记，原登记失效 |
| 4 | 创始人已不是中国税务居民但**未留证据链** | founders_tax_residency 切换无证明 | 监管追溯 5 年内按中国居民追责 |
| 5 | 新 option 授予前未做**员工 37 号文指引**流程 | 缺 `modes/stage-4-hiring-equity.md` 员工入职 4 件套 | 批量遗漏的种子 |
| 6 | 同一人通过**多层 SPV**持股且未层层登记 | 信托 / 多层 SPV 架构 | 只登记最底层 = 登记不完整 |

## 写回 profile

命令结束时询问"写回 _profile.md？ [y/n]"：

```yaml
stage_4_output:
  next_funding_dd_date: 2026-10-15              # Q6 输入（用于算 deadline，可填"暂无"）
  37hao_exposure_snapshot:
    scan_date: 2026-04-21
    applicable: true
    founder_status: no | in_progress | yes_current | yes_stale | unknown
    employee_pending_count: 3
    employee_registered_count: 7
    employee_exercised_without_filing_count: 1
    dd_explosion_risk_score: 7
    red_flags_triggered: [founder_not_registered, employees_exercised_without_filing]
  37hao_action_deadline: 2026-06-20             # 绝对日期，从 next_funding_dd_date 反推
  37hao_followup_commands:
    - /startup-101 redflags                     # 若风险评分 ≥ 6
    - /startup-101 check cross-border-payment   # 若员工期权 + 疑似 RF3 联动
```

## 限界

- **本命令不办登记** — 只做暴露扫描和风险评分
- **不判定跨境股权税务**（属 Stage 7 转让定价 + 分红扣缴范畴）
- **不覆盖 37 号文以外的外管局登记**（如 ODI / FDI / 境外放款）
- **政策时效性** — 顶部 `last_policy_review`；外管局窗口指导变化频繁，超 180 天请复核
