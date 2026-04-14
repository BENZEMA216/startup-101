# Changelog

All notable changes to startup-101 are documented here.
This project adheres to [Keep a Changelog](https://keepachangelog.com/) format and [Semantic Versioning](https://semver.org/).

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
