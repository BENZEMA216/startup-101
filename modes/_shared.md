# Shared Rules (_shared.md)

> 本文件定义 startup-101 的全局规则、7 阶段定义、disclaimer 文案。所有 stage 和 mode 文件 MUST 加载此文件。

## Disclaimer（每个阶段入口必须展示）

> ⚠️ startup-101 不是律师 / 会计师 / 税务师意见。
> 所有具体决策必须由专业机构二次确认。
> 政策变化快（尤其 AI 合规、跨境数据、EU AI Act），请交叉验证最新信息。

## 7 阶段定义

| Stage | 名称 | 进入条件 | 核心交付物 |
|---|---|---|---|
| 1 | Pre-incorporation | 还没注册公司 | 联创协议 / 股权初分 / 架构选择 |
| 2 | Incorporation | 决定架构，准备注册 | 执照 + 章程 + 公章 + 开户 |
| 3 | Day-30 | 刚拿到执照 | 税务登记 / 代账 / 发票规范 / 社保 |
| 4 | Hiring & Equity | 要招人、发期权 | ESOP 文件 / 劳动合同 / IP Assignment |
| 5 | AI 产品上线前 | 产品将 go-live | 算法备案 / GDPR / AI Act / PIPL 出境 |
| 6 | Fundraising | 准备融资 | BP / Termsheet 审阅 / SAFE / 条款红线 |
| 7 | Ongoing | 已融完 | 月/季/年报 / 审计 / 转让定价 / GPAI 年检 |

## 3 档 Archetype

| Archetype | 判定 | 推荐路径 |
|---|---|---|
| A. 纯内资 | ≥70% 中国用户 + 不融美元 + 非订阅出海 | 内资有限 → 国内合规 → 人民币基金 |
| B. 双层出海（默认） | 研发在中国 + 用户全球或美元融资 | Cayman/SG + WFOE / Delaware + HK / 37号文 + ODI |
| C. 创始人已出海 | 创始人已在海外 + 研发分布式 | 纯 Delaware C-corp / SG Pte Ltd / Mercury / QSBS |

## 6 条红旗清单（跨阶段主动扫描）

1. **37 号文未办** — 中国居民境外 SPV 持境内权益未登记 → 分红/退出汇不回
2. **IP Assignment 未指向海外主体** — 融资 DD 爆雷
3. **个人 PayPal/微信收订阅规模化** — >$50k/年 涉嫌非法结汇
4. **Llama Community License 违规** — 月活 7 亿上限 / 不得改进其他 LLM
5. **AGPL 污染** — 传染 SaaS 闭源代码
6. **EU 无 Art. 27 代表** — 欧盟用户 >0 必须有欧盟代表

## Skill 路由原则

- 每次调用先读 `_profile.md`（用户当前目录）
- 未完成 profile → 跳 stage-0-profile.md
- 已完成 → 根据 `current_stage` 字段或用户选择进入对应 stage
- 每个 stage 结束后 append 结果到 profile，询问是否继续

## 引用策略

- 内置全文仅限 License 清楚的资源（见 references/README.md）
- 其他一律通过 references/index/ 做摘要 + URL
- 用户本地 clip（如 Obsidian）通过环境变量 `$OBSIDIAN_CLIPPINGS` 引用，开源版剔除

## v0.2 stage 覆盖状态

| Stage | 状态 | 文件 |
|---|---|---|
| 0 | ✅ | modes/stage-0-profile.md |
| 1 | ✅ | modes/stage-1-pre-incorp.md |
| 2 | ✅ | modes/stage-2-incorporation.md |
| 3 | ✅ | modes/stage-3-day30.md |
| 4 | ✅ | modes/stage-4-hiring-equity.md |
| 5 | ✅ | modes/stage-5-ai-launch.md |
| 6 | ✅ | modes/stage-6-fundraising.md |
| 7 | ✅ | modes/stage-7-ongoing.md |

## 政策复核时间戳约定

每个 stage / appendix 文件顶部 MUST 标注 `last_policy_review: YYYY-MM-DD`，便于未来重校。v0.2 基线：**2026-04-15**。

## Profile Linkage Contract（v0.3 新增）

为保证多 stage 之间上下文不丢，v0.3 规定以下**强约束**：

### 1. Schema 版本

- `_profile.template.md` 顶部声明 `profile_schema_version: 0.3`
- Skill 每次读取用户 `_profile.md` 时**必须**先检查该字段：
  - 无字段 / 字段 < 0.3 → 提示用户迁移或重建
  - 字段 = 当前版本 → 正常流程

### 2. Read-before-enter（进入前读取）

- 进入 `stage-N.md` **之前**，skill MUST 读取所有 `stage_M_output` (M < N) section
- 把其中非 null 的关键字段总结为 2-5 行摘要呈现给用户
- 示例："你在 Stage 2 选了 B1（Cayman+HK+WFOE），37 号文已登记，银行账户部分开通。Stage 3 将基于此展开。确认继续？"

### 3. Write-on-exit（退出时写入）

- 每个 `stage-N.md` 底部 MUST 定义该 stage 要写入的 `stage_N_output` keys
- Stage 结束时，skill MUST 把收集到的答案按 schema append / 更新到用户 `_profile.md` 的 `stage_N_output` section
- `completed_at: YYYY-MM-DD` 必填（使用当天日期）
- `completed_stages` 数组同步追加 `N`

### 4. Schema 冲突处理

- 如果用户 `_profile.md` 的 schema 版本 < 当前，skill 采取 **"保留答案 + 追加空 stage_N_output section"** 的非破坏性迁移
- 用户可选：`migrate` / `fresh_start` / `abort`

### 5. 每个 stage 文件结构约定（v0.3 起）

```markdown
# Stage N: <名称>
> last_policy_review: YYYY-MM-DD

## 读取前置状态    ← v0.3 新增
<列出依赖哪些 stage_M_output 字段>

## 何时进入
## Disclaimer
## 核心决策点
...
## 本阶段输出（写入 _profile.md）   ← v0.3 替换旧的"本阶段结束状态"
<以 yaml 列出该 stage 要写入 stage_N_output 的 keys>
```
