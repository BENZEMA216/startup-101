# Stage 0: Profile 分流

> 目标：4 个核心问题 + 若干补充问题，判定用户属于 A/B/C 哪档，初始化 `_profile.md`。

## 读取前置状态

Stage 0 是入口，**无前置依赖**。但若 `_profile.md` 已存在：
- 检查 `profile_schema_version`，若 < 0.3 走 SKILL.md 的迁移流程
- 检查 `archetype` 是否已填，若已填则询问用户是否重做 profile

## Flow

### 开场

> 先做个 Profile（约 2 分钟），帮我判断你的情况。一次问一个。

### 核心 4 问（决定 Archetype）

**Q1. 你的目标用户主要在哪？**
- [a] ≥70% 在中国
- [b] ≥70% 在海外
- [c] 均衡 / 还不确定

**Q2. 你计划融什么币种的钱？**
- [a] 人民币基金
- [b] 美元基金
- [c] 暂不融 / 靠收入
- [d] 都想要

**Q3. 产品是否收订阅费 / C 端付费？**
- [a] 是，订阅制
- [b] 按次计费 / 买断
- [c] ToB 大客定制
- [d] 免费 / 广告

**Q4. 研发团队必须在中国吗？**
- [a] 必须，核心在国内
- [b] 可以分布式
- [c] 我已经在海外 / 打算搬过去

### Archetype 判定规则

```
IF Q1=a AND Q2=a AND Q3≠a:
  → Archetype A (纯内资)
ELIF Q4=c OR (Q1=b AND Q4=b):
  → Archetype C (创始人已出海)
ELSE:
  → Archetype B (双层出海 — 默认)
```

### 补充信息（按 Archetype 分别收集）

**所有 archetype 都问：**
- 团队规模（1 / 2-5 / 6-15）
- 城市（深圳 / 北京 / 上海 / 杭州 / 其他）
- AI 方向（LLM 应用 / Agent / AIGC / 基础模型 / 具身 / 其他）
- 是否自研模型（yes / no — 决定算法备案 vs 登记路径）
- 是否面向公众（yes / no — 决定是否触发舆论属性备案）

**仅 Archetype B/C 额外问：**
- 创始人当前税务居民身份（中国 / 香港 / 新加坡 / 美国 / 其他）
- 是否已在境外设 SPV（yes / no — 决定 37 号文紧急度）

### 输出

1. 写入 `./_profile.md` 全部字段
2. `archetype` 字段填充为 A/B/C
3. `completed_stages` append `0`
4. 展示判定结果：

```
你的 Archetype：B（双层出海）

推荐路径：
- 架构：Cayman + HK + WFOE（或 Delaware + HK）
- 收款：Stripe SG / US + Airwallex 对冲
- 融资：美元基金为主
- 合规：PIPL 出境 + GDPR + EU AI Act 三重叠加
- 必办：37 号文 + IP Assignment 指向海外主体

接下来你想进入哪个阶段？
[1] 还没注册，纠结架构 → Stage 1
[2] 已决定架构，准备注册 → Stage 2
[3] 刚拿到执照，不知道接下来 30 天干啥 → Stage 3
[4] 要招人、发期权 → Stage 4
[5] AI 产品要上线，不懂合规 → Stage 5
[6] 准备融资 → Stage 6
[7] 已融完，要处理持续义务 → Stage 7
```

## 完成条件

用户 `_profile.md` 的前 5 组字段全部填充，`archetype` 非空。

## 本阶段输出（写入 _profile.md）

```yaml
stage_0_output:
  completed_at: <YYYY-MM-DD>
  archetype: <A | B | C>
  primary_ambiguity: <若有 profile 答案歧义 / 还不确定项，在此记录；否则 null>
```

并在 `completed_stages` 追加 `0`。
