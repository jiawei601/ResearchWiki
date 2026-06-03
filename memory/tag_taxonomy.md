---
type: memory
status: template
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Tag Taxonomy

本页定义 ResearchWiki 的统一标签体系。新增标签前，先检查是否已有同义标签。领域专属标签应根据 `memory/project_profile.md` 逐步添加。

## Naming Rules

- frontmatter tags 默认使用英文小写短语，单词用连字符连接。
- 同一概念只保留一个主标签。
- 中文术语可以写在正文和标题中，但 tags 尽量统一。
- 不确定是否应新增标签时，先写到 `inbox.md` 的“待整理标签”，并标注为“待确认”。
- 领域标签一旦确定，应在本页登记，不要只散落在页面 frontmatter 中。

## General Tags

- `paper`
- `author`
- `topic`
- `method`
- `dataset`
- `metric`
- `claim`
- `gap`
- `review`
- `synthesis`
- `context`
- `style`
- `positioning`
- `open-question`
- `zotero`
- `zotero-import`
- `ingestion`
- `import-plan`
- `possible-duplicate`
- `needs-check`
- `needs-review`
- `needs-metadata`
- `ai-inference`

## Paper Processing Status Tags

- `unread`
- `reading`
- `processed`

## Domain Tags

在这里添加你的领域标签。

Example:

- `example-domain`
- `example-method`
- `example-dataset`

## Duplicate Tag Policy

| Not Recommended | Recommended | Note |
|---|---|---|
| `lit-review`, `survey` | `review` | 统一指综述类输出 |
| `research-gap`, `gap-analysis` | `gap` | 统一指研究空白 |
| `uncertain`, `to-check` | `needs-check` | 统一指需要进一步核对 |
