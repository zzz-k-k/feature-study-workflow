# Feature & Codebase Study Workflows

一个包含两个独立 Codex Skills 的学习型技能包：一个用于从需求开始构建新功能，另一个用于分析和理解已经存在的代码库。

## 两个调用入口

### `$feature-study-workflow`

用于新功能或较大功能改造。用户先提出需求、行为流程和整体施工路线，AI 负责评审；随后一次只实现一个可观察流程，并分别跟踪代码完成度、风险审计和用户理解程度。

```text
Use $feature-study-workflow to guide this feature from requirements to implementation.
```

### `$codebase-study-workflow`

用于既有、陌生、遗留或 AI 生成的代码。先建立系统地图，再按功能模块和真实运行流学习；AI 可以从最终代码推导教学重建顺序，但必须明确说明这不是实际 Git 历史。

```text
Use $codebase-study-workflow to map this repository and teach one runtime flow at a time.
```

它默认只读分析。每个学习步骤优先做到可运行；做不到时，必须至少可测试、可验证或可检查。大型项目只做浅层全局地图，然后逐模块深入，不要求完整重写。每个模块结束后可以选择继续讲解、做独立的简化类比练习，或在明确批准后对原项目做安全微改动。

## 如何选择

| 你的主要目标 | 使用 Skill |
|---|---|
| 从需求开始做一个新功能 | `$feature-study-workflow` |
| 看懂一个已经存在的项目或模块 | `$codebase-study-workflow` |
| 开发新功能前先看懂相关旧代码 | 先用代码库 Skill，再切换到功能 Skill |

## 包结构

```text
feature-study-workflow/
  .codex-plugin/
    plugin.json
  skills/
    feature-study-workflow/
      SKILL.md
      agents/openai.yaml
    codebase-study-workflow/
      SKILL.md
      agents/openai.yaml
      references/artifact-templates.md
  SKILL.md
  README.md
  LICENSE
```

根目录 `SKILL.md` 是兼容入口，让原来直接放在个人 skills 目录中的 `$feature-study-workflow` 继续可用。标准插件安装时，以 `skills/` 下的两个 Skill 为准。

## English

This plugin contains two independent learning workflows:

- `$feature-study-workflow` guides user-led construction of a new feature from requirements through one observable flow at a time.
- `$codebase-study-workflow` maps and teaches an existing codebase through verified functional modules and runtime flows. Its pedagogical reconstruction order is explicitly labeled as an inference, not historical fact.

The codebase workflow is read-only by default and scales to large repositories through a shallow global map followed by selective deep dives. Optional labs and source micro-changes require an explicit user choice.

## License

MIT
