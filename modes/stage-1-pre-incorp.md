# Stage 1: Pre-incorporation — 注册前

> last_policy_review: 2026-04-15

## 读取前置状态

从 `_profile.md` 读取：
- `team_size`, `roles`, `founder_background` — 决定是否需要联创协议 + 主创背景
- `archetype` — 决定本阶段分支提问重点（A 可跳过 37 号文 / 税籍迁移讨论）
- `founders_tax_residency` — 决定决策 4（个人税籍锁定）
- `fundraising_intent` + `target_currency` — 决定决策 3（架构前置判断）
- `stage_0_output.archetype` — 作为决策依据

## 何时进入

- 还没注册公司
- 和联创已经开始讨论但没落地
- 纠结架构选择

## Disclaimer

> ⚠️ 本阶段涉及股权 / 合伙协议 / 个人税籍 / 架构选择等影响未来 10 年的决策。
> Skill 只给决策框架。**联创协议和架构设计必须找律师起草。**

## 核心决策点

### 决策 1：要不要先签联合创始人协议？

**判定：**
- 1 人 solo → 不需要
- 2+ 人联创 → **强烈建议注册公司前就签**

**原因：** 很多联创关系在公司注册前就破裂，没协议则无法追索。

**联创协议关键条款：**
- vesting 4 年 + 1 年 cliff（防止有人拿了股份立刻跑）
- 股权分配（见决策 2）
- 决策机制（谁拍板 / 一票否决范围）
- 退出条款（good leaver / bad leaver）
- IP 归属（在注册公司前做的所有 IP 自动转给未来公司）
- 竞业限制（离开后不能做同类产品多久）

**模板参考：** Cooley GO `Founders' Agreement Template`（见 references/index/02-incorporation.md）

---

### 决策 2：股权初分

**三种典型分法：**

| 分法 | 适用 | 风险 |
|---|---|---|
| **均分 50/50（2 人）** | 真正 50/50 投入 + 互补 + 都能全职 | **治理死穴** — 一方离开就僵局 |
| **主导 60-80% + 联创 20-40%** | 有明显主 founder | 相对健康 |
| **55/45 带 tiebreaker 条款** | 双方贡献相当但想避免僵局 | 需要明确 tiebreaker 机制 |

**期权池预留：**
- 首轮融资前预留 **10-15%** ESOP（期权池）
- 注意：期权池稀释的是创始人，不是新投资人（典型坑）

**建议范围：**
- 创始人总股权：45-70%
- 联创：20-40%
- 期权池：10-15%
- （未来融资稀释：每轮 15-25%）

**红旗：**
- 🚩 50/50 均分没 tiebreaker 条款
- 🚩 联创没 vesting
- 🚩 过早引入产业资本占 20%+（见石头《融资指南》§10）

---

### 决策 3：架构前置判断

**这不是决定最终架构，而是判断你现在的 profile 适合哪条路。**

参考 `appendix/entity-matrix.md` 决策树：

```
融美元？
├─ 是 → 研发在中国？
│       ├─ 是 → Cayman + HK + WFOE（非 VIE）→ Stage 2 走「红筹路径」
│       └─ 否 → Delaware C-corp 或 SG Pte Ltd → Stage 2 走「纯海外路径」
└─ 否 → 订阅制 / 海外用户 >30%？
        ├─ 是 → HK Ltd + Paddle MoR → Stage 2 走「HK 路径」
        └─ 否 → 纯内资有限公司 → Stage 2 走「内资路径」
```

**输出：** 在 `_profile.md` 的日志 section 记录你的架构选择。

---

### 决策 4：个人税籍锁定

**Archetype B/C 必须处理：**

| 当前身份 | 影响 | 建议 |
|---|---|---|
| **中国税务居民** | 全球收入理论上都要交中国个税（但有 6 年豁免境外收入规则）| 融资前决定是否保留 |
| **香港优才/高才通** | 7 年转永居，HK 税率低 | 推荐，但要考虑离开中国的时间 |
| **新加坡 EP** | 2024 后门槛高（COMPASS SGD 5.6k+）| 难度上升，谨慎 |
| **美国绿卡/公民** | 全球征税，最重 | 融资前决定是否放弃 |

**红旗：**
- 🚩 美国绿卡持有人做 Delaware C-corp 创始人：未来退出要交巨额全球税
- 🚩 融资后才想换税籍：可能触发 exit tax

---

## 必查清单

- [ ] 联创协议已签（2+ 人）
  - [ ] vesting 4+1
  - [ ] 股权分配表
  - [ ] IP 归属条款
  - [ ] 退出 good/bad leaver
- [ ] 股权初分决定（见决策 2）
- [ ] 期权池规模确定（10-15%）
- [ ] 架构前置判断完成（4 条路径选一）
- [ ] 个人税籍规划完成（Archetype B/C）
- [ ] 找到预选律所（跨境律所名单，见 references）

## 典型避坑场景

**场景 1：50/50 均分的代价**
某 AI 创业公司两个联创 50/50 均分，一年后理念分歧，一方要卖公司另一方不同意。因为没有 tiebreaker 也没有 vesting，公司卡死 8 个月，最终被迫低价 acqui-hire。

**场景 2：期权池后加的稀释陷阱**
某 A 轮融资时才临时预留期权池，结果期权池是**从创始人而非新投资人稀释**，创始人多稀释了 10%，直接损失数百万。

**场景 3：架构没前置的代价**
某 AI 公司融人民币基金 5000 万，一年后想转美元路径融下一轮，翻红筹花 10 个月 + 重组税 800 万，相当于烧掉半年 runway。

## 红旗扫描（本阶段）

调用 `modes/red-flags.md`，重点关注：
- Red Flag 2（IP Assignment 起点就要对）
- 联创协议缺失（新增未在 6 条主红旗中，但本阶段要扫）

## 推荐阅读

- `references/index/02-incorporation.md` § Cooley GO Founders' Agreement
- `references/index/05-fundraising.md` § 石头《融资指南》§10.2 创始人个人责任 / §10.3 控制权
- Paul Graham *How to Start a Startup*

## 本阶段输出（写入 _profile.md）

按 `_profile.template.md` 中 `stage_1_output` schema 写入：

```yaml
stage_1_output:
  completed_at: <YYYY-MM-DD>
  founder_count: <1 | 2 | 3 | 4+>
  founder_agreement_signed: <yes | no | not_applicable>
  vesting_structure: <"4+1" | "3+1" | "other:..." | none>
  equity_split_decided: <yes | no>
  esop_pool_reserved_pct: <0-20>
  arch_path_shortlist: <A | B1 | B2 | C1 | C2>
  personal_tax_residency_plan: <不动 | 迁港 | 迁新 | 迁美 | 其他>
  counsel_shortlisted: <yes | no>
```

并在 `completed_stages` 追加 `1`，然后进入 Stage 2 Incorporation。
