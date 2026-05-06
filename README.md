# AI 助手规则仓库

这是一个单文件维护的 AI 助手规则仓库。

## 目录结构

```text
.
├── agent.md
├── agent.en.md
├── LICENSE
├── README.md
└── README.en.md
```

## 核心文件

- `agent.md`：默认中文规则源，包含 AI 助手的权限边界、任务路由、执行流程、验证要求、专项流程和技能使用规则。
- `agent.en.md`：`agent.md` 的英文版，供需要英文规则上下文的工具或团队使用。
- `README.md`：默认中文仓库说明。
- `README.en.md`：英文仓库说明。
- `LICENSE`：许可证。

## 使用方式

将 `agent.md` 作为 AI 助手的规则源或系统提示词源使用。

如工具、团队或上下文需要英文规则，可改用 `agent.en.md`。除非项目明确选择英文版，否则默认以 `agent.md` 为主。

## 适用工具

`agent.md` 是纯 Markdown 规则文件，适用于任何支持自定义规则、系统提示词、项目说明或 agent instructions 的 AI 编程工具。

| 工具 / 环境 | 使用方式 | 说明 |
| ----------- | -------- | ---- |
| Cursor | 作为项目规则、用户规则或手动附加上下文使用 | 当前规则中包含 Cursor 专属工具约束和 Cursor 技能说明 |
| Claude Code | 作为 `CLAUDE.md`、用户规则或会话上下文使用 | 如安装 Superpowers，可配合其 skills 自动触发机制 |
| Codex CLI / Codex App | 作为 agent instructions 或项目上下文使用 | skills 相关规则按实际可用插件 / skill 机制执行 |
| Gemini CLI | 作为项目规则或会话上下文使用 | skills 相关规则按实际可用 skill 激活机制执行 |
| OpenCode / Copilot CLI / 其它 agent 工具 | 作为系统提示词、项目说明或规则文件使用 | 不支持 skill 的环境只执行通用规则和手动流程 |
| ChatGPT / Web 对话 | 作为长提示词或项目规则上下文使用 | 无法调用本地工具时，只执行问答、方案、审查和手动检查类规则 |

## 第三方技能仓库

本规则会引用第三方技能仓库，但它们是**增强项**，不是 `agent.md` 生效的硬依赖。

| 技能仓库 | 建议状态 | 用途 |
| -------- | -------- | ---- |
| `obra/superpowers` | 推荐安装 | 提供默认工程流程技能，如需求澄清、计划、TDD、调试、验证、代码审查 |
| `mattpocock/skills` | 选择性安装 | 只建议安装 `grill-me`、`zoom-out`、`to-prd`、`to-issues`、`grill-with-docs` |
| Cursor 官方 / Cursor 本地技能 | 按工具环境决定 | Cursor 专属能力，如创建规则、Canvas、设置修改、SDK 指南等 |

如果已安装对应技能：

- 任务触发时必须先读取对应 `SKILL.md`，再按技能流程执行。
- 仍然必须遵守 `agent.md` 中的权限边界、项目阶段、停止条件和完成前验证。
- `mattpocock/skills` 不建议全量启用，只使用规则中列出的精选技能。

如果未安装对应技能：

- `agent.md` 仍然可以独立使用。
- 不得假装已经调用或读取某个 skill。
- 将技能名视为流程意图，使用通用能力手动执行同等流程。
- 遇到需要 skill 特有能力的任务，应说明当前未安装，并给出两种选择：继续按通用流程执行，或先安装对应技能后再执行。

## 维护原则

- 新增、修改、删除规则时，只维护 `agent.md`。
- 当英文版需要保持同步时，再同步更新 `agent.en.md`。
- 不再拆分维护多个规则文件、模板文件或旧版提示词文件。
- 如果需要沉淀新的工具模板或专项 skill，优先放到独立仓库，避免污染唯一规则源。
- README 中的说明必须与 `agent.md` 和 `LICENSE` 保持一致。

## 许可

见 `LICENSE`。
