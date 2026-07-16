# Skill 拆解、优化与治理套件

[简体中文](README.md) | [English](README_EN.md)

> 一套用于拆解、优化、评测、编排和持续治理 AI Skill 的五 Skill 协作体系。

本仓库不是某一个业务 Skill，而是一套帮助团队**理解外部 Skill、规划安全改进、验证新版本并管理长期演进**的标准工作流。它适合需要把重复操作封装成 Skill 的团队，尤其适用于跨境电商运营、ERP 报表处理、财务对账和内部标准流程沉淀。

核心原则：

- 先收集证据，再做判断；
- 拆解默认只读，不修改来源；
- 优化先提交差异和变更计划，批准后才生成派生版本；
- 评测必须保留可复现证据，关键失败不能被平均分掩盖；
- 中央套件默认只能提交改进提案；
- 个人分支必须由使用者明确选择；
- 运行时 Skill 与维护测试材料分开安装。

## 这套工具解决什么问题

当团队拿到一个别人分享的 `SKILL.md` 或完整 Skill 目录时，常见问题并不是“能不能打开”，而是：

- 它什么时候应该触发，什么时候不应该触发？
- 它需要哪些文件、字段、脚本、模板和外部工具？
- 它的流程、判断分支、异常处理和验收标准是否完整？
- 文件中描述的行为是事实、合理推断，还是尚未验证？
- 如果要加入公司规则，哪些内容保留、修改、新增、删除或拆分？
- 改进是否经过明确批准，是否保留了原始版本？
- 新版本是否通过触发、功能、异常、回归和可移植性测试？
- 一次有效改进应该进入中央版本，还是只保留为个人分支？

本套件用五个职责清晰的 Skill 回答这些问题，并用标准产物把前一阶段的结果传递给下一阶段。

## 适用与不适用场景

### 适用场景

- 拆解一个 `SKILL.md`，还原它的触发、输入、流程、规则、输出和失败路径；
- 检查完整 Skill 包中的 `references/`、`scripts/`、`assets/` 和文件引用是否齐全；
- 在不覆盖来源的前提下，规划修改、拆分、重构或公司化适配；
- 测试 Skill 是否会正确触发、能否处理缺失或异常输入、输出是否符合合同；
- 编排“拆解 → 优化 → 评测 → 安装/发布”的跨阶段任务；
- 管理本套件自身的提案、审批、版本、个人分支、合并、发布和回滚；
- 将 ERP 表格处理、平台对账、财务账单输出等标准流程逐步封装为可维护 Skill。

### 不适用场景

- 只想完成一次性的表格清洗，而不需要沉淀或评审流程；
- 希望在没有数据口径、黄金样例或审批人的情况下自动决定核心业务规则；
- 希望绕过评测，直接把未验证版本安装到生产环境；
- 希望用行业常识补写来源 Skill 中缺失的 reference、脚本或模板；
- 希望在只授权分析时直接覆盖或修改对方的源文件。

## 五个 Skill 如何分工

| Skill | 何时使用 | 是否修改目标 Skill | 主要输入 | 主要产物 |
|---|---|---:|---|---|
| [`analyzing-skills`](runtime/analyzing-skills/SKILL.md) | 检查、解释、审计、逆向分析或拆解 | 否，只读 | 单个 `SKILL.md` 或完整 Skill 包 | `analysis-brief`、证据表、缺失依赖和问题清单 |
| [`improving-skills`](runtime/improving-skills/SKILL.md) | 明确要求修改、优化、拆分、重构或生成派生版本 | 是，但只生成非破坏性派生版本 | `analysis-brief`、新增需求、来源版本 | `change-plan`、差异分类、获批后的派生 Skill |
| [`evaluating-skills`](runtime/evaluating-skills/SKILL.md) | 测试、验证、评审、比较或判断能否发布 | 默认不修改 | 目标版本、输入合同、测试环境、黄金样例 | `evaluation-report`、测试矩阵、`release/revise/blocked` 结论 |
| [`governing-skill-evolution`](runtime/governing-skill-evolution/SKILL.md) | 修改的是本套拆解体系自身，或需要提案、审批、版本、分支、合并、发布、回滚 | 管理变化，不代替实现 | 失败案例、风险、影响范围、回归证据 | `improvement-proposal`、审批与版本记录 |
| [`orchestrating-skill-work`](runtime/orchestrating-skill-work/SKILL.md) | 一个请求跨越两个或更多阶段 | 取决于下游阶段 | 用户目标、来源、允许操作、期望交付 | `task-brief`、阶段状态、标准产物交接和最终汇总 |

