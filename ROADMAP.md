# Roadmap

> startup-101 未来迭代计划。按优先级排序，不保证时间。
> 历史版本见 [CHANGELOG.md](./CHANGELOG.md)。

## v0.4 — Skill Pack 架构升级（进行中）

**目标：** 从单一 skill 升级成 **stage-driven 主线 + atomic commands 工具箱** 的双入口产品形态。参考 arc-kit 的分发模式，但保留 startup-101 的 profile 联动优势。

### 新增目录结构

- [x] `commands/` — 原子命令工具箱（5 类动词：check / review / generate / compare / redflags）
- [x] `commands/README.md` — 命令索引 + frontmatter 约定
- [x] **范式文件：`commands/check/algorithm-filing.md`**（反拆自 `appendix/ai-filing-guide.md`）
- [x] SKILL.md 增加原子命令路由分支

### 高优先级补齐（反拆已有 appendix / stage 内容）

**第一批已完成（2026-04-21）：**

- [x] `commands/check/37hao-exposure.md`（37 号文暴露自查，反拆自 stage-4 + RF1）
- [x] `commands/check/pipl-gap.md`（PIPL 差距分析，反拆自 compliance-matrix § 二）
- [x] `commands/check/eu-ai-act-tier.md`（EU AI Act 分级，反拆自 compliance-matrix § 三）
- [x] `commands/check/cross-border-payment.md`（跨境收款路径，反拆自 payment-matrix + RF3）
- [x] `commands/check/license-scan.md`（Llama + AGPL 合扫，反拆自 RF4 + RF5）
- [x] `commands/redflags/scan-all.md`（从 modes/red-flags.md 派生）

**第二批待补：**

- [ ] `commands/check/ip-assignment.md`（RF2 专项）
- [ ] `commands/review/safe-terms.md`（YC SAFE 四变体审查，引用 references/bundled/yc-safe）
- [ ] `commands/review/term-sheet.md`（VC term sheet 逐条解读）
- [ ] `commands/review/employment-contract.md`
- [ ] `commands/review/privacy-policy.md`
- [ ] `commands/compare/entity-structure.md`（5 种架构对比，反拆自 entity-matrix）
- [ ] `commands/compare/payment-rails.md`（反拆自 payment-matrix）
- [ ] `commands/compare/jurisdictions.md`
- [ ] `commands/generate/cap-table.md`
- [ ] `commands/generate/dpia.md`
- [ ] `commands/generate/ip-assignment.md`
- [ ] `commands/generate/investor-update.md`
- [ ] `commands/redflags/hidden-vie.md`
- [ ] `commands/redflags/founder-visa.md`
- [ ] `commands/redflags/ai-data-source.md`

## v0.5 — Agent 深度推理层（已完成首个）

**目标：** 把"重推理活"和"实时合规数据查询"落成独立组件。这是 arc-kit 已有、中文生态还没人做的位置。

### agents/ — 深度推理子代理

**已完成（2026-04-22）：**

- [x] `agents/README.md` — agent 约定 + commands vs agents 对照
- [x] `agents/ai-compliance-auditor.md` — 产品全面合规体检（12 维度 × 4 分组，读 25 profile 字段，产出 DD 就绪报告 + 合规状态声明两份 artifact）

**待补：**

- [ ] `agents/vc-term-sheet-reviewer.md` — 完整 term sheet → 逐条影响 + 谈判话术
- [ ] `agents/jurisdiction-advisor.md` — 业务模型 → 推荐架构（5 分支决策）
- [ ] `agents/fundraising-strategist.md` — 当前 profile + metrics → 融资策略
- [ ] `agents/incorporation-checklist-gen.md` — 基于 profile 生成个性化开办清单

### modes/_schema_signals.md — 跨命令 schema 登记册（已完成）

**已完成（2026-04-22）：**

- [x] 5 类字段登记（跨命令判定信号 / 时间锚点 / 标准化后缀 / 联动字段 / 值域规范）
- [x] `next_funding_dd_date` 双 stage 冲突规则（stage_6 权威）
- [x] SKILL.md 字段命名权威指向

## v0.6 — MCP 实时合规数据护城河

**目标：** 把「命令 → agent」的决策链接入实时合规数据源。这是 arc-kit 没做过、**中文 AI 创业合规生态独家位置**。

### mcp/ — 实时合规数据查询

- [ ] `mcp/cac-filing-server.py` — 网信办算法备案查询（https://beian.cac.gov.cn/） + json config
- [ ] `mcp/gsxt-server.py` — 国家企业信用信息公示系统（工商信息 / 经营范围变更历史）
- [ ] `mcp/cyberspace-admin-server.py` — 信通院大模型备案状态
- [ ] `mcp/hkcr-server.py` — 香港公司注册处（公司搜索 / 周年申报状态）
- [ ] `mcp/sec-edgar.json` — 美国 SEC EDGAR（Reg D / Form D，可直接用现成 MCP）

