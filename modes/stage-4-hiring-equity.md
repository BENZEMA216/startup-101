# Stage 4: Hiring & Equity — 招人与期权

> last_policy_review: 2026-04-15

## 何时进入

- 公司运营跑通（Stage 3 完成）
- 准备招第一个或第 2-10 个员工
- 或：已招但没正式处理 labor contract / ESOP / IP

## Disclaimer

> ⚠️ 本阶段涉及 **劳动合同**、**员工期权**、**IP Assignment**，每一项都影响融资 DD。
> **所有劳动合同 / ESOP 文件 / IP 条款必须由律师起草或 review**。Skill 只给框架。

## 按 Archetype 分流

| Archetype | 本阶段重点 |
|---|---|
| A（纯内资） | 劳动合同 + 内资期权（有限公司期权或预留股权池） + IP 归属境内主体 |
| B（双层出海） | **WFOE 劳动合同 + Cayman 层 ESOP + IP 指向 Cayman + 37 号文（员工）** |
| C（创始人已出海） | US employment agreement + 期权发 Delaware + 若仍有中国员工走 WFOE 独立处理 |

---

## 决策 1：劳动合同基础（WFOE / 内资侧）

### 时间窗口
- **员工入职日起 30 日内必签书面劳动合同**。逾期 = 双倍工资惩罚性赔偿（30 日至 1 年内）。

### 核心条款
- [ ] 岗位 / 职责
- [ ] 薪酬结构（base / 年终 / 奖金 / 期权）
- [ ] 工作时长（标准工时 / 综合工时 / 不定时工时需审批）
- [ ] 试用期（根据合同期长度：3 个月以上 → 最长 6 个月试用）
- [ ] 保密条款
- [ ] **IP Assignment（职务发明归公司）** — 详见决策 3
- [ ] **竞业限制**（可选 + 有代价，详见决策 6）
- [ ] 解除条件

### 社保 + 公积金
- 与劳动合同同步启动（Stage 3 已开户）

### 红旗
- 🚩 "实习生"长期用（>3 个月 + 全职强度） → 劳动关系认定风险
- 🚩 只签保密不签劳动合同 → 30 日后双倍工资
- 🚩 试用期薪资 <80% 正式期 → 违法

---

## 决策 2：ESOP 池设立

### Archetype A：内资有限公司的"类期权"
- 中国《公司法》没有典型 ESOP 框架
- 替代方案：
  1. **预留股权** — 增资扩股前预留 10-15% 给员工持股平台（LP 有限合伙）
  2. **虚拟期权 / Phantom Shares** — 合同约定"达成条件获得等价现金"，不涉及真实股权
  3. **持股平台** — 员工跟投 LP，GP 由创始人持
- **退出路径受限**：内资公司没有 IPO / 转让就无法兑现
- **建议：** A 类如有长期 IPO 想法 → 考虑翻红筹，别勉强做内资 ESOP

### Archetype B：Cayman 层 ESOP（最关键）

#### 为什么必须在 Cayman 层
- 员工期权最终价值 = Cayman 母公司股权，退出时跟投资人同层
- WFOE 层发的"虚拟期权"无法换算 Cayman 股权 → 员工不认
- Cayman Option Plan 是美元融资 DD 标准

#### 池子规模
- **首轮融资前预留 10-15%**
- 每轮融资稀释创始人（不是投资人）— 记入 TS 谈判

#### 文件包
- [ ] **Stock Incentive Plan（SIP）** — Cayman 母公司章程附件
- [ ] 每员工的 **Option Grant Letter / Notice**
- [ ] **Option Agreement**（vesting / 行权价 / 到期）
- [ ] Cooley GO Option Plan Template（参考）

#### 关键参数
- **Vesting：4 + 1**（4 年成熟 + 1 年 cliff）
- **行权价：** Fair Market Value（早期 = 融资估值 / 总股数；没融资用 409A 估值或创始人合理判断）
- **Option 类型：** 一般 NSO（非合格股票期权）；ISO 有 US 税优但仅限 US 员工
- **行权期：** 10 年
- **离职行权窗口：** 90 天（标准）/ 1-10 年（创始人友好版）