### 关键边界

- `analyzing-skills` 发现问题，不代表已经获得修改授权。
- `improving-skills` 即使收到“直接改”的要求，也要先输出 `change-plan` 并等待针对当前计划的明确批准。
- `evaluating-skills` 负责提供发布证据，但不通过修改期望规则来让测试“变绿”。
- `governing-skill-evolution` 只治理本套件自身；普通业务 Skill 的优化仍交给 `improving-skills`。
- `orchestrating-skill-work` 只负责路由、状态和交接，不替代四个专业 Skill 完成工作。

## 如何选择正确的 Skill

按照请求的最终产物选择，而不是只看句子中出现了哪些动词：

1. **只想理解或审计，不要求改动**：使用 `analyzing-skills`。
2. **明确要求修改或生成新版本**：使用 `improving-skills`；如果还没有证据化分析，先补做分析。
3. **想知道是否正确、是否退化、是否可发布**：使用 `evaluating-skills`。
4. **想修改本套拆解流程本身**：使用 `governing-skill-evolution`。
5. **一次提出拆解、优化、测试、安装等两个以上结果**：使用 `orchestrating-skill-work`。

详细路由条件见 [`routing-rules.md`](runtime/orchestrating-skill-work/references/routing-rules.md)。

### 容易混淆的例子

| 用户请求 | 正确入口 | 原因 |
|---|---|---|
| “解释这个 Skill 的风险，再判断它能不能发布” | `evaluating-skills` | “解释风险”服务于评测，不要求独立拆解产物 |
| “先完整拆解，再生成适合财务团队的新版本” | `orchestrating-skill-work` | 同时要求独立分析和优化两个阶段 |
| “优化我们这套拆解 Skill 的审批规则” | `governing-skill-evolution` | 目标是本套件自身 |
| “优化一个亚马逊库存分析 Skill” | `improving-skills` | 目标是外部业务 Skill |
| “只列出这个 SKILL.md 引用了哪些缺失文件” | `analyzing-skills` | 只读检查，无修改需求 |

## 完整工作流程

一次跨阶段任务采用以下状态序列：

```text
received
  → source-checked
  → analyzed
  → awaiting-change-approval
  → derived
  → evaluating
  → awaiting-release-approval
  → released
```

### 第 1 步：建立任务边界

总控先生成 `task-brief`，记录：

- 用户目标；
- 来源文件和位置；
- 请求包含哪些阶段；
- 允许的变更模式：`read-only`、`derive-new` 或安装已通过评测的版本；
- 期望交付物；
- 审批角色和门槛；
- 缺失依赖与已知限制；
- 计划状态序列。

覆盖来源文件不是有效模式。用户要求覆盖时，应改为新名称、新版本，或明确选择个人分支。

### 第 2 步：证据化拆解

分析阶段先盘点实际收到的文件，并把引用标记为：

- `present`：文件存在且可读取；
- `missing`：来源引用了它，但未提供；
- `external`：依赖位于当前包之外；
- `unverified`：当前环境不能确认。

每条结论再区分为 `FACT`、`INFERENCE`、`MISSING`、`ISSUE` 或 `OPPORTUNITY`。单个 `SKILL.md` 只能支持文件级分析，不能冒充完整包级审计。

### 第 3 步：生成变更计划

