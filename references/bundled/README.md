# References / Bundled — 内置资源

> last_license_review: 2026-04-15

## 两种 bundling 形态

1. **🟢 Structured summary + URL**（v0.3 起默认形态）
   - 针对法律文件 / 反复更新的合同模板（如 YC SAFE），我们不内置二进制 PDF/DOCX
   - 而是提供**结构化摘要 + 官方 URL + 使用指引**的 Markdown 文件
   - 好处：不怕过期、agent 可直接读、用户按需跳原文
2. **🟡 Full-text（候选）**
   - 针对公有领域文档（法规正文）或明确 permissive license 的内容
   - 逐项核对后再内置，避免版权风险

## 内置原则

只有满足以下条件之一才考虑 full-text 内置：

1. **公有领域**（如政府文件、法规正文 — 按中国《著作权法》第 5 条与 US public domain 规则）
2. **明确的 permissive License**（CC0 / CC-BY / MIT / Apache 2.0 等）
3. **作者 / 机构明确授权转载**

否则走 structured summary 或 `references/index/`（更轻量的 URL 摘要）。

---

## 计划清单（v0.3 目标）

| 候选资源 | 预估 License | 状态 | 备注 |
|---|---|---|---|
| **YC Post-Money SAFE**（Cap / Discount / Cap+Discount / MFN 四变体） | YC 公开授权任意使用 | 🟢 summarized with URLs | v0.3 已完成：见 [yc-safe/](./yc-safe/) — 结构化摘要 + 官方 URL（不内置 DOCX，用户按需从 ycombinator.com 下载最新版） |
| **Karpathy — Intro to LLMs**（含幻灯片 / 文字稿） | MIT（若 GitHub repo 有）/ YouTube 公开 | 🟡 待核 | 部分幻灯片来自其讲座未明确 License，需确认 |
| **Simon Willison — Prompt Injection 精选 10 篇 Markdown** | CC-BY 4.0（博客明确） | 🟢 候选 | 允许转载 + 注明出处链接 |
| **Cooley GO Founders' Agreement Template** | 免费使用 + 非转售 | 🟡 待核 | Cooley GO "Terms of Use" 允许个人使用，批量再分发需联系 |
| **Cooley GO SAFE Template**（与 YC SAFE 不同变体） | 同上 | 🟡 待核 | 同上 |
| **《生成式人工智能服务管理暂行办法》**（CAC 2023-07） | 公有领域（中国法规） | 🟢 候选 | 直接从 cac.gov.cn 抓取 |
| **《促进和规范数据跨境流动规定》**（CAC 2024-03） | 公有领域 | 🟢 候选 | 直接抓取 |
| **《网络安全法》修订版**（2026-01-01 生效） | 公有领域 | 🟢 候选 | 从 npc.gov.cn 抓取 |
| **EU AI Act Regulation 2024/1689 正式文本** | EU 公共文件 CC-BY 4.0 | 🟢 候选 | 从 eur-lex.europa.eu 下载 |
| **Sequoia — Writing a Business Plan / Pitch Deck Template** | 公开但未声明 License | 🟡 待核 | 需联系 Sequoia |
| **Bill Gurley — All Revenue Is Not Created Equal** | 博客全文公开 | 🟡 待核 | 未见明确 CC 授权 |

---

## v0.3 执行计划

每个候选资源执行如下步骤：

1. **访问原站** — 核对最新 License 声明
2. **下载文件**（或 archive snapshot）+ 记录下载日期 + 来源 URL
3. **添加 header**：
   ```markdown
   > Source: [URL]
   > Downloaded: YYYY-MM-DD
   > License: [License 名称 + URL]
   > Original Author: [作者/机构]
   ```
4. **提交到 bundled/** 并更新本 README 状态为 ✅

---

## 为什么 v0.2 不直接下载

- **License 核对不能自动化** — 部分条款需人眼判断合理使用边界
- **YC SAFE 等 PDF 版本经常变动** — 内置快照可能过期
- **开源 repo 打包大文件增加 clone 成本** — 权衡价值

**结论：** v0.2 只交付 index/（摘要 + URL），让 skill 使用者在需要时点击原链接获取最新版。v0.3 根据实际使用反馈决定哪些高频资源值得内置。

---

## v0.3 已交付

- **[yc-safe/](./yc-safe/)** — YC Post-Money SAFE 四变体结构化摘要（Cap / Discount / Cap+Discount / MFN）+ Pro Rata Side Letter 引用 + 使用指引 + 与 Pre-money 对比

## 当前已提供的替代方案（未 bundled 项）

- **Simon Willison Prompt Injection**：`references/index/04-ai-tech.md` → 单篇必读链接
- **Cooley GO 模板**：`references/index/02-incorporation.md` / `03-hiring-equity.md` 都已链接
- **CAC 2024-03 规定**：`references/index/07-cross-border.md` 直链官方原文

---

## 用户本地 clips 的对接（可选）

开发机上若有本地克隆（如 Obsidian）：
```bash
export OBSIDIAN_CLIPPINGS=~/Obsidian/Clips
```
skill 在某些 index 条目会检测此环境变量，如 `$OBSIDIAN_CLIPPINGS/石头融资指南.md` 若存在则在建议中附加"本地已有"提示。开源版 `.md` 文件不包含私人路径。

---

## 反馈 / 建议新增

发现某资源 License 清楚且高频引用但未收录：
- 提 Issue 到 BENZEMA216/startup-101
- 或 PR 直接加到 bundled（附 License 证据截图）
