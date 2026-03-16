# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Vincent Vango is a MkDocs documentation site documenting the conversion of a 2020 Ford Transit T-250 van. It uses the Material for MkDocs theme and is deployed to GitHub Pages.

## Commands

```bash
# Install dependencies
pip install mkdocs-material

# Local development server with live reload
mkdocs serve

# Build static site to /site directory
mkdocs build

# Deploy to GitHub Pages (gh-pages branch)
mkdocs gh-deploy --force
```

## Architecture

**Stack:** MkDocs + Material theme, Python only, no Node.js or custom build scripts.

**Key files:**
- `mkdocs.yml` — site config, navigation structure, plugins, theme settings
- `docs/*.md` — all content pages (24 pages organized in 6 sections)
- `docs/assets/` — optimized images (committed to repo, 800x600px max)
- `docs/assets-large/` — raw source images (gitignored, not committed)

**Image workflow:** Place large images in `docs/assets-large/`. The `resize-images` plugin automatically downsizes them to `docs/assets/` (800x600px max) during `mkdocs serve` or `mkdocs build`. The `.resize-hash` cache file is also gitignored.

**Navigation** is explicitly defined in `mkdocs.yml` under `nav:`. New pages must be added there to appear in the sidebar. The sections follow the physical build sequence: First Steps → Insulation → Roof → Electrical → Van Upgrades → Interior.

**CI/CD:** GitHub Actions (`.github/workflows/ci.yml`) auto-deploys on push to `main` or `master` by running `mkdocs gh-deploy --force`.
