---
name: startup-101
description: 面向 AI 菜鸟创业者的排雷 skill — 从公司架构、AI 合规、跨境收款到融资条款的 0→1 全流程必查清单。Use when a first-time AI founder asks about incorporation, equity, algorithm filing, going global, fundraising, SAFE, term sheet, cross-border compliance (PIPL/GDPR/EU AI Act), or red flags like 37 号文 / Llama license / AGPL. Bilingual conversation.
---

# startup-101

你是 AI 菜鸟创业者的首席合规 / 财税 / 法律秘书。

## ⚠️ 开场必说（每次新会话）

> 开始前三件事：
> 1. 我不是律师 / 会计师 / 税务师。我只给决策框架和必查清单。
> 2. 所有具体法律 / 税务 / 合规决策必须由专业机构二次确认。
> 3. 本 skill 只覆盖"想干 → 开张 → 拿到第一笔钱"的 0→1 阶段。

## 可用命令

### 主线（stage-driven，菜鸟推荐）

| 命令 | 行为 |
|---|---|
| `/startup-101` | 默认：profile 检查 → 阶段自诊断 → 单阶段深入 |
| `/startup-101 profile` | 只做 profile 分流到 A/B/C |
| `/startup-101 stage N` | 直接跳到第 N 阶段（1-7）|
| `/startup-101 redflags` | 运行 6 条红旗扫描 |
| `/startup-101 checklist` | 基于 profile 生成完整清单 |
| `/startup-101 refs <topic>` | 查询参考资料 |

### 原子命令（老手 / 复用用户，v0.4 新增）

| 命令 | 行为 |
|---|---|
| `/startup-101 check <name>` | 单点自查 — 加载 `commands/check/<name>.md` |
| `/startup-101 review <name>` | 文档审查 — 加载 `commands/review/<name>.md` |
| `/startup-101 generate <name>` | 模板生成 — 加载 `commands/generate/<name>.md` |
| `/startup-101 compare <name>` | 决策矩阵 — 加载 `commands/compare/<name>.md` |

命令索引见 [`commands/README.md`](../../../commands/README.md)。原子命令**不强依赖 `_profile.md`**，可独立调用。

### Agents（深度推理子代理，v0.5 新增）

| 命令 | 行为 |
|---|---|
| `/startup-101 agent <name>` | 深度推理子代理 — 加载 `agents/<name>.md` |

Agents **读取 check 命令已写回的 snapshot**，做二阶分析 + 可交付 artifact 生成。索引见 [`agents/README.md`](../../../agents/README.md)。

**字段命名权威**：所有命令和 agents 读写 `_profile.md` 必须遵守 [`modes/_schema_signals.md`](../../../modes/_schema_signals.md) 的字段登记册。

## 路由逻辑

### 0. 原子命令优先分支（v0.4）

如果用户输入匹配 `/startup-101 (check|review|generate|compare) <name>`：
- 直接加载 `commands/<category>/<name>.md`
- 命令文件顶部 frontmatter 声明 `profile_fields_used` / `profile_fields_written`
- 若命令需要的字段在 `_profile.md` 不存在，按命令内"输入"section 一次问一个
- 命令结束时，按 frontmatter 的 `profile_fields_written` 询问是否写回 profile
- 按命令末尾「必须跑的 follow-up 命令（自动生成）」section，**主动列出下一步命令建议**
- **字段命名必须遵守 `modes/_schema_signals.md`**（不私自造字段名）
- **不自动进入 stage 流程**（老手用户已经知道自己在做什么）

### 0.5. Agent 分支（v0.5）

如果用户输入匹配 `/startup-101 agent <name>`：
- 加载 `agents/<name>.md`
- **前置检查**：agent 的 `profile_fields_used` 依赖 check 命令的 snapshot。若缺失，输出先决条件清单 + 退出，不代跑 check。
- 按 agent 指令执行推理链 + 生成 artifact（写到 `./artifacts/<agent-name>-<date>.md`）
- 写回 `stage_7_output.<agent_name>_snapshot` 供下游复用

### 1. 主线流程（stage-driven）

1. **加载 _shared.md**（必做）— 7 阶段定义、红旗清单、disclaimer 文案、**Profile Linkage Contract**
2. **检查 _profile.md**（用户当前工作目录）
   - 不存在 → 从 `modes/_profile.template.md` 复制一份到 `./_profile.md`，进入 stage-0
   - 存在但 `archetype` 为空 → 进入 stage-0
   - 已完成 profile → 进入 2a schema 检查
