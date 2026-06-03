---
type: memory
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Hard Memory

本页保存 ResearchWiki 长期稳定、默认不可违背的通用规则。具体研究领域、用户目标、Zotero 设置和写作偏好写入 `memory/project_profile.md`。

## Project Boundary

- 本项目默认只面向论文知识库。
- 原始资料以论文 PDF、论文导出的 Markdown、补充材料、图表附件和论文阅读笔记为主。
- 不主动扩展到商业资料、医学病历、个人日记、会议纪要或其他非论文知识库来源。
- 如果用户要求扩展边界，先记录为“待确认”，不要直接改写项目规则。

## Layering Rules

- `raw/` 保存原始资料。除非用户明确要求，不修改、不删除、不重命名原始文件。
- `wiki/` 保存结构化知识页面，例如 paper、author、topic、method、dataset、metric、claim、gap 和 review。
- `synthesis/` 保存跨论文综合成果，例如 literature map、open questions、research positioning 和 review outline。
- `memory/` 保存长期规则、项目配置、错误记录、标签体系和术语别名。
- `agents/` 保存任务型操作规程。
- `templates/` 保存输出格式模板。

## Evidence Rules

- 重要判断必须尽量回链到具体论文、章节、页码、图表、claim 或相关 wiki 页面。
- 不确定的信息必须标注为 `待确认`、`待核查`、`不确定` 或 `AI 推断`。
- 不允许把 AI 推断写成论文作者的原始结论。
- 不允许把综述性概括写成单篇论文结论，除非有明确证据。

## Maintenance Rules

- 每次重要操作后更新 `index.md` 和 `log.md`。
- 新增标签前先查 `memory/tag_taxonomy.md`。
- 新建 topic、method、dataset、metric、gap 或 claim 前先查 `memory/term_aliases.md` 和已有页面。
- 一旦发现错误，或用户指出错误，必须更新 `memory/error_log.md`。
- 不追求一次性完美，追求持续更新、持续纠错、持续形成研究地图。

## Output Rules

- 默认使用 `memory/project_profile.md` 中指定的语言、术语和引用偏好。
- 如果 project profile 尚未填写，默认用中文、学术简洁风格输出，并把缺失项标注为“待确认”。
- 页面应尽量使用 YAML frontmatter，方便 Obsidian Dataview 查询。
- 不要只做论文摘要；入库时应尽量更新相关 topic、method、dataset、metric、claim 和 gap。
