---
name: check-algorithm-filing
description: 判定 AI 产品需要走算法备案三轨中的哪一条（A 算法备案 / B 大模型备案 / C 大模型登记），产出备案路径 + 时间规划 + 关键红旗
argument-hint: '[--self-trained] [--china-facing] [--api-only] [--generative] [--deep-synthesis]'
trigger: /startup-101 check algorithm-filing
source_appendix: appendix/ai-filing-guide.md
profile_fields_used:
  - stage_0_output.archetype
  - stage_2_output.entity_structure
  - stage_5_output.ai_product_type
  - stage_5_output.target_market
  - stage_5_output.self_trained_model
  - stage_5_output.base_model_family
  - stage_5_output.target_launch_date
  - stage_5_output.deep_synthesis_features
  - stage_5_output.ships_to_eu
  - stage_5_output.training_data_outbound
profile_fields_written:
  - stage_5_output.filing_tracks
  - stage_5_output.filing_target_launch_date
  - stage_5_output.filing_timeline_months
  - stage_5_output.filing_deadlines
  - stage_5_output.filing_red_flags
  - stage_5_output.filing_followup_commands
last_policy_review: 2026-04-15
---

# Check: 算法备案三轨判定

> 📎 **完整政策细节**：见 [`appendix/ai-filing-guide.md`](../../appendix/ai-filing-guide.md)
> 本命令只做**判定 + 路径 + 时间 + 红旗**，不复述政策文本。

## 何时用这个命令

- 你的 AI 产品准备在中国大陆上线（To C / To B 严肃应用）
- 不确定要走"算法备案 / 大模型备案 / 大模型登记"哪一条
- 要做年度时间规划，需要倒推 T-6~T-9 个月的合规起点
- 拿到投资前 / 融资 DD 被问到备案状态

## 输入

从 `./_profile.md` 读取（若存在）：

| 字段 | 作用 |
|---|---|
| `stage_5_output.self_trained_model` | 是否自研基础 / 垂直大模型 |
| `stage_5_output.base_model_family` | `llama` / `qwen` / `deepseek` / `mistral` / `in-house` / `api-only` — 触发境外语料红旗 |
| `stage_5_output.ai_product_type` | `generative` / `recommendation` / `deep_synthesis` / `ranking` / `retrieval` / `scheduling` |
| `stage_5_output.target_market` | `china_c` / `china_b` / `global_only` |
| `stage_5_output.target_launch_date` | 用于计算每个里程碑的绝对 deadline（**必填**）|
| `stage_5_output.deep_synthesis_features` | 人脸 / 语音 / 数字人 / 强编辑 的 bool flags |
| `stage_5_output.ships_to_eu` | 是否同时上欧盟（触发 EU AI Act 叠加）|
| `stage_5_output.training_data_outbound` | 训练 / 推理数据是否跨境（触发 PIPL 叠加）|
| `stage_2_output.entity_structure` | 判定备案主体是否适格（经营范围需含 AI） |

若 profile 不存在或字段为空，**一次只问一个问题**（遵循 `_shared.md` 交互原则）：

1. 你的模型是自研，还是调用别人已备案的 API？ `[A] 自研` `[B] 调 API` `[C] 混合（自研 + 调外部）`
2. 若 Q1 = 自研 / 混合：基础模型家族？ `[a] Llama 2/3 微调` `[b] Qwen (Apache 2.0)` `[c] DeepSeek (Apache 2.0)` `[d] Mistral` `[e] 自训 from scratch` `[f] 其他` — **命中 Llama 自动联动 `check/license-scan`**
3. 目标用户是否面向中国大陆 C 端 / 具舆论属性的 B 端？ `[A] 是` `[B] 仅海外` `[C] 仅内部 / 科研`
4. 产品主要能力类型？ `[A] 生成内容（文/图/音/视频）` `[B] 推荐 / 排序 / 检索` `[C] 深度合成（换脸 / 语音克隆 / 数字人）` `[D] 调度决策`
5. 产品是否包含以下任一深度合成能力？（多选） `[a] 人脸合成/换脸` `[b] 语音合成/克隆` `[c] 数字人/虚拟形象` `[d] 图文/视频强编辑` `[e] 以上都没有`
6. **目标上线日？（必填，用于算绝对 deadline）** `YYYY-MM-DD`
7. 是否同时面向**欧盟用户**上线？ `[Y/N/未定]` — 命中 Y 或未定将叠加 EU AI Act 检查
8. 训练 / 推理数据是否涉及**中国境内 PI 出境**？ `[Y/N/未定]` — 命中 Y 或未定将叠加 PIPL 检查
9. 已完成 Stage 2？ 营业执照经营范围是否含"人工智能技术开发 / 技术服务"？ `[Y/N/不确定]`