> 💡 这些 MCP 多数需要**自己写 Python + httpx wrapper**（公共 API 或爬虫），工作量 0.5-1 天/个。

### templates/ — 独立模板文件

- [ ] `templates/cap-table.template.md`
- [ ] `templates/board-resolution.template.md`
- [ ] `templates/dpia.template.md`
- [ ] `templates/ip-assignment.template.md`
- [ ] `templates/esop-plan.template.md`

## v0.7 — 安装 + 站点 + Bundled references 补齐

### cli/ — 一键安装

- [ ] `cli/install.sh` — 拷贝 skill + commands + agents 到 `~/.claude/`，配 MCP
- [ ] `cli/init.py` — 交互式初始化新项目的 `_profile.md`
- [ ] `cli/update.sh` — 增量更新已安装版本

### docs/ — GitHub Pages 站

- [ ] `docs/index.md` — 产品首页（讲"菜鸟走 stage，老手走 commands"双入口）
- [ ] `docs/commands-catalog.md` — 全命令索引（自动从 commands/ 生成）
- [ ] `docs/quickstart-cn.md` / `docs/quickstart-en.md`
- [ ] `docs/case-studies.md` — 真实使用案例

### Bundled references 补齐

- [ ] **Cooley GO 模板逐项核对 + 内置**
  - Founders' Stock Purchase Agreement
  - Stockholders Agreement
  - Option Plan & Grant Letter
  - SAFE 中文改写版
- [ ] **Karpathy《Intro to LLMs》讲义** — MIT 风授权
- [ ] **Simon Willison Prompt Injection 精选** — CC-BY
- [ ] **政府公开文件合集**（公有领域）

## v0.8 — 审计 & 模板扩展

**目标：** Stage 7 的持续义务不能只给框架，要给模板。

- [ ] **转让定价合同模板**（Cayman/HK ↔ WFOE Cost+ markup）中英双语
- [ ] **董事会季度 Business Review 模板**（参考 a16z 16 Startup Metrics）
- [ ] **GPAI 训练数据摘要披露模板**（EU AI Act 要求）
- [ ] **FBAR / FATCA 合规 checklist**（US 股东/员工）
- [ ] **年度合规日历**（月/季/年任务自动生成）

## v0.9 — 场景化深挖

**目标：** 从"通用 skill"走向"具体场景"。

- [ ] **ToB AI Agent 细分路径** — 企业服务 Agent 的定价 / 渠道 / 销售合规
- [ ] **ToC AIGC 细分路径** — 图/视频/音频生成的深度合成 + 标识 + 版权
- [ ] **开源模型商业化路径** — Apache 2.0 发布 → 融资 → 商业化平衡
- [ ] **从大厂出来创业的路径** — 竞业期如何安全启动 / IP 带出风险

## v1.0 — 社区与权威

**目标：** 从个人 skill 走向社区维护。

- [ ] **Review board 机制** — 邀请 1-2 名律师、1-2 名资深创业者做年度内容审阅
- [ ] **Policy review 自动化** — 定期 crawl 官方来源，标记内容过期
- [ ] **多语言支持** — 至少英文版本（海外华人创始人）
- [ ] **提交 superpowers-marketplace** 并维护长期响应

## 长期想法（未排期）

- **startup-101 × office-hours 协作** — office-hours 做需求验证，startup-101 做架构设计，形成 0→1 双剑合璧
- **startup-101 × life-compass 协作** — 创业是否符合 compass，在融资决策前嵌入检查
- **中国特色增长策略 skill** — 小红书 / 抖音 / 公众号 / B站冷启动 cookbook（独立 skill，不在本 repo）
- **post-B-round skill** — 本 skill 只覆盖 0→1，B 轮之后（扩张、并购、上市准备）另开
- **解散清算 skill** — 公司关停的合规流程（避雷）

## 贡献思路

欢迎 issue / PR 讨论：

- 政策更新（如新出的 AI 合规规定）
- 新的真实案例（特别是翻车案例）
- 律所/会计师/税务师推荐（需去除营销成分）
- 模板文件（需明确 license）
- 翻译（英文 / 日文 / 韩文）

**不接受的方向：**

- 具体法律意见（skill 定位就不是这个）
- 商业化推广（推自己家的律所 / 代账 / 投行服务）
- 非 AI 行业通用创业建议（超出 skill 范围）

---

*Living document，随社区反馈更新。*
