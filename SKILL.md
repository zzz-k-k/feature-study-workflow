---
name: feature-study-workflow
description: Use for large feature development where the user wants to learn by proposing the requirements, user flow, and overall construction roadmap before AI review; then build one observable flow at a time, let AI audit real pain points after each completed flow, evolve architecture from evidence, track progress, analyze design drift, run a user-filled retrospective, and capture reusable patterns. Trigger for systematic feature construction, architecture learning, implementation progress queries, code-understanding workflows, and learning-centered retrospectives.
---

# Feature Study Workflow

Guide a large feature as a user-led construction and learning workflow. Let the user own the initial reasoning and construction order. Act as reviewer, coach, implementer, and post-flow auditor.

## Core Contract

- Ask the user to propose the overall construction roadmap before AI designs the implementation.
- Review the roadmap for requirement coverage, dependency order, observable outcomes, and stage size. Do not inject precise pain points, class names, design patterns, or a complete architecture at this stage.
- Build one observable user or system flow at a time. Do not organize implementation primarily by technical layers such as “all Models” or “all Repositories.”
- Let architecture evolve from working flows and real constraints. Treat future architecture as provisional.
- After each flow works, proactively inspect the actual behavior and code for pain points the user may not yet recognize. Present one pain point at a time and let the user propose the solution.
- Review user reasoning in this order: correctness, requirement completeness, simplicity, clarity and naming, then justified extensibility.
- Do not replace a workable user idea with a hidden preselected answer. State concrete consequences, ask one focused question, and escalate hints gradually.
- Introduce abstractions only when required by the current flow, an observed problem, or the next accepted roadmap step. Avoid speculative extensibility.
- Track implementation completion and user understanding separately.
- Record decisions and changed reasoning compactly; never store chat transcripts.
- Keep generated project documents in Chinese unless the user requests another language.

## Pause Rules

- Stop after each major document review and wait for user confirmation.
- Stop whenever the user must propose or revise requirements, a user flow, the roadmap, a construction plan, or a pain-point solution.
- After implementing and validating one flow, stop before starting another flow.
- During post-flow audit, present and resolve or defer exactly one pain point at a time, then stop.
- Never interpret a routine “下一步” as permission to skip unfinished review, audit, or understanding checks.

## Artifact Set

Maintain artifacts under `docs/feature-study/<feature-slug>/`, or follow an existing project docs convention:

- `progress.md`: current phase, active roadmap step, cycle state, blockers, and next action.
- `requirements-clarification.md`: user requirement, AI clarification review, confirmed scope, assumptions, and risks.
- `requirements-user-flow.md`: user-authored flows, AI review, edge cases, acceptance criteria, and changes.
- `architecture-implementation.md`: user roadmap, requirement coverage matrix, accepted construction order, current actual architecture, and evolution log.
- `construction-learning-log.md`: per-flow user plan, AI review, accepted plan, code mapping, validation, post-flow pain audits, and understanding check.
- `bug-repair-log.md`: reproduced bugs, cause, repair, validation, and design lesson.
- `implementation-summary.md`: final behavior, actual architecture, roadmap drift, and lessons.
- `learning-retrospective.md`: user-filled explanation followed by AI critique.
- `reusable-patterns.md`: reusable patterns, checks, snippets, and future prompts.

For an existing workflow that has `problem-solving-log.md`, preserve it. When resuming that workflow, migrate only meaningful reasoning and decisions into `construction-learning-log.md`; do not duplicate conversational history.

## Progress Model

Use these phases:

1. `requirements-clarification`
2. `requirements-user-flow`
3. `construction-roadmap-review`
4. `single-flow-construction`
5. `post-flow-pain-audit`
6. `roadmap-repeat-and-completion-check`
7. `implementation-summary-and-drift-analysis`
8. `learning-retrospective-and-critique`
9. `reusable-pattern-capture`
10. `complete`

Include these fields in `progress.md`:

```markdown
# Feature Study Progress

- Feature:
- Current phase:
- Status: not-started | in-progress | waiting-for-user | blocked | complete
- Current roadmap step:
- Current observable outcome:
- Current cycle stage: awaiting-user-plan | plan-under-review | approved-for-implementation | implementing | validating | post-flow-audit | pain-under-review | awaiting-understanding | mastered
- Implementation status: not-started | in-progress | complete
- Understanding status: not-started | in-progress | mastered
- Completed roadmap steps:
- Completed artifacts:
- Open questions:
- Blockers:
- Next action:
- Last updated:
```

