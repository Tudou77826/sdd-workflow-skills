# SDD Workflow Skills

SDD (Software Detailed Design) module-level detailed design workflow skills, supporting the complete ASIS analysis, TOBE design, and design gate review process.

## Skill Overview

| Skill | Description |
|-------|-------------|
| sdd-module-asis-analysis | Reverse analysis of code modules related to specific requirements, producing evidence-backed ASIS analysis |
| sdd-module-tobe-design | Design detailed TOBE schemes based on ASIS evidence and upstream SDD artifacts |
| sdd-module-design-gate | Quality gate check for module detailed design, determining if it's ready for AICoding |
| sdd-module-detailed-design-flow | Lightweight orchestration flow that chains ASIS, TOBE, and gate review |

## Workflow

```
1. ASIS Analysis (sdd-module-asis-analysis)
   -> Reverse-analyze current code, gather evidence, build ASIS chapter
2. TOBE Design (sdd-module-tobe-design)
   -> Design target state based on ASIS facts and upstream requirements
3. Design Gate (sdd-module-design-gate)
   -> Check design quality, produce pass/fail/block verdict
4. Rework Loop (if gate fails)
   -> Return to ASIS or TOBE stage, fix issues, re-run gate
```

## Directory Structure

```
sdd-workflow-skills/
  sdd-module-asis-analysis/
    SKILL.md                          # Main skill definition
    agents/openai.yaml                # Agent interface config
    references/asis-output-template.md  # ASIS output template
    references/evidence-checklist.md    # Evidence mining checklist
  sdd-module-design-gate/
    SKILL.md                          # Main skill definition
    agents/openai.yaml                # Agent interface config
    references/gate-checklist.md      # Gate review checklist
    references/gate-result-template.md  # Gate result template
  sdd-module-detailed-design-flow/
    SKILL.md                          # Main skill definition
    agents/openai.yaml                # Agent interface config
    references/flow-summary.md        # Flow summary
  sdd-module-tobe-design/
    SKILL.md                          # Main skill definition
    agents/openai.yaml                # Agent interface config
    references/aicoding-task-template.md  # AICoding task template
    references/tobe-output-template.md    # TOBE output template
```

## Key Concepts

- **ASIS**: Current state analysis with code evidence, focusing on requirement-related module areas
- **TOBE**: Target design based on ASIS facts, including component design, flow design, test design, and task breakdown
- **Design Gate**: Quality checkpoint ensuring design completeness, evidence traceability, and implementation readiness
- **AICoding**: Automated implementation stage after gate approval

## Usage

These skills are designed to work with AI coding agents (e.g., Codex, Cursor, or custom agents) that support the skill interface format. Install them to your agent's skills directory to use.

## License

MIT
