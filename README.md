# ResearchWiki

ResearchWiki is a Codex + Obsidian starter kit for building a personal or lab paper knowledge base.

It helps turn scattered papers into structured Markdown pages for reading, literature mapping, research gap analysis, positioning, and review writing.

## Who It Is For

- Researchers who read many papers and want reusable notes.
- Graduate students preparing literature reviews or thesis topics.
- Labs that want a maintainable Obsidian-based paper wiki.
- Users who want Codex/LLM agents to follow stable rules instead of producing one-off summaries.

## Core Idea

ResearchWiki separates the project into three layers:

- `raw/`: original materials such as PDFs, notes, images, and Zotero import plans.
- `wiki/`: structured knowledge pages such as papers, topics, methods, claims, gaps, datasets, metrics, and reviews.
- `agents/`, `templates/`, `memory/`: rules that tell Codex how to ingest, synthesize, check, and maintain the knowledge base.

## Directory Overview

```text
ResearchWiki/
├── AGENTS.md
├── README.md
├── QUICKSTART.md
├── index.md
├── log.md
├── inbox.md
├── agents/
├── templates/
├── memory/
├── raw/
├── wiki/
└── synthesis/
```

## First Setup

1. Open `memory/project_profile.md`.
2. Fill in your research field, goals, source settings, and output preferences.
3. Add initial tags to `memory/tag_taxonomy.md`.
4. Add common aliases to `memory/term_aliases.md`.
5. Import your first paper using `agents/pdf_read_agent.md`, or generate a Zotero import plan using `agents/import_zotero.md`.

## Zotero Workflow

Use `agents/import_zotero.md` when you want Codex to read a specific Zotero collection.

The import agent should:

- read only the user-specified collection;
- generate `raw/zotero_imports/<collection_name>/import_plan.md`;
- generate `raw/zotero_imports/<collection_name>/manifest.json`;
- check whether papers are already in `wiki/papers/`;
- wait for the user to choose which paper to ingest;
- hand a confirmed single paper to `agents/pdf_read_agent.md`.

It should not scan your full Zotero storage, modify Zotero items, or move original PDFs.

## Ingesting the First Paper

Ask Codex to read one paper and follow:

```text
AGENTS.md
agents/pdf_read_agent.md
templates/pdf_ingestion_template.md
templates/paper.md
memory/project_profile.md
memory/tag_taxonomy.md
memory/term_aliases.md
```

The first ingestion should create or update:

- `wiki/papers/`
- relevant `wiki/topics/`
- relevant `wiki/methods/`
- relevant `wiki/claims/`
- relevant `wiki/gaps/`
- `index.md`
- `log.md`

## Using Other Agents

- `agents/synthesis_agent.md`: build literature maps and compare methods.
- `agents/gap_agent.md`: generate research gap candidates and positioning.
- `agents/review_agent.md`: draft review outlines or related work.
- `agents/lint_agent.md`: check tags, aliases, duplicate pages, missing evidence, and index/log consistency.

## Privacy And Copyright

Do not commit copyrighted PDFs, private Zotero records, raw attachments, personal paths, or private paper notes.

This template includes `.gitignore` rules to avoid uploading common private files, but you should still review your repository before publishing.

## License

This project is licensed under the MIT License. See `LICENSE` for details.
