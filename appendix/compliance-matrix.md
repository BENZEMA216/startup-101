# Compliance Matrix — 跨境合规矩阵

> last_policy_review: 2026-04-15
> 用于 Stage 5（AI 产品上线前）+ Stage 7（Ongoing）。

## 一、总览表

| 法规 | 辖区 | 触发阈值（粗） | 最低合规动作 | 估算成本 |
|---|---|---|---|---|
| **GDPR** | 欧盟 / EEA | 欧盟用户 ≥1 | Privacy Policy + Cookie Banner + DPA + SCC + Art. 27 代表 | €200-400/月（代表）+ 一次性律师 €3-8k |
| **UK GDPR** | 英国 | 英国用户 ≥1 | 基本同 GDPR + 独立 UK 代表 | €150-300/月 |
| **CCPA / CPRA** | 美国加州 | 年营收 $25M+ 或年处理 100k+ CA 居民数据 或 ≥50% 营收来自卖数据 | Privacy Notice + "Do Not Sell/Share" link + 用户请求响应 | 律师 $5-10k |
| **Colorado AI Act (SB24-205)** | 科罗拉多 | 部署"consequential decision" AI + 影响 CO 居民 | Risk mgmt + Impact assessment + 用户通知；**生效 2026-06-30** | $10-30k（首次 impact assessment） |
| **California SB-53 (TFAIA)** | 加州 | frontier 模型 + 面向 CA 用户；**2026-01-01 已生效** | frontier AI framework 公示 + 年度更新 + 重大事件报告 | 合规顾问 $20k+（大模型方） |
| **PIPL** | 中国 | 处理中国境内居民 PI | 用户同意 / 个人信息保护负责人 / 出境评估 | 5-20 万 RMB |
| **PIPL 出境（CAC 2024-03）** | 中国 | 累计出境 PI 阈值（见下表） | 安评 / SCC 备案 / 认证三选一 | 10-50 万 RMB（安评路径） |
| **EU AI Act（通用义务）** | 欧盟 | AI 系统投放欧盟市场 | 风险分类 + 相应义务；大部分 2026-08-02 生效 | 视风险级别差异巨大 |
| **EU AI Act — GPAI** | 欧盟 | 通用目的 AI 模型（基模）provider；**2025-08-02 生效** | 训练数据摘要 + 版权政策 + 技术文档 + 下游披露 | 合规顾问 €20k+ |
| **EU AI Act — Art. 50** | 欧盟 | 生成 / 交互 AI 系统对欧盟用户 | AI 生成内容标识 + 告知用户在与 AI 交互；**2026-08-02 生效** | 工程 + 文案工作 |
| **算法备案** | 中国 | 具舆论属性或社会动员能力算法 | 向网信办备案（双随机 + 公示） | 服务商 2-5 万 RMB |
| **大模型备案** | 中国 | 自研生成式模型面向公众 | 材料 + 安全评估；审批 3 个月 | 30-80 万 RMB（含合规顾问 + 安评） |
| **大模型登记** | 中国 | 调用已备案模型 API 提供公众服务 | 较轻材料 | 0.5-3 万 RMB |
| **深度合成备案** | 中国 | 生成图 / 视频 / 音 / 文本涉深度合成 | 单独备案 + 内容标识 | 2-5 万 RMB |

---

## 二、PIPL 出境三档阈值（2024-03-22 CAC 新规）

> 以"从每年 1 月 1 日起累计"为计量基准。

| 出境量级 | 动作 | 周期 | 有效期 |
|---|---|---|---|
| **<10 万人 PI**（非敏感）且无敏感 PI | **免申报**（新规豁免） | — | — |
| **10-100 万人 PI**（非敏感）或 **<1 万人敏感 PI** | **SCC 备案 或 个人信息保护认证**（二选一） | 备案 1-3 个月 | 3 年 |
| **≥100 万人 PI**（非敏感）或 **≥1 万人敏感 PI** | **安全评估**（省级 CAC → 国家 CAC） | 安评 45-60 工作日 + 补正可延长 | 3 年 |
| 关键信息基础设施运营者 或 涉"重要数据" | **一律安全评估** | 同上 | 3 年 |

**自贸区清单豁免：** 2024-03 新规支持自贸区（上海 / 海南 / 北京等）发布"负面清单"，清单外数据免出境评估。**具体范围每地不同，部署前核对。**

**典型 AI 场景对照：**
- To C 问答 Bot，月活 < 10 万 → 可能免申报（但用户同意仍要）
- To C 月活 10-100 万 → SCC 备案路径
- To C 月活 >100 万 或 存储人脸/生物特征/14 岁以下未成年 PI >1 万 → 安评
- 模型训练语料含中国用户行为日志出境 → 视情况可能踩"重要数据"红线

