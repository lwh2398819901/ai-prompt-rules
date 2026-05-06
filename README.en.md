# AI Assistant Rules Repository

This repository maintains AI assistant rules as a small, single-source rule set.

## File Structure

```text
.
├── agent.md
├── agent.en.md
├── LICENSE
├── README.md
└── README.en.md
```

## Core Files

- `agent.md`: The default Chinese rule source. It defines permission boundaries, task routing, workflows, verification requirements, special-purpose procedures, and skill usage rules.
- `agent.en.md`: English version of `agent.md`.
- `README.md`: Default Chinese repository overview.
- `README.en.md`: English repository overview.
- `LICENSE`: License.

## Usage

Use `agent.md` as the default rule source or system-prompt source.

Use `agent.en.md` when an English version is needed. The Chinese file remains the canonical default unless a project explicitly chooses the English version.

## Supported Tools

`agent.md` and `agent.en.md` are plain Markdown rule files. They can be used with any AI coding tool that supports custom rules, system prompts, project instructions, or agent instructions.

| Tool / Environment | How to Use | Notes |
| ------------------ | ---------- | ----- |
| Cursor | Use as project rules, user rules, or manually attached context | The rules include Cursor-specific tool constraints and skill guidance |
| Claude Code | Use as `CLAUDE.md`, user rules, or session context | If Superpowers is installed, it can work with automatic skill triggering |
| Codex CLI / Codex App | Use as agent instructions or project context | Skill-related rules depend on the available plugin / skill mechanism |
| Gemini CLI | Use as project rules or session context | Skill-related rules depend on the available skill activation mechanism |
| OpenCode / Copilot CLI / other agent tools | Use as a system prompt, project description, or rule file | Environments without skill support should follow the general rules and manual workflows |
| ChatGPT / Web chat | Use as a long prompt or project-rule context | When local tools are unavailable, only Q&A, planning, review, and manual-check workflows apply |

## Third-Party Skill Repositories

These rules refer to third-party skill repositories, but they are enhancements rather than hard dependencies.

| Skill Repository | Recommended Status | Purpose |
| ---------------- | ------------------ | ------- |
| `obra/superpowers` | Recommended | Provides the default engineering workflow skills, such as clarification, planning, TDD, debugging, verification, and code review |
| `mattpocock/skills` | Selective install | Only the selected skills are recommended: `grill-me`, `zoom-out`, `to-prd`, `to-issues`, `grill-with-docs` |
| Cursor official / local Cursor skills | Depends on the tool environment | Cursor-specific capabilities such as creating rules, Canvas, settings updates, and SDK guidance |

If the relevant skills are installed:

- Read the corresponding `SKILL.md` before executing a triggered skill workflow.
- Still obey the permission boundaries, project stage rules, stop conditions, and completion verification rules in the rule file.
- Do not enable all of `mattpocock/skills` by default; use only the selected skills listed in the rules.

If the relevant skills are not installed:

- The rule file still works independently.
- Do not pretend that a skill was read or invoked.
- Treat the skill name as workflow intent and manually perform an equivalent process using general capabilities.
- If a task requires skill-specific behavior, state that the skill is unavailable and offer two options: continue with the general workflow, or install the skill first.

## Maintenance Principles

- Maintain rule changes in `agent.md` first.
- Keep `agent.en.md` aligned when the English version is needed.
- Do not split the rules into multiple rule files, templates, or legacy prompt files.
- If a new tool template or specialized skill needs to be preserved, put it in a separate repository to keep this repository focused.
- README files must remain consistent with `agent.md`, `agent.en.md`, and `LICENSE`.

## License

See `LICENSE`.