## 决策逻辑

### 第一步：主轨判定

```
self_trained == 是？
├─ 是 + 面向中国公众 + ai_product_type == generative
│   → 【B 大模型备案】+【A 算法备案（生成合成类）】  ← 双备案
├─ 是 + 面向中国公众 + ai_product_type ∈ {recommendation, ranking, retrieval, scheduling}
│   → 【A 算法备案】仅单轨
├─ 是 + 仅海外 / 内部科研
│   → 免备案（但 ToB 严肃场景建议至少登记一轨）
├─ 否（调 API）+ 面向中国公众
│   → 【C 大模型登记】
└─ 否 + 仅海外 / 仅 B 端内部
    → 免备案
```

### 第二步：叠加触发器（自动判定，不依赖用户自觉）

基于 Q5 / Q7 / Q8 **自动**输出叠加项，并把对应的 follow-up command 注入输出：

```
Q5 含 a/b/c/d（任一）？
└─ 是 → 叠加【深度合成算法备案】 + filing_tracks 加入 "deep_synthesis"

Q7 == Y 或 未定？
└─ 是 → 叠加【EU AI Act】
        filing_followup_commands 加入 "/startup-101 check eu-ai-act-tier"

Q8 == Y 或 未定？
└─ 是 → 叠加【PIPL 出境】
        filing_followup_commands 加入 "/startup-101 check pipl-gap"
```

> 🚫 **不要只展示 checkbox 让用户自己勾** — 实战中菜鸟会漏勾。一定走 Q5/Q7/Q8 的主动提问。

### 第三步：基模联动（Llama 自动触发境外语料红旗）

```
Q1 ∈ {自研, 混合} AND Q2 == a (Llama 2/3 微调)?
└─ 是 → 自动触发：
        🚩 "境外语料大概率 >30% 红线"（B 轨大模型备案最常见打回）
        🚩 Llama Community License 合规（见 `check/license-scan` Red Flag 4）
        filing_followup_commands 加入 "/startup-101 check license-scan"
        建议：评估 Qwen / DeepSeek 替换可行性（Apache 2.0，无 MAU 限制 + 语料本地化）

Q1 ∈ {自研, 混合} AND Q2 ∈ {Qwen, DeepSeek}?
└─ 境外语料风险较低（本地基模 + 本地数据 ≈ 红线友好）
   但仍需人工核对训练数据来源占比
```

### 第四步：主体适格检查

```
entity_structure == 境内实体 + 经营范围含 AI?
├─ 是 → 主体 OK
├─ 否（经营范围缺 AI）→ 🚩 必须先回 Stage 2 做【经营范围变更】再备案
└─ 纯境外架构（无境内实体）→ 🚩 无法备案，需先落地境内实体（WFOE 或境内运营方）
```

### 第五步：绝对 deadline 计算

以 Q6 的 `target_launch_date` 为锚点，反推每个里程碑的绝对日期：

| 里程碑 | 相对提前量 | 计算 |
|---|---|---|
| 第三方安评 kickoff（仅 B 轨） | T-9 月 | `target_launch_date - 9 months` |
| 材料齐全 | T-4 月 | `target_launch_date - 4 months` |
| 提交初审 | T-3 月 | `target_launch_date - 3 months` |
| 预期批复 | T-0 | `target_launch_date` |
| 若 A 轨单独（非 B+A 双备） | T-3 月 kickoff | `target_launch_date - 3 months` |
| 若 C 轨 | T-2 月 kickoff | `target_launch_date - 2 months` |

如果任何里程碑 < 今天 → 🚩 **时间线告警**：你已经晚了。建议：延后上线 / 临时先走 C 轨 API 过渡 / 放弃中国市场先上海外。

## 输出 schema（呈现给用户）