把每项需求分类为：

- 保留；
- 修改；
- 新增；
- 删除；
- 拆分。

`change-plan` 必须说明目标名称、目标架构、受影响文件、迁移方法、回滚方法、失败处理和回归用例。生成计划后状态停在 `awaiting-change-approval`。

### 第 4 步：批准后生成派生版本

批准必须绑定当前 `case_id`、产物类型、产物版本、目标名称和目标版本。过去的一般性同意、口头催办或“直接改”都不能替代本次批准。

来源文件保持不变。派生 Skill 应使用不同名称或清晰版本标记。

### 第 5 步：评测

评测至少覆盖八类用例：

- `trigger`：应该触发和不应该触发；
- `function`：正常功能；
- `missing`：缺失输入或依赖；
- `abnormal`：异常和冲突数据；
- `contract`：输出合同；
- `repeatability`：重复执行；
- `regression`：旧问题是否修复、旧能力是否退化；
- `portability`：换环境或换使用者后是否仍成立。

每个用例记录输入、预期、实际、证据和状态。关键用例未运行、必需依赖缺失或关键回归失败时，不得给出 `release`。

### 第 6 步：发布或返回正确阶段

- 来源或依赖缺失：返回分析，状态 `incomplete`；
- 核心业务规则冲突：返回优化，状态 `blocked-by-business-rule`；
- 触发、合同、回归或可移植性失败：停在 `evaluation-failed`；
- 账号、权限、密钥或生产边界：状态 `blocked-by-permission`；
- 评测通过且获得发布批准：进入安装或发布。

标准产物头字段和交接规则见 [`artifact-contracts.md`](runtime/orchestrating-skill-work/references/artifact-contracts.md)。

## 审批式迭代机制

本套件区分两类审批：

### 工作流审批

- 分析或改进范围；
- 当前 `change-plan`；
- 发布或安装；
- 本套件自身的改进提案。

### 目标业务审批

- 财务复核；
- 法务或合规审核；
- 安全审批；
- 业务口径负责人确认；
- 目标 Skill 中定义的其他审批。

目标业务审批是分析和变更计划的输入，不等于批准 `change-plan`。例如，财务负责人批准账单结果，并不自动授权修改中央 Skill。

### 中央改进生命周期

```text
observed
  → proposed
  → under-review
  → approved
  → implemented
  → evaluated
  → released
```

被拒绝的提案记录为 `rejected` 并保留原因；证据或权限不足时保持 `proposed` 或 `blocked`。时间紧急不会自动升级为批准。

中央改进进入评审需要满足以下基本条件：

1. 问题至少出现在两个不同案例中，或属于高风险缺陷；
2. 改动能够减少遗漏、错误判断、不安全行为或重复劳动；
3. 不会给所有用户增加不合理的上下文成本；
4. 至少有一个回归用例在旧版失败、候选版通过；
5. 指定维护者批准准确的提案和目标版本。

完整规则见 [`improvement-protocol.md`](runtime/governing-skill-evolution/references/improvement-protocol.md)。

## 中央版本与个人分支

### 中央版本

- 只有一个受维护的规范版本；
- 默认接收其他使用者的改进提案；
- 变更必须经过提案、明确批准、回归、评测和发布决定；
- 单个普通案例通常不足以直接改变所有用户的中央流程；
- 发布时保留上一中央版本，便于回滚。

### 个人分支

只有使用者明确选择“维护个人分支”后才创建。个人分支必须记录：

- 带所有者标记的不同 Skill `name`；
- 来源中央版本；
- 所有者和预期使用者；
- 个人规则与适用范围；
- 兼容性和分歧风险；
- 个人测试结果。

个人分支不代表中央官方版本，也不会自动同步回中央版本。若希望合并回中央版本，必须重新提交差异、多个案例的证据、回归结果和新的中央改进提案。

