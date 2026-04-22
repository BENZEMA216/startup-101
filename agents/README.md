# startup-101 / agents

**深度推理子代理**（subagents）。与 `commands/` 的原子命令互补：

| | `commands/` | `agents/` |
|---|---|---|
| 复杂度 | 单轮、确定性决策树 | 多轮、推理链 |
| 输入 | profile 字段 + fallback 提问 | 大段文本（term sheet / 隐私政策 / 完整 profile）|
| 输出 | 判定结论 + deadline + follow-up | 分析报告 + 谈判话术 + 改写建议 |
| 数量 | 多（> 20 条）| 少（< 10 条）|
| 典型触发 | `/startup-101 check <x>` | `/startup-101 agent <x>` |

## 设计原则

1. **读取命令级结论**：agents 不应重新跑 check。而是读取 `_profile.md` 中已有的 `*_snapshot` / `*_red_flags` / `*_deadlines`，做二阶分析。
2. **聚焦深度推理**：agent 的价值在于"看完整上下文"，不是多跑几个判定。
3. **产出可落地 artifacts**：分析报告 / 谈判话术 / 改写版文档，用户能直接拿去用。
4. **schema 消费**：所有 agent 必须按 `modes/_schema_signals.md` 规范读字段，不自己造。

## 文件约定

与 commands/ 相同 frontmatter 结构，但多一个 `inputs_beyond_profile` 字段：

```yaml
---
name: <agent 名>
description: <一句话能力>
argument-hint: <参数>
trigger: /startup-101 agent <name>
inputs_beyond_profile:
  - 用户粘贴的 term sheet 文本
  - 用户粘贴的 commit diff / 代码 PR
profile_fields_used: [...]
profile_fields_written: [...]
produces_artifacts:
  - path/to/<agent-name>-report-<date>.md
last_policy_review: YYYY-MM-DD
---
```

## 当前状态（v0.5）

### 已完成

- [x] `agents/ai-compliance-auditor.md` — 全面合规体检（读全部 Stage 5 snapshot，输出 audit report）

### 待补

- [ ] `agents/vc-term-sheet-reviewer.md` — VC term sheet 逐条解读 + 谈判话术
- [ ] `agents/jurisdiction-advisor.md` — 业务模型 → 推荐架构（5 分支）
- [ ] `agents/fundraising-strategist.md` — profile + metrics → 融资策略
- [ ] `agents/incorporation-checklist-gen.md` — 基于 profile 生成个性化开办清单

## 路由

主 SKILL.md 新增分支：

```
/startup-101 agent <name> [--input <path>]
└─ 加载 agents/<name>.md
   读取 _profile.md 中声明的字段
   执行 agent 指令
   写回 snapshot 到 profile
   在 ./artifacts/ 目录产出报告文件
```
