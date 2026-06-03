# Quickstart

## 1. Clone And Open

Clone this repository and open the folder in Obsidian.

Before importing papers, read:

- `AGENTS.md`
- `memory/project_profile.md`
- `memory/hard_memory.md`

## 2. Fill Project Profile

Open `memory/project_profile.md` and fill:

- your research field;
- your research goal;
- included and excluded scope;
- Zotero settings, if you use Zotero;
- output language and citation preferences.

## 3. Set Tags And Aliases

Open `memory/tag_taxonomy.md` and add your domain tags.

Open `memory/term_aliases.md` and add common aliases so Codex does not create duplicate topic, method, claim, or gap pages.

## 4. Generate A Zotero Import Plan

Ask Codex:

```text
请按照 agents/import_zotero.md，读取 Zotero collection：<your collection name>。
只生成候选清单，不要入库。
```

Then review:

```text
raw/zotero_imports/<collection_name>/import_plan.md
raw/zotero_imports/<collection_name>/manifest.json
```

## 5. Ingest One Paper

After reviewing the import plan, ask Codex:

```text
请按照 agents/pdf_read_agent.md，入库 import_plan.md 中编号 1 的论文。
```

For a local PDF, ask:

```text
请按照 agents/pdf_read_agent.md，读取 raw/papers/<paper.pdf> 并完成单篇论文入库。
```

## 6. Run Lint

After importing papers, ask:

```text
请调用 agents/lint_agent.md，对当前知识库进行健康检查。
```

The lint agent should check:

- duplicate pages;
- tag drift;
- term aliases;
- missing evidence;
- index/log updates;
- context compression needs.

## 7. Build Synthesis

After several papers are imported, ask Codex to use:

- `agents/synthesis_agent.md` for literature maps;
- `agents/gap_agent.md` for research gaps;
- `agents/review_agent.md` for review outlines.

