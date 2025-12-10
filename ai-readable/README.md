# AI-Readable 提示词目录

此目录包含针对 AI 优化的提示词版本。

## 目录结构

```
ai-readable/
├── CLAUDE/
│   ├── CLAUDE.md              ← AI优化版核心规则
│   ├── agents/
│   │   └── api-docs-extractor.md  ← 原本已是AI格式，直接复制
│   └── profiles/
│       └── USER_PROFILE.md    ← 用户档案，非指令，直接复制
├── 代码规则/
│   ├── 代码审查规则.md         ← AI优化版
│   └── 代码编写规则.md         ← AI优化版
└── 文档规则/
    ├── AI编程文档规范.md       ← AI优化版
    └── 代码对齐文档规则.md     ← AI优化版
```

## 人类版 vs AI版 对比

| 特征 | 人类友好版（根目录） | AI友好版（本目录） |
|------|---------------------|-------------------|
| 语言 | 中文为主 | 英文指令 + 中文术语 |
| 结构 | Markdown层级标题 | 条件逻辑、决策树 |
| 冗余 | 低，简洁 | 高，重复强调关键规则 |
| 强调 | 隐含 | 显式（MUST/NEVER/CRITICAL） |
| 格式 | 人类阅读舒适 | 机器解析友好 |

## 使用方式

- **人类维护**：编辑根目录的原始文档
- **AI执行**：将本目录的文档作为系统提示词

## 转换说明

| 人类写法 | AI写法 |
|---------|--------|
| 必须 | MUST / MANDATORY |
| 禁止 | NEVER / ❌ ABSOLUTE PROHIBITION |
| 建议 | SHOULD / Recommended |
| 如果...则... | If X → Do Y |
| 注意 | ⚠️ CRITICAL / WARNING |