当使用者没有选择目标分支时，默认只生成 `improvement-proposal`，不自动创建 feature 分支、个人分支、实现文件或发布产物。详见 [`branch-policy.md`](runtime/governing-skill-evolution/references/branch-policy.md)。

## 跨境电商团队应用示例

以下例子展示如何把常见业务映射到本体系。字段、阈值、公式和审批人均为示意，实际业务口径必须由使用者或业务负责人提供。

| 场景 | 推荐流程 | 关键输入 | 主要产物 |
|---|---|---|---|
| ERP 销售、库存和广告表格流程 | 拆解 → 改进提案 → 获批实现 → 评测 | 原 Skill、字段说明、样例表、业务口径 | 分析简报、派生 Skill、测试报告 |
| 平台对账单到标准财务账单 | 拆解 → 风险审查 → 获批实现 → 评测 | 对账单、字段映射、币种与期间、输出模板 | 财务处理 Skill、异常规则、标准账单 |
| 外部 Skill 的公司化适配 | 只读拆解 → 差异表 → 改进提案 | 完整 Skill 包、依赖文件、公司规则 | 证据表、缺口清单、变更计划 |

### 案例一：ERP 运营报表流程

运营人员从 ERP 导出销售、库存、广告或利润表，希望把重复清洗、字段映射、指标计算和异常标记封装为 Skill。

重点检查：

- 日期、站点、币种、SKU/ASIN 的关联口径；
- 空值、重复行、退货、取消订单和在途库存处理；
- 输入表发生字段变化时如何失败；
- 输出指标是否能追溯到来源列；
- 是否存在公司特有阈值，不应写入所有用户的中央版本。

不要凭行业经验自行补写缺失字段，也不要把示例安全库存天数当成公司正式口径。

### 案例二：平台对账单与标准财务账单

财务人员下载平台对账单，经过清洗、科目映射、币种换算、期间归属、异常核对后输出标准账单。

重点检查：

- 原始文件是否完整保留；
- 币种、汇率来源、税费和期间口径；
- 未匹配交易如何单列，而不是静默丢弃；
- 审核角色、证据、拒绝和超时处理是否明确；
- 黄金样例是否足以判断输出正确性。

没有业务负责人确认的财务口径时，状态应为 `blocked-by-business-rule`，不能由 Skill 自行决定。

### 案例三：外部 Skill 的公司化适配

收到别人分享的 Skill 后：

1. 先确认收到的是单个 `SKILL.md`，还是完整目录；
2. 盘点被引用但未提供的 reference、script、asset 或模板；
3. 输出证据化拆解表；
4. 将公司新增需求分类为保留、修改、新增、删除或拆分；
5. 生成待审批变更计划；
6. 获批后用新名称创建派生版本；
7. 评测通过后再安装或分享。

## 仓库结构

```text
analyzing-and-improving-skills/
├── README.md                         # 中文主文档
├── README_EN.md                      # 英文文档
├── INSTALL.md                        # 安装说明
├── runtime/                          # 可安装的五个运行时 Skill
│   ├── analyzing-skills/
│   ├── improving-skills/
│   ├── evaluating-skills/
│   ├── governing-skill-evolution/
│   └── orchestrating-skill-work/
├── governance/                       # 维护、测试和发布记录，不安装到运行时
│   ├── tests/
│   ├── samples/
│   └── release/
└── docs/                             # 架构、设计和实施计划
```

每个运行时 Skill 至少包含：

```text
skill-name/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
```

V1 运行时不包含 `scripts/` 或 `assets/`。如果未来新增，应同时定义接口、失败行为、执行测试和可移植性要求。

## 快速安装

个人安装只复制 `runtime/` 下的五个直接子目录到：

```text
~/.codex/skills/
```

Windows PowerShell 示例：

```powershell
$target = Join-Path $HOME '.codex\skills'
New-Item -ItemType Directory -Force -Path $target | Out-Null
Get-ChildItem '.\runtime' -Directory | ForEach-Object {
    Copy-Item $_.FullName -Destination $target -Recurse -Force
}
```

