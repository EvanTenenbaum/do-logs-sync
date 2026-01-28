# DO Logs Sync

Automatically syncs DigitalOcean App Platform deploy logs to a GitHub Gist every 5 minutes.

## Purpose

This solves the problem of Manus agents having unreliable connections to DO's API/MCP. Instead:
- GitHub Actions fetches logs from DO every 5 minutes
- Logs are written to a public Gist
- Manus can reliably fetch the raw Gist URL (no auth needed)

## Setup Required

### 1. Add Repository Secrets

Go to **Settings → Secrets and variables → Actions → New repository secret** and add:

| Secret Name | Description |
|-------------|-------------|
| `DO_API_TOKEN` | Your DigitalOcean API token ([create here](https://cloud.digitalocean.com/account/api/tokens)) |
| `GIST_TOKEN` | GitHub PAT with `gist` scope ([create here](https://github.com/settings/tokens)) |

### 2. Run the Workflow

The workflow runs automatically every 5 minutes. You can also trigger it manually:
- Go to **Actions** tab
- Select "Sync DO Deploy Logs to Gist"
- Click "Run workflow"

## For Manus

**Raw URL to fetch:**
```
https://gist.githubusercontent.com/EvanTenenbaum/476cdd17d06727172f0190057683f046/raw/do-deploy-logs.txt
```

**Gist Page:**
https://gist.github.com/EvanTenenbaum/476cdd17d06727172f0190057683f046

## Configuration

Edit `.github/workflows/sync-logs.yml` to change:
- `DO_APP_ID`: Your DO App Platform app ID
- `GIST_ID`: The target Gist ID
- Cron schedule (default: every 5 minutes)
