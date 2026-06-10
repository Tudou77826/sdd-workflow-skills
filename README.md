# SDD 工作流 Skills

SDD（Software Detailed Design）模块级详细设计工作流技能集，覆盖 ASIS 逆向分析、TOBE 目标设计和设计门禁评审的完整流程。

## Skill 概览

| Skill | 说明 |
|-------|------|
| sdd-module-asis-analysis | 对代码模块中与需求相关的部分进行 ASIS 逆向分析，产出有代码证据支撑的现状分析 |
| sdd-module-tobe-design | 基于 ASIS 证据和上游 SDD 产物，设计模块 TOBE 详细方案 |
| sdd-module-design-gate | 模块详细设计质量门禁，判断设计是否可进入 AICoding |
| sdd-module-detailed-design-flow | 轻量编排流程，串联 ASIS、TOBE 和门禁三个阶段 |

## 工作流程

```
1. ASIS 分析 (sdd-module-asis-analysis)
   -> 逆向分析当前代码，收集证据，构建 ASIS 章节
2. TOBE 设计 (sdd-module-tobe-design)
   -> 基于 ASIS 事实和上游需求，设计目标方案
3. 设计门禁 (sdd-module-design-gate)
   -> 检查设计质量，输出 通过/不通过/阻塞 结论
4. 返工复检（门禁不通过时）
   -> 回到 ASIS 或 TOBE 阶段补齐问题，重新门禁
```

## 目录结构

```
sdd-workflow-skills/
  sdd-module-asis-analysis/
    SKILL.md                            # 主 skill 定义
    agents/openai.yaml                  # Agent 接口配置
    references/asis-output-template.md  # ASIS 输出模板
    references/evidence-checklist.md    # 证据挖掘清单
  sdd-module-design-gate/
    SKILL.md                            # 主 skill 定义
    agents/openai.yaml                  # Agent 接口配置
    references/gate-checklist.md        # 门禁检查清单
    references/gate-result-template.md  # 门禁结果模板
  sdd-module-detailed-design-flow/
    SKILL.md                            # 主 skill 定义
    agents/openai.yaml                  # Agent 接口配置
    references/flow-summary.md          # 流程摘要
  sdd-module-tobe-design/
    SKILL.md                            # 主 skill 定义
    agents/openai.yaml                  # Agent 接口配置
    references/aicoding-task-template.md  # AICoding 实施任务模板
    references/tobe-output-template.md    # TOBE 输出模板
```

## 核心概念

- **ASIS**：基于代码证据的现状分析，聚焦需求相关的模块区域
- **TOBE**：基于 ASIS 事实的目标设计，包括组件设计、流程设计、测试设计和任务拆分
- **设计门禁**：质量关卡，确保设计完整性、证据可追溯性和工程可实现性
- **AICoding**：门禁通过后的自动化编码实施阶段

## 使用方式

这些 skill 适用于支持 skill 接口格式的 AI 编码 Agent（如 Codex、Cursor 等），将其安装到 Agent 的 skills 目录下即可使用。

## 许可证

MIT
