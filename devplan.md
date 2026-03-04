# Dev Plan: WhatsNew — Publish to GitHub + GitHub Pages

## Context

The WhatsNew landing page (`index.html` + `styles.css`) was complete and ready to share
with the dev team. The goal was to: replace expiring Figma-hosted asset URLs with local
files, initialize a Git repo, push it to GitHub, and enable GitHub Pages — no server or
build step required.

---

## Steps Executed

### 1. Replace Figma-hosted asset URLs

Two image URLs in `index.html` pointed to Figma's MCP asset API (expire in ~7 days).
Downloaded both and replaced with local paths:

```bash
mkdir assets/
curl -sL "https://www.figma.com/api/mcp/asset/4241dc3f-..." -o assets/logo-winsupply.png
curl -sL "https://www.figma.com/api/mcp/asset/6a7c3dc5-..." -o assets/icon-arrow.svg
```

> Note: the logo asset resolved as a **PNG** (not SVG), so it was saved as `.png`.

Updated `index.html` (lines 75 and 308):

| Before | After |
|---|---|
| `figma.com/api/mcp/asset/4241dc3f…` | `assets/logo-winsupply.png` |
| `figma.com/api/mcp/asset/6a7c3dc5…` | `assets/icon-arrow.svg` |

---

### 2. Add `.gitignore`

Created `WhatsNew/.gitignore`:

```
.DS_Store
```

---

### 3. Initialize Git repo and commit

```bash
git init
git add index.html styles.css .gitignore assets/
git commit -m "Initial commit: WhatsNew landing page"
```

Files committed: `index.html`, `styles.css`, `.gitignore`, `assets/logo-winsupply.png`, `assets/icon-arrow.svg`

---

### 4. Install GitHub CLI

`gh` was not pre-installed. Installed via Homebrew:

```bash
/opt/homebrew/bin/brew install gh
```

Authenticated as `yagozardo` (existing credentials picked up from keyring).

---

### 5. Create GitHub repo and push

```bash
gh repo create winsupply-whats-new \
  --public \
  --description "AMVS-26 What's New release campaign landing page" \
  --source=. \
  --push
```

This created the repo, set `origin`, and pushed `main` in one command.

---

### 6. Enable GitHub Pages

The `-f source.branch=main` flag syntax was rejected by the API (HTTP 422).
Workaround: pass a JSON body directly:

```bash
gh api repos/yagozardo/winsupply-whats-new/pages \
  --method POST \
  --input - <<'EOF'
{"source": {"branch": "main", "path": "/"}}
EOF
```

Pages enabled successfully on `main` / root.

---

## Result

| | |
|---|---|
| **GitHub repo** | https://github.com/yagozardo/winsupply-whats-new |
| **Live page** | https://yagozardo.github.io/winsupply-whats-new/ |

---

## Files in this repo

```
WhatsNew/
├── index.html              # Page markup + Tailwind config
├── styles.css              # Design tokens (CSS custom properties) + base styles
├── .gitignore
├── README.md
├── devplan.md              # This file
└── assets/
    ├── logo-winsupply.png
    └── icon-arrow.svg
```
