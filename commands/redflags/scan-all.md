---
name: redflags-scan-all
description: 运行 6 条主红旗全扫描 + 命中条目跳转到对应 /check 命令深入检查；独立调用入口，也可作为 stage 结束钩子
argument-hint: '[--severity-only <critical|high>] [--json]'
trigger: /startup-101 redflags
source_appendix:
  - modes/red-flags.md
profile_fields_used:
  - stage_0_output.archetype
  - stage_2_output.chosen_path
  - stage_2_output.37_wen_registered
  - stage_3_output.payment_path_chosen
  - stage_4_output.ip_assignment_executed_to
  - stage_4_output.pending_37_wen_employees
  - stage_5_output.base_model_family
  - stage_5_output.user_geography
  - stage_5_output.mau_estimate
profile_fields_written:
  - red_flags_triggered
  - red_flags_last_scan_at
last_policy_review: 2026-04-15
---

# Red Flags: 6 条主扫描 + 深入命令路由

> 📎 每条红旗的补救细节仍在 [`modes/red-flags.md`](../../modes/red-flags.md)。
> 本命令做"扫描 + 路由"：命中一条 → 建议用户跳到对应 `/check` 深入命令。

## 何时用这个命令

- 主线 stage 结束后自动扫（由 SKILL.md 路由触发）
- 老手独立调用：每月 / 每季度 / 融资前做体检
- 创始人换架构后重新扫
- 新合规政策发布（本命令顶部 `last_policy_review` 过期）后重扫

## 输入

主要读 `./_profile.md`。若 profile 完全空，本命令退化为**交互式最小问卷**（6 个 yes/no）先建一份临时 profile。

一次问一个（仅在 profile 空时）：

1. Archetype？ `[A 纯内资 / B 双层出海 / C 纯海外 / 未定]`
2. 创始人中国税务居民？ `[Y/N]`
3. 已发境外母公司 option 给中国员工？ `[Y/N]`
4. 已在用个人 PayPal / 微信收境外订阅款且月流水 > $4k？ `[Y/N]`
5. 基础模型是 Llama 家族？ `[Y/N]`
6. 产品是 SaaS / 网络服务？ `[Y/N]`
7. 欧盟用户 > 0（哪怕 1 人）？ `[Y/N]`

## 扫描逻辑

对 6 条红旗逐一判定：

### 🚩 Red Flag 1: 37 号文未办

```
触发：
  (archetype == B) OR
  (archetype == C AND founders_tax_residency 含 China) OR
  (37_wen_registered ∈ {no, unknown, stale})
→ 命中 → 建议深入：/startup-101 check 37hao-exposure
```

**严重度**：Critical（融资 DD 第一爆点）
**补救窗口**：2-6 个月
**补救成本**：创始人 5-10 万 / 员工 1-3 万/人

### 🚩 Red Flag 2: IP Assignment 未指向海外主体

```
触发：
  archetype == B AND (
    ip_assignment_executed_to IN {wfoe, 个人, null} OR
    (已签劳动合同 AND IP Assignment 缺失)
  )
→ 命中 → 深入暂无独立 command，先参考 modes/stage-4-hiring-equity.md § 决策 3
```

**严重度**：Critical（估值打折 10-20%）
**补救窗口**：全员补签 2-6 周（遇离职员工更难）

### 🚩 Red Flag 3: 个人 PayPal / 微信收订阅规模化

```
触发：
  payment_model == subscription AND
  target_currency 含 USD AND
  payment_path_chosen IN {null, "个人 PayPal", "微信个人"} AND
  月流水估算 > $4000
→ 命中 → 建议深入：/startup-101 check cross-border-payment
```

**严重度**：Critical（非法结汇刑事风险 + 外管局 5 年追溯）
**补救窗口**：**立即中止**，7-14 天内搭 MoR 过渡

### 🚩 Red Flag 4: Llama Community License 违规

```
触发：
  base_model_family == llama AND (
    (用 Llama 输出改进其他 LLM) OR
    (预期 MAU ≥ 7 亿 无 Meta 单独许可) OR
    (缺 "Built with Llama" 标注)
  )
→ 命中 → 建议深入：/startup-101 check license-scan
```

**严重度**：High（许可撤销 + 下架）
**补救窗口**：停止违规行为立即生效 / 替换基模 1-3 个月

### 🚩 Red Flag 5: AGPL / SSPL 污染

```
触发：
  product_form ∈ {saas, api} AND (
    依赖树含 AGPL OR
    依赖树含 SSPL（如 MongoDB Community）AND 产品做托管分发
  )
→ 命中 → 建议深入：/startup-101 check license-scan
```

**严重度**：High（被迫开源 = 商业模式死亡）
**补救窗口**：替换依赖 2-8 周

