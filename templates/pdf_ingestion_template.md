---
type: template
template_for: pdf-ingestion
status: active
created: 2026-06-02
updated: 2026-06-02
tags:
  - ingestion
---

# PDF Ingestion Template

本模板用于单篇论文读取与入库前的结构化整理。最终论文页面应保存到 `wiki/papers/YYYY-ShortTitle.md`。

## 0. Processing Metadata

- Processing date: 待确认
- Agent: `agents/pdf_read_agent.md`
- Source type: PDF / Zotero PDF / Markdown export / 待确认
- Source file: 待确认
- Copied to `raw/papers/`: 是 / 否 / 待确认
- Related existing paper page: 待确认

## 1. Paper Metadata

- Title: 待确认
- Authors: 待确认
- Year: 待确认
- Venue: 待确认
- DOI / arXiv / URL: 待确认
- Zotero collection: 待确认
- Zotero item key: 待确认
- Zotero attachment key: 待确认
- PDF attachment name: 待确认
- Citation string: 待确认

## 2. Reading Coverage

- Abstract: 已读 / 未读 / 待确认
- Introduction: 已读 / 未读 / 待确认
- Method: 已读 / 未读 / 待确认
- Experiments / Results: 已读 / 未读 / 待确认
- Discussion / Limitations: 已读 / 未读 / 待确认
- Conclusion: 已读 / 未读 / 待确认

## 3. One-Sentence Takeaway

- 待确认

## 4. Abstract Rewritten

- 待确认

## 5. Research Problem

- Problem:
- Why it matters:
- Source section/page: 待确认

## 6. Method / Model / Framework

- Method name:
- Core idea:
- Key components:
- Assumptions:
- Source section/page: 待确认

## 7. Innovations

- Innovation:
  - Evidence:
  - Compared with:
  - Source section/page: 待确认

## 8. Experiments

- Datasets / objects / materials:
- Metrics:
- Baselines:
- Main results:
- Ablation / sensitivity analysis:
- Source tables/figures/pages: 待确认

## 9. Key Claims

每个重要 claim 应能回链到论文证据；重要 claim 可创建到 `wiki/claims/`。

- Claim:
  - Evidence:
  - Evidence strength: strong / weak / AI 推断 / 待确认
  - Limitation:
  - Source section/page: 待确认

## 10. Limitations

- Limitation:
  - Stated by authors: 是 / 否 / 待确认
  - Evidence:
  - Source section/page: 待确认

## 11. Potential Gaps

每个 gap 应链接或创建到 `wiki/gaps/`；无直接证据时标注 `AI 推断`。

- Gap:
  - Evidence:
  - Evidence strength: strong / weak / AI 推断 / 待确认
  - Why it matters:
  - Possible research question:

## 12. Links to Existing Wiki

- Topics:
- Methods:
- Datasets:
- Metrics:
- Claims:
- Gaps:
- Reviews:

## 13. Uncertainty and Follow-Up

- 待确认：
- 待核查：
- 需要用户判断：

## Maintenance Checklist

- [ ] Paper page created or updated in `wiki/papers/`.
- [ ] Related topic/method/dataset/metric/claim/gap pages checked.
- [ ] New important pages added to `index.md`.
- [ ] Operation appended to `log.md`.
- [ ] Uncertain content marked as `待确认`、`待核查` or `AI 推断`.
