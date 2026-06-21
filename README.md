# SDD 工作流 Skills

SDD（Software Detailed Design）模块级详细设计工作流技能集，用于在 AICoding 前完成模块 ASIS 逆向分析、TOBE 目标设计、测试用例设计和设计门禁评审。每轮模块详设产出同名前缀成果物：

- 正式《{AR编号}-{需求短名}-{模块名}模块详细设计说明书.md》：最终设计交付物和后续 AICoding 拆分依据，只由 TOBE 阶段创建或编辑；面向用户、评审和开发，不承载检索、推导、反证、采样、追踪矩阵等过程性内容。
- `{同名前缀}.context.md`：过程文档，记录 ASIS 证据、检索过程、TOBE 推导、门禁采样和复检留痕。
- 独立《{AR编号}-{需求短名}-{模块名}模块测试用例设计.md》：由测试设计阶段创建或编辑，承接 TOBE 的可测试性输入，输出最小充分测试用例集、覆盖矩阵、断言和缺口。

本仓库也包含前置项目认知 skill：`module-deep-research`。它用于让 Agent 持续研究模块，沉淀 `.sdd/project-understanding/` 下的模块认知资产。

## 快速开始

Windows PowerShell 读取中文 skill 文件时建议显式使用 UTF-8，例如：

```powershell
$OutputEncoding = [Console]::OutputEncoding = [Text.UTF8Encoding]::new($false)
Get-Content -Raw -Encoding UTF8 .\module-asis-analysis\SKILL.md
```

正式使用时按阶段调用原子 skill：

```text
1. 使用 $module-asis-analysis 分析 {模块名} 与 {需求/AR} 相关的 ASIS。
2. 使用 $module-tobe-design 基于 ASIS context 生成或更新正式模块详细设计说明书。
3. 使用 $module-test-design 基于正式说明书生成独立模块测试用例设计。
4. 使用 $module-design-gate 检查正式说明书和测试设计是否可进入 AICoding。
```

也可以只调用某个阶段：

```text
使用 $module-asis-analysis 分析 {模块名} 与 {需求/AR} 相关的 ASIS，只更新同名前缀 .context.md 中的证据、结论、边界和检索过程。
```

```text
使用 $module-tobe-design 基于 .context.md 中的 ASIS 证据设计 TOBE，按正式大纲生成或更新模块详细设计说明书。
```

```text
使用 $module-test-design 基于正式模块详细设计说明书生成独立模块测试用例设计。
```

```text
使用 $module-design-gate 检查正式模块详细设计说明书和模块测试用例设计是否可进入 AICoding。
```

需要顺序串联时，可以使用 flow：

```text
使用 $module-detailed-design-flow 按 ASIS -> TOBE -> Test Design -> Gate 顺序串联四个原子 skill。各阶段规则以对应原子 skill 为准。
```

需要让 Agent 持续理解一个模块时，使用：

```text
使用 $module-deep-research 深入研究 {模块名}，只读代码、测试、文档和 git 历史，并将模块认知资产更新到 .sdd/project-understanding/modules/{模块名}/。
```

## Skill 概览

| Skill | 何时使用 | 主要输出 |
|-------|----------|----------|
| `module-deep-research` | 需要持续研究模块、沉淀可复用项目认知时 | `.sdd/project-understanding/modules/<module>/` 下的模块认知资产 |
| `module-detailed-design-flow` | 需要按 ASIS -> TOBE -> Test Design -> Gate 顺序串联原子 skill 时 | 原子 skill 的状态汇总 |
| `module-asis-analysis` | 需要用代码证据确认现状、边界、隐藏约束、风险和测试覆盖时 | `.context.md` 中的 ASIS 结论、证据索引和过程 |
| `module-tobe-design` | 已有 ASIS context，需要设计目标方案和可测试性输入时 | 按正式大纲生成/更新面向用户的正式说明书，并补充 TOBE 推导 context |
| `module-test-design` | 已有正式 TOBE 说明书，需要生成最小充分测试用例集、覆盖矩阵、断言和缺口时 | 独立《模块测试用例设计.md》 |
| `module-design-gate` | 需要判断正式说明书和测试设计是否能进入 AICoding，或门禁不通过后复检时 | `.context.md` 中的通过/不通过/阻塞结论、五链摘要、阻断问题和整改清单 |

