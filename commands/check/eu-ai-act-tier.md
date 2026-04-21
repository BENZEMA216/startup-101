---
name: check-eu-ai-act-tier
description: EU AI Act 分级判定 — 判断你的 AI 系统是否触发 GPAI Provider 义务 / Art. 50 透明度义务 / 高风险分级，产出时间表 + 动作清单
argument-hint: '[--is-gpai] [--is-deployer] [--deploys-in-eu]'
trigger: /startup-101 check eu-ai-act-tier
source_appendix:
  - appendix/compliance-matrix.md  # § 三 EU AI Act 时间线
  - modes/stage-5-ai-launch.md
profile_fields_used:
  - stage_5_output.self_trained_model
  - stage_5_output.ai_product_type
  - stage_5_output.target_market
  - stage_5_output.user_geography
  - stage_5_output.training_compute_flops
  - stage_5_output.training_data_includes_china_pi
  - stage_5_output.china_public_facing
profile_fields_written:
  - stage_5_output.eu_ai_act_role
  - stage_5_output.eu_ai_act_obligations
  - stage_5_output.eu_ai_act_deadline
  - stage_5_output.eu_ai_act_followup_commands
last_policy_review: 2026-04-15
---

# Check: EU AI Act 分级判定

> 📎 完整时间线见 [`appendix/compliance-matrix.md`](../../appendix/compliance-matrix.md) § 三。
> 本命令只做"**你是什么角色、走哪些义务、截止到哪天**"的判定。

## 何时用这个命令

- 产品已在 / 计划在欧盟 / EEA 投放（含 B2B SaaS、API 服务）
- 你训练了基础模型或发布了大模型 API（GPAI Provider 判定）
- 生成式 AI 应用（chatbot / AI 生成内容 / 深度合成）对欧盟用户可见
- 融资 DD 问到"EU AI Act roadmap"
- 合规团队想确认 2026-08-02 大日期前还有什么没做

## 输入

从 `./_profile.md` 读取：

| 字段 | 作用 |
|---|---|
| `stage_5_output.self_trained_model` | 自研基模 = 可能 GPAI Provider |
| `stage_5_output.ai_product_type` | generative / decision / biometric 影响分级 |
| `stage_5_output.target_market` | 是否 EU 市场 |
| `stage_5_output.training_compute_flops` | ≥ 10^25 FLOPs → systemic risk |

若字段缺失，一次问一个：

1. 产品是否在欧盟 / EEA 投放？（含欧盟 B2B 客户 / 欧盟终端用户 / 欧盟 region 部署） `[Y/N]`
2. 你是**提供方 (Provider)** 还是**部署方 (Deployer)**？
   - Provider = 开发并以自己名义投放 AI 系统 / 模型
   - Deployer = 使用他人的 AI 系统
   - 可能同时是两者（如你用 OpenAI API 做了自己的 chatbot） `[P/D/两者]`
3. 是否自研基础模型或通用大模型？（非微调） `[Y/N]`
4. 若自研：训练算力（累计 FLOPs）？ `[≥10^25 / <10^25 / 未知]`
5. 产品是否属于以下场景之一？
   - [a] 与人交互的 AI（chatbot、语音助手）
   - [b] 生成 synthetic 内容（文 / 图 / 音 / 视频）
   - [c] 情感识别 / 生物分类
   - [d] Deep fake / 深度合成
   - [e] HR / lending / housing / credit / law enforcement / migration / biometric ID（高风险候选）
   - [f] 禁用类（social scoring / 大规模生物识别抓取 / 操纵） `[多选]`
6. **训练语料是否含中国境内 PI？** `[Y/N/未定]` — 命中将叠加 PIPL 出境检查
7. 产品同时面向**中国大陆公众**上线？ `[Y/N]` — 命中将叠加算法 / 大模型备案检查

## 决策逻辑

### 第一层：是否适用

```
target_market 含 EU?
├─ 否 → ✅ 本命令不适用（但仍建议 Privacy / GDPR 单独走 check）
└─ 是 → 进入角色判定
```

### 第二层：角色判定

```
你是 Provider（发布 AI 系统 / 模型）吗？
├─ 是 + 自研基模 / 通用大模型 → 【GPAI Provider 义务】2025-08-02 已生效
├─ 是 + 高风险用途（场景 e） → 【高风险系统 Provider 义务】2026-08-02 / 2027-08-02
└─ 是 + 生成式 / 交互式 → 【Art. 50 透明度义务】2026-08-02 生效

你是 Deployer（使用 AI 系统）吗？
├─ 是 + 场景 a/b/c/d → 需履行 Deployer 侧的通知 / 人工监督等义务
└─ 是 + 场景 e → 高风险 Deployer 义务（冲击评估、人工监督、使用日志保存）

你是两者？
└─ 叠加，Provider 义务优先
```

### 第三层：GPAI Systemic Risk

```
training_compute_flops ≥ 10^25？
├─ 是 → 【Systemic Risk GPAI】额外义务：
│       - 模型评估 + 对抗测试
│       - 严重事件上报
│       - 网络安全措施
│       - 能源消耗披露
└─ 否 → 普通 GPAI 义务即可
```

### 第四层：自动 follow-up 命令注入

