# AI 助手规则仓库

这是一个以中文 `agent.md` 为唯一权威规则源、以中文 `skills/` 承载专项流程的 AI 助手规则仓库。

## 目录结构

```text
.
├── agent.md
├── LICENSE
├── README.md
└── skills/
    ├── aligning-docs-with-code/
    ├── analyzing-refactors/
    ├── reviewing-code/
    ├── simplifying-without-behavior-change/
    └── writing-ai-coding-docs/
```

## 核心文件

- `agent.md`：唯一权威规则源，包含 AI 助手的权限边界、任务路由、执行流程、验证要求和技能使用规则。
- `skills/`：项目内中文专项技能，承接代码审查、重构分析、行为保持简化、文档对齐和 AI 编程文档等长流程。
- `README.md`：默认中文仓库说明。
- `LICENSE`：许可证。

## 使用方式

将 `agent.md` 作为 AI 助手的规则源或系统提示词源使用。命中专项任务时，按 `agent.md` 第 4 章读取 `skills/` 下的对应 `SKILL.md`。

### 添加技能

`agent.md` 第 4 章会路由到三类技能来源：**本仓库 `skills/`**、**`obra/superpowers`**、**`mattpocock/skills` 精选子集**；在 Cursor 下还可能用到 **Cursor 官方 / 本地技能**。下面按来源说明典型安装方式（具体 CLI 选项以你本机 `npx skills` 版本的帮助为准）。

#### 1. 本仓库项目内技能（`skills/`）

```bash
npx skills@latest add lwh2398819901/ai-prompt-rules
```

主要安装本仓库 `skills/` 下的中文专项技能（与「项目内技能」表格一致）。

#### 2. `agent.md` 默认工程底座：`obra/superpowers`（推荐）

```bash
npx skills@latest add obra/superpowers
```

对应 `agent.md` 4.0 表中「Superpowers」所列流程技能（如 `using-superpowers`、`brainstorming`、`writing-plans`、`test-driven-development`、`systematic-debugging` 等）。未安装时规则仍可用，但需按通用流程手动执行等价步骤。

#### 3. `agent.md` 精选补充：`mattpocock/skills`（按需）

```bash
npx skills@latest add mattpocock/skills
```

安装器会让你选择要装到哪些 agent 上。**请只勾选**与 `agent.md` 4.4 一致的五个技能：`grill-me`、`zoom-out`、`to-prd`、`to-issues`、`grill-with-docs`，**不要默认全量安装**整仓。上游 README 会提到 `setup-matt-pocock-skills`：按本仓库规则，**除非你要配置 issue tracker / 标签词汇 / 文档布局并已与使用者确认**，否则不必运行该 setup（见 `agent.md` 4.4）。

#### 4. Cursor 官方 / Cursor 本地技能

在 Cursor 中通过 **Settings → Agents / Skills**（或当前版本等效入口）添加官方与市场技能；本机 `~/.cursor/skills-cursor/` 等路径下的本地技能由 Cursor 管理。`agent.md` 中列名的 `create-rule`、`canvas`、`sdk` 等即属此类，**是否安装由你的 Cursor 环境决定**，不是 Git 仓库 CLI 的必选步骤。

---

**共同说明**：`agent.md` 是完整规则源，请照旧载入为项目规则、用户规则或会话上下文；上述命令只解决「技能包」安装到 agent 的问题。任何环境若无法使用 `npx skills`，可将对应仓库 skills 目录**手动复制**到你所用工具的 skill 扫描路径，并核对 skill 名称与 `agent.md` 第 4 章一致。

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

## 生成其它语言版本

本仓库不长期维护英文或其它语言的规则副本。`agent.md` 和 `skills/` 中的中文内容是唯一权威源。

如果需要英文、日文或其它语言版本，建议将本仓库交给目标 AI 编程工具，让它基于当前中文源文件生成对应语言的 `agent` 规则和 skills，并安装到该工具的规则 / skill 目录中。

生成时应要求智能体：

