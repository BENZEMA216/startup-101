# Schema Signals — 跨命令共享 profile 字段登记册

> 所有原子命令（`commands/**`）和 stage 文件（`modes/stage-N.md`）读写 `_profile.md` 时，**必须**引用本文件登记的字段，不得私自造新字段名。
> 更新本文件 = schema 变更 = 升 patch version。

## 为什么需要这份登记册

v0.4 + v0.4.1 + v0.4.2 迭代过程中积累了一批**跨命令引用**的信号字段（比如 `ships_to_eu` 被 algorithm-filing / pipl-gap / eu-ai-act-tier / license-scan 四个命令同时读）。没有集中登记会导致：

- 字段名漂移：`eu_market` vs `ships_to_eu` vs `target_eu` 同义不同名
- 值域不一致：有的命令用 `Y/N`，有的用 `true/false`，有的用 `yes/no/未定`
- 新命令忘记读已有字段，用户被重复问同一个问题
- v0.5 agents 想做全局体检时找不到权威定义

## 字段分类

### 1. 跨命令判定信号（最高优先级）

这些字段**被 2 条以上命令共同引用**，任何命令收集到都应写回，避免重复提问。

| 字段 | 类型 | 值域 | 读者 | 写入者（收集问题） |
|---|---|---|---|---|
| `stage_5_output.self_trained_model` | bool | `yes / no / hybrid` | algorithm-filing, eu-ai-act-tier, license-scan, pipl-gap | algorithm-filing Q1, stage-5 |
| `stage_5_output.base_model_family` | enum | `llama / qwen / deepseek / mistral / gemma / phi / in-house / api-only / other` | algorithm-filing, license-scan | algorithm-filing Q2, license-scan Q2 |
| `stage_5_output.china_public_facing` | bool | `yes / no / undecided` | algorithm-filing, pipl-gap, license-scan, eu-ai-act-tier | algorithm-filing Q3, eu-ai-act-tier Q7, license-scan Q7, pipl-gap Q9 |
| `stage_5_output.ships_to_eu` | bool | `yes / no / undecided` | algorithm-filing, pipl-gap, license-scan, eu-ai-act-tier | algorithm-filing Q7, eu-ai-act-tier Q1, license-scan Q8, pipl-gap Q8 |
| `stage_5_output.training_data_includes_china_pi` | bool | `yes / no / undecided` | eu-ai-act-tier, pipl-gap | eu-ai-act-tier Q6, pipl-gap Q1+Q2 |
| `stage_5_output.training_data_outbound` | bool | `yes / no / undecided` | algorithm-filing, pipl-gap | algorithm-filing Q8, pipl-gap Q2 |
| `stage_5_output.deep_synthesis_features` | list | subset of `[face, voice, digital_human, editing]` | algorithm-filing, 未来 art50 细项 | algorithm-filing Q5 |
| `stage_5_output.mau_estimate` | int | monthly active users | redflags/scan-all, license-scan（Llama 7 亿线）, pipl-gap | stage-5, redflags mini-survey |

### 2. 时间锚点字段（绝对 deadline 计算的输入）

这组字段是所有"绝对 deadline 表"的锚点。每条命令问一次即可，写回后其他命令复用。

| 字段 | 用途 | 典型来源 |
|---|---|---|
| `stage_5_output.target_launch_date` | 产品上线日，触发备案/PIPL 倒推 | algorithm-filing Q6, pipl-gap Q7 |
| `stage_3_output.payment_target_start_date` | 首次正式收款日 | cross-border-payment Q5 |
| `stage_4_output.next_funding_dd_date` | 37 号文 deadline 锚 | 37hao-exposure Q6 |
| `stage_6_output.next_funding_dd_date` | license-scan / redflags 的锚（Stage 6 的权威写法）| license-scan Q6, redflags/scan-all Q8 |

> ⚠️ **双 stage 位置同名问题**：`next_funding_dd_date` 同时出现在 `stage_4_output` 和 `stage_6_output`。规定：
> - **Stage 6 是权威源**（融资是 stage-6 的核心内容）
> - 其他命令读写时**优先写 stage_6_output.next_funding_dd_date**，stage_4_output 只作缓存
> - v0.5 迁移：`stage-6-fundraising.md` 写入时同步更新 stage_4 缓存