**引用：** [促进和规范数据跨境流动规定](http://www.cac.gov.cn/2024-03/22/c_1712776611775634.htm)

---

## 三、EU AI Act 时间线（GPAI / Art. 50 重点）

| 日期 | 生效内容 |
|---|---|
| 2025-02-02 | 禁止性 AI 实践（social scoring / 操纵 / 大规模生物识别抓取） |
| **2025-08-02** | **GPAI Provider 义务开始生效** |
| 2026-08-02 | 大部分高风险 AI 系统义务 + Art. 50 透明度义务 |
| 2027-08-02 | Annex II 高风险类（医疗器械等）嵌入产品的 AI 合规完成 |

### GPAI Provider 义务（2025-08-02 起）

1. **技术文档**（Annex XI）— 模型架构 / 训练方法 / 能力 / 评估
2. **训练数据摘要（Training Data Summary）** — 按 AI Office 模板公示，涵盖主要数据来源
3. **版权政策（Copyright Policy）** — 说明如何尊重版权 opt-out + 禁止爬侵权内容
4. **下游 Provider 信息披露** — 协助下游完成其义务
5. **若被认定"systemic risk"**（如训练算力 ≥ 10^25 FLOPs）— 额外模型评估 / 对抗测试 / 严重事件上报 / 网络安全措施

### Art. 50 透明度义务（2026-08-02 起）

| 系统类型 | 义务 |
|---|---|
| 与人交互的 AI（如 chatbot） | 必须明确告知用户"你在与 AI 交互" |
| 生成 synthetic 内容（图/音/视/文） | 输出必须机器可读标识为 AI 生成 |
| 情感识别 / 生物分类 | 告知数据主体 |
| Deep fake | 披露内容为人工生成/操纵 |
| 影响公共利益的 AI 生成文本 | 披露（若无人工编辑审核） |

### Code of Practice

**非强制但可作为 compliance pathway**：签 Code of Practice → 视为"推定符合 GPAI 义务"，直到欧洲标准落地。大型模型方（OpenAI / Anthropic / Google / Mistral）已签。

**引用：**
- [EU AI Act Implementation Timeline](https://artificialintelligenceact.eu/implementation-timeline/)
- [Guidelines for GPAI Providers](https://digital-strategy.ec.europa.eu/en/policies/guidelines-gpai-providers)
- [AI Act Code of Practice 介绍](https://artificialintelligenceact.eu/introduction-to-code-of-practice/)

---

## 四、GDPR 最小合规清单

- [ ] Privacy Policy（声明 controller / 处理目的 / 法律基础 / 保留期 / 用户权利）
- [ ] Cookie Banner（非必需 cookie 必须 opt-in）
- [ ] DPA（与处理方签 Data Processing Agreement）
- [ ] SCC（数据出欧必须，China/US 传输专用）
- [ ] **Art. 27 欧盟代表**（非欧盟公司 + 欧盟用户 >0）
- [ ] DPO（大规模监控 / 敏感数据 / 公共机构才需要）
- [ ] DPIA（高风险处理活动必做）
- [ ] 用户权利响应机制（30 天内回复访问 / 删除 / 更正 / 携带请求）

**罚款：** 最高 €20M 或全球营收 4%。

---

## 五、CCPA/CPRA 核对

**触发任一：**
- 年营收 ≥$25M（注意 2023-07 起为全球营收，不只加州）
- 年处理 ≥100k CA 居民/家庭/设备 PI
- ≥50% 营收来自出售 / 分享 PI

**必做：**
- [ ] Privacy Notice at collection（收集前告知）
- [ ] "Do Not Sell or Share My Personal Information" 链接（首页 footer）
- [ ] 敏感 PI 使用限制告知（CPRA 新增）
- [ ] 用户请求响应（访问 / 删除 / 更正 / 限制 sensitive PI 使用）
- [ ] 员工 / B2B 数据也在覆盖范围内（CPRA 2023-01 扩大）

---

## 六、叠加场景（AI 出海典型）

### 场景 1：ByteDance 式（中国训练 + 欧盟发布）

1. **PIPL 出境**（训练语料含中国用户 → 按阈值走安评/SCC）
2. **EU AI Act GPAI**（模型 provider 义务，2025-08 起）
3. **GDPR**（欧盟终端用户数据处理）
4. **Art. 50**（2026-08 起，AI 生成内容标识）

**冲突点：** PIPL 对"重要数据 / 核心数据"要求不得境外披露；而 AI Act 要求训练数据摘要公开。**建议：训练数据摘要采用高层"数据类别 + 大致占比 + 来源类型"粒度，不披露具体数据集明细，律师审阅语义边界。**

### 场景 2：纯 Archetype C（Delaware C-corp + 全球用户）

1. **GDPR + Art. 27**（欧盟用户）
2. **CCPA/CPRA**（加州用户）
3. **SB-53**（如属 frontier 大模型开发者）
4. **Colorado AI Act**（2026-06-30 起，若做 HR / lending / housing 决策类 AI）

### 场景 3：Archetype A（纯内资）

1. **PIPL**（本地合规）
2. **算法备案 / 大模型备案 / 登记** — 详见 `ai-filing-guide.md`
3. **《网络安全法》修订 2026-01-01**（AI 正式入法 § 20）
4. **深度合成标识**

---

## 七、推荐服务商类型

| 合规点 | 典型服务商 | 月费 |
|---|---|---|
| Art. 27 EU 代表 | Prighter / VeraSafe / EDPO | €200-400 |
| UK 代表 | VeraSafe / Rickert | £150-300 |
| 算法备案/大模型备案顾问 | 数美 / 中伦网络 / 观韬中茂 / 锦天城 | 2-80 万 RMB 项目 |
| PIPL 安评 | 中国信通院 / 省级评估机构 | 10-50 万 RMB |
| GDPR 外部 DPO | OneTrust / TrustArc / 本地律所 | €500-2000 |

（**非背书**，示例用于方向定位。）

---

## 红旗对照

- 🚩 欧盟用户 >0 但无 Art. 27 → Red Flag 6
- 🚩 训练语料境外占比 >30% → 大模型备案打回
- 🚩 PIPL 出境量 >100 万人但未安评 → 上千万罚款 + 暂停业务
- 🚩 GPAI provider 未公示训练数据摘要 → AI Act 罚款最高 €15M 或 3% 全球营收
