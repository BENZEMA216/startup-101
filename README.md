# startup-101

> 面向 AI 菜鸟创业者的排雷 Claude Code Skill — 从"想干"到"拿到第一笔钱"的 0→1 阶段，跨境原生。

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

```
/startup-101                # 默认：profile → 阶段自诊断
/startup-101 profile        # 只做 profile 分流
/startup-101 stage N        # 直接跳到第 N 阶段（1-7）
/startup-101 redflags       # 红旗扫描
/startup-101 checklist      # 生成完整清单
```

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