### 🚩🚩 中国员工拿 Cayman 期权 = 37 号文员工篇

**触发：** 中国籍员工（中国税务居民）获得境外母公司 option

**要求：**
1. 员工个人登记 37 号文（外管局）
2. 行权时外汇通道合规
3. 退出 / 卖股时外汇汇回合规

**补救（如果已发未登记）：**
- 跨境律所补做员工侧 37 号文
- 如员工已行权但未登记 → 融资 DD 爆雷风险 + 员工自己的外汇罚款风险

**操作惯例：**
- 期权给之前就建立"员工 37 号文指引 + 律所转介"
- 每个员工入职包含：劳动合同 + ESOP Offer + 37 号文办理指引

### Archetype C：Delaware 层

- **Stock Incentive Plan + ISO / NSO Grants**
- ISO 对 US 员工税优（但 $100k/年授予上限）
- NSO 无限额，适合创始人 + Contractor
- **Rule 701 / S-8** 等 SEC 豁免

---

## 决策 3：IP Assignment

### Red Flag 2 核心动作

**所有员工（含 Contractor / 实习生 / 兼职 / 创始人自己）必须签 IP Assignment 追溯条款。**

### 受让方必须是"最终持 IP 的主体"

| Archetype | IP 受让方 |
|---|---|
| A | 境内主体 |
| B | **Cayman 母公司**（关键 — 不是 WFOE！） |
| C | Delaware C-corp |

**为什么 Archetype B 必须指向 Cayman：**
- 美元融资 DD 验证：Cayman 是否持核心 IP
- 如果 IP 停留在 WFOE → Cayman 仅是"空壳" → 估值打折 / 交易延期

### 三件套

1. **劳动合同**（含基础 IP 条款）
2. **IP Assignment Agreement**（独立文件，受让方 = Cayman）
3. **发明创造归属协议**（对关键研发员工额外签）

**模板参考：** Cooley GO IP Assignment Agreement Template

### 追溯条款

- 覆盖入职前的准备工作（pre-employment IP clause）
- 覆盖工作时间外的相关工作（moonlighting IP clause，适度）
- 员工自己的背景 IP 需要白名单（Prior IP list）

### 红旗

- 🚩 只签劳动合同不签 IP Assignment
- 🚩 IP 受让方写成 WFOE（Archetype B 错配）
- 🚩 Contractor 无 IP Assignment → 外包代码 IP 不归公司

---

## 决策 4：Vesting 与章程

### 创始人 Vesting

- **4 年 + 1 年 cliff** — 业界标准
- Cayman 层写进 Stockholders Agreement
- Delaware 层写进 Founders' Stock Purchase Agreement
- 投资人强烈要求（不 vest 的联创跑路 → 剩余股权冻结 / 加速机制）

### 员工 Vesting

- 同 4+1
- 1 年 cliff = 1 年内离开 0 股权
- 此后每月 1/48 成熟

### Acceleration（并购时加速）

| 类型 | 含义 | 推荐 |
|---|---|---|
| **Single-trigger** | 并购 = 自动加速 100% vesting | 对创始人最好，投资人常拒 |
| **Double-trigger** | 并购 + 被解雇 = 加速 | **标配** |
| **No acceleration** | 无加速 | 早期员工常见 |

**写进文件：** Cayman Stockholders Agreement 或 Delaware Bylaws + Option Agreement

---

## 决策 5：竞业限制

### 法律要求（中国）

**竞业补偿是对价：** 劳动者离开后，公司若要求不从事同行业，**必须每月支付补偿金** — 不能低于离职前 **12 个月平均工资的 30%** 或当地最低工资（以高者）。

不给补偿 → 竞业协议无效，员工可自由入职同行。

### 范围 / 时间
- 最长 2 年
- 范围必须与原岗位直接相关，不能泛化"所有 AI 行业"
- 违约金可约定（通常是年薪 2-6 倍）

