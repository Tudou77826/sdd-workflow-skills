# 轻量编排流程摘要

本 skill 仅用于测试或临时串联，不替代正式 SDD 工作流编排器。

## 顺序

1. ASIS：使用 `$sdd-module-asis-analysis`。
2. TOBE：使用 `$sdd-module-tobe-design`。
3. 门禁：使用 `$sdd-module-design-gate`。
4. 返工复检：按门禁整改清单回到 ASIS 或 TOBE。

## 终止条件

- 门禁通过，可以进入 AICoding。
- 出现无法自行解决的阻塞，需要用户、代码负责人或上游设计补充输入。

## 成果物

遵循当前 SDD 工作流指定的目标成果物；未指定时默认使用 `xxx模块详细设计说明书`。