### 3. 命令写回的标准化后缀

每条命令的 `profile_fields_written` 统一使用以下后缀，方便 agents 批量读取：

| 后缀 | 含义 | 示例 |
|---|---|---|
| `*_scan_date` | 本次命令运行日期 | `filing_scan_date: 2026-04-22` |
| `*_deadlines` | yaml map 格式的里程碑 → 绝对日期 | `pipl_deadlines: {kickoff: ..., submission: ...}` |
| `*_followup_commands` | 自动推导的下一步命令列表 | `filing_followup_commands: [/startup-101 check license-scan]` |
| `*_red_flags` | 本命令命中的红旗字符串数组 | `filing_red_flags: [overseas_corpus_exceeds_30pct]` |
| `*_snapshot` | 整体状态快照（扫描类命令）| `37hao_exposure_snapshot: {...}` |
| `*_action_deadline` | 最早的 kickoff 日（一个 scalar 方便排序）| `pipl_action_deadline: 2026-04-04` |

### 4. 联动字段（触发 follow-up 的判定信号）

这些字段不是用户直接输入，而是**命令 A 运行后推断出的结论**，命令 B 读取后决定是否自动跑。

| 字段 | 产生者 | 消费者 |
|---|---|---|
| `stage_4_output.pending_37_wen_employees` | stage-4 / 37hao-exposure | redflags/scan-all（RF1 判定） |
| `stage_4_output.ip_assignment_executed_to` | stage-4 | redflags/scan-all（RF2 判定）|
| `stage_3_output.historical_personal_account_usage` | cross-border-payment Q6 | redflags/scan-all（RF3 判定）, 37hao-exposure |
| `stage_5_output.license_scan_snapshot.risk_score` | license-scan | redflags/scan-all, algorithm-filing |
| `stage_5_output.filing_tracks` | algorithm-filing | stage-6 DD 检查 |
| `stage_2_output.entity_structure` | stage-2 | algorithm-filing 主体适格 |
| `stage_2_output.37_wen_registered` | stage-2 | 37hao-exposure / redflags |

### 5. 值域规范

**布尔字段的标准值域**：
- `yes` / `no` / `undecided`
- **不用** `Y/N/?` 或 `true/false`，统一字符串值方便 yaml 阅读

**日期字段**：
- `YYYY-MM-DD`（ISO 8601）
- 允许特殊值：`"immediate"`, `"not_applicable"`, `"暂无"`

**数量字段**：
- 整数 + 单位后缀（`employee_count_total: 12`，不写 `"12 人"`）
- 金额统一 USD 或 RMB，字段名标注（`estimated_cost_usd` / `estimated_cost_rmb`）

## 新增字段的审查清单

任何命令想新增 `_profile.md` 字段前，先检查：

- [ ] 本文件是否已有语义相近的字段？有就直接复用。
- [ ] 字段是否可能被 ≥ 2 条命令引用？是 → 登记到「1. 跨命令判定信号」。
- [ ] 字段是否是时间锚点？是 → 登记到「2. 时间锚点」并遵守"哪个 stage 权威"规则。
- [ ] 写入后缀是否符合标准化规范？（`_deadlines`, `_followup_commands` 等）
- [ ] 值域是否遵守「5. 值域规范」？

## 变更记录

| 日期 | 版本 | 变更 |
|---|---|---|
| 2026-04-22 | v0.4.2 | 初版登记册，收录 v0.4 + v0.4.1 + v0.4.2 累积的所有跨命令字段 |

## 下游消费者

- `agents/ai-compliance-auditor.md`（v0.5）：读取全部 `*_snapshot` / `*_red_flags` / `*_deadlines` 做全面体检
- `modes/stage-6-fundraising.md`（v0.5 升级）：读取全部 Stage 5 结论作为 DD 自查清单
- `agents/vc-term-sheet-reviewer.md`（v0.5）：读取 `37hao_exposure_snapshot.dd_explosion_risk_score` 做谈判建议
