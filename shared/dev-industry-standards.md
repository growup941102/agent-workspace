# 开发组 · 行业黑话 / 配套工具（交接手册）

- **日期**：2026-10-20（Asia/Shanghai）
- **用途**：开发组跨工种交接的**黑话释义、交付物名、验收清单、常用工具/路径**；减少「交了但验不过」的返工
- **效力**：参考；**冲突时**：用户拍板 > 部门 dept-spec（《AI 辅助研发与 Spec 管理建设方案》）> 本文件
- **互补主文（流程 / DoD / ISO 映射）**：同目录 [`INDUSTRY-COLLAB-DELIVERY.md`](./INDUSTRY-COLLAB-DELIVERY.md) — **本文件不重写**其标准表与 DoD 勾选细则
- **入库镜像（伯德维护）**：`agent-workspace` → `shared/dev-industry-standards.md`（Origin：`k4k85pts5d/agent-workspace`）
- **站立**：未说减则闸门 **0–8 全开**；Ops Agent **§8 仍冻结**；**无用户明示不启 cloud agent**；子内容默认 **Modal/Drawer**（纯导航除外）

---

## 0. 边界（必读）

| 边界 | 说明 |
| --- | --- |
| **与办公组** | **不混写**。办公组黑话/工具见付老师侧 `shared/office-industry-standards.md`；IA/线框/架构/Spec 不归办公组「做 PPT」 |
| **与算法组** | 算法文档/基准经**总工**协调；实现侧对接 **sqltool**（`/Users/zyc/self/sqltool`）；邓肯/罗德曼交付仍进开发组 Gate 产物链 |
| **§8 冻** | Ops Agent §8（含相关 DDL/能力）**冻结至用户明示打开**；提示词与交接包**禁止**暗示解冻或写入 cloud 启动步骤 |
| **本文件不做** | 不替代 dept-spec；不重写 ISO/DoD 表；不扩单人提交范围；不发明未确认 URL |

---

## 1. 黑话词表（term → 白话 → 主责）

