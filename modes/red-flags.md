# Red Flags — 6 条最高死亡率坑

> 独立扫描模式：`/startup-101 redflags`
> 每个 stage 结束后也会自动扫一次。

## 扫描逻辑

读 `./_profile.md`，对每条红旗匹配触发条件：
- **命中** → 🚩 警告 + 补救方案 + 对应 references
- **可能命中** → ⚠️ 提示需要核对
- **未命中** → ✅ 跳过

---

## 🚩 Red Flag 1: 37 号文未办

**触发条件：**
- `archetype` = B
- `archetype` = C AND `founders_tax_residency` 包含中国
- 或 profile 日志中出现 Cayman/BVI/SG SPV + 中国创始人 + 未显式登记 37 号文

**后果：**
- 上市前员工期权无法行权
- 退出时分红/对价无法合法汇回中国
- 外管局处罚（通常 50-100 万罚款）

**补救：**
- 找跨境律所做 37 号文补登记，通常 2-6 个月
- 补登记费用 ~5-10 万 RMB
- 推荐咨询：汉坤 / 方达 / 君合（非背书，示例）

**阅读：** `references/index/02-incorporation.md` § 37 号文 / 石头《融资指南》§11

---

## 🚩 Red Flag 2: IP Assignment 未指向海外主体

**触发条件：**
- `archetype` = B
- AND profile 日志中出现「已签员工劳动合同」「已分配股权」但未显式记录 IP Assignment 条款

**后果：**
- 美元基金 DD 阶段爆雷
- Cayman 母公司无法证明持有核心 IP
- 融资被迫延期或估值打折

**补救：**
- 所有员工（含已离职）补签 IP Assignment 追溯条款
- 受让方必须是 Cayman / Delaware 母公司，不能是 WFOE
- 劳动合同 + IP Assignment + 发明创造归属协议三件套

**阅读：** `references/index/02-incorporation.md` § IP 归属 / Cooley GO 模板

---

## 🚩 Red Flag 3: 个人 PayPal / 微信收订阅规模化

**触发条件：**
- `payment_model` = 订阅制
- AND `target_currency` 含 USD
- AND profile 中未记录「已开 Stripe / Paddle 商户」
- AND 用户自述月流水 >$4000（≈ $50k/年）

**后果：**
- 涉嫌非法结汇 / 逃汇
- 外管局可追溯 5 年，处罚 30-50% 涉案金额
- 个人征信影响

**补救：**
- 立即搭建合规收款链路：
  - Path 1：Delaware / SG 公司 + Stripe → Mercury / 银行 → 转至中国对公
  - Path 2：内资公司 + Paddle (MoR) → 对公美元户 → 结汇
- 已发生的历史流水：咨询税务师是否需要补申报

**阅读：** `appendix/payment-matrix.md`

---

## 🚩 Red Flag 4: Llama Community License 违规

**触发条件：**
- `ai_track` ∈ {LLM 应用, Agent, 基础模型}
- AND `self_trained_model` = yes
- AND 用户自述基础模型基于 Llama 2 / 3 微调
- AND（目标用户 >7 亿月活 OR 用 Llama 输出改进其他 LLM）

**后果：**
- Meta 有权撤销使用许可
- 产品可能被迫下架
- 法律风险（违反 License）

**核对要点：**
- 读 Llama 3 Community License § 2 的 7 亿月活上限条款
- 读 § 1.b 不得用 Llama 输出改进其他 LLM

**替代方案：**
- Qwen (Apache 2.0) — 无月活上限，商用自由
- DeepSeek (Apache 2.0) — 同上
- Mistral (Apache 2.0 / 部分 Research Only) — 按版本核对
- 自训 from scratch

---

## 🚩 Red Flag 5: AGPL 污染

**触发条件：**
- AND 产品形态 = SaaS / 网络服务
- AND 依赖栈中含 AGPL 组件（用户自述或 profile 提示）

**典型 AGPL 陷阱：**
- MongoDB Community (2018 前版本)
- Ghostscript
- 部分 AI 工具（如某些向量数据库 AGPL 版）

**后果：**
- AGPL 要求所有通过网络访问该软件的用户都能获得源代码
- SaaS 闭源代码必须被迫开源
- 商业模式死亡

**补救：**
- 审计整个依赖树，替换 AGPL 组件（或买商业 License）
- MongoDB 升级到 SSPL 版（仍有问题，建议换 Postgres）
- Apache 2.0 / MIT / BSD 是安全的

---

## 🚩 Red Flag 6: EU 无 Art. 27 代表

**触发条件：**
- `user_geography` = ≥70% 海外 OR 均衡
- AND 产品已 live OR 即将 live
- AND 欧盟用户 > 0（即使只有 1 个）

**后果：**
- 违反 GDPR Art. 27
- 欧盟监管机构可直接向本地代表发投诉
- 罚款最高 €20M 或全球营收 4%

**补救：**
- 找第三方代表服务（Prighter / VeraSafe / EDPO），通常 €200-400/月
- Privacy Policy 中必须公示代表联系方式
- 同时检查：Privacy Policy / Cookie Banner / DPA 模板 / SCC (如数据出欧)

**阅读：** `appendix/compliance-matrix.md` § GDPR / `modes/stage-5-ai-launch.md` 决策 4

---

## 扫描完成后的输出格式

```
🚩 命中 N 条红旗：
1. [红旗名] — [一句话原因]
   补救：[一句话]

⚠️ 可能命中 M 条：
1. [红旗名] — 需要你核对：[具体问题]

✅ 其余 K 条未命中。

建议优先处理：[按严重度排序的前 3 条]
```
