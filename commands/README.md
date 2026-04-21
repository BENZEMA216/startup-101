# startup-101 / commands

**原子命令工具箱**。与 `modes/` 的 stage-driven 主线互补：

- **菜鸟**：走 `modes/` 主线（`/startup-101` → 阶段自诊断 → 按 stage 走）
- **老手 / 复用用户**：直接调 `commands/` 里的原子命令做单点检查

## 设计原则

1. **无强依赖 `_profile.md`**：有就用，没有就问。每个命令自己能跑。
2. **单一职责**：一个命令只回答一个问题。
3. **输出可追加到 profile**：命令结束时，关键结论可写入 `_profile.md` 的 `stage_N_output` 字段（兼容 v0.3 schema）。
4. **引用 appendix 而不复制**：知识源仍在 `appendix/`，命令只做决策封装。

## 命令分类（按动词）

| 目录 | 意图 | 典型命令 |
|---|---|---|
| `check/` | 自查：我这样会不会踩雷？ | `check/algorithm-filing` `check/37hao-exposure` `check/pipl-gap` |
| `review/` | 审查：这份文档有没有坑？ | `review/safe-terms` `review/term-sheet` |
| `generate/` | 生成：给我一份 XX 模板 | `generate/cap-table` `generate/dpia` |
| `compare/` | 比较：A 还是 B？ | `compare/entity-structure` `compare/payment-rails` |
| `redflags/` | 扫描：主动找雷 | `redflags/scan-all` `redflags/hidden-vie` |

## 调用形式

通过主 skill 路由：

```
/startup-101 check algorithm-filing
/startup-101 review safe-terms
/startup-101 compare entity-structure
```

或直接让 Claude Code 读取对应文件：

```
按 commands/check/algorithm-filing.md 帮我判定我的产品需要哪条备案轨道
```

## 命令文件约定

每个命令文件顶部 frontmatter：

```yaml
---
name: <命令标识>
description: <一句话能力说明>
argument-hint: [可选参数]
trigger: /startup-101 <category> <name>
source_appendix: <引用的 appendix 路径>
profile_fields_used: [list of _profile.md keys read]
profile_fields_written: [list of _profile.md keys appended]
last_policy_review: YYYY-MM-DD
---
```

Body 结构：

1. **何时用这个命令**（2-3 句场景）
2. **输入要求**（profile 字段 / 缺失则问什么）
3. **决策逻辑**（决策树 / 判定表）
4. **输出 schema**（返回给用户 / 写回 profile 的字段）
5. **红旗**（必答的风险提示）
6. **深入阅读**（指向 appendix 链接）

## 当前状态（v0.4）

### 已完成（第一批 6 条高优）

- [x] `check/algorithm-filing` — 算法备案三轨判定
- [x] `check/37hao-exposure` — 37 号文暴露扫描（创始人 + 员工两侧）
- [x] `check/pipl-gap` — PIPL 出境三档判定
- [x] `check/eu-ai-act-tier` — EU AI Act 角色 + 义务清单
- [x] `check/cross-border-payment` — 跨境收款路径选择
- [x] `check/license-scan` — Llama / AGPL / SSPL 合扫（RF4 + RF5）
- [x] `redflags/scan-all` — 6 条主红旗扫描 + 深入命令路由

### 待补（v0.5+）

- [ ] `check/ip-assignment` — IP Assignment 追溯（RF2 专项）
- [ ] `review/safe-terms` — YC SAFE 四变体逐条审查
- [ ] `review/term-sheet` — VC term sheet 逐条解读
- [ ] `review/employment-contract`
- [ ] `review/privacy-policy`
- [ ] `compare/entity-structure` — 5 种架构对比
- [ ] `compare/payment-rails`
- [ ] `compare/jurisdictions`
- [ ] `generate/cap-table`
- [ ] `generate/dpia`
- [ ] `generate/ip-assignment`
- [ ] `generate/investor-update`
- [ ] `redflags/hidden-vie`
- [ ] `redflags/founder-visa`
- [ ] `redflags/ai-data-source`

补齐节奏见 `ROADMAP.md`。
