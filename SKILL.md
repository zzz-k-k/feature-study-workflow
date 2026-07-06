---
name: feature-study-workflow
description: Use for large feature changes where the user wants a document-driven coding workflow with learning capture: requirements clarification, user-flow docs, architecture and implementation design, stepwise coding, bug and repair-path tracking, progress/status queries, final design-drift analysis, user-filled retrospective, AI critique, and reusable pattern capture. Trigger when the user asks to develop a larger feature systematically, summarize architecture for a feature, maintain implementation learning docs, query current feature progress, or run a learning/retrospective workflow around a code change.
---

# Feature Study Workflow

Use this skill to guide a large feature change as a learning-centered, document-driven workflow. Do not use it for tiny fixes unless the user explicitly asks.

## Operating Rules

- Do not jump straight into coding.
- Proceed by phases. Stop after each major document and wait for the user to confirm or say "下一步".
- Maintain written artifacts in the project, preferably under `docs/feature-study/<feature-slug>/`.
- If the project has an existing docs convention, follow it instead and keep the same artifact names.
- Keep all generated docs in Chinese unless the user asks otherwise.
- During implementation, update docs when reality changes:
  - Bugs and repair paths go to `bug-repair-log.md`.
  - Requirement changes go to `requirements-user-flow.md`.
  - Architecture or implementation design changes go to `architecture-implementation.md`.
- When the user asks "当前进度", "进度", "status", "到哪一步了", or similar, run the Progress Query behavior.

## Artifact Set

For each feature, maintain these files:

- `progress.md`: current phase, completed docs, open questions, blockers, next action.
- `requirements-clarification.md`: goal, restated requirement, boundaries, open questions, assumptions, risks.
- `requirements-user-flow.md`: user flow, main scenarios, edge cases, acceptance criteria, requirement change log.
- `architecture-implementation.md`: code entry points, architecture understanding, call chain, module responsibilities, data flow, task split, change log.
- `bug-repair-log.md`: bug symptoms, reproduction, cause, fix path, validation, and design-doc lesson.
- `implementation-summary.md`: final implementation and design-drift analysis after coding is complete.
- `learning-retrospective.md`: user-filled learning review plus AI critique.
- `reusable-patterns.md`: reusable patterns, snippets, checklists, and future prompts.

Create the folder and `progress.md` at the start of the workflow. If the user is only asking for progress, do not create new docs; inspect existing docs first.

## Progress Model

Use these phases:

1. `requirements-clarification`
2. `requirements-user-flow`
3. `architecture-implementation-design`
4. `stepwise-implementation`
5. `implementation-summary-and-drift-analysis`
6. `learning-retrospective-and-critique`
7. `reusable-pattern-capture`
8. `complete`

`progress.md` must include:

```markdown
# Feature Study Progress

- Feature:
- Current phase:
- Status: not-started | in-progress | waiting-for-user | blocked | complete
- Last completed phase:
- Current artifact:
- Completed artifacts:
- Open questions:
- Blockers:
- Next action:
- Last updated:
```

Update `progress.md` whenever a phase starts, pauses for confirmation, completes, or becomes blocked.

## Progress Query

When the user asks for current progress:

1. Locate the active feature-study folder. Prefer the most recently modified `docs/feature-study/*/progress.md`. If there are multiple plausible active folders, list them and ask which one.
2. Read `progress.md` and briefly inspect the current artifact if needed.
3. Respond with:
   - Current phase
   - Completed artifacts
   - Waiting on user or not
   - Open questions/blockers
   - Next recommended action
4. Do not continue the workflow unless the user explicitly asks to continue.

If no progress file exists, say that no active feature-study workflow was found and offer to start one.

## Workflow

### Phase 1: Requirements Clarification

Start here for a new large feature. Create `requirements-clarification.md` with:

```markdown
# 需求澄清文档

## 功能目标

## 当前需求复述

## 需求边界

## 不明确的问题

## 暂定假设

## 风险点
```

Ask at most 5 key questions. If reasonable assumptions can unblock progress, list them clearly. Update `progress.md` to `waiting-for-user` and stop.

### Phase 2: Requirements And User Flow