| 黑话 | 白话含义 | 主责 / 常用方 |
| --- | --- | --- |
| **OpenSpec** | Spec 驱动：行为规格与实现设计分离；变更以 change 为单位，可 archive | 波波维奇（写）· 全组（读） |
| **change** | 一次可追溯变更目录（kebab-case），含 proposal / specs / tasks 等；行为变更必有 AC | 波波维奇 |
| **delta** | 相对现行 Spec 的增量行为规格（改行为先改 delta，再实现） | 波波维奇 |
| **AC** | Acceptance Criteria：可判定的验收准则（Given/When/Then 或等价） | 波波维奇（写）· 库里（验） |
| **Acceptance Path** | 每条 AC 的验收路径：`auto` \| `manual` \| `n/a` | 库里（与波波维奇对齐） |
| **SpecGov** | 首期默认结构门禁（`specgov check` / Action）；查产物链完整等；部门只做薄扫描小核 | 詹姆斯（接入）· 乔丹（放行核对） |
| **files.yaml** | 变更文件清单；相对目标分支 diff **对称差须为零**；条目标 `purpose`/`reason` 等 | 詹姆斯（补全）· 库里（挂验收入口） |
| **evidence.yaml** | 验证证据清单；自动化项硬绑 **ci_job + SHA + success**；路径/入口变则旧证失效 | 库里 · 詹姆斯 |
| **常规审查** | Gate 8 默认轨：合并前第二人（或规定角色）批准；高风险/行为变更优先 | 乔丹协调 · 审查人 |
| **单人提交** | Gate 8 例外轨：免第二人批准，**不免** Gate 7 必检；仅技术负责人预定义范围 | 乔丹 · 技术负责人规则 |
| **tip** | 待合并 / 待验收的**候选提交 tip SHA**（evidence / 同步本机须对齐此 SHA） | 詹姆斯（出 tip）· 库里（验 tip） |
| **bogon** | 用户本机工作栈标签（路径常为 `/Users/zyc/self/ops_agent`）；**tip → bogon** 同步后做真机/本地冒烟 | 乔丹协调同步 · 詹姆斯/库里验收 |
| **UI-IA** | 界面信息架构 + 关键流程说明（非像素视觉规范正文） | 麦迪 |
| **线框拍板** | Gate 5：线框/IA 经**用户拍板**后詹姆斯才可按该界面实现 | 麦迪（交稿）· 用户（拍板）· 乔丹（记闸门） |
| **Gate n** | 部门闸门编号 0–8（立项→…→合并审查）；未说减则全开 | 乔丹（守门） |
| **ADR** | Architecture Decision Record：上下文 / 决策 / 后果短文 | 杜兰特 |
| **C4** | 架构沟通图：Context / Container /（按需）Component | 杜兰特 |
| **冒烟** | 最小可自动化/可手工的关键路径通过检查；P0 优先 `auto` | 库里 · 詹姆斯自测 |
| **P0** | 最高优先级用例/缺陷；未过不得宣称可合并 | 库里 |
| **DoD** | Definition of Done：未达则不得宣称「完成/可合并」；细则见主文 §4 | 乔丹 · 全组 |
| **对称差** | `files.yaml` 路径集合 ↔ `git diff` 路径集合差应为 **空**（GOV-002） | 詹姆斯 · SpecGov/部门扫描 |
| **ci_job + SHA** | evidence 必填绑定：必检 CI job 名 + 候选/`commit` SHA + success（字段名或作 `ci_job_name`/`candidate_sha`） | 库里 · 詹姆斯 |
| **dept-spec** | 部门《AI 辅助研发与 Spec 管理建设方案》及 OpenSpec 定制设计；权威高于本参考 | 全组服从 |
| **archive** | OpenSpec 变更合并后归档语义；apply/archive 前证据须有效 | 波波维奇 · 詹姆斯 |
| **GOV-00x** | 部门薄扫描规则编号（如 GOV-002 对称差、GOV-005 job+SHA）；与 SpecGov 分工 | 詹姆斯 · 乔丹 |

> 共 **24** 条。视觉像素规范另见 `FRONTEND-SPEC.md` / `COMPONENT-SPARE.md`，**不是**本黑话主文。

---

## 2. 闸门 0–8：交付物 · 主责 · 验收 · 工具/路径

> 流程含义与标准映射见 [`INDUSTRY-COLLAB-DELIVERY.md`](./INDUSTRY-COLLAB-DELIVERY.md) §2；此处只给**交接用检查单**。

### Gate 0 — 立项

| 项 | 内容 |
| --- | --- |
| **交付物名** | 立项说明（问题 / 范围 / 非目标 / 干系人 / 成功判据） |
| **主责** | 波波维奇（起草）· 乔丹（是否放行下一闸） |
| **验收清单** | - [ ] 问题与价值一句话说清<br>- [ ] 范围与非目标成对出现<br>- [ ] 干系人含用户拍板角色<br>- [ ] 成功判据可日后对照<br>- [ ] 未暗示跳过后续闸门 |
| **工具/路径** | change 提议草稿；长期可落入 `openspec/changes/<name>/proposal.md`（仓内） |

### Gate 1 — OpenSpec + AC

| 项 | 内容 |
| --- | --- |
| **交付物名** | OpenSpec **change**（proposal + **delta**/specs + **AC**） |
| **主责** | 波波维奇 |
| **验收清单** | - [ ] 行为优先；实现细节未冒充唯一真相<br>- [ ] 每条 AC 可判定（无「尽量/适当」）<br>- [ ] 行为变更有 delta，而非只改代码口头说<br>- [ ] 命名 kebab-case；与库里约定 Acceptance Path 草案<br>- [ ] 不影响 §8 冻区（Ops Agent） |
| **工具/路径** | `<repo>/openspec/changes/<change-id>/`；权威 Spec 概念见 OpenSpec；部门定制见 docs/`部门OpenSpec定制设计.md`（本机常在 `/Users/zyc/self/` 侧文档） |

