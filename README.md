# DocsUpdater

Self-updating technical documentation powered by **MkDocs Material**, **n8n**, **Linear**, and **Claude AI**.

An n8n workflow reads completed sprint tickets from Linear, sends them to Claude to generate documentation updates, and opens a pull request for human review. When merged, GitHub Actions rebuilds and deploys the MkDocs site.

## Architecture

```
Schedule/Webhook
      |
      v
n8n fetches completed Linear sprint tickets
      |
      v
n8n fetches current .md files from GitHub
      |
      v
Claude generates updated markdown
      |
      v
n8n creates a branch + opens a PR
      |
      v
Human reviews & merges
      |
      v
GitHub Actions deploys to GitHub Pages
```

## Quick Start — Documentation Site

```bash
# Create a virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run locally
mkdocs serve
# Open http://127.0.0.1:8000

# Build for production
mkdocs build
```

## Quick Start — n8n Workflow

1. Import `n8n/docs-updater-workflow.json` into your n8n instance
2. Configure credentials (see Environment Variables below)
3. Update the `{{GITHUB_REPO}}` and `{{GITHUB_TOKEN}}` placeholders in the Code nodes
4. Activate the workflow

## Environment Variables

Configure these as credentials/variables in n8n:

| Variable | Description | Where to get it |
|----------|-------------|-----------------|
| `LINEAR_API_KEY` | Linear personal API key | Linear > Settings > API |
| `ANTHROPIC_API_KEY` | Claude API key | [Anthropic Console](https://console.anthropic.com/) |
| `GITHUB_TOKEN` | GitHub PAT with `repo` scope | GitHub > Settings > Developer settings > PATs |
| `GITHUB_REPO` | Repository in `owner/repo` format | Your GitHub repository |

## Customization

- **Doc structure** — Edit `mkdocs.yml` nav section and add/remove files in `docs/`
- **Label mapping** — Edit the `labelToSection` object in the "Process Linear Data" n8n node to map your Linear labels to doc paths
- **Claude prompt** — Edit `prompts/update-docs-prompt.md` to change how docs are updated
- **Schedule** — Edit the Schedule Trigger node in n8n (default: daily at 09:00 UTC)

## Deployment

The site auto-deploys to GitHub Pages via `.github/workflows/deploy-docs.yml` on push to `main`. To set up:

1. Push this repo to GitHub
2. Go to repo Settings > Pages > Source: Deploy from a branch > `gh-pages` / `/ (root)`
3. The next push to `main` that changes `docs/` or `mkdocs.yml` will trigger a deploy
