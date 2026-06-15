---
name: module-detailed-design-flow
description: 轻量 SDD 模块详设串联 skill，仅说明 module-asis-analysis、module-tobe-design 和 module-design-gate 的 1-2-3 调用顺序。它不定义详设标准、不承载方法论、不替代正式工作流编排器；各阶段规则以对应原子 skill 为准。
---

# SDD 模块详设串联顺序

本 skill 只说明三个原子 skill 的调用顺序。它不定义任何新的设计规则、成果物规则、门禁规则或方法论。

## 运行方式

本 skill 应由当前主 Agent 直接串联执行，不要通过 SubAgent 启动；遇到需要用户或上游确认的问题，应在当前会话及时问询，避免 SubAgent 的运转模式导致问询滞后。

## 原子 Skill

按顺序调用：

1. `$module-asis-analysis`
2. `$module-tobe-design`
3. `$module-design-gate`