- 保持权限边界、任务路由、停止条件和验证要求不变。
- 保持 skill 的触发条件、硬边界和执行流程等价。
- 不新增未确认规则。
- 不把中英文内容合并到同一个运行时文件中。
- 生成后检查章节编号、交叉引用和 skill 名称一致性。

## 项目内技能

本仓库维护以下项目内技能：

| 技能 | 触发场景 |
| ---- | -------- |
| `reviewing-code` | 代码审查、review、风险评估 |
| `analyzing-refactors` | 重构分析、结构整理、复杂度降低 |
| `simplifying-without-behavior-change` | 行为保持型优化、简化、清理 |
| `aligning-docs-with-code` | 文档对齐真实代码逻辑 |
| `writing-ai-coding-docs` | 面向 AI 编程代理的文档编写或重构 |

## 第三方技能仓库

本规则也会引用第三方技能仓库，但它们是**增强项**，不是 `agent.md` 和项目内 `skills/` 生效的硬依赖。

| 技能仓库 | 建议状态 | 用途 |
| -------- | -------- | ---- |
| `obra/superpowers` | 推荐安装 | 提供默认工程流程技能，如需求澄清、计划、TDD、调试、验证、代码审查 |
| `mattpocock/skills` | 选择性安装 | 只建议安装 `grill-me`、`zoom-out`、`to-prd`、`to-issues`、`grill-with-docs` |
| Cursor 官方 / Cursor 本地技能 | 按工具环境决定 | Cursor 专属能力，如创建规则、Canvas、设置修改、SDK 指南等 |

### 上游仓库与浏览索引

便于对照版本、阅读说明或确认技能清单时，可直接打开下列地址（与 `agent.md` 4.0 一致；**不等同于**「凡是相关都要装」）：

| 资源 | 说明 |
| ---- | ---- |
| [github.com/obra/superpowers](https://github.com/obra/superpowers) | Superpowers 源码、内置 `skills/` 目录与各 skill 的 `SKILL.md` |
| [github.com/mattpocock/skills](https://github.com/mattpocock/skills) | mattpocock 技能集源码；目录结构以该仓库为准 |
| [skills.sh](https://skills.sh/) | 第三方技能包索引与展示（可按仓库检索；安装命令仍以 `npx skills@latest add <owner>/<repo>` 等 CLI 说明为准） |
| 本仓库发布页 | 若你在 GitHub 上 fork 或镜像本规则仓库，项目内技能的发布名可能与 README 中 `npx skills add …` 一致；以你实际托管的 `owner/repo` 为准 |

### 其它已发布为 Agent Skill 包的仓库（自选）

许多团队或社区也会把流程写成符合 Agent Skills 约定的 GitHub 仓库。只要该仓库支持 `skills` 生态的常见安装方式，一般可尝试：

```bash
npx skills@latest add <owner>/<repo>
```

**与 `agent.md` 的关系**：`agent.md` 第 4 章**只固定路由**本仓库 `skills/`、`obra/superpowers`、`mattpocock/skills`（精选子集）及 Cursor 技能四类来源。其它仓库安装后 **不会自动进入 4.2 路由表**；使用前需自行判断其流程是否与 `agent.md` 的权限边界、阶段规则、停止条件和完成前验证冲突。若某第三方 skill 要在团队内长期作为「默认入口」，应在 `agent.md` 第 4 章补充登记来源与硬边界，而不是仅在 README 中口头推荐。

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

- 新增、修改、删除规则时，只维护中文 `agent.md`。
- 新增长流程、专项方法论或可复用检查清单时，优先维护为 `skills/<skill-name>/SKILL.md`，并在 `agent.md` 第 4 章登记路由和硬边界。
- 其它语言版本由使用方按需生成和安装，不在本仓库长期维护。
- 不再拆分维护多个规则文件、模板文件或旧版提示词文件。
- `agent.md` 保留入口路由、权限边界和硬约束；`skills/` 保存按需读取的长流程细则。
- README 中的说明必须与 `agent.md` 和 `LICENSE` 保持一致。

## 许可

见 `LICENSE`。
