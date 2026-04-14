# Marketplace Submission Checklist

> Status (2026-04-15): **ready-for-user-review** — all technical prep done. Actual submission requires human actions marked 🤚 below.

## Context

`startup-101` is a Claude Code Skill packaged as a plugin for the **superpowers-marketplace** ecosystem (reference format: `~/.claude/plugins/cache/superpowers-marketplace/superpowers/5.0.6/`).

## What's in place

- [x] `.claude/skills/startup-101/SKILL.md` — valid frontmatter (`name`, `description` with "Use when..." trigger, bilingual conversation)
- [x] `.claude-plugin/plugin.json` — plugin metadata (name / version / description / author / license / homepage / repository / keywords)
- [x] `LICENSE` — MIT
- [x] `README.md` (Chinese) + `README_EN.md` (English)
- [x] `CHANGELOG.md` — Keep-a-Changelog format, v0.1 / v0.2 / v0.3 documented
- [x] `references/bundled/yc-safe/` — structured summaries, no license-ambiguous binaries
- [x] All stage files (0-7) carry `last_policy_review: 2026-04-15`
- [x] Profile schema v0.3 linkage contract (schema version check + stage entry/exit)

## SKILL.md frontmatter (current)

```yaml
---
name: startup-101
description: 面向 AI 菜鸟创业者的排雷 skill — 从公司架构、AI 合规、跨境收款到融资条款的 0→1 全流程必查清单。Use when a first-time AI founder asks about incorporation, equity, algorithm filing, going global, fundraising, SAFE, term sheet, cross-border compliance (PIPL/GDPR/EU AI Act), or red flags like 37 号文 / Llama license / AGPL. Bilingual conversation.
---
```

This matches the superpowers skill format exactly (single `name` + single `description` with "Use when..." trigger).

## Plugin.json (current)

Mirrors the superpowers `.claude-plugin/plugin.json` schema:
- `name`, `description`, `version`, `author`, `homepage`, `repository`, `license`, `keywords`

## Submission flow (requires human actions)

The exact marketplace submission process for `superpowers-marketplace` is not fully automatable from a skill author's side. Based on observing the repo structure, the likely flow is:

1. 🤚 **Create public GitHub repo** `BENZEMA216/startup-101` (currently local only, no remote pushed per v0.3 rules)
2. 🤚 **Verify working installation** on a fresh machine:
   ```bash
   git clone https://github.com/BENZEMA216/startup-101 ~/startup-101
   cd ~/.claude/skills && ln -s ~/startup-101/.claude/skills/startup-101 startup-101
   # Launch Claude Code in a test project dir, run /startup-101
   ```
3. 🤚 **Submit PR to superpowers-marketplace** adding an entry to its top-level `marketplace.json`:
   ```json
   {
     "name": "startup-101",
     "description": "...",
     "version": "0.3.0",
     "source": "https://github.com/BENZEMA216/startup-101",
     "author": { "name": "BENZEMA216" }
   }
   ```
   (Or whatever the maintainer's current process requires — check their CONTRIBUTING.md before submitting.)
4. 🤚 **Alternative path**: publish as a standalone installable plugin outside the Jesse Vincent marketplace if they have a different curation policy.

## Pre-submission manual verification

- [ ] Run `/startup-101` in a throwaway directory → should initialize `_profile.md` and start Stage 0
- [ ] Run `/startup-101 stage 6` with a completed profile → should show stage entry summary pulling from `stage_M_output` fields
- [ ] Run `/startup-101 redflags` → should scan all 6 red flags without errors
- [ ] Verify `README.md` ↔ `README_EN.md` ↔ `CHANGELOG.md` cross-links work
- [ ] Open `references/bundled/yc-safe/README.md` and verify all URLs resolve
- [ ] Check `last_policy_review: 2026-04-15` dates — update if significant time passes before submission

## Known caveats to disclose to marketplace reviewers

1. **Jurisdictional scope**: skill primarily written for Chinese-background founders. Pure US / EU founders will find limited value in domestic China stages.
2. **Policy freshness**: Chinese AI / cross-border policy changes quarterly. `last_policy_review` timestamps exist; users should cross-check.
3. **Not legal advice**: skill explicitly disclaims being a substitute for counsel. Every stage carries this warning.
4. **Bilingual conversation**: LLM behavior is language-adaptive; skill works in Chinese and English inputs.

## Readiness assessment (self)

| Dimension | Status |
|---|---|
| Technical packaging | ✅ Done |
| Content completeness (stages 0-7) | ✅ Done |
| Documentation (README CN/EN, CHANGELOG) | ✅ Done |
| Plugin metadata | ✅ Done |
| Dogfooding evidence | 🟡 Author uses it; no third-party beta testers yet |
| Public GitHub release | 🤚 Requires user action |
| Marketplace PR | 🤚 Requires user action |

**Recommendation**: Before marketplace submission, recruit 2-3 first-time AI founder beta testers to validate Stage 1 → Stage 2 → Stage 6 end-to-end on a real profile. Update any red-flag / time-sensitive facts found stale during beta.