### Gate 2 — tests.md

| 项 | 内容 |
| --- | --- |
| **交付物名** | `tests.md`（相对 AC；含 Acceptance Path） |
| **主责** | 库里（可与波波维奇并行对齐） |
| **验收清单** | - [ ] 每条 AC 有 `auto`\|`manual`\|`n/a`<br>- [ ] P0/冒烟优先标 `auto`<br>- [ ] 用例可追溯到 AC 编号<br>- [ ] 不强制 AC↔自动化 1:1<br>- [ ] 入口日后可挂 `files.yaml` verification |
| **工具/路径** | `openspec/changes/<id>/tests.md`（与代码同仓约定） |

### Gate 3 — 产品材料（含表结构）用户拍板

| 项 | 内容 |
| --- | --- |
| **交付物名** | 产品材料包（业务规则 + **表结构/数据契约** 等） |
| **主责** | 波波维奇（材料）· **用户拍板** · 乔丹记闸门 |
| **验收清单** | - [ ] 表结构与关键业务规则齐全<br>- [ ] 与 Gate 1 AC 无矛盾<br>- [ ] **用户已拍板**（无拍板不得进实现侧扩张）<br>- [ ] §8 相关 DDL/能力未擅自解冻<br>- [ ] 变更后须回闸，禁止静默漂移 |
| **工具/路径** | 例：`openspec/changes/<id>/product/`（如 `gate3-product-materials.md`）；Ops Agent 设计/schema 文档在仓 `docs/` |

### Gate 4 — 架构拍板

| 项 | 内容 |
| --- | --- |
| **交付物名** | 架构设计文档 + **ADR**（关键决策）+ **C4**（至少 Context/Container） |
| **主责** | 杜兰特（可写）· 乔丹协调 · **用户拍板** |
| **验收清单** | - [ ] 关键决策有 ADR（上下文/决策/后果）<br>- [ ] C4 能让实现方看懂边界<br>- [ ] 非功能目标可验证表述<br>- [ ] 不确定处标「待用户拍板」<br>- [ ] **用户已拍板**；偏离须 ADR/变更单 |
| **工具/路径** | 例：`openspec/changes/<id>/architecture/`；调研来源须真 URL |

### Gate 5 — 界面拍板

| 项 | 内容 |
| --- | --- |
| **交付物名** | **UI-IA** + **线框**（及约定的 html-blue / 线框图） |
| **主责** | 麦迪 · **用户拍板** · 乔丹记闸门 |
| **验收清单** | - [ ] IA/关键流程可测，非仅视觉口号<br>- [ ] 子内容默认 Modal/Drawer（纯导航除外）<br>- [ ] 影响行为时已通知波波维奇改 OpenSpec/AC<br>- [ ] **用户已拍板**；拍板前詹姆斯**勿实现该界面增量**<br>- [ ] 与库里约定可自动化 UI 冒烟范围 |
| **工具/路径** | 设计参考：`/Users/zyc/self/design-refs/`（及 box 镜像 `/workspace/design-refs/`：`FRONTEND-SPEC.md`、`COMPONENT-SPARE.md`）；变更内 `ui-ia.md` / `docs/` 线框 |

### Gate 6 — 实现

| 项 | 内容 |
| --- | --- |
| **交付物名** | 相对已拍板 Spec/设计的代码变更（**tip**） |
| **主责** | 詹姆斯 |
| **验收清单** | - [ ] Gate 1–5 所需拍板已就绪（未说减则全开）<br>- [ ] 冲突先停写、提 Spec 修订，禁止先写后补<br>- [ ] 自测覆盖 P0/冒烟<br>- [ ] 变更可被 `files.yaml` 对称差核对<br>- [ ] 不扩单人提交范围；高风险默认常规审查<br>- [ ] 不触碰 §8 冻区；不启 cloud（无明示） |
| **工具/路径** | 主仓本机：`/Users/zyc/self/ops_agent`（**bogon**）；技术栈约定 FastAPI + React/Vite/AntD + MySQL |