After confirmation, create `requirements-user-flow.md`:

```markdown
# 需求与用户流程文档

## 用户视角流程
按“入口 -> 操作 -> 系统反馈 -> 最终结果”描述。

## 主要场景

## 边界场景
包括异常、空状态、权限不足、数据缺失、网络失败等。

## 需求验收标准
写成可检查条目。

## 后续需求变化记录
### 变化 1
- 变化内容：
- 变化原因：
- 影响范围：
- 是否已同步到实现：
```

Update `progress.md` and stop for confirmation.

### Phase 3: Architecture And Implementation Design

Combine architecture reverse-engineering and implementation design in `architecture-implementation.md`:

```markdown
# 架构与实现设计文档

## 相关代码入口

## 当前架构理解

## 调用链路
用户操作 -> 前端组件 -> 状态/请求 -> 后端/API -> 数据层 -> 返回结果 -> UI 更新

## 核心模块职责

## 数据流

## 实现任务拆分

## 每个任务的修改点

## 方案选择
包括简单方案、更可维护方案、推荐方案和取舍。

## 设计风险

## 架构变化记录
### 变化 1
- 原设计：
- 实际发现：
- 调整原因：
- 影响文件：
- 是否已同步到实现：
```

Update `progress.md` and stop for confirmation.

### Phase 4: Stepwise Implementation

Implement one task at a time. Before each task, state:

- What will change
- Why it changes
- Which part of `architecture-implementation.md` it corresponds to

After each task, state:

- Files changed
- Core logic
- Validation method
- Whether docs need updates

Maintain `bug-repair-log.md` when bugs appear:

```markdown
# Bug 与修复路径文档

## Bug 记录

### Bug 1：标题
- 现象：
- 触发步骤：
- 影响范围：
- 初步判断：
- 根本原因：
- 修复方案：
- 修改文件：
- 验证方式：
- 是否暴露了前期设计问题：
- 对应的设计文档位置：
- 后续避免方式：
```

If requirements change, update `requirements-user-flow.md`. If architecture changes, update `architecture-implementation.md`. Keep `progress.md` current.

When the user says coding is complete or says "下一步" after implementation, move to Phase 5.

### Phase 5: Implementation Summary And Design-Drift Analysis

Create `implementation-summary.md`:

```markdown
# 修改总结与设计偏差分析文档

## 最终实现了什么

## 实际修改文件

## 编码过程中遇到的问题
列出 bug、需求变化、架构变化。

## 问题原因分析
对每个问题回答：
- 这是 bug、需求变化，还是架构变化？
- 它最早暴露在哪个阶段？
- 它对应前面哪份文档中的哪一点设计不足？
- 是需求理解不完整、用户流程没想清楚、架构判断错误，还是实现细节遗漏？
- 如果重来一次，前面的文档应该如何改？

## 设计文档修正建议

## 经验教训
```

Update `progress.md` and stop before the retrospective.

### Phase 6: Learning Retrospective And AI Critique

Create `learning-retrospective.md` with a user-fillable section first:

```markdown
# 学习复盘填写文档

## 1. 我理解的功能目标

## 2. 我理解的用户流程

## 3. 我理解的架构链路
用户操作 -> 前端 -> API/状态 -> 数据层 -> UI 更新

## 4. 我理解的核心代码

## 5. 本次最重要的 bug 或变化

## 6. 如果下次做类似功能

## 7. 我还没理解的地方

---

# AI 点评
等待用户填写后再补充。
```

Ask the user to fill it. Do not fill it for them.

After the user fills it, critique:

- Which parts are accurate
- Which parts are vague
- Where the user remembers conclusions but not causes
- Three follow-up questions that test real understanding

Append the critique under `# AI 点评`, update `progress.md`, and stop before reusable capture.

### Phase 7: Reusable Pattern Capture

Create `reusable-patterns.md`:

```markdown
# 可复用沉淀记录

## 功能模式名称

## 适用场景

## 通用实现步骤

## 可复用代码块

## 易错点

## 设计前检查清单

## 下次可直接发给 AI 的提示词
```

Focus on reusable insight rather than a verbose transcript. Mark `progress.md` as complete.

