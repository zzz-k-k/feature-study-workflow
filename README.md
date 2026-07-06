# Feature Study Workflow / 大功能学习闭环 Skill

## English

Feature Study Workflow is a portable AI agent skill for large feature changes. It turns feature development into a document-driven learning loop: clarify requirements, write user-flow and architecture docs, implement step by step, track bugs and repair paths, analyze design drift, run a user-filled retrospective, and capture reusable patterns.

Use this skill when a feature is large enough that direct coding would hide important decisions, architecture assumptions, bugs, requirement changes, or learning opportunities.

### What It Does

- Creates and maintains feature progress documentation.
- Produces requirements clarification docs.
- Produces user-flow and acceptance-criteria docs.
- Produces architecture and implementation design docs.
- Guides stepwise implementation.
- Tracks bugs and repair paths in a dedicated document.
- Updates requirement and architecture docs when reality changes during coding.
- Generates a final implementation summary and design-drift analysis.
- Asks the user to fill a learning retrospective, then critiques it.
- Captures reusable implementation patterns, snippets, checklists, and future prompts.

### Skill Files

Minimum portable version:

```text
feature-study-workflow/
  SKILL.md
```

Codex-friendly version:

```text
feature-study-workflow/
  SKILL.md
  agents/
    openai.yaml
```

`SKILL.md` contains the actual workflow. `agents/openai.yaml` is optional Codex UI metadata.

### Usage

In an AI tool that supports agent skills, install or copy this folder into the tool's skills directory, then invoke:

```text
Use $feature-study-workflow to guide this large feature change.
```

You can also ask:

```text
当前进度
到哪一步了
status
```

The skill will inspect the active `progress.md` file and report the current phase, completed artifacts, blockers, and next recommended action.

### Generated Artifacts

For each feature, the skill prefers this structure:

```text
docs/feature-study/<feature-slug>/
  progress.md
  requirements-clarification.md
  requirements-user-flow.md
  architecture-implementation.md
  bug-repair-log.md
  implementation-summary.md
  learning-retrospective.md
  reusable-patterns.md
```

If a project already has a documentation convention, the skill should follow the existing convention while preserving the same artifact roles.

### License

MIT License.

---

## 中文

Feature Study Workflow 是一个可移植的 AI Agent Skill，用于较大的功能开发。它把功能开发变成一个“文档驱动的学习闭环”：先澄清需求，再产出用户流程文档和架构实现文档，然后分步编码，过程中记录 Bug 与修复路径，完成后分析设计偏差，让用户填写学习复盘，最后沉淀可复用模式。

当一个功能比较大，直接让 AI 写代码会隐藏很多关键决策、架构假设、Bug、需求变化和学习机会时，适合使用这个 skill。

### 它能做什么

- 创建并维护功能进度文档。
- 输出需求澄清文档。
- 输出用户流程和验收标准文档。
- 输出架构与实现设计文档。
- 引导分步编码。
- 用单独文档记录 Bug 与修复路径。
- 编码过程中如果需求或架构发生变化，会要求回写到对应文档。
- 完成后输出修改总结和设计偏差分析。
- 要求用户填写学习复盘，然后由 AI 点评。
- 沉淀可复用实现模式、代码片段、检查清单和未来提示词。

### Skill 文件

最小可移植版本：

```text
feature-study-workflow/
  SKILL.md
```

Codex 友好版本：

```text
feature-study-workflow/
  SKILL.md
  agents/
    openai.yaml
```

`SKILL.md` 是真正的工作流主体。`agents/openai.yaml` 是可选的 Codex UI 元数据。

### 使用方式

在支持 Agent Skills 的 AI 工具中，把整个文件夹复制到对应的 skills 目录，然后调用：

```text
Use $feature-study-workflow to guide this large feature change.
```

也可以直接询问进度：

```text
当前进度
到哪一步了
status
```

skill 会读取当前功能的 `progress.md`，并汇报当前阶段、已完成产物、阻塞点和下一步建议。

### 生成的文档结构

每个功能默认使用下面的文档结构：

```text
docs/feature-study/<feature-slug>/
  progress.md
  requirements-clarification.md
  requirements-user-flow.md
  architecture-implementation.md
  bug-repair-log.md
  implementation-summary.md
  learning-retrospective.md
  reusable-patterns.md
```

如果项目已经有自己的文档规范，应优先遵循项目现有规范，但保留这些文档的职责。

### 许可证

MIT License。