### Gate 7 — files / evidence / CI

| 项 | 内容 |
| --- | --- |
| **交付物名** | `files.yaml` + `evidence.yaml` + **CI 绿**（+ SpecGov/部门扫描通过） |
| **主责** | 詹姆斯（清单与实现对齐）· 库里（证据与用例）· 乔丹（是否宣称完成） |
| **验收清单** | - [ ] `files.yaml` 对称差为零；purpose/reason 完备<br>- [ ] 验收入口已挂 verification<br>- [ ] `evidence.yaml` 绑 **ci_job + SHA**；SHA = 待合并 **tip**<br>- [ ] 路径/入口变更后旧证据已失效并重跑<br>- [ ] `manual` AC 有最小人工记录<br>- [ ] 必检 CI + SpecGov/扫描通过（细则见主文 DoD） |
| **工具/路径** | `openspec/changes/<id>/files.yaml`、`evidence.yaml`；`.specgov.yml`；部门扫描小核（GOV-002/005 等） |

### Gate 8 — 合并审查

| 项 | 内容 |
| --- | --- |
| **交付物名** | 合并记录（**常规审查**批准 **或** **单人提交**留痕） |
| **主责** | 乔丹（轨选择与放行）· 审查人 / 提交人 |
| **验收清单** | - [ ] Gate 7 全部满足（单人轨也不免）<br>- [ ] 已标明常规审查 vs 单人提交<br>- [ ] 单人仅落在预定义范围；原因与规则版本可查<br>- [ ] 高风险/行为变更未擅自走单人<br>- [ ] 平台留痕（账户/原因/候选 SHA）；进入抽查池（单人） |
| **工具/路径** | 仓托管平台 PR/合并队列（具体 host **以该仓实际为准**，见 §5） |

---

## 3. 跨工种交接矩阵（交付包必须含）

每次交接 = **产物 + 版本/tip SHA（如有）+ 本闸验收勾选结果 + 未决问题**。缺包可打回。

| 从 → 到 | 交付包必须含 | 下游开收勾 |
| --- | --- | --- |
| **波波维奇 → 库里** | Gate 1 change 路径；AC 列表/编号；已知边界与非目标；Acceptance Path 草案（若有） | AC 可判定；可写 tests.md；无「口头 Spec」 |
| **库里 → 詹姆斯** | `tests.md`；P0/冒烟范围；`auto`/`manual` 划分；不可自动化说明 | 自测目标清晰；manual 有最小步骤预期 |
| **麦迪 → 詹姆斯** | 已拍板 UI-IA + 线框/参考实现；Modal/Drawer 约定；与 Spec 差异说明（若有） | **拍板凭证**；拍板前不实现该增量 |
| **杜兰特 → 詹姆斯** | 已拍板架构文 + ADR + C4；开放问题清单（应为空或已拍板） | 边界可编码；非功能可测 |
| **詹姆斯 → 库里（证据）** | **tip SHA**；本地/CI 自测说明；拟写入的 evidence 字段；变更路径列表 | tip 可检出；证据可绑 ci_job+SHA；与 bogon 同步策略清楚 |
| **詹姆斯 → 乔丹（申请 Gate 7/8）** | files.yaml；evidence.yaml；CI 链接或 job 名；审查轨建议（常规/单人） | 对称差；SHA 一致；轨合法 |
| **乔丹 ↔ 各角色** | 当前 **Gate n**；是否已用户拍板（3/4/5）；§8/cloud 约束；打回缺口列表 | 角色只推进本闸；不跳闸口头放行 |
| **邓肯 → 罗德曼 / 詹姆斯** | 算法契约（I/O、边界、失败模式）+ 与 AC 映射 | 基准可复现；实现不偷偷改契约 |
| **罗德曼 → 库里 / 乔丹** | 基准报告路径 + 数据集/环境/种子 + 对齐 tip SHA | 可作 Gate 7 证据类型之一 |
| **算法组 / 总工 → 开发组** | sqltool 侧约定接口或文档指针；总工确认的对接范围 | 不绕开总工私接；产物仍进 files/evidence |