```
Q6 ∈ {Y, 未定}（训练语料含中国 PI）?
└─ 注入：/startup-101 check pipl-gap
        （并特别注意 § 六 场景 1 的语义冲突：PIPL 不鼓励披露 vs AI Act 要求披露）

Q7 == Y（中国公众）?
└─ 注入：/startup-101 check algorithm-filing

self_trained_model == Y + Llama 基模?
└─ 注入：/startup-101 check license-scan   # § 2 MAU 7 亿阈值 + 境外语料联动

禁用类场景 (f) 命中?
└─ 🚩🚩 立即停止开发；不是 follow-up，是 blocker
```

### 第五层：Art. 50 透明度义务逐项

| 系统类型 | 义务 | 命中？ |
|---|---|---|
| 与人交互的 AI (chatbot) | 必须明确告知"你在与 AI 交互" | a? |
| 生成 synthetic 内容 | 输出机器可读标识（watermark + metadata） | b? |
| 情感识别 / 生物分类 | 告知数据主体 | c? |
| Deep fake | 披露人工生成 / 操纵 | d? |
| 影响公共利益的 AI 文本 | 披露（无人工编辑审核时） | 特定场景 |

## 输出 schema

```markdown
# 🎯 EU AI Act 判定结果

**你的角色**：GPAI Provider / 高风险 Provider / Deployer / Art. 50 主体（可多选）
**是否 Systemic Risk GPAI**：Y / N
**关键截止日期**：
| 日期 | 必须完成的事项 |
|---|---|
| 2025-08-02 ✅（已生效）| GPAI Provider 义务已开始 |
| 2026-08-02 🎯 | Art. 50 透明度 + 多数高风险义务 |
| 2027-08-02 | Annex II 嵌入式产品 AI |

## 你的义务清单

### GPAI Provider（若命中）
- [ ] 技术文档（Annex XI）— 架构 / 训练 / 能力 / 评估
- [ ] 训练数据摘要（按 AI Office 模板）
- [ ] 版权政策（Art. 53 (1)(c)）
- [ ] 下游 Provider 信息披露
- [ ] Code of Practice 签署（可选但推荐）

### Systemic Risk 额外（若 FLOPs ≥ 10^25）
- [ ] 模型评估报告（含 red-team）
- [ ] 事件上报流程
- [ ] 能源消耗披露

### Art. 50（若命中）
- [ ] Chatbot：UI 明确标注"AI 助手"
- [ ] 生成内容：嵌入水印 + 元数据 + 肉眼可见标签
- [ ] Deep fake：披露文案模板
- [ ] 隐私政策中加入 Art. 50 专章

## 🚩 常见踩坑
1. <基于命中场景动态生成>
2. ...

## 必须跑的 follow-up 命令（自动生成）
- [ ] `/startup-101 check pipl-gap`（命中条件：Q6 = Y/未定）
- [ ] `/startup-101 check algorithm-filing`（命中条件：Q7 = Y）
- [ ] `/startup-101 check license-scan`（命中条件：自研 + Llama 基模）

## 冲突管理（中国 × EU）
- PIPL 不鼓励披露训练数据细节 vs AI Act 要求训练数据摘要公开
- 建议：训练数据摘要采用"数据类别 + 粗占比 + 来源类型"粒度披露
- 律师审阅语义边界（详见 appendix/compliance-matrix.md § 六 场景 1）

## 估算成本
- GPAI 合规顾问：€20-50k 一次性 + €5-10k/年维护
- 水印 / 元数据工程：2-6 周研发
- 技术文档起草 + 维护：€10-20k

## 深入阅读
- 完整时间线：appendix/compliance-matrix.md § 三
- 叠加场景：§ 六 场景 1
- 官方：https://artificialintelligenceact.eu/implementation-timeline/
- Code of Practice：https://artificialintelligenceact.eu/introduction-to-code-of-practice/
```

## 关键红旗

| # | 红旗 | 判定条件 | 后果 |
|---|---|---|---|
| 1 | **GPAI 未公示训练数据摘要** | self_trained + EU 投放 + 过期未发布 | AI Act 罚款最高 €15M 或 3% 全球营收 |
| 2 | **生成式 AI 无水印 + 无 UI 标识** | Art. 50 场景 + 2026-08 后 | 每次违规可追罚 |
| 3 | **Systemic Risk 但未履行额外义务** | FLOPs ≥ 10^25 + 缺事件上报 | 最重等级罚款 |
| 4 | **Deployer 不知道自己有义务** | Deployer 场景 e | 高风险 Deployer 义务漏做 |
| 5 | **Code of Practice 未签但也未自证合规** | 无 pathway | 监管默认视为"待证实" |
| 6 | **禁用类 AI 实践**（social scoring 等） | 场景 f | 2025-02-02 已禁 |

## 写回 profile

```yaml
stage_5_output:
  eu_ai_act_role: [gpai_provider, art50_subject]
  eu_ai_act_systemic_risk: false
  eu_ai_act_obligations:
    - training_data_summary
    - copyright_policy
    - art50_chatbot_disclosure
    - art50_watermarking
  eu_ai_act_deadline: 2026-08-02                # EU 硬截止日
  eu_ai_act_followup_commands:
    - /startup-101 check pipl-gap               # Q6 命中
    - /startup-101 check algorithm-filing       # Q7 命中
    - /startup-101 check license-scan           # Llama 基模命中
  eu_ai_act_scan_date: 2026-04-21
```

## 限界

- **本命令不判定 Annex III 高风险分类细节** — 若命中场景 e，需律师专项判定
- **不覆盖各成员国本地附加**（如德国 BDSG / 法国 CNIL 特别意见）
- **不判定出口管制 / 双重用途**（另类合规）
- **Code of Practice 条款逐条解读** 见律所专项服务