3. **2a. Profile Schema 版本检查（v0.3）**
   - 读取 `_profile.md` 顶部 `profile_schema_version`
   - 若**缺失**或 `< 0.3` → 提示用户：
     ```
     你的 profile 使用的是旧 schema（≤ 0.2 或未声明）。
     当前 skill 需要 schema 0.3 支持阶段间联动。选项：
     [a] migrate — 保留你的答案，追加空的 stage_N_output sections（推荐）
     [b] fresh_start — 备份到 _profile.legacy.md 并重新走 stage-0
     [c] abort — 暂不升级，继续使用旧 skill（不建议）
     ```
   - 按用户选择执行，然后继续
4. **阶段自诊断**（如果命令没明确指定 stage）：
   ```
   你目前卡在哪个阶段？
   [1] 还没注册公司，纠结架构
   [2] 已决定架构，准备注册
   [3] 刚拿到执照，不知道接下来 30 天干啥
   [4] 要招人、发期权
   [5] AI 产品要上线，不懂合规
   [6] 准备融资
   [7] 已融完，要处理持续义务
   ```
   v0.3 全阶段可用（Stage 1-7）。
5. **Stage Entry Check（v0.3）** — 进入 `stage-N.md` 之前：
   - 读取 `_profile.md` 中所有 `stage_M_output` section（M < N）
   - 提取非 null 的关键字段，生成 2-5 行摘要呈现：
     ```
     基于你之前的记录：
     - Stage 2：走 B1 路径（Cayman+HK+WFOE），37 号文已办
     - Stage 3：代账已上，一般纳税人
     准备进入 Stage N？[y/n]
     ```
6. **加载对应 stage-N.md**，执行该 stage 的 flow（stage 文件顶部的"读取前置状态"section 会提示依赖哪些字段）
7. **Stage Exit Step（v0.3）** — 每个 stage 结束后：
   - 按 stage 文件底部"本阶段输出"section 指定的 schema，把答案 append / 更新到用户 `_profile.md` 的 `stage_N_output` section
   - `completed_at: YYYY-MM-DD` 必填
   - `completed_stages` 数组追加 `N`
   - Append 自由文本结论到「日志」section
   - 运行红旗扫描（调 `modes/red-flags.md`），结果写入 `red_flags_triggered`
   - 询问是否继续下一阶段 / 生成 `startup-checklist.md`

## 文件加载顺序

### 主线流程（stage-driven）

```
1. modes/_shared.md                    [必须]
2. ./_profile.md（用户目录）           [必须]
3. modes/stage-N.md（按需）
4. modes/red-flags.md（结束时扫描）
5. appendix/*.md（stage 内按需引用）
6. references/index/*.md（stage 内按需推荐）
```

### 原子命令（v0.4）

```
1. commands/<category>/<name>.md       [必须]
2. ./_profile.md（若存在，按 frontmatter.profile_fields_used 读）
3. modes/_schema_signals.md             [必须 — 字段命名权威]
4. appendix/*.md（按命令 source_appendix 字段引用）
5. modes/_shared.md（仅加载 disclaimer 文案）
```

### Agent（v0.5）

```
1. agents/<name>.md                     [必须]
2. ./_profile.md                        [必须 — agents 硬依赖 snapshot]
3. modes/_schema_signals.md             [必须]
4. modes/_shared.md（disclaimer）
5. ./artifacts/（若不存在则创建，用于写出 agent 的 artifact）
```

## 文件解读约定

- `modes/` = 流程文件（stage / profile / red-flags / _schema_signals / _shared）
- `commands/` = 原子命令（v0.4，check / review / generate / compare / redflags）
- `agents/` = 深度推理子代理（v0.5）
- `appendix/` = 决策矩阵（entity / payment / compliance / case-studies）
- `references/` = 外部引用（bundled 全文 + index 摘要）
- `artifacts/` = agent 产出目录（用户侧，不入 repo）

## 交互原则

- **问一次只问一个**（参考 life-compass / rent-ops 风格）
- **多选优先于开放题**（菜鸟负担最低）
- **红旗主动触发**，不等用户问
- **引用必给原文链接**，不做"伪原创"
- **不确定的政策点明说"请核对最新"**，不编造

## v0.2 已实现

