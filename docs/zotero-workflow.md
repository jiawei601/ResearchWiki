# Zotero Workflow

ResearchWiki supports a cautious Zotero workflow.

1. Read a user-specified Zotero collection.
2. Generate an import plan and manifest.
3. Check whether papers are already in `wiki/papers/`.
4. Wait for user confirmation.
5. Ingest confirmed papers one at a time through `agents/pdf_read_agent.md`.

The import workflow should not scan the full Zotero storage, modify Zotero items, or move original PDFs.