```markdown
# 🎯 你的算法备案判定结果

**目标上线日**：YYYY-MM-DD（用户输入）
**主轨道**：<A / B / C / 免备案>
**叠加项**：<深度合成 / EU AI Act / PIPL 出境 ... 或 无>

## 绝对时间表（基于目标上线日倒推）
| 里程碑 | 绝对日期 | 状态 |
|---|---|---|
| 第三方安评 kickoff（仅 B 轨） | YYYY-MM-DD | ✅ 还有 N 天 / 🚩 已晚 X 天 |
| 材料齐全 | YYYY-MM-DD | ✅ / 🚩 |
| 提交初审 | YYYY-MM-DD | ✅ / 🚩 |
| 预期批复 | YYYY-MM-DD | = 目标上线日 |

> ⚠️ 若任何里程碑状态为 🚩，立即评估：延后上线 / 降轨（B → C API 过渡） / 放弃中国市场先上海外。

## 成本区间
- 服务商费用：<X-Y> 万 RMB
- 第三方安评：<仅 B 轨> <X-Y> 万 RMB
- 人工审核团队搭建：<X> 万 RMB / 年

## 🚩 必须在启动前解决的红旗
1. <具体红旗 1（如 Llama 基模 → 境外语料 >30% 红线）>
2. <具体红旗 2>
3. <具体红旗 3>

## 必须跑的 follow-up 命令（自动生成）
- [ ] `/startup-101 check license-scan`（命中条件：基模 = Llama）
- [ ] `/startup-101 check eu-ai-act-tier`（命中条件：Q7 = Y/未定）
- [ ] `/startup-101 check pipl-gap`（命中条件：Q8 = Y/未定）

## 下一步行动
- [ ] <具体动作 1>
- [ ] <具体动作 2>
- [ ] <具体动作 3>

## 深入阅读
- 完整政策细节：appendix/ai-filing-guide.md
- 语料合规 30% 红线：appendix/ai-filing-guide.md#四-b-大模型备案
- 跨境叠加：commands/check/eu-ai-act-tier.md
- 数据出境：commands/check/pipl-gap.md
- Llama license：commands/check/license-scan.md
```

## 关键红旗（主动触发，不等用户问）

| # | 红旗 | 判定条件 | 后果 |
|---|---|---|---|
| 1 | **境外语料 > 30%** | B 轨 + 训练数据境外来源占比高 | 大模型备案一刀切打回，最常见卡点 |
| 2 | **营业执照经营范围漏 AI** | stage_2_output.business_scope 不含"人工智能技术开发/技术服务"等 | 主体不适格，所有轨道都挡住 |
| 3 | **未做双水印**（显式+隐式） | 生成类产品 2026 新规硬要求 | 备案必打回 |
| 4 | **纯境外架构无境内主体** | entity_structure == Cayman-only / Delaware-only | 无法备案，商务合作都进不去国内客户 |
| 5 | **语料授权证明缺失** | 训练数据来源无授权链 | B 轨一票否决 |
| 6 | **双备案漏做**（只做 B 漏 A） | 自研生成模型只做了大模型备案 | 监管抽查必补 |
| 7 | **调 API 但切换模型未重新登记** | C 轨切换底层模型 | 登记失效 |
| 8 | **拒答率测试 < 95%** | B 轨 TC260-003 要求 | 补正拖延 2-3 个月 |

## 写回 profile（stage_5_output）

命令结束时，询问用户"将以下结论写入 _profile.md？ [y/n]"：

```yaml
stage_5_output:
  filing_tracks: [B, A, deep_synthesis]          # 数组，可多值
  filing_target_launch_date: 2026-12-01          # **必填**（Q6 输入）
  filing_timeline_months: 8                      # 最长轨道所需月数（从 launch 反推）
  filing_deadlines:                              # 绝对日期（由 target_launch_date 计算）
    safety_assessment_kickoff: 2026-03-01
    materials_ready: 2026-08-01
    initial_submission: 2026-09-01
    expected_approval: 2026-12-01
  filing_followup_commands:                      # 自动生成的 follow-up
    - /startup-101 check license-scan            # 若基模 = Llama
    - /startup-101 check eu-ai-act-tier          # 若 Q7 = Y/未定
    - /startup-101 check pipl-gap                # 若 Q8 = Y/未定
  filing_red_flags:
    - overseas_corpus_exceeds_30pct
    - missing_business_scope_ai
  filing_decision_locked_at: 2026-04-21
```

下游命令 / stage 可直接读取这些字段：
- `stage-6-fundraising.md` → 融资 DD 时自动引用备案状态
- `commands/check/pipl-gap.md` → 判定出境路径时读取 `filing_tracks`
- `commands/redflags/scan-all.md` → 扫描 `filing_red_flags` 是否已清

## 限界

- **本命令不替代专业合规律师**（开场 disclaimer 依 `_shared.md` 走）
- **政策时效性** — 顶部 `last_policy_review` 字段，超过 180 天请重新 review
- **不覆盖等保 2.0 定级**（属 Stage 5 独立子任务）
- **不覆盖个人信息保护影响评估（PIIA）细则**（见 `commands/check/pipl-gap.md`）