macOS / Linux 示例：

```bash
mkdir -p ~/.codex/skills
cp -R runtime/* ~/.codex/skills/
```

安装后应看到五个同级目录，每个目录有自己的 `SKILL.md` 和 `agents/openai.yaml`。不要把 `governance/` 复制到运行时 Skill 目录；它只用于维护、测试和发布证据。

如果 Codex 没有立即发现新 Skill，请重启 Codex。完整说明见 [`INSTALL.md`](INSTALL.md)。

## 第一次使用

### 只拆解一个 Skill

```text
请使用 analyzing-skills，只读拆解我提供的 Skill。

要求：
1. 不修改来源文件。
2. 区分事实、推断、缺失项、问题和改进机会。
3. 检查所有 references、scripts 和 assets 引用。
4. 输出版本化 analysis-brief。
```

### 拆解、优化并评测

```text
请使用 orchestrating-skill-work，编排这个 Skill 的拆解、改进和评测。

先生成 task-brief；完成 analysis-brief 后生成 change-plan，并停在审批节点。
未经我批准当前 change-plan，不要创建派生版本。
来源文件必须保持不变。
```

### 改进本套拆解体系

```text
请使用 governing-skill-evolution，为我发现的流程问题创建 improvement-proposal。
默认只提交中央改进提案，不自动实现。
如证据只来自单个普通案例，请明确标记证据范围。
```

## 常用提示词

| 目的 | 示例提示词 |
|---|---|
| 单文件拆解 | “只读拆解这个 `SKILL.md`，并列出无法进行包级验证的部分。” |
| 完整包审计 | “审计整个 Skill 目录，建立文件树和引用完整性表。” |
| 生成差异表 | “基于 `analysis-brief`，把新需求分为保留、修改、新增、删除和拆分。” |
| 规划派生版本 | “生成 `change-plan`，使用新名称，保留来源不变，并等待我批准。” |
| 评测触发 | “测试应触发、近似触发和不应触发的提示词，保留实际证据。” |
| 发布评审 | “覆盖八类测试，并给出单一 `release`、`revise` 或 `blocked` 结论。” |
| 个人分支 | “我明确选择维护个人分支；请记录来源版本、所有者、个人规则和兼容风险。” |
| 中央改进提案 | “不要直接修改中央套件，先提交带回归用例的改进提案。” |

## 标准输出物与证据要求

所有标准产物使用共同头字段：

```yaml
artifact_type: task-brief | analysis-brief | change-plan | evaluation-report | improvement-proposal
artifact_version: "1.0"
case_id: stable-case-id
source_skill: source-name-or-path
generated_at: ISO-8601 timestamp
status: current-workflow-state
owner: responsible-person-or-role
```

事实未知时填写 `unknown` 或 `not-assigned`，不要删除字段，也不要用看似精确的猜测替代。

| 产物 | 由谁生成 | 进入下一阶段前的最低要求 |
|---|---|---|
| `task-brief` | 编排 Skill | 范围、来源、允许变更、交付、审批和限制明确 |
| `analysis-brief` | 分析 Skill | 证据等级、文件引用、缺失项和边界明确 |
| `change-plan` | 优化 Skill | 差异分类、目标名称、影响文件、迁移、回滚和回归明确 |
| `evaluation-report` | 评测 Skill | 环境、八类用例、预期/实际/证据、单一 verdict 完整 |
| `improvement-proposal` | 治理 Skill | 问题、案例范围、风险、上下文成本和回归用例明确 |

已批准的产物不能被静默改写。需要补充证据时，应追加证据或生成新版本，并让新的批准绑定到准确版本。

## 评测、发布与回滚

### 评测状态

- `passed`：预期与实际一致，并有证据；
- `failed`：已经执行，结果不符合预期；
- `blocked`：必需依赖、权限、业务规则或黄金样例不可用；
- `not-run`：用例存在，但没有执行。

