# API 文档爬取任务提示词

## 使用方法

将下方「任务提示词」复制给 AI，**只需修改底部任务表格**（填平台缩写、平台全称、接口名称、URL），然后发送。

---

## 任务提示词（复制此块，修改任务表格后发送）

````
请先阅读规则文件：
@ai-prompt-word-rule-repository/human-readable/CLAUDE/agents/api-docs-extractor.md

然后按照该文件中的规范，使用 chrome-devtools-mcp 工具完成以下 API 文档爬取任务。

## 补充说明（优先级高于规则文件中的默认值）

- 输出目录：`docs/ocean_engine_api/{平台缩写}/`
- 文件命名：`{序号}-{平台缩写}平台-{接口名称}.md`，序号续接目录中已有文件的最大编号
- 参考已有文档风格：`docs/ocean_engine_api/QC/` 和 `docs/ocean_engine_api/AD/` 下的现有文件
- 提取时使用 `mcp0_take_snapshot` 快照的 StaticText 节点逐字段读取，**禁止使用 innerText 正则匹配**
- 请求示例代码块须去除行号、语言Tab、`xxxxxxxxxx` 等 UI 噪声，只保留纯净代码
- 响应参数嵌套字段用 `data.xxx[].yyy` 路径格式表示，不要拍平
- 每条处理完立即生成文件，再处理下一条


## 本次任务

| 平台缩写 | 平台全称 | URL |
|----------|----------|-----|
| QC | 巨量千川 | https://... |
| AD | 巨量营销 | https://... |
````

---

## 填写示例

```
| QC | 巨量千川 | https://open.oceanengine.com/labels/12/docs/1809915753481348?origin=left_nav |
| AD | 巨量营销 | https://open.oceanengine.com/labels/7/docs/1809915654787136?origin=left_nav |
```

---

## 常见注意事项

- **序号**：查看 `docs/ocean_engine_api/{平台缩写}/` 目录，取最大编号 +1
- **枚举值**：写在描述列，格式：`` `VALUE`（含义）、`VALUE2`（含义） ``
- **嵌套字段**：用 `data.list[].field` 路径格式，不要拍平
- **不同平台同名接口**：字段描述可能不同，须分别核实（如 `optimizer_id` 在 QC 是"负责人id"，在 AD 是"竞价权限负责人id"）