### 实操

- 对核心研发 / 算法岗签
- 对普通员工不必签（补偿成本高）
- **签了就要真付钱** — 不付钱的"保护"一文不值

### 红旗

- 🚩 竞业协议签了不付补偿金 → 协议无效 + 员工可维权补偿
- 🚩 范围泛化（"所有 AI 公司"）→ 法院倾向无效

---

## 决策 6：Offer Letter / Employment Agreement（海外侧）

### Delaware / US 员工
- **At-will employment** 条款（美国标配，可随时解雇除非违反 anti-discrimination）
- **Confidential Information Agreement**
- **Proprietary Information & Invention Assignment (PIIA)** — US 版 IP Assignment
- **Benefits**（401k / 医保 / PTO）
- Cooley GO Offer Letter Template

### SG / HK 员工
- 本地 Employment Act / Ordinance 遵从
- 试用期惯例 3-6 个月
- 年假 / 病假法定下限

---

## 必查清单

### 所有 Archetype
- [ ] Cooley GO 劳动 / 期权模板已下载
- [ ] 律师审阅所有合同模板
- [ ] 期权池规模决定（10-15%）
- [ ] Vesting 4+1 写进所有文件

### Archetype A
- [ ] 劳动合同（入职 30 日内）
- [ ] 股权激励池方案（虚拟期权 / 持股平台）
- [ ] IP Assignment → 境内公司
- [ ] 竞业协议（核心岗 + 补偿）

### Archetype B（增量）
- [ ] **Cayman SIP + Option Plan 章程附件**
- [ ] **WFOE 劳动合同 + IP Assignment → Cayman**
- [ ] 员工 37 号文指引文档
- [ ] 律所转介（给员工办 37 号文）
- [ ] Double-trigger acceleration 条款

### Archetype C（增量）
- [ ] Delaware SIP + ISO/NSO Grants
- [ ] US Offer Letter + PIIA
- [ ] Payroll 对接（Stage 3 已开 Gusto）

---

## 典型避坑场景

**场景 1：IP Assignment 指错受让方**
某 Archetype B 公司所有员工签的 IP Assignment 受让方写成 WFOE。A 轮 DD 阶段 Cooley 发现 → 要求全员重签受让方改 Cayman。2 个月 + 3 个老员工拒签 → TS 估值打折 15%。

**场景 2：中国员工期权未办 37 号文**
某 AI 公司融 B 轮时 DD 发现所有中国员工拿了 Cayman option 但没办 37 号文。律师要求补登记 + 合规整改 → 3 个月 + 2 个员工期权作废。

**场景 3：竞业协议不付补偿**
某 AI 公司 12 个核心研发离职后跳到直接竞品，公司起诉。法院查到竞业期间未付补偿 → 判协议无效，员工胜诉。公司反向赔诉讼费。

---

## 红旗扫描（本阶段）

调用 `modes/red-flags.md`：
- **Red Flag 1**（37 号文）— 员工拿 Cayman option 前必查
- **Red Flag 2**（IP Assignment）— 本阶段必过关

**本阶段新增红旗（未入 6 条主清单）：**
- 🚩 劳动合同 30 日逾期
- 🚩 试用期薪资违规
- 🚩 竞业协议不付补偿金
- 🚩 IP Assignment 受让方错配（B → 写 WFOE）

## 推荐阅读

- `references/index/03-hiring-equity.md` — Index Option Plan Handbook / Cooley GO
- `references/index/02-incorporation.md` — 37 号文专题
- Index Ventures — *Rewarding Talent* Handbook
- 汉坤 / 方达《中国员工境外期权合规指引》

## 本阶段结束状态

用户能回答：
1. 所有员工劳动合同签了？30 日内完成？
2. ESOP 池规模定了？Cayman/Delaware 层文件齐了？
3. 所有人 IP Assignment 指向正确主体？
4. 中国员工 Cayman option 的 37 号文指引？
5. 竞业协议范围合理 + 付补偿？

确认后进入 Stage 5 AI 产品上线前。
