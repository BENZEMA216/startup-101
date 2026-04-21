---
name: check-license-scan
description: 依赖 license 扫描 — 识别 AGPL 污染 / Llama Community License 违规 / 其他高风险 license，给出替换方案 + 风险评分
argument-hint: '[--dep-file <package.json|pyproject.toml|go.mod|...>] [--model <llama|qwen|deepseek|mistral|...>]'
trigger: /startup-101 check license-scan
source_appendix:
  - modes/red-flags.md  # Red Flag 4 + Red Flag 5
  - references/index/04-ai-tech.md
profile_fields_used:
  - ai_track
  - product_form
  - stage_5_output.self_trained_model
  - stage_5_output.base_model_family
  - stage_5_output.mau_estimate
profile_fields_written:
  - stage_5_output.license_scan_snapshot
  - stage_5_output.license_remediation_deadline
last_policy_review: 2026-04-15
---

# Check: 依赖 License 扫描（AGPL × Llama × 其他）

> 📎 完整原理见 [`modes/red-flags.md`](../../modes/red-flags.md) § Red Flag 4（Llama）+ Red Flag 5（AGPL）。
> 本命令把两类最致命的 license 陷阱合成一次扫描，不复述每类 license 全文。

## 何时用这个命令

- 产品形态 = **SaaS / 网络服务 / API**（AGPL 的风险载体）
- 基础模型用 **Llama 2 / Llama 3 / Llama Guard 系**
- 融资前做"法务体检"
- 预计 MAU 将突破 **7 亿月活**（Llama 条款触发线）
- 依赖了向量数据库 / 图数据库 / PDF 处理 / 文本搜索等容易踩 AGPL 的领域
- 代码仓库在外部律所 DD 之前

## 输入

从 `./_profile.md` 读取：

| 字段 | 作用 |
|---|---|
| `ai_track` | 是否 LLM 应用 / Agent / 基模方向 |
| `product_form` | saas / on-prem / cli / library |
| `stage_5_output.self_trained_model` | 是否自训 |
| `stage_5_output.base_model_family` | llama / qwen / deepseek / mistral / in-house |
| `stage_5_output.mau_estimate` | 是否接近 7 亿 Llama 阈值 |

若字段缺失，一次问一个：

1. 产品形态？ `[a] SaaS / 网络服务` `[b] 自部署（客户本地跑）` `[c] CLI / 库` `[d] 混合`
2. 你的基础模型家族？ `[llama / qwen / deepseek / mistral / gemma / phi / 自训 / 仅调 API / 无基模]`
3. （若选 llama）是否用 Llama 输出**训练 / 微调 / 蒸馏**其他 LLM？ `[Y/N]`
4. （若选 llama）预期 18 个月内 MAU 是否可能超过 **7 亿**？ `[很可能 / 不可能 / 未知]`
5. 请粘贴你的依赖清单（选一）：
   - `package.json` / `package-lock.json`
   - `pyproject.toml` / `requirements.txt` / `uv.lock`
   - `go.mod` / `go.sum`
   - `Cargo.toml` / `Cargo.lock`
   - 或直接告诉我几个核心依赖名字

## 决策逻辑

### 第一层：Llama 条款扫描（Red Flag 4）

```
base_model_family == llama?
├─ 否 → ✅ Llama 侧跳过
└─ 是 → 检查 3 条硬线：
    ├─ 🚩 用 Llama 输出改进其他 LLM（§ 1.b）→ 违规
    ├─ 🚩 MAU ≥ 7 亿 无单独许可（§ 2）→ 违规
    └─ 🚩 未在 app / site / 文档显示 "Built with Llama" 标注 → 合规缺口
```

**Llama 3 Community License 关键硬线（2024-04 版）：**

| 条款 | 要点 |
|---|---|
| § 2 许可范围 | 授予"免费非独占使用权"，但若前一个完整日历月 MAU ≥ 7 亿，**必须向 Meta 申请单独商业许可** |
| § 1.b 输出限制 | 不得用 Llama 输出**改进 / 训练 / 蒸馏**其他 LLM |
| § 5 商标 | 产品显著位置标注 "Built with Llama" / "Meta Llama" |
| § 6 归属 | 分发时附带本 License 文本 |
| § 7 终止 | Meta 有权因违反条款**撤销许可** |

### 第二层：AGPL 污染扫描（Red Flag 5）

```
product_form ∈ {saas, api, 网络服务}?
├─ 否（CLI / on-prem 库）→ AGPL 风险低（但仍受 GPL 限制）
└─ 是 → 扫描依赖树：
    ├─ 直接依赖 AGPL → 🚩🚩 一级污染
    ├─ 传递依赖 AGPL → 🚩 二级污染（同样要治）
    └─ 依赖"曾 AGPL 现 SSPL / 商业双许可" → ⚠️ 核对实际版本
```

**常见 AGPL / SSPL 陷阱**：

| 组件 | 历史 | 现状 |
|---|---|---|
| MongoDB Community | AGPL → SSPL | SSPL 对 SaaS 同样杀伤 |
| Ghostscript | AGPL | 替换为 poppler (GPL) 或商业版 |
| TigerGraph Free | AGPL 部分 | 商用需看具体版本 |
| PrinceXML | 商业 / AGPL 双 | 商用必须买 license |
| Plausible Analytics | AGPL | 自托管 SaaS 会触发开源条款 |
| Mautic / Metabase 部分 | AGPL | 按部署形态 |
| some vector DB 历史版本 | AGPL | 新版多数已切 Apache 2.0 |

### 第三层：其他中高危 license

