# Import Zotero Agent

本 agent 用于通过 Codex Zotero 插件 / connector 读取用户指定的 Zotero collection 或文件夹，生成候选入库清单，并在用户确认后把单篇论文交给 `agents/pdf_read_agent.md` 入库。

本 agent 不直接深度解读论文，不批量写 paper 页面，不读取 Zotero 本地数据库文件，也不要求用户手动复制 PDF 到项目中。

## 启动前读取

1. `AGENTS.md`
2. `memory/project_profile.md`
3. `memory/hard_memory.md`
4. `memory/context_policy.md`
5. `memory/error_log.md`
6. `memory/tag_taxonomy.md`
7. `memory/term_aliases.md`
8. `index.md`
9. `log.md`
10. `agents/pdf_read_agent.md`

## 适用任务

- 用户给出 Zotero collection / 文件夹名称，要求识别其中论文。
- 使用 Codex Zotero 插件 / connector 读取指定 collection 中的条目。
- 读取论文元数据：题名、作者、年份、DOI、Zotero item key、附件 key。
- 检查条目是否已存在于 `wiki/papers/` 或 `index.md`。
- 生成候选入库清单和机器可读 manifest。
- 等待用户确认编号后，将单篇论文交给 `pdf_read_agent.md` 入库。

## 不适用任务

- 不读取 Zotero 本地数据库文件。
- 不新增 `scripts/zotero_collection_sync.py`。
- 不新增 `configs/zotero_sync_config.yaml`。
- 不要求用户手动复制 Zotero PDF 到项目中。
- 不扫描整个 Zotero storage。
- 不扫描整个 `raw/papers/`。
- 不修改、不删除、不重命名 Zotero 条目、附件或原始 PDF。
- 不深度解读论文内容。
- 不默认批量入库。

## 输入要求

执行前必须确认：

- Zotero collection / 文件夹名称：待确认
- 是否只生成候选清单：默认是
- 是否继续入库：默认否
- 若继续入库，用户必须明确指定编号或编号范围

示例用户输入：

```text
使用 import_zotero.md 读取 Zotero collection：Example Collection，先生成候选清单，不要入库。
```

```text
根据 raw/zotero_imports/Example Collection/import_plan.md，入库编号 1 和 3。
```

## Zotero 插件读取规则

- 默认通过 Codex Zotero 插件 / connector 读取用户指定 collection。
- 只读取该 collection 中的论文条目。
- 如果 collection 名称不唯一，必须让用户确认目标 collection。
- 只在准备入库具体论文时读取该条目的附件路径或全文。
- 不遍历整个 Zotero library。
- 不扫描整个 Zotero storage。
- 不修改 Zotero library。

## 候选条目字段

每个候选条目至少记录：

- 编号
- Zotero collection 名称
- Zotero item key
- Zotero attachment key，如果有
- 论文题名
- 作者
- 年份
- DOI
- 是否已有 `wiki/papers/` 页面
- 推荐状态：待入库 / 已入库 / 待核查
- 备注

## 去重检查

对每个 Zotero 条目，至少检查：

- `wiki/papers/` 中是否已有相同或近似标题页面。
- `index.md` 是否已有相同标题、DOI、Zotero item key 或 arXiv ID。
- `log.md` 是否记录过该论文入库。
- 若有 DOI，优先用 DOI 判断重复。
- 若无 DOI，使用标题、作者、年份和 Zotero item key 判断。

推荐状态：

- `待入库`：未发现重复，可由用户确认后入库。
- `已入库`：已存在对应 wiki/papers 页面，不重复处理。
- `待核查`：元数据缺失、疑似重复或匹配不确定。

## 输出位置

每次读取 Zotero collection 后，生成：

```text
raw/zotero_imports/<collection_name>/import_plan.md
raw/zotero_imports/<collection_name>/manifest.json
```

如果 collection 名称包含不适合文件名的字符，应使用安全文件夹名，并在文件中记录原始 collection 名称。

## import_plan.md 格式

```markdown
# Zotero Import Plan: <collection_name>

- Generated: YYYY-MM-DD
- Source: Zotero plugin / connector
- Collection: <collection_name>
- Status: draft

| 编号 | Zotero collection | Zotero item key | Attachment key | 论文题名 | 作者 | 年份 | DOI | 已有 wiki/papers | 推荐状态 | 备注 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 待确认 | 待确认 | 待确认 | 待确认 | 待确认 | 待确认 | 待确认 | 否 | 待入库 |  |
```

## manifest.json 结构

```json
{
  "collection_name": "待确认",
  "generated": "YYYY-MM-DD",
  "source": "zotero-plugin",
  "items": [
    {
      "number": 1,
      "collection_name": "待确认",
      "zotero_item_key": "待确认",
      "zotero_attachment_key": "待确认",
      "title": "待确认",
      "authors": ["待确认"],
      "year": "待确认",
      "doi": "待确认",
      "existing_wiki_page": null,
      "recommended_status": "待入库",
      "notes": ""
    }
  ]
}
```

## 执行流程

1. 确认用户指定的 Zotero collection / 文件夹名称。
2. 使用 Zotero 插件 / connector 读取该 collection。
3. 提取条目元数据和附件 key。
4. 检查 `wiki/papers/`、`index.md` 和 `log.md`，判断是否已入库。
5. 生成 `import_plan.md` 和 `manifest.json`。
6. 向用户汇报候选数量、已入库数量、待入库数量、待核查数量。
7. 等待用户选择编号或编号范围。
8. 对用户确认的单篇论文，交给 `pdf_read_agent.md` 读取附件并入库。

## 批量入库规则

- 默认禁止批量入库。
- 用户必须明确指定编号或编号范围，例如 `入库编号 1-3`。
- 对 `已入库` 条目不重复入库。
- 对 `待核查` 条目必须先确认，不自动入库。

## 收尾检查

完成前确认：

- 是否只读取了用户指定 collection。
- 是否没有扫描整个 Zotero storage。
- 是否没有扫描整个 `raw/papers/`。
- 是否没有修改、删除、重命名 Zotero 条目或 PDF。
- 是否生成了 `import_plan.md`。
- 是否生成了 `manifest.json`。
- 是否等待用户确认后才把论文交给 `pdf_read_agent.md`。
- 是否更新了 `log.md`。