### 🚩 Red Flag 6: EU 无 Art. 27 代表

```
触发：
  user_geography 含 EU OR 均衡 AND
  产品已 live OR 即将 live AND
  EU 用户 > 0（哪怕 1 人） AND
  无记录 Art. 27 代表指定
→ 命中 → 建议深入：/startup-101 check eu-ai-act-tier（本 check 覆盖完整 EU 义务）
```

**严重度**：High（GDPR 罚款最高 €20M 或 4% 全球营收）
**补救窗口**：第三方代表 1-2 周开通

## 输出 schema

```markdown
# 🚩 Red Flags 扫描结果（YYYY-MM-DD）

**扫描范围**：主 6 条 + profile 附加项
**命中数**：<C 条 Critical / H 条 High / M 条可能命中 / K 条未命中>

## 🔴 Critical（立即处理）
| # | 红旗 | 命中原因 | 深入命令 | 严重度 |
|---|---|---|---|---|
| 1 | Red Flag 1: 37 号文未办 | 创始人侧 unknown + 已有 Cayman | `/startup-101 check 37hao-exposure` | Critical |
| 3 | Red Flag 3: 个人 PayPal 规模化 | 月流水估算 $8k | `/startup-101 check cross-border-payment` | Critical |

## 🟡 High（30 天内处理）
| # | 红旗 | 命中原因 | 深入命令 | 严重度 |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

## ⚠️ 可能命中（需核对）
| # | 红旗 | 需核对 | 怎么核对 |
|---|---|---|---|

## ✅ 未命中
- Red Flag X: <一句话为什么跳过>

## 推荐处理顺序
1. 先解 Critical（可能 blocking 融资 / 业务 / 外汇）
2. 再解 High（30-90 天窗口）
3. 可能命中项排期核对

## 写入 profile
- red_flags_triggered: [1, 3, 5]
- red_flags_last_scan_at: 2026-04-21

## 深入阅读
- 每条红旗的补救细节：modes/red-flags.md
- 单点深入 commands：commands/check/
- 整体架构回顾：modes/stage-0-profile.md
```

## 路由表（命中 → 推荐深入命令）

| 红旗 | 推荐深入命令 | Fallback 阅读 |
|---|---|---|
| RF1: 37 号文 | `/startup-101 check 37hao-exposure` | `modes/red-flags.md` + `modes/stage-4-hiring-equity.md` |
| RF2: IP Assignment | （v0.5 补 `check/ip-assignment.md`） | `modes/stage-4-hiring-equity.md` § 决策 3 |
| RF3: 个人收款 | `/startup-101 check cross-border-payment` | `appendix/payment-matrix.md` |
| RF4: Llama | `/startup-101 check license-scan` | `modes/red-flags.md` |
| RF5: AGPL | `/startup-101 check license-scan` | `modes/red-flags.md` |
| RF6: EU 代表 | `/startup-101 check eu-ai-act-tier` | `appendix/compliance-matrix.md` § 四 |

## 交互原则

- **不问已经在 profile 里有答案的字段**（v0.3 Profile Linkage Contract）
- **命中条目先呈现"为什么命中"**（引用 profile 具体字段值），不干巴巴说"命中"
- **一次性输出所有命中**，不逐条追问（除非用户要求 deep dive 单条）
- **默认按严重度排序**（Critical → High → 可能命中 → 未命中）
- **Critical 命中时主动提示用户暂停当前高风险动作**（融资 / 规模化 / 新员工授权）

## 写回 profile

```yaml
red_flags_last_scan_at: 2026-04-21
red_flags_triggered: [1, 3, 5]
red_flags_snapshot:
  critical:
    - id: 1
      name: 37hao_not_registered
      reason: "stage_2_output.37_wen_registered = unknown AND cayman_entity_formed = yes"
      deep_dive: /startup-101 check 37hao-exposure
      deadline: 2026-06-20
    - id: 3
      name: personal_paypal_subscription_scale
      reason: "payment_path_chosen = null AND monthly_flow_estimate_usd = 8000"
      deep_dive: /startup-101 check cross-border-payment
      deadline: immediate
  high:
    - id: 5
      name: agpl_in_saas
      reason: "product_form = saas AND dep includes mongodb_community"
      deep_dive: /startup-101 check license-scan
      deadline: 2026-05-20
```

## 限界

- **本命令只扫主 6 条红旗** — stage 内部的局部红旗（如劳动合同 30 天逾期、竞业不付补偿）仍在 stage 文件自己的"本阶段新增红旗" section
- **不做自动补救** — 只做扫描 + 路由
- **不替代律师 DD** — 只是自查工具
- **准确性取决于 profile 完整度** — profile 空 / 过旧 → 扫描保守偏乐观