### 打回话术（乔丹或下游）

```
【打回】<角色> · Gate <n>
缺口：…
缺文件/ tip / 拍板：…
请补：…
补齐前不要进 Gate <n+1>。
§8 冻 / 未说减则全开：仍有效。
```

---

## 4. 工具与路径清单（仅已知；不确定标「待确认」）

| 名称 | 路径 / 标识 | 备注 |
| --- | --- | --- |
| **Ops Agent 本机（bogon）** | `/Users/zyc/self/ops_agent` | tip→bogon 同步后真机/本地验；§8 冻 |
| **sqltool** | `/Users/zyc/self/sqltool` | 算法组/总工对接；历史试点叙述可能涉及，**以总工当前指定为准** |
| **design-refs（本机）** | `/Users/zyc/self/design-refs` | 设计与行业参考源 |
| **design-refs（box 镜像）** | `/workspace/design-refs` | 本文件与 `INDUSTRY-COLLAB-DELIVERY.md` 等 |
| **agent-workspace（Origin）** | owner `k4k85pts5d` / repo `agent-workspace`；clone：`https://origin.cursor.com/k4k85pts5d/agent-workspace.git` | 伯德维护；目标放入 `shared/dev-industry-standards.md` |
| **agent-workspace 闸门摘要** | `shared/dev-gates.md` | 已有简版闸门表；本文件为黑话+验收补强 |
| **OpenSpec 目录（仓内）** | `<repo>/openspec/changes/`、`openspec/specs/`、`openspec/schemas/dept-gov/` | 以各仓 tip 为准 |
| **files / evidence** | `openspec/changes/<id>/files.yaml`、`evidence.yaml` | 例见 Ops Agent 变更目录 |
| **SpecGov 配置** | 仓根 `.specgov.yml`（及 `governance/`，若已接入） | 首期默认 strict；待确认各仓是否已齐 |
| **dept-spec 文档** | 用户/部门文档侧（建设方案修订稿、部门 OpenSpec 定制设计） | box 曾有 `/workspace/docs/`、`/workspace/openspec-materials/` 副本；**权威以用户指定版本为准** |
| **Ops Agent 远程托管 URL** | **待确认**（以该仓实际 remote 为准；勿臆造） | 交接写 tip SHA + remote 名即可 |
| **办公组标准** | `shared/office-industry-standards.md`（agent-workspace / 付老师侧） | **不与本文件混写** |

---

## 5. 明确冻结与不混写

1. **Ops Agent §8**：冻结，直至用户明确打开。  
2. **Cloud agent**：无用户明示 → 不启动、提示词不写启动步骤。  
3. **未说减则全开**：Gate 0–8；不得擅自裁剪 3/4/5 拍板。  
4. **办公组**：文稿/幻灯/表格/文档册/制图标准另册；开发组不把 IA/架构塞进办公交付。  
5. **算法组**：对接总工 + sqltool；邓肯/罗德曼仍遵守本开发组 files/evidence 习惯。  
6. **Modal/Drawer**：点按钮出子内容默认浮层；纯路由导航除外。

---

## 6. 维护

- 修订注明日期（Asia/Shanghai），通知**伯德**同步 `agent-workspace/shared/dev-industry-standards.md` 与提示词片段。  
- 流程/DoD/ISO 变更改 [`INDUSTRY-COLLAB-DELIVERY.md`](./INDUSTRY-COLLAB-DELIVERY.md)；本文件只跟黑话与交接包。  
- 片段入口见同目录 [`DEV-INDUSTRY-STANDARDS-SNIPPET.md`](./DEV-INDUSTRY-STANDARDS-SNIPPET.md)。

*效力：参考。用户拍板 > dept-spec > 本文件。*