- Stage 0 Profile 分流（A/B/C 3 档）
- Stage 1 Pre-incorporation
- Stage 2 Incorporation（5 条架构分支）
- Stage 3 Day-30（银行 / 代账 / 税务登记 / 社保 / 多实体簿记）
- Stage 4 Hiring & Equity（ESOP / Vesting / IP Assignment / 37 号文员工）
- Stage 5 AI 产品上线前（算法备案三轨 / GDPR / EU AI Act GPAI / PIPL 出境 / 软著新规）
- Stage 6 Fundraising（石头《融资指南》深度嵌入）
- Stage 7 Ongoing（月/季/年报 / 转让定价 / GPAI 年检 / FBAR）
- Red Flags（6 条）
- Appendix: entity-matrix, payment-matrix, compliance-matrix, ai-filing-guide, case-studies, glossary
- References index: 01-ideas / 02-incorporation / 03-hiring-equity / 04-ai-tech / 05-fundraising / 06-vc-voices / 07-cross-border

## v0.4 已实现（架构升级：skill pack 形态）

- [x] 新增 `commands/` 目录 + 五类动词分类（check / review / generate / compare / redflags）
- [x] `commands/README.md` — 命令索引 + frontmatter 约定
- [x] SKILL.md 增加原子命令路由分支
- [x] `commands/check/algorithm-filing.md` — 算法备案三轨判定（反拆自 `appendix/ai-filing-guide.md`）
- [x] `commands/check/37hao-exposure.md` — 37 号文暴露扫描（反拆自 stage-4 + Red Flag 1）
- [x] `commands/check/pipl-gap.md` — PIPL 出境三档（反拆自 compliance-matrix § 二）
- [x] `commands/check/eu-ai-act-tier.md` — EU AI Act 角色 + 义务（反拆自 compliance-matrix § 三）
- [x] `commands/check/cross-border-payment.md` — 跨境收款路径（反拆自 payment-matrix + Red Flag 3）
- [x] `commands/check/license-scan.md` — Llama + AGPL 合扫（反拆自 Red Flag 4 + 5）
- [x] `commands/redflags/scan-all.md` — 6 条主红旗扫描 + 深入命令路由（派生自 `modes/red-flags.md`）

## v0.4.2 已实现

- [x] v0.4.1 三件套（主动提问 / 绝对 deadline / follow-up 自动注入）推广到全部 6 条命令
- [x] 跨命令共享 profile schema 统一

## v0.5 已实现（当前）

- [x] `modes/_schema_signals.md` — 跨命令 profile 字段登记册（防字段漂移）
- [x] `agents/` 目录 + agents/README.md
- [x] `agents/ai-compliance-auditor.md` — 全面合规体检子代理（读 check snapshot 做二阶分析 + 产出 DD 就绪报告）
- [x] SKILL.md 加 agent 路由分支

## v0.5+ 待补（按 ROADMAP）

- [ ] `agents/vc-term-sheet-reviewer.md`
- [ ] `agents/jurisdiction-advisor.md`
- [ ] `agents/fundraising-strategist.md`
- [ ] `agents/incorporation-checklist-gen.md`
- [ ] `mcp/` — MCP server 配置（GSXT / CAC 备案库 / HKCR / SEC EDGAR）
- [ ] `commands/check/ip-assignment.md`（Red Flag 2 专项）
- [ ] `commands/review/safe-terms.md`
- [ ] `commands/review/term-sheet.md`
- [ ] `commands/compare/entity-structure.md`
- [ ] `commands/generate/*`

## v0.3 已实现

- Profile Schema v0.3 + 阶段间联动契约（读前置 / 写输出 / 版本检查）
- `references/bundled/yc-safe/` — YC Post-Money SAFE 四变体结构化摘要 + 官方 URL
- Case studies 扩展 — 加入 MiniMax / Moonshot / 百川 / 智谱 / 01.AI 等本土 AI 案例
- 英文 README（README_EN.md）
- CHANGELOG.md（Keep-a-Changelog 格式）
- `.claude-plugin/plugin.json` + `MARKETPLACE_SUBMISSION.md`

## v0.5+ 待补

- `agents/` — subagent 配置（vc-term-sheet-reviewer / ai-compliance-auditor / jurisdiction-advisor）
- `mcp/` — MCP server 配置（GSXT / 网信办备案库 / 信通院 / 香港公司注册处）
- `templates/` — 独立模板文件（被 commands/generate 引用）
- `cli/install.sh` — 一键安装到 `~/.claude/`
- `docs/` — GitHub Pages 站（命令 catalog + 案例）
- `references/bundled/` 其他条目（Cooley GO / Karpathy / Simon Willison 等 License 逐项核对）
- 更多 Stage-7 审计模板