### 发布结论

- `release`：所有关键用例通过，非关键限制已明确并被接受；
- `revise`：存在可修复的触发、行为、合同或兼容问题；
- `blocked`：当前证据无法建立正确性。

下列情况属于关键失败：来源或目标版本不明确、必需文件或工具缺失、脚本执行失败、来源被意外修改、审批门槛可绕过、预期和实际无法比较、关键回归或触发冲突失败。

发布前使用 [`release-checklist.md`](governance/release/release-checklist.md)；当前版本状态见 [`manifest.md`](governance/release/manifest.md)。回滚恢复一个已知中央版本，但不能删除失败案例和回归证据。

## 常见问题

### 1. 只收到一个 `SKILL.md`，能不能完整拆解？

可以做文件级拆解，但不能宣称完成包级审计。文件中引用但未提供的 reference、script、asset 或模板必须标记为 `missing` 或 `unverified`。

### 2. 发现明显问题后，为什么不能直接修改？

因为分析授权和修改授权是两件事。先用 `change-plan` 展示准确差异、目标名称、风险和回归，能够避免误解用户意图或破坏来源。

### 3. 用户说“直接改”是否算批准？

不算。先生成当前任务的 `change-plan`，再取得绑定当前 `case_id`、产物版本和目标版本的明确批准。

### 4. 可以覆盖原 Skill 吗？

本套件不接受覆盖来源作为变更模式。使用新名称、新版本或明确选择的个人分支。

### 5. 公司特有规则应该放进中央版本吗？

通常不应该。单个普通案例默认保留为提案、配置候选或个人分支。只有跨案例重复问题或高风险缺陷，才具备申请中央评审的条件。

### 6. 测试文档写得很完整，能不能算运行通过？

不能。静态审阅、实际执行、真实观察和未验证项必须分开。关键用例没有运行时不得发布。

### 7. 为什么不能把 `governance/` 一起安装？

因为它包含测试、样例和发布记录，不是日常运行时指令。一起安装会增加无关上下文，并可能让维护规则干扰业务任务。

### 8. 其他人使用后发现的新问题会自动更新中央版本吗？

不会。默认只能提交改进提案；中央更新需要证据、回归、维护者批准、评测和发布决定。

### 9. 个人分支可以继续使用中央 Skill 名称吗？

不可以。个人分支必须使用不同名称并记录所有者，避免和中央版本混淆。

### 10. 评测失败后应该回到哪里？

来源不完整回分析阶段；规则或实现缺陷回优化阶段；权限问题保持阻塞；不得绕过失败直接安装。

## 贡献和维护

### 提交普通业务 Skill 改进

1. 附上来源版本和 `analysis-brief`；
2. 说明需求来源和适用范围；
3. 提交保留、修改、新增、删除、拆分的差异表；
4. 提交回归用例和失败处理；
5. 等待变更计划批准；
6. 生成非破坏性派生版本；
7. 提交完整评测证据。

### 提交本套件中央改进

1. 记录可复现失败症状；
2. 说明案例数量、风险和上下文成本；
3. 使用 `improvement-proposal`；
4. 设计旧版失败、候选版通过的回归；
5. 取得指定维护者对准确提案和目标版本的批准；
6. 完成实现、评测和发布检查；
7. 保留上一中央版本用于回滚。

分享仓库或 ZIP 前，请移除本地测试输出、业务数据、账号标识、密钥和机器特定路径。

## 版本状态

当前发布候选版本：`1.0.0`（2026-07-16）。

- 运行时 Skill：5 个；
- 结构验证：通过；
- 前向测试：通过；
- 集成测试：通过；
- 来源覆盖：禁止；
- 中央改进默认：只提交提案；
- 个人分支：明确选择后才创建。

版本信息以 [`governance/release/manifest.md`](governance/release/manifest.md) 为准。发布或团队分发前，请同时阅读 [`INSTALL.md`](INSTALL.md) 和治理参考文件。
