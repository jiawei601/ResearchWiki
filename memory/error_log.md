---
type: memory
status: template
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Error Log

本页记录 AI 在维护论文知识库时犯过的错误，以及以后必须遵守的修正规则。没有实际错误时，只保留记录模板。

## Record Format

```markdown
## [YYYY-MM-DD] Error Title

- Error:
- Cause:
- Correction rule:
- Impact:
- Fixed: yes / no / pending
```

## Example

> Example only. Replace this section after real use.

## [YYYY-MM-DD] Example: Tag Drift

- Error: 同一概念被写成多个标签。
- Cause: 新建页面前没有检查 `memory/tag_taxonomy.md`。
- Correction rule: 新增标签前必须先查标签体系和已有页面。
- Impact: topic、method、claim 或 gap 可能分散。
- Fixed: pending
