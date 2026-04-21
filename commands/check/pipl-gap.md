---
name: check-pipl-gap
description: PIPL（个人信息保护法）差距分析 — 判定出境路径三档阈值、给出最低合规清单、罚款风险评分
argument-hint: '[--scenario <training|inference|telemetry|mixed>] [--user-base <size>]'
trigger: /startup-101 check pipl-gap
source_appendix:
  - appendix/compliance-matrix.md  # § 二 PIPL 出境三档 / § 六 场景 1
  - modes/stage-5-ai-launch.md
profile_fields_used:
  - stage_0_output.archetype
  - stage_2_output.chosen_path
  - stage_5_output.target_market
  - stage_5_output.user_geography
  - stage_5_output.data_flow_includes_china_pi
  - stage_5_output.monthly_active_users
profile_fields_written:
  - stage_5_output.pipl_outbound_track
  - stage_5_output.pipl_action_deadline
  - stage_5_output.pipl_red_flags
last_policy_review: 2026-04-15
---

# Check: PIPL 差距分析

> 📎 完整矩阵见 [`appendix/compliance-matrix.md`](../../appendix/compliance-matrix.md) § 二、PIPL 出境三档 + § 六、叠加场景。
> 本命令专注"**处理中国境内 PI + 是否 / 如何出境**"的决策，不复述 PIPL 全文。

## 何时用这个命令

- 产品有**中国大陆用户**（即使只是部分）
- 训练语料 / 推理日志 / 用户数据 **需要跨境流动**（训练在境内、推理在境外；或反之）
- 搭了 Archetype B / C 架构，数据事实上在 Cayman / Delaware / SG 落盘
- 计划去欧盟 / 美国 / SG 扩市场，但原始数据来自中国用户
- 合规尽调被问"PIPL 出境走了哪条路"

## 输入

从 `./_profile.md` 读取：

| 字段 | 作用 |
|---|---|
| `stage_5_output.data_flow_includes_china_pi` | 是否处理中国 PI |
| `stage_5_output.monthly_active_users` | MAU 估算 → 映射阈值 |
| `stage_5_output.user_geography` | 用户地理分布 |
| `stage_2_output.chosen_path` | 决定境内主体是否具备（无境内主体 = 无法走出境合规通道） |

若字段缺失，一次问一个：

1. 你是否处理任何**中国大陆居民**的个人信息？（用户注册信息、行为日志、内容、人脸 / 语音等） `[Y/N]`
2. 这些信息是否存储 / 处理 / 传输到**中国境外**（含 Cayman / HK / Delaware / SG / EU 机房）？ `[Y/N/部分]`
3. 涉及的用户量级最近 12 个月累计？（按出境 PI 量算） `[<10 万 / 10-100 万 / >100 万]`
4. 是否含**敏感 PI**（14 岁以下未成年 / 人脸生物特征 / 金融账户 / 健康医疗 / 行踪轨迹 / 宗教 / 性取向）？若含，数量？
5. 你是否是**关键信息基础设施运营者**（公用事业、金融、交通等）？ `[Y/N]`
6. 数据流动场景？ `[A] 训练（境内采集 → 境外训练）` `[B] 推理（境内用户 → 境外模型 API）` `[C] Telemetry / 错误日志` `[D] 混合`

## 决策逻辑

### 第一层：是否适用

```
处理中国境内 PI？
├─ 否 → ✅ 不适用（但若收集 cookie / IP，仍要核对是否无意命中）
└─ 是 → 继续

PI 是否出境？
├─ 否（全程境内）→ 仅做 PIPL 本地合规（用户同意 / 保护负责人 / 制度）
└─ 是 → 进入三档判定
```

### 第二层：出境三档（2024-03 CAC 新规）

> 计量基准：**"从每年 1 月 1 日起累计"出境 PI 自然人数**

```
是否 CII 或涉"重要数据"？
├─ 是 → 【轨道 1】一律安全评估
└─ 否 → 按量级：
     ├─ 累计出境 <10 万人 PI（非敏感）+ 无敏感 PI  → 【轨道 0】免申报
     ├─ 10-100 万人 PI（非敏感）或 <1 万人敏感 PI  → 【轨道 2】SCC 备案 / 个保认证（二选一）
     └─ ≥100 万人 PI（非敏感）或 ≥1 万人敏感 PI     → 【轨道 1】安全评估
```

| 轨道 | 动作 | 周期 | 有效期 | 成本 |
|---|---|---|---|---|
| 0 | 免申报（用户同意 + 本地合规仍要） | — | — | 基础合规 5-10 万 RMB |
| 2 | SCC 备案（最常见）或 个保认证 | 1-3 个月 | 3 年 | 10-25 万 RMB |
| 1 | 省级 CAC → 国家 CAC 安全评估 | 45-60 工作日 + 补正 | 3 年 | 30-60 万 RMB |