Update progress whenever a phase or cycle stage starts, pauses, completes, or becomes blocked.

## Progress Query

When the user asks for progress or status:

1. Locate the most recently modified active `docs/feature-study/*/progress.md`.
2. Read it and the current artifact when needed.
3. Report the current phase, active roadmap step, completed steps, waiting party, open questions or blockers, and next action.
4. Do not continue implementation unless the user explicitly asks.

If multiple active workflows are plausible, list them and ask which one. If none exists, say so and offer to start one.

## Phase 1: Requirements Clarification

Create `progress.md` and `requirements-clarification.md`. Preserve the user’s own wording before normalization:

```markdown
# 需求澄清文档

## 用户原始需求

## AI 澄清评审
- 已明确部分：
- 歧义与缺口：
- 边界与风险：

## 用户补充与修正

## 最终确认需求

## 明确不做的内容

## 暂定假设
```

Ask at most five high-impact questions. Discuss goals and boundaries, not implementation architecture. Set progress to `waiting-for-user` and stop for confirmation.

## Phase 2: Requirements And User Flow

Ask the user to describe the main flow first using `入口 -> 操作 -> 系统反馈 -> 最终结果`. If the user already supplied it, preserve and review it.

Create `requirements-user-flow.md`:

```markdown
# 需求与用户流程文档

## 用户提出的流程

## AI 流程评审
- 已覆盖需求：
- 遗漏场景：
- 异常与边界：
- 需要用户修正：

## 用户修正后的流程

## 验收标准

## 后续需求变化记录
```

Review behavior, feedback, missing scenarios, permissions, empty states, data failure, and other relevant edges. Do not design code. Update progress and stop for confirmation.

## Phase 3: User Construction Roadmap And AI Coverage Review

Inspect the existing project only to understand its baseline and constraints. Then ask the user to propose an overall construction roadmap that covers the confirmed requirements.

Require the roadmap to describe high-level build order and an observable result for each step. Do not require exact files, class names, patterns, or precise pain points.

Review the user roadmap only for:

- Coverage: every acceptance criterion maps to at least one roadmap step.
- Dependency order: prerequisites appear before dependent behavior.
- Observability: each step ends in a runnable or inspectable result.
- Scope: each step is small enough to build and verify independently.
- Unknowns: unresolved choices are visible rather than silently assumed.

Do not generate a replacement roadmap unless the user explicitly asks or remains blocked after graduated hints. Create or update `architecture-implementation.md`:

```markdown
# 架构与实现演进文档

## 当前项目基础

## 用户提出的整体构建流程

## AI 需求覆盖评审

## 需求覆盖矩阵
| 需求/验收标准 | 对应构建步骤 | 覆盖状态 |
|---|---|---|

## 用户修正后的构建流程

## 已确认施工路线

## 当前实际架构
只记录已经存在并被验证的结构。

## 架构演进记录
```

Ask the user to revise or confirm. Set progress to `waiting-for-user` and stop. Do not start implementation in the same turn.

## Phase 4: Build One Observable Flow

Select exactly one accepted roadmap step. Ask the user to explain how they would build it from the current project state. Allow plain process language; do not require code terminology.

Create a flow card in `construction-learning-log.md`:

```markdown
## 构建流程 N：标题

- 对应需求：
- 当前可观察目标：
- 用户提出的构建步骤：
- AI 评审：等待用户方案
- 用户修正方案：
- 规范化后的职责与命名：
- 已确认实现方案：
- 代码对应关系：
- 验证结果：
- 理解状态：not-started
```

Review the user plan in order:

1. Identify correct and useful reasoning.
2. Identify missing steps or incorrect assumptions and state their concrete consequences.
3. Ask one focused question or give the smallest useful hint.
4. Let the user revise while progress is possible.
5. After correctness and coverage are sufficient, improve responsibility boundaries, naming, readability, and only evidence-backed extensibility. Explain every normalization so the user can connect it to their idea.

When the plan is accepted, record it, set the cycle stage to `approved-for-implementation`, and stop for explicit implementation confirmation.

### Implement The Accepted Flow

Before editing code, state:

- The observable result being implemented.
- The accepted user construction steps.
- The minimum files or responsibilities that must change and why.

Implement only this flow. Do not add structures solely for later roadmap steps. If the implementation unexpectedly spans several unrelated responsibilities, stop and re-split the flow with the user.

