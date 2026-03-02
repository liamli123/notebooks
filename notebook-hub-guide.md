# Notebook Hub Setup Guide

A complete guide to publishing Jupyter Notebooks online as a central hub, accessible from any device.

---

## Overview

- **Tool:** JupyterBook v2 (MyST)
- **Source repo:** GitHub (private or public)
- **Hosting:** GitHub Pages (free)
- **Live URL:** `https://liamli123.github.io/notebooks/`

---

## One-Time Setup

### 1. Prerequisites

Make sure these are installed:

```powershell
pip install jupyter-book ghp-import
node --version   # must be >= 18
npm --version    # must be >= 8.6
```

### 2. Create the Hub Folder

> ⚠️ Do NOT create this inside Google Drive or OneDrive — npm will fail.

```powershell
cd C:\Users\YourName\Documents   # or any local drive (E:, C:, etc.)
mkdir my-hub
cd my-hub
jupyter-book init
# When asked to run jupyter-book start → Yes (to download theme)
# Then Ctrl+C to stop the local server
```

### 3. Add Your Notebooks

Simply drag and drop `.ipynb` files into the `my-hub` folder using File Explorer.

> **Tip:** Always run notebooks in Jupyter first and save with output before dropping them in. This ensures students see full results on the site.

### 4. Build the Site Locally (First Time)

```powershell
cd E:\Websites\Notebooks\my-hub   # your hub folder
jupyter-book build
```

### 5. Set Up GitHub Pages Deployment

Make sure your hub folder is a Git repo connected to GitHub, then run:

```powershell
jupyter-book init --gh-pages
# Branch: master
# Action name: deploy.yml (press Enter)
```

This creates a `.github/workflows/deploy.yml` file automatically.

### 6. Create GitHub Repo and Push

Go to [github.com](https://github.com) → **New Repository** → name it `notebooks` → **Public** → Create.

Then run:

```powershell
cd E:\Websites\Notebooks\my-hub
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/liamli123/notebooks.git
git push -u origin master
```

> Note: Use `master` not `main` — this machine defaults to `master`.

### 7. Enable GitHub Pages

Go to **github.com/liamli123/notebooks** → **Settings** → **Pages** → under **Source** select **GitHub Actions** → Save.

Wait 2-3 minutes. Your site is live at:

```
https://liamli123.github.io/notebooks/
```

---

## Adding New Notebooks (Regular Workflow)

Every time you finish a notebook and want to publish it:

**Step 1:** Drop the `.ipynb` file into `E:\Websites\Notebooks\my-hub\`

**Step 2:** Run:

```powershell
cd E:\Websites\Notebooks\my-hub
jupyter-book build
git add .
git commit -m "added new notebook"
git push origin master
```

**Step 3:** Wait 2-3 minutes → site auto-updates.

---

## Adding Notebooks from Another Computer

```powershell
# First time on a new computer — clone the repo
git clone https://github.com/liamli123/notebooks.git
cd notebooks

# Drop in new notebooks, then:
jupyter-book build
git add .
git commit -m "added new notebook"
git push origin master
```

---

## Folder Structure

```
my-hub/
├── .github/
│   └── workflows/
│       └── deploy.yml       ← GitHub Action (auto-deploy)
├── myst.yml                 ← hub config
├── Assignment1.ipynb
├── Assignment2.ipynb
├── ML_Deep_Dive.ipynb
└── _build/                  ← auto-generated, do not edit
```

---

## Key Notes

- **Never put the hub folder inside Google Drive/OneDrive** — npm breaks
- **Always run notebooks before dropping them in** — so output is saved
- **`_build/` is auto-generated** — no need to touch it
- **GitHub repo must be Public** for free GitHub Pages hosting
- **Branch name is `master`** on this machine (not `main`)
- **Vercel does NOT work** with MyST v2 as a static site — GitHub Pages is the correct solution
- **`myst` command is not in PATH** — use `jupyter-book` instead

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `npm TAR_ENTRY_ERROR` | Hub folder is inside Google Drive — move to local drive |
| `myst: not recognized` | Use `jupyter-book` instead of `myst` |
| `src refspec main does not match` | Use `git push origin master` not `main` |
| GitHub Pages 404 | Make sure Source is set to **GitHub Actions** not "Deploy from branch" |
| Vercel 404 | Don't use Vercel — use GitHub Pages instead |
| Notebooks show no output | Re-run notebook in Jupyter, save, then re-add to hub |

---

## Useful Links

- Live site: https://liamli123.github.io/notebooks/
- GitHub repo: https://github.com/liamli123/notebooks
- GitHub Actions log: https://github.com/liamli123/notebooks/actions