## 目录结构

技能目录内的引用文件在规则文本中统一写成 `<skill-dir>/references/文件名`，避免安装到不同 Agent skills 目录后出现相对路径歧义。

```text
sdd-workflow-skills/
  README.md
  module-deep-research/
    SKILL.md                           # 前置模块认知深度研究
    agents/openai.yaml                 # Agent 接口配置
    references/asset-structure.md      # 模块认知资产结构
    references/research-loop.md        # 队列驱动的持续研究循环策略
  module-asis-analysis/
    SKILL.md                           # ASIS 阶段规则
    agents/openai.yaml                 # Agent 接口配置
    references/asis-output-template.md # ASIS context 模板
    references/evidence-checklist.md   # 证据挖掘清单
  module-tobe-design/
    SKILL.md                           # TOBE 阶段规则
    agents/openai.yaml                 # Agent 接口配置
    references/tobe-output-template.md # 正式说明书 TOBE 模板
    references/tobe-context-template.md # TOBE context 过程模板
  module-test-design/
    SKILL.md                           # 测试用例设计阶段规则
    agents/openai.yaml                 # Agent 接口配置
    references/test-design-template.md # 测试设计模板
  module-design-gate/
    SKILL.md                           # 门禁阶段规则
    agents/openai.yaml                 # Agent 接口配置
    references/gate-result-template.md # 门禁 context 模板
    references/gate-checklist.md       # 可选检查清单
  module-detailed-design-flow/
    SKILL.md                           # 串联顺序
    agents/openai.yaml                 # Agent 接口配置
    references/flow-summary.md         # 流程摘要
  docs/presentations/
    sdd-methodology-huawei-style/      # 演示材料
```

## 核心概念

- **前置项目认知系统**：长期沉淀在 `.sdd/project-understanding/` 下的模块理解资产，记录模块职责、核心运行路径、数据模型、不变量、风险、历史原因、变更规律、证据索引、研究队列和覆盖地图。
- **模块深度研究**：由 `$module-deep-research` 执行的长时间自主研究过程，用于提升 Agent 对既有模块的稳定理解。
- **正式说明书**：`{AR编号}-{需求短名}-{模块名}模块详细设计说明书.md`，最终设计交付和后续 AICoding 拆分依据；只呈现设计结论、现状约束摘要、接口契约、模块边界、实现方案、风险、可测试性输入和待确认事项。
- **context 文件**：`{AR编号}-{需求短名}-{模块名}模块详细设计说明书.context.md`，记录 ASIS 证据、TOBE 推导、门禁采样和复检。
- **测试设计**：`{AR编号}-{需求短名}-{模块名}模块测试用例设计.md`，独立承接 TOBE 可测试性输入，输出最小充分测试用例集、覆盖矩阵、断言、建议位置和缺口。
- **ASIS**：基于代码证据的现状分析，只确认事实、推断和不确定性，不提前设计 TOBE。
- **TOBE**：基于 ASIS context 和模块边界的目标设计，是正式说明书唯一写入阶段，必须落到工程位置、契约、流程、风险和可测试性输入；不生成测试用例，不拆分 AICoding 任务。
- **测试用例设计**：基于正式 TOBE 说明书生成独立测试设计，不替 TOBE 补设计，不拆分 AICoding 任务。
- **设计门禁**：判断正式说明书和测试设计是否能支撑进入 AICoding，并在 context 或当前会话输出整改或阻塞结论。
- **AICoding**：门禁通过后的自动化编码实施阶段。

## 使用方式

这些 skill 适用于支持 skill 接口格式的 AI 编码 Agent（如 Codex、Cursor 等）。将本仓库中的 skill 目录安装到 Agent 的 skills 目录后，即可通过 `$module-...` 名称调用。

推荐正式工作流直接按阶段调用 ASIS、TOBE、Test Design 和 Gate 原子 skill。`$module-detailed-design-flow` 只说明调用顺序，不承载任何阶段规则。`$module-deep-research` 可以在设计工作流之外独立运行，用于长期建设项目认知资产。

## 许可证

MIT