| License | 危险点 | 处置 |
|---|---|---|
| **GPL-2.0 / GPL-3.0** | 链接你的代码 → 整体 GPL 污染（若动态链接也可能） | 替换或买豁免 |
| **BSL (Business Source License)** | 非生产商用限制 + 4 年后转 Apache | 读清 Usage Grant |
| **Elastic License / SSPL** | SaaS 托管他人 = 禁用 | 换 Apache 分支（OpenSearch 等） |
| **Commons Clause** | 不允许"销售" | 商用审慎 |
| **Llama Community** | 见上 | 条款硬线核对 |
| **研究专用 (Research Only)** | 商用禁止 | 替换（如早期 Mistral Research）|
| **CC BY-NC** | 禁商用 | 替换 |
| **Custom / 未知** | 风险最高 | 默认视为不可用直到律师核定 |

### 第四层：风险评分

按下表加权（满分 10）：

| 条件 | 分数 |
|---|---|
| Llama + 用输出训其他 LLM | +5 |
| Llama + MAU ≥ 7 亿无许可 | +5 |
| Llama + 无 "Built with Llama" 标注 | +1 |
| SaaS + 直接依赖 AGPL | +4 |
| SaaS + 传递依赖 AGPL（未审计） | +2 |
| 依赖含 SSPL / Elastic 且托管分发 | +3 |
| 依赖含 Custom / 未知 license | +2 |
| Research Only 模型用于商用 | +4 |

- **0-2**：低风险，年度复查
- **3-5**：中风险，30 天内治理
- **6-8**：高风险，停止新功能发布，优先替换
- **≥ 9**：立即下线 / 停止对外商用

## 输出 schema

```markdown
# 🎯 License 扫描结果

**扫描日期**：2026-04-21
**覆盖范围**：<依赖文件 / 模型家族>
**总体风险评分**：X / 10
**建议治理窗口**：<立即 / 30 天 / 90 天 / 无需>

## 🚩 命中的硬红旗
| # | 红旗 | 组件 / 模型 | 建议动作 |
|---|---|---|---|
| 1 | ... | ... | ... |

## ⚠️ 中等风险
| # | 问题 | 组件 | 建议 |
|---|---|---|---|

## ✅ 已核对无风险
- <list>

## 替换方案对照

### 基模替换（若 Llama 有风险）
- Qwen（Apache 2.0）— 无 MAU 上限，商用自由
- DeepSeek（Apache 2.0）— 同上
- Mistral（按版本核对，部分 Apache 2.0，部分 Research Only）
- 自训 from scratch（成本最高）

### 常见 AGPL 组件替换
- MongoDB → PostgreSQL + JSONB
- Ghostscript → poppler（GPL）或商业 Adobe
- Plausible（SaaS 托管）→ PostHog / Umami（MIT）

## 下一步
- [ ] 将扫描结果写入 _profile.md (stage_5_output.license_scan_snapshot)
- [ ] 若风险评分 ≥ 6：暂停 license 范围内功能的新发布
- [ ] 生成依赖治理 TODO
- [ ] 融资 DD 前 30 天再跑一次

## 深入阅读
- Red Flag 4（Llama）：modes/red-flags.md
- Red Flag 5（AGPL）：modes/red-flags.md
- Llama 3 License：https://llama.meta.com/llama3/license/
- AI 技术栈选型：references/index/04-ai-tech.md
```

## 关键红旗

| # | 红旗 | 判定条件 | 后果 |
|---|---|---|---|
| 1 | **Llama 输出用于训其他 LLM** | 任何"distillation from Llama" 事实 | Meta 撤销许可 + 产品下架风险 |
| 2 | **Llama + 预期 MAU 接近 7 亿** | 社交 / 工具类产品增速快 | 需 Meta 单独许可，大概率谈不下来 |
| 3 | **SaaS 直接依赖 AGPL** | 依赖树一级有 AGPL | 必须开源 SaaS 所有代码 |
| 4 | **依赖里有 MongoDB Community 但运行于 SaaS** | SSPL 同样禁止 | 业务模式冲突 |
| 5 | **"曾 AGPL 现商业双许可"但未买商业** | 白嫖违规 | 侵权诉讼 |
| 6 | **自研模型却声称 "based on Llama" 做营销** | 表述不一 | 一旦翻脸 Meta 可诉 |
| 7 | **使用 Research Only 模型做商用** | 任何 RL-only 许可 | 侵权 + 诉讼 |
| 8 | **依赖锁文件 (lock file) 未提交** | 无法验证版本 | DD 时盲扫 = 视为高风险 |

## 写回 profile

```yaml
stage_5_output:
  license_scan_snapshot:
    scan_date: 2026-04-21
    risk_score: 7
    llama_issues: [mau_threshold_close, missing_attribution]
    agpl_issues: [mongodb_community_in_saas]
    other_issues: []
    remediation_plan:
      - swap_mongodb_to_postgres_by: 2026-05-20
      - add_built_with_llama_badge_by: 2026-04-28
      - evaluate_qwen_migration: exploratory
  license_remediation_deadline: 2026-05-20
```

## 限界

- **本命令不做代码级依赖树展开** — 需配合工具（`npm ls` / `pnpm why` / `pipdeptree` / `go mod graph` / `cargo tree`）
- **不覆盖 Patent Grant 条款差异**（Apache vs MIT 专利条款差异需律师审）
- **不覆盖合同 license（如 SaaS 供应商条款）** — 属合同法范畴
- **政策时效性** — Llama license 可能出新版本，顶部 `last_policy_review` 需定期复核