Validate the observable result and relevant regressions. Then record:

- Files changed and core behavior.
- A mapping from each accepted construction step to concrete code.
- Validation evidence.
- Any actual architecture change.

Update `architecture-implementation.md` with only the architecture that now exists. Set progress to Phase 5 and stop before proposing the next roadmap step.

## Phase 5: AI Post-Flow Pain Audit

After a flow works, proactively inspect its actual code, behavior, validation results, and the next accepted roadmap dependency. Look for pain points the user may not yet recognize.

Only propose a pain point when at least one condition holds:

- Current behavior can be incorrect, unsafe, inconsistent, or lose data.
- The pain is visible in the current code through duplication, mixed responsibilities, unclear state ownership, or fragile coupling.
- The pain blocks or materially complicates the next accepted roadmap step.
- A confirmed requirement or edge case is not actually satisfied.

Do not propose pain based only on hypothetical future reuse. Classify each candidate:

- `must-fix`: current correctness, safety, or requirement failure.
- `next-step-needed`: required before the next accepted roadmap step.
- `optional-later`: useful but not worth current complexity.

Present exactly one highest-priority pain point. Describe the triggering scenario and consequence without naming the intended pattern or giving the solution. Ask the user to propose a response and stop.

Record a pain card under the current flow:

```markdown
### 完成后痛点 N：标题

- 分类：must-fix | next-step-needed | optional-later
- 观察依据：
- 触发场景与后果：
- 用户初步方案：
- AI 评审：
- 用户修正方案：
- 最终决定：解决 | 延后
- 延后原因：
- 对应修改与验证：
```

Review the user solution with the same graduated-hint rules. If the pain is accepted for resolution, confirm the smallest fix, stop for implementation approval, implement it, and rerun the completed flow’s acceptance checks. If deferred, record why and do not add code.

Repeat Phase 5 one pain point per turn until no `must-fix` or `next-step-needed` pain remains. Optional items may stay deferred.

### Understanding Check

After the audit is complete, ask the user to explain:

- What observable flow was built.
- Their original construction reasoning and what changed.
- How the runtime call or data flow maps to the code.
- Why each new responsibility exists.
- How one small requirement change would affect the design.

Critique concisely. Mark understanding `mastered` only when the user connects requirement, construction flow, code, and change impact. Otherwise remain on the same flow and give one focused correction.

## Phase 6: Update Roadmap And Repeat

After a flow is implemented, audited, and mastered:

1. Update the requirement coverage matrix and actual architecture.
2. Record roadmap or architecture changes and why they occurred.
3. Check whether all acceptance criteria are satisfied.
4. If work remains, ask the user to select the next roadmap step and return to Phase 4.
5. If all work is complete, ask the user to confirm the implementation phase is complete before Phase 7.

Do not automatically select or implement the next flow.

## Bug And Change Tracking

When a bug appears, update `bug-repair-log.md` with symptom, reproduction, impact, cause, fix, validation, and the earlier decision that allowed it. Update requirements or architecture documents when reality changes.

## Phase 7: Implementation Summary And Design Drift

Create `implementation-summary.md`:

```markdown
# 实现总结与设计偏差分析

## 最终满足的需求

## 最终构建流程与实际架构

## 用户原始施工路线与实际路线对比

## 每次架构变化由什么真实问题触发

## 提前设计、遗漏与返工

## 如果重来，施工顺序如何调整

## 验证结果与剩余风险
```

Update progress and stop before retrospective.

## Phase 8: Learning Retrospective And AI Critique

Create `learning-retrospective.md` and ask the user to fill it before AI comments:

```markdown
# 学习复盘

## 1. 我理解的需求和用户流程

## 2. 我最初设计的整体构建流程

## 3. 实际构建顺序发生了哪些变化

## 4. 我能解释的核心调用与数据流

## 5. AI 提出的关键痛点及我的解决办法

## 6. 哪些抽象是必要的，哪些曾经过早

## 7. 下次我会怎样从零开始

## 8. 我仍不理解的地方

---

# AI 点评
等待用户填写后补充。
```

After the user fills it, identify accurate reasoning, vague claims, remembered conclusions without causes, and three questions that test transfer. Append the critique and stop.

## Phase 9: Reusable Pattern Capture

Create `reusable-patterns.md` with the reusable construction sequence, justified abstractions, pain signals, checks, concise code patterns, and a future prompt. Avoid transcript-like history. Mark progress `complete`.
