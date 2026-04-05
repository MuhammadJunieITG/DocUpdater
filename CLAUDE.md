# DocsUpdater

Self-updating documentation system. MkDocs Material site backed by markdown files, auto-updated via n8n + Linear + Claude.

## Structure

- `docs/` — Markdown documentation files (MkDocs source)
- `n8n/` — n8n workflow JSON (importable)
- `prompts/` — Claude prompt templates used by the n8n workflow
- `mkdocs.yml` — MkDocs configuration (theme, nav, plugins, extensions)
- `.github/workflows/` — GitHub Actions for deploying to GitHub Pages

## Commands

- `mkdocs serve` — Local dev server at http://127.0.0.1:8000
- `mkdocs build` — Build static site to `site/`
- `pip install -r requirements.txt` — Install dependencies

## Notes

- `docs/sprint-changelog/` is auto-updated by the n8n workflow — manual edits there may be overwritten
- The n8n workflow JSON should be re-exported after changes made in the n8n UI
- Label-to-section mapping is in the "Process Linear Data" node in the n8n workflow