### 第三层：自贸区负面清单豁免

上海 / 海南 / 北京自贸区发布**数据出境负面清单**，**清单外**数据可免走合规通道。

- 若境内主体注册在自贸区 → 让用户检查当地清单
- 清单每地不同且更新频繁，需逐项比对

### 第四层：典型 AI 场景对照

| 场景 | 典型映射 |
|---|---|
| To C 问答 Bot，MAU < 10 万 | 轨道 0 免申报（但用户同意 + 告知必做） |
| To C MAU 10-100 万 | 轨道 2 SCC 备案（最常见路径） |
| To C MAU ≥ 100 万 | 轨道 1 安评 |
| 存人脸 / 生物特征 / 14 岁以下 PI > 1 万 | 轨道 1 安评（敏感 PI 阈值严格） |
| 训练语料含中国用户行为日志出境 | 可能触"重要数据"→ 轨道 1 |
| 纯 B 端（销售线索 / 员工账号）跨境 | 视量级按轨道 0/2 |

## 输出 schema

```markdown
# 🎯 你的 PIPL 出境差距分析

**适用性**：<命中 / 不命中 / 部分场景命中>
**建议轨道**：轨道 0 / 2 / 1
**目标完成时间**：T- <N> 月（相对上线日）
**估算成本区间**：<X-Y> 万 RMB

## 出境数据清单（需用户确认）
| 数据类别 | 量级 | 是否敏感 | 出境目的地 |
|---|---|---|---|
| <User registration info> | <X 万> | <Y/N> | <Cayman/Delaware/SG/EU/HK> |
| ... | | | |

## 轨道选择理由
<1-3 句话解释为什么是该轨道>

## 🚩 必须立即补齐的基础项（无论走哪轨）
1. 用户告知 + 单独同意（PIPL Art. 13, 14, 39）
2. 个人信息保护负责人（PIPL Art. 52，规模达标必设）
3. 个人信息保护影响评估（PIIA，PIPL Art. 55）
4. 境外接收方尽调报告

## 轨道 2 / 1 额外动作
- SCC 备案模板（CAC 发布）+ 签约
- 安评路径：事前自评估 → 省级 CAC → 国家 CAC 复核

## 叠加场景提示
- 若同时上线欧盟 → 运行 /startup-101 check eu-ai-act-tier
- 若自研模型面向中国公众 → 运行 /startup-101 check algorithm-filing
- 跨境数据流对应的转让定价合同见 Stage 7

## 深入阅读
- 完整矩阵：appendix/compliance-matrix.md § 二
- ByteDance 式叠加场景：appendix/compliance-matrix.md § 六 场景 1
- 法规：《促进和规范数据跨境流动规定》CAC 2024-03-22
```

## 关键红旗

| # | 红旗 | 判定条件 | 后果 |
|---|---|---|---|
| 1 | **出境量级 ≥ 100 万但未安评** | MAU 达标 + 轨道选错 | 上千万罚款 + 业务暂停（PIPL Art. 66） |
| 2 | **敏感 PI ≥ 1 万但走轨道 0 / 2** | 敏感 PI 量达标 | 同上 |
| 3 | **无境内主体但有中国 PI** | archetype C 纯海外 + 中国用户 | 无法走任何合规通道，只能立即落地境内运营方 |
| 4 | **未做 PIIA 个保影响评估** | PIPL Art. 55 要求场景 | 监管要求立即补做，补不全直接暂停 |
| 5 | **用户同意机制是"捆绑同意"** | 隐私政策用一个大勾同意 | 违反 PIPL Art. 14 单独同意原则 |
| 6 | **境外接收方未签 SCC** | 走轨道 2 但无标准合同 | 备案不受理 |
| 7 | **训练语料含"重要数据"**（地理、公共卫生、工业等） | 按场景判定 | 自动升级为轨道 1 安评且可能禁止出境 |
| 8 | **CII 运营者未走安评** | CII 判定命中 | 重大罚款 + 刑事风险 |

## 写回 profile

```yaml
stage_5_output:
  pipl_outbound_track: 0 | 2 | 1 | not_applicable
  pipl_estimated_cost_rmb: [100000, 250000]
  pipl_target_completion: 2026-08-30
  pipl_action_deadline: 2026-06-15  # 启动律所 kickoff 的 deadline
  pipl_red_flags:
    - no_separate_consent
    - overseas_recipient_missing_scc
  pipl_scan_date: 2026-04-21
```

## 限界

- **本命令不做 PIIA 模板** — 模板见 `templates/dpia.template.md`（v0.5 补）
- **不覆盖个人信息跨境认证**（第三方认证路径较小众，需专项咨询）
- **不替代 CAC 备案材料起草** — 需专业合规律所 / 顾问
- **政策解读随 CAC 指南更新** — 顶部 `last_policy_review`
