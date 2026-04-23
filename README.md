<p align="center">
  <img src="./assets/social-preview.png" alt="startup-101" width="100%">
</p>

# startup-101

> 面向 AI 菜鸟创业者的排雷 Claude Code Skill — 从"想干"到"拿到第一笔钱"的 0→1 阶段，跨境原生。

**English**: see [README_EN.md](./README_EN.md) · **Roadmap**: see [ROADMAP.md](./ROADMAP.md)

## 这是什么

startup-101 是一个 [Claude Code](https://claude.com/claude-code) Skill，帮第一次创业的 AI 工程师/研究员理清：

- **公司架构**：内资 / VIE / Cayman / Delaware / Singapore 怎么选？
- **AI 合规**：算法备案 / 大模型备案 / 登记三轨怎么走？
- **出海收款**：Stripe / Paddle / Airwallex 怎么对接？
- **跨境合规**：PIPL 出境 + GDPR + EU AI Act 怎么叠加？
- **融资条款**：回购 / 对赌 / 反稀释哪些能签哪些必死？
- **高死亡坑**：37 号文 / IP Assignment / 个人收款 / Llama License / AGPL / EU Art.27

## 免责声明

1. 不是律师 / 不是会计师 / 不是税务师的意见
2. 所有具体法律/税务/合规决策必须由专业机构二次确认
3. 政策变化快，请交叉验证最新信息

## 安装

```bash
cd ~/.claude/skills
ln -s ~/startup-101/.claude/skills/startup-101 startup-101
```

## 使用

startup-101 支持**双入口**：菜鸟走 stage 主线，老手直接打原子命令或跑 agent 体检。

### 主线（stage-driven，v0.3）

```
/startup-101                # 默认：profile → 阶段自诊断
/startup-101 profile        # 只做 profile 分流
/startup-101 stage N        # 直接跳到第 N 阶段（1-7）
/startup-101 redflags       # 红旗扫描
/startup-101 checklist      # 生成完整清单
```

### 原子命令工具箱（v0.4，7 条高优 check + 扫描）

```
/startup-101 check algorithm-filing       # 算法备案 A/B/C 三轨判定
/startup-101 check 37hao-exposure         # 37 号文创始人 + 员工双侧扫描
/startup-101 check pipl-gap               # PIPL 出境三档判定
/startup-101 check eu-ai-act-tier         # EU AI Act 分级 + GPAI / Art.50
/startup-101 check cross-border-payment   # Stripe / Paddle / Airwallex 路径
/startup-101 check license-scan           # Llama / AGPL / SSPL 合扫
/startup-101 redflags                     # 6 条主红旗扫描 + 深入命令路由
```

每条命令：主动提问（非 checkbox）+ 绝对 deadline（按目标日倒推）+ 自动注入 follow-up 命令。完整索引见 [`commands/README.md`](./commands/README.md)。

### Agent 深度推理层（v0.5，基于 check snapshot 的二阶分析）

```
/startup-101 agent ai-compliance-auditor  # 全面合规体检，产出 DD 就绪报告
```

Agent 读取前置 check 命令写回的 snapshot，做 12 维交叉检验 + 生成可交付 DD 的 Markdown 报告。索引见 [`agents/README.md`](./agents/README.md)。

### Schema 规范

所有命令和 agent 读写 `_profile.md` 必须遵守 [`modes/_schema_signals.md`](./modes/_schema_signals.md) 的字段登记册，防止字段名漂移。

## 致谢

本 skill 的结构和内容借鉴大量公开资源：

- **锦秋基金 / 石头看未来**《给年轻 AI 创业者的融资指南》
- **Y Combinator**: Startup School, YC Library, SAFE 文档
- **a16z**: AI Canon, Emerging Architectures for LLM Applications, 16 Startup Metrics
- **Sequoia Capital**: Pitch Deck Template, Sonya Huang Generative AI 系列
- **Stripe Atlas Guides** & **Cooley GO** templates
- **Index Ventures** Option Plan Handbook
- **Paul Graham / Sam Altman** essays
- 中国律所 AI 合规白皮书：中伦、汉坤、锦天城

完整引用见 `references/` 目录。

## License

MIT. 各 reference 原文保留原 License。
