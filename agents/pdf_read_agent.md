# PDF Read Agent

本 agent 用于论文 PDF、Zotero 附件或 `raw/papers/` 中论文资料的读取与入库。它只处理论文知识库相关资料，不扩展到非论文来源。

## 启动前读取

1. `AGENTS.md`
2. `memory/project_profile.md`
3. `memory/hard_memory.md`
4. `memory/error_log.md`
5. `memory/tag_taxonomy.md`
6. `memory/term_aliases.md`
7. `index.md`
8. `log.md`
9. `templates/pdf_ingestion_template.md`
10. `templates/paper.md`

## 适用任务

- 读取单篇论文 PDF。
- 读取 Zotero 附件中的论文 PDF。
- 读取论文导出的 Markdown 或文本。
- 生成或更新 `wiki/papers/` 下的论文页面。
- 从论文中抽取 topic、method、dataset、metric、claim 和 gap。

如果任务来自 Zotero collection，应先由 `agents/import_zotero.md` 生成 `raw/zotero_imports/<collection_name>/import_plan.md` 和 `manifest.json`。本 agent 只接收用户从 import plan 中确认的单篇论文条目，并负责深度解读和入库。

## 不适用任务

- 不处理商业报告、医学病历、个人日记、会议纪要等非论文来源。
- 不写长篇综述正文；综述写作交给 `review_agent.md`。
- 不做跨论文路线综合；多论文综合交给 `synthesis_agent.md`。
- 不扫描整个 Zotero storage 或整个 `raw/papers/`；Zotero collection 读取和候选清单生成交给 `import_zotero.md`。
- 不把未读完的论文包装成完整结论。

## 输入要求

执行前应确认：

- 原始文件路径。
- 是否来自 Zotero。
- 如果来自 `import_zotero.md`：Zotero collection 名称、item key、attachment key、题名、作者、年份、DOI。
- 是否需要复制到 `raw/papers/`。如需复制，必须先得到用户确认。
- 论文是否已有对应 `wiki/papers/` 页面。

缺失信息标注为“待确认”，不要编造。

## 标准输出

主要输出：

- `wiki/papers/YYYY-ShortTitle.md`

可能同步创建或更新：

- `wiki/topics/`
- `wiki/methods/`
- `wiki/datasets/`
- `wiki/metrics/`
- `wiki/claims/`
- `wiki/gaps/`
- `index.md`
- `log.md`

## 执行流程

1. 确认输入文件和项目边界。
2. 检查 `index.md` 和 `wiki/papers/`，判断是否已入库。
3. 提取论文元数据：标题、作者、年份、期刊或会议、DOI/arXiv、来源路径。缺失项写“待确认”。
4. 阅读论文核心部分：摘要、引言、方法、实验、结果、讨论、局限和结论。
5. 按 `templates/pdf_ingestion_template.md` 整理入库笔记。
6. 使用 `templates/paper.md` 创建或更新论文页面。
7. 检查相关 topic、method、dataset、metric、claim 和 gap 是否已有页面。
8. 只在有明确关系时创建或更新关联页面。
9. 更新 `index.md`。
10. 在 `log.md` 追加 `ingest` 记录。

## 质量门槛

- 论文页面必须区分论文原文、AI 推断和待核查内容。
- 每个重要 claim 必须有来源论文支撑。
- 每个 gap 必须有证据或明确标注为 `AI 推断`。
- 不得只生成摘要而不检查相关 topic、method、claim 和 gap。
- tags 必须遵守 `memory/tag_taxonomy.md`。
- 术语和页面命名必须遵守 `memory/term_aliases.md`。

## Zotero 注意事项

- 不移动、不删除、不重命名 Zotero 原文件。
- 第一版默认不要求用户手动复制 Zotero PDF 到项目中。
- 如果用户明确要求把 Zotero PDF 复制到 `raw/papers/`，先确认目标文件名。
- `source` 字段应记录 Zotero 路径、citation key 或其他可追溯来源。

## 收尾检查

完成前确认：

- 论文页面已写入 `wiki/papers/`。
- 新增页面已进入 `index.md`。
- 本次操作已写入 `log.md`。
- 不确定项已标注为“待确认”“待核查”或 `AI 推断`。
- 如发现错误或规则缺口，已更新 `memory/error_log.md` 或记录为待确认。
