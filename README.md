# DatabaseReleases

This repository contains the release builds of the EhTagTranslation database.

## Sync Process

This repository is automatically synchronized with the `release` branch of [EhTagTranslation/Database](https://github.com/EhTagTranslation/Database) using GitHub Actions.

### Automatic Sync

The sync process runs:
- **Daily at 2 AM UTC** via scheduled workflow
- **On-demand** via manual workflow dispatch  
- **When triggered** by the Database repository via repository_dispatch

### How it Works

1. **Change Detection**: Compares the SHA stored in the `sha` file with the latest commit on Database's release branch
2. **File Sync**: If changes are detected, downloads all files from the Database release branch
3. **Safe Update**: Preserves repository-specific files (`.github/`, `.gitignore`, `README.md`)
4. **Commit**: Creates a new commit with reference to the source Database commit

### Manual Sync

To manually trigger a sync:

1. Go to the [Actions tab](../../actions)
2. Select "Sync from Database Release Branch" workflow  
3. Click "Run workflow"

### Permissions

The workflow uses `GITHUB_TOKEN` with `contents: write` permission to:
- Fetch from the Database repository (public, no auth needed)
- Commit and push changes to this repository

### Files

The repository contains the following database files:
- `db.ast.js` / `db.ast.json` - AST format database
- `db.full.js` / `db.full.json` - Full database with all fields  
- `db.html.js` / `db.html.json` - HTML formatted database
- `db.raw.js` / `db.raw.json` - Raw database format
- `db.text.js` / `db.text.json` - Text-only database
- `*.gz` files - Compressed versions of the JSON files
- `sha` - Contains the commit hash from the source Database repository

## Usage

These files can be used directly in web applications or downloaded for offline use. See the [main Database repository](https://github.com/EhTagTranslation/Database) for documentation on the data format and usage instructions.