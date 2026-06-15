# SDD 工作流 Skills

SDD（Software Detailed Design）模块级详细设计工作流技能集，用于在 AICoding 前完成模块 ASIS 逆向分析、TOBE 目标设计和设计门禁评审。每轮模块详设产出同名前缀双文件：

- 正式《{AR编号}-{需求短名}-{模块名}模块详细设计说明书.md》：最终交付物和唯一开发依据，只由 TOBE 阶段创建或编辑。
- `{同名前缀}.context.md`：过程文档，记录 ASIS 证据、检索过程、TOBE 推导、门禁采样和复检留痕。

## 快速开始

Windows PowerShell 读取中文 skill 文件时建议显式使用 UTF-8，例如：

```powershell
$OutputEncoding = [Console]::OutputEncoding = [Text.UTF8Encoding]::new($false)
Get-Content -Raw -Encoding UTF8 .\sdd-module-asis-analysis\SKILL.md
```

正式使用时按阶段调用原子 skill：

```text
1. 使用 $sdd-module-asis-analysis 分析 {模块名} 与 {需求/AR} 相关的 ASIS。
2. 使用 $sdd-module-tobe-design 基于 ASIS context 生成或更新正式模块详细设计说明书。
3. 使用 $sdd-module-design-gate 检查正式说明书是否可进入 AICoding。
```

也可以只调用某个阶段：

```text
使用 $sdd-module-asis-analysis 分析 {模块名} 与 {需求/AR} 相关的 ASIS，只更新同名前缀 .context.md 中的证据、结论、边界和检索过程。
```

```text
使用 $sdd-module-tobe-design 基于 .context.md 中的 ASIS 证据设计 TOBE，按正式大纲生成或更新模块详细设计说明书。
```

```text
使用 $sdd-module-design-gate 检查正式模块详细设计说明书是否可作为唯一开发依据进入 AICoding。
```

需要顺序串联时，可以使用 flow：

```text
使用 $sdd-module-detailed-design-flow 按 ASIS -> TOBE -> Gate 顺序串联三个原子 skill。各阶段规则以对应原子 skill 为准。
```

## Skill 概览

| Skill | 何时使用 | 主要输出 |
|-------|----------|----------|
| `sdd-module-detailed-design-flow` | 需要按 ASIS -> TOBE -> Gate 顺序串联三个原子 skill 时 | 三个原子 skill 的状态汇总 |
| `sdd-module-asis-analysis` | 需要用代码证据确认现状、边界、隐藏约束、风险和测试覆盖时 | `.context.md` 中的 ASIS 结论、证据索引和过程 |
| `sdd-module-tobe-design` | 已有 ASIS context，需要设计可直接指导 AICoding 的目标方案时 | 按正式大纲生成/更新说明书，并补充 TOBE 推导 context |
| `sdd-module-design-gate` | 需要判断正式说明书是否能进入 AICoding，或门禁不通过后复检时 | `.context.md` 中的通过/不通过/阻塞结论、四链摘要、阻断问题和整改清单 |

## 目录结构

技能目录内的引用文件在规则文本中统一写成 `<skill-dir>/references/文件名`，避免安装到不同 Agent skills 目录后出现相对路径歧义。

```text
sdd-workflow-skills/
  README.md
  sdd-module-asis-analysis/
    SKILL.md                           # ASIS 阶段规则
    agents/openai.yaml                 # Agent 接口配置
    <skill-dir>/references/asis-output-template.md # ASIS context 模板
    <skill-dir>/references/evidence-checklist.md   # 证据挖掘清单
  sdd-module-tobe-design/
    SKILL.md                           # TOBE 阶段规则
    agents/openai.yaml                 # Agent 接口配置
    <skill-dir>/references/tobe-output-template.md # 正式说明书 TOBE 模板
    <skill-dir>/references/aicoding-task-template.md
  sdd-module-design-gate/
    SKILL.md                           # 门禁阶段规则
    agents/openai.yaml                 # Agent 接口配置
    <skill-dir>/references/gate-result-template.md # 门禁 context 模板
    <skill-dir>/references/gate-checklist.md       # 可选检查清单
  sdd-module-detailed-design-flow/
    SKILL.md                           # 串联顺序
    agents/openai.yaml                 # Agent 接口配置
    <skill-dir>/references/flow-summary.md         # 流程摘要
  docs/presentations/
    sdd-methodology-huawei-style/      # 演示材料
```

## 核心概念

- **正式说明书**：`{AR编号}-{需求短名}-{模块名}模块详细设计说明书.md`，最终交付和唯一开发依据。
- **context 文件**：`{AR编号}-{需求短名}-{模块名}模块详细设计说明书.context.md`，记录 ASIS 证据、TOBE 推导、门禁采样和复检。
- **ASIS**：基于代码证据的现状分析，只确认事实、推断和不确定性，不提前设计 TOBE。
- **TOBE**：基于 ASIS context 和模块边界的目标设计，是正式说明书唯一写入阶段，必须落到工程位置、任务、验收标准和最小验证集。
- **设计门禁**：判断正式说明书是否能作为唯一开发依据进入 AICoding，并在 context 或当前会话输出整改或阻塞结论。
- **AICoding**：门禁通过后的自动化编码实施阶段。

## 使用方式

这些 skill 适用于支持 skill 接口格式的 AI 编码 Agent（如 Codex、Cursor 等）。将本仓库中的 skill 目录安装到 Agent 的 skills 目录后，即可通过 `$sdd-module-...` 名称调用。

推荐正式工作流直接按阶段调用 ASIS、TOBE 和 Gate 原子 skill。`$sdd-module-detailed-design-flow` 只说明调用顺序，不承载任何阶段规则。

## 许可证

MIT
