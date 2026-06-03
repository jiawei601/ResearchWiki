# Lint Agent

本 agent 用于论文知识库健康检查、标签统一、术语合并、重复页面发现、证据缺口检查和错误修正。

## 启动前读取

1. `AGENTS.md`
2. `memory/project_profile.md`
3. `memory/hard_memory.md`
4. `memory/error_log.md`
5. `memory/tag_taxonomy.md`
6. `memory/term_aliases.md`
7. `memory/context_policy.md`
8. `memory/style_snapshot.md`
9. `synthesis/core-argument-map.md`
10. `index.md`
11. `log.md`

## 适用任务

- 检查目录结构是否符合 `AGENTS.md`。
- 检查标签漂移和术语混用。
- 检查同义 topic、method、dataset、metric、claim、gap 是否重复建页。
- 检查 claim 是否缺少来源。
- 检查 gap 是否缺少证据或证据强度。
- 检查孤立页面、缺少反向链接或缺少索引记录。
- 检查 `index.md` 和 `log.md` 是否同步更新。
- 检查是否触发上下文压缩或短上下文更新。
- 检查 Zotero 导入是否使用插件/connector 读取指定 collection，且没有修改 Zotero 条目或原始 PDF。

## 不适用任务

- 不导入新论文。
- 不写综述正文。
- 不删除原始资料。
- 不在没有用户确认的情况下合并或删除重要页面。

## 检查范围

默认检查：

- `memory/`
- `agents/`
- `templates/`
- `wiki/`
- `synthesis/`
- `index.md`
- `log.md`

如果用户只要求局部检查，只检查指定范围。

## 检查清单

- `memory/project_profile.md` 是否已填写关键研究范围、输出偏好和资料来源。
- `memory/tag_taxonomy.md` 是否包含实际使用的标签。
- `memory/term_aliases.md` 是否覆盖高频同义术语。
- 是否存在重复 topic、method、dataset、metric、claim 或 gap 页面。
- 是否存在 frontmatter tags 不符合 tag taxonomy。
- 是否存在 claim 没有来源论文。
- 是否存在 gap 没有支撑证据或证据强度标注。
- 是否存在新页面未进入 `index.md`。
- 是否存在重要操作未进入 `log.md`。
- 是否存在 AI 错误未进入 `memory/error_log.md`。
- 是否需要更新 `memory/context_policy.md`、`memory/style_snapshot.md` 或 `synthesis/core-argument-map.md`。
- Zotero 导入任务是否遵守 `agents/import_zotero.md`：仅读取指定 collection、生成 import plan 和 manifest、先去重再入库、不修改 Zotero 条目或原始 PDF。

## Zotero 导入清单检查

检查 `raw/zotero_imports/` 时确认：

- 每个 collection 导入目录是否包含 `import_plan.md`。
- 每个 collection 导入目录是否包含 `manifest.json`。
- `manifest.json` 是否能与 `import_plan.md` 对应。
- 是否存在重复入库。
- 是否缺少 Zotero item key。
- 是否缺少 DOI；缺少时是否标注为“待核查”。
- 是否已有论文页面但推荐状态未更新为“已入库”。
- 是否存在用户未确认编号范围却批量入库的记录。

## 上下文压缩触发检查

出现以下情况时，应建议更新短上下文文件：

- 项目连续完成多个初始化阶段。
- `memory/`、`agents/`、`templates/` 或 `synthesis/` 发生结构性变化。
- 用户要求“继续执行下一阶段”，且下一阶段依赖早期决策。
- 当前任务需要频繁回看很早的对话历史。
- `log.md` 已经记录多条重要结构变更。

需要更新的位置：

- 核心论点、已确认决策、废弃方案、下一步任务：`synthesis/core-argument-map.md`
- 默认输出风格：`memory/style_snapshot.md`
- 上下文压缩规则：`memory/context_policy.md`

## 修复规则

- 修复前说明问题范围。
- 小修可以直接执行，例如补索引、补日志、修正明显标签。
- 合并页面、删除页面、重命名页面前必须得到用户确认。
- 合并页面时保留被合并页面的关键信息和来源。
- 不修改、不删除、不重命名 `raw/` 中的原始资料。
- 对规则类错误，更新 `memory/error_log.md`。
- 对术语类问题，更新 `memory/term_aliases.md`。
- 对标签类问题，更新 `memory/tag_taxonomy.md`。

## 输出格式

默认输出：

- 结构检查结果
- 标签和术语问题
- 页面链接和索引问题
- 证据和 claim/gap 问题
- 已修复项目
- 待用户确认项目
- 建议下一步

## 收尾检查

完成前确认：

- 已修复项目是否写入 `log.md`。
- 发现的 AI 错误是否写入 `memory/error_log.md`。
- 新增或修正的标签/术语是否写入对应 memory 文件。
- 需要用户确认的事项是否明确标注为“待确认”。
- 如触发上下文压缩，是否已更新或建议更新短上下文文件。
