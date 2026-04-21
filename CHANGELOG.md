# Changelog

All notable changes to startup-101 are documented here.
This project adheres to [Keep a Changelog](https://keepachangelog.com/) format and [Semantic Versioning](https://semver.org/).

## [0.4.0] - 2026-04-21

### Added — Skill Pack 架构升级

- **原子命令工具箱** — 新增 `commands/` 目录（check / review / generate / compare / redflags 五类动词），与 `modes/` stage-driven 主线形成双入口：菜鸟走 stage，老手 / 复用用户走原子命令。参考 arc-kit 的 skill pack 分发模式但保留 profile 联动。
- **第一批 6 条高优命令**（反拆自已有 appendix / stage / red-flags）：
  - `commands/check/algorithm-filing.md` — 算法备案三轨（A / B / C）判定 + 时间规划 + 红旗
  - `commands/check/37hao-exposure.md` — 37 号文创始人 + 员工两侧扫描，含融资 DD 爆雷风险评分
  - `commands/check/pipl-gap.md` — PIPL 出境三档判定（<10w / 10-100w / ≥100w + 敏感 PI）+ 自贸区豁免
  - `commands/check/eu-ai-act-tier.md` — Provider / Deployer 角色 + GPAI / Art. 50 / Systemic Risk 判定
  - `commands/check/cross-border-payment.md` — Stripe / Paddle / Airwallex 路径选择 + 成本对照
  - `commands/check/license-scan.md` — Llama Community License + AGPL / SSPL 合扫（RF4 + RF5）
  - `commands/redflags/scan-all.md` — 6 条主红旗扫描 + 深入命令路由
- **frontmatter 约定** — 每个命令文件声明 `profile_fields_used` / `profile_fields_written` / `source_appendix` / `last_policy_review`，命令结束时按 schema 写回 `_profile.md`，完全兼容 v0.3 Profile Linkage Contract。

### Changed

- `SKILL.md` 新增「原子命令优先分支」路由：匹配 `/startup-101 (check|review|generate|compare) <name>` 直接加载 `commands/<category>/<name>.md`，不进入 stage 主线。
- `SKILL.md` 命令表分两栏：主线（stage-driven）+ 原子命令（v0.4 新增）。
- `SKILL.md` 文件加载顺序拆成两套：主线 vs 原子命令。
- `ROADMAP.md` v0.4 从"bundled references 补齐"改为"skill pack 架构升级"；bundled references 延后到 v0.6；新增 v0.5（agents + mcp 护城河）和 v0.6（cli + docs + bundled）。

### Rationale

GitHub trending（2026-04）显示 arc-kit（1.5k stars，UK 企业架构 skill pack）验证了"**垂直知识 × 原子命令包**"的产品形态。startup-101 原先是单一 skill，此版本保留 stage-driven 陪伴式优势，同时获得 skill pack 的分发能力 + 老手复用体验。下一步 v0.5 的 agents / mcp 是该形态的护城河（中文生态还没人做实时合规 MCP）。

## [0.3.0] - 2026-04-15

### Added
- **Profile auto-linkage (schema v0.3)** — `_profile.template.md` now has structured `stage_N_output` sections; `_shared.md` codifies the read-before-enter / write-on-exit contract; SKILL.md router enforces schema version check + stage entry/exit steps.
- **YC SAFE bundled as structured summaries** — `references/bundled/yc-safe/` with 4 variants (Cap-only / Discount-only / Cap+Discount / MFN-only) plus Pro Rata Side Letter cross-reference. Each `.md` includes structure, key parameters, red flags, cross-refs to Stage 6. We link to canonical YC URLs rather than mirroring PDFs to avoid staleness.
- **5 new Chinese AI case studies** — MiniMax (HK IPO + Talkie overseas), Moonshot/Kimi (Alibaba 36% concentration warning), 百川智能 (pure-domestic + medical pivot), 智谱/Z.ai (US Entity List Footnote 4 + subsidiary workaround + HK IPO), 01.AI (contraction playbook into Alibaba Cloud joint lab). Cross-case rules expanded: HK IPO as default exit path, big-tech concentration threshold, Entity List pre-planning, end of generic base-model window.
- **English README** (`README_EN.md`) — for international users who discover the skill in a marketplace. Clear positioning (primarily for Chinese-background founders), bilingual conversation, installation, feature summary.
- **This CHANGELOG** in Keep-a-Changelog format.
- **Marketplace submission prep** — `.claude-plugin/plugin.json` with plugin metadata + `MARKETPLACE_SUBMISSION.md` with submission checklist and current readiness assessment.

### Changed
- Each `modes/stage-N.md` (N=0..7) now has explicit `## 读取前置状态` (read prerequisite state) and `## 本阶段输出（写入 _profile.md）` (stage output spec) sections, replacing the earlier free-form "本阶段结束状态" closing.
- `references/bundled/README.md` distinguishes two bundling forms: 🟢 structured-summary-with-URL (new default for legal docs) vs 🟡 candidate-for-full-text (pending license verification).
- `SKILL.md` "v0.2 已实现" / "v0.3+ 待补" replaced by "v0.3 已实现" / "v0.4+ 待补" sections reflecting current state.
- `README.md` top-matter now points to `README_EN.md`.

## [0.2.0] - 2026-04-15

### Added
- **Stages 3 / 4 / 5 / 7 activated** — completing the 7-stage skeleton. Stage 3 covers banking + bookkeeping + tax registration + social insurance across 3 archetypes. Stage 4 covers ESOP / vesting / IP Assignment / 37号文 for employees. Stage 5 covers the three-track AI filing system + GDPR + EU AI Act GPAI + PIPL outbound + software copyright rules. Stage 7 covers monthly/quarterly/annual obligations including transfer pricing, audit, GPAI annual review, FBAR.
- **Appendix v0.2** — `compliance-matrix.md` (GDPR/CCPA/PIPL/EU AI Act side-by-side), `ai-filing-guide.md` (three-track decision tree), `case-studies.md` (6 real companies), `glossary.md` (VIE/37号文/QSBS/SAFE/SCC/GPAI terms).
- **References/index v0.2** — topic indices 01 (ideas), 03 (hiring & equity including 37号文), 04 (AI tech — Karpathy / a16z / Simon Willison), 06 (VC voices — 锦秋/真格/经纬/朱啸虎/戴雨森), 07 (cross-border — Manus/HeyGen cases, EU AI Act, PIPL outbound).
- **References/bundled/ README** — license-verification plan for future full-text bundling.

### Research updates (v0.2 policy baseline)
- TC260-003 (2026): overseas corpus ≤ 30% hard cap
- EU AI Act GPAI obligations: effective 2025-08-02
- PIPL outbound three-tier thresholds: 免评估 / 标准合同 / 安全评估
- China Cybersecurity Law revision: effective 2026-01-01 (AI explicitly in scope)
- Colorado AI Act: enforcement deferred to 2026-06-30
- California SB-53: effective 2026-01-01
- China 2026 rules on AI-ghostwritten software copyright filings

## [0.1.0] - 2026-04-15

### Added
- **SKILL.md router** — 6-command surface (`/startup-101`, `profile`, `stage N`, `redflags`, `checklist`, `refs`) + profile-gated dispatch.
- **Stages 0 / 1 / 2 / 6** — the four most commonly-stuck stages. Stage 0 is a 4-question A/B/C archetype router. Stage 1 covers cofounder agreement + equity split + architecture pre-decision + personal tax residency. Stage 2 lays out 5 architecture paths (A / B1 / B2 / C1 / C2). Stage 6 navigates Shi Tou's Fundraising Guide with 6 decision points and the founder-personal-buyback hard red line.
- **6 red flags** with trigger conditions and remediation paths.
- **Appendix v0.1** — `entity-matrix.md` (6 architectures × cost/time/red flags), `payment-matrix.md` (MoR/Stripe/banks/payroll/capital flow).
- **References v0.1** — `references/README.md`, `index/02-incorporation.md`, `index/05-fundraising.md` (deep digest of Shi Tou's guide).
- **LICENSE** (MIT), `.gitignore`, initial Chinese `README.md`.
