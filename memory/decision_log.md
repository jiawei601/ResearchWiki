---
type: memory
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Decision Log

本页记录 ResearchWiki 的重要结构和规则决策。

## Record Format

```markdown
## [YYYY-MM-DD] Decision Title

- Decision:
- Reason:
- Impact:
- Status:
```

## [2026-06-03] Open-Source Template Initialization

- Decision: 将当前项目初始化为可开源的空白论文知识库模板。
- Reason: 开源版本应保留框架、agent、template 和通用 memory，不应包含个人论文数据、Zotero 记录、真实论文分析或本机路径。
- Impact: 新用户 clone 后需要先填写 `memory/project_profile.md`，再导入自己的论文。
- Status: active
