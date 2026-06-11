---
name: sdd-module-detailed-design-flow
description: 测试用的轻量 SDD 模块详细设计编排 skill，用于在没有正式编排器时串联 sdd-module-asis-analysis、sdd-module-tobe-design 和 sdd-module-design-gate，围绕当前 SDD 工作流指定的目标成果物完成模块 ASIS、TOBE、门禁和必要返工复检。仅用于本地验证或临时串联，不替代正式 SDD 工作流编排。
---

# SDD 模块详设轻量流程

## 方法论

先阅读共享方法论：`C:\Users\15802\.codex\skills\sdd-module-design-method.md`。

本 skill 只是薄编排，用于串联 ASIS -> TOBE -> Gate，不定义新的详设标准。

## 目标

在没有正式编排器时，临时串联模块 ASIS、TOBE 和门禁三个原子 skill，验证它们能围绕当前 SDD 工作流指定的目标成果物协作。

正式 SDD 工作流存在时，优先服从正式编排器。本 skill 只做薄编排，不定义新的设计标准。

## 演练模式

当用户要求“练手”“验证 skill”“forward-test”“不改仓库”或没有正式上游 SDD 产物时，启用演练模式。

- 明确标记当前需求为 `样例需求` 或 `演练需求`。
- ASIS、TOBE、Gate 摘要区都必须标记 `运行模式=演练`；演练模式不得在后续流转中被改写为 `真实`。
- 允许输出纯叙述式验证结果，而不是强制落盘到仓库内成果物。
- 不修改目标代码仓，除非用户明确要求。
- 门禁结论需区分 `skill 有效性结论` 和 `真实 AICoding 准入结论`。
- 缺少正式需求、AR、`softWare.md` 或目标成果物路径时，不应直接判定 skill 失败；应记录为真实流程的文档元信息缺口。

## 使用的原子 skill

按顺序使用：

1. `$sdd-module-asis-analysis`
2. `$sdd-module-tobe-design`
3. `$sdd-module-design-gate`

## 输入

可以接受：

- 当前 SDD 工作流指定的目标成果物；未指定时默认为 `xxx模块详细设计说明书`。
- 代码仓路径。
- 目标模块。
- 需求、功能点、AR、模块影响性分析、模块间交互设计。
- 用户关注的接口、数据、配置、风险、测试或验收标准。

## 流程

### 1. 确认目标成果物

- 如果工作流指定了目标成果物，使用该成果物。
- 如果未指定，默认创建或更新 `xxx模块详细设计说明书`，但该名称只是占位名；同一轮流程中 ASIS、TOBE、Gate 必须引用同一个目标成果物。
- 如果是演练模式且用户要求不改仓库，可以在当前会话或外部输出目录产出验证报告。
- 保留已有成果物内容，只更新本轮涉及的 ASIS、TOBE 和门禁章节。

### 2. 执行 ASIS

使用 `$sdd-module-asis-analysis`：

- 根据 `softWare.md` 识别模块边界。
- 围绕本次需求相关切片分析 ASIS。
- 写入 ASIS 章节、需求/AR 与 ASIS 证据映射、证据索引、阻塞项或待确认问题。

如果 ASIS 阻塞且无法继续 TOBE，停止流程并输出阻塞原因。

### 3. 执行 TOBE

使用 `$sdd-module-tobe-design`：

- 基于 ASIS 证据和上游 SDD 产物设计 TOBE。
- 写入 TOBE 职责、组件设计、流程设计、接口/数据/配置、测试设计、风险回滚和 AICoding 任务拆分。

如果 TOBE 阻塞且无法进入门禁，停止流程并输出阻塞原因。

### 4. 执行门禁

使用 `$sdd-module-design-gate`：

- 检查目标成果物是否可进入 AICoding。
- 固定输出证据追踪链、ASIS 倾向采样、TOBE 严格探索、日志与可观测性专项、测试矩阵复核。
- 输出通过、不通过或阻塞结论。
- 不通过时生成整改清单和返工阶段。

### 5. 返工复检

如果门禁不通过：

- 返工阶段为 ASIS 时，回到 `$sdd-module-asis-analysis` 补证据或修正 ASIS。
- 返工阶段为 TOBE 时，回到 `$sdd-module-tobe-design` 修正设计。
- 返工阶段为上游设计对齐或模块间交互设计时，记录需要外部输入；如果当前上下文足够，先补齐目标成果物中的对齐说明。
- 返工后重新运行 `$sdd-module-design-gate`。

最多持续到门禁通过或出现无法自行解决的阻塞。不要用猜测消除阻塞项。

## 输出

最终输出应说明：

- 目标成果物。
- ASIS 状态。
- TOBE 状态。
- 门禁结论。
- ASIS 倾向采样是否发现问题。
- TOBE 严格探索是否发现问题。
- 日志与可观测性、测试矩阵是否通过复核。
- 是否可进入 AICoding。
- 若不可进入，列出阻断问题和下一步需要补充的输入。

## 引用文件

- 核心方法论：`C:\Users\15802\.codex\skills\sdd-module-design-method.md`
