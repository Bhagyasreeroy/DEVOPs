# Lab 1 — Git Branching & Merge Conflict Resolution

A tiny static website (`index.html` + `style.css`) is used here as the
shared codebase to demonstrate the core Git workflow: branching, clean
merges, and resolving a merge conflict.

## What this repo's history shows

1. **Initial commit** — a basic one-page site (`index.html`, `style.css`)
   on `main`, showing a title and a tagline.
2. **Branch `feature-add-footer`** — adds a footer section to `index.html`.
   Merges into `main` cleanly (touches a different part of the file).
3. **Branch `feature-blue-theme`** and **branch `feature-green-theme`** —
   both branched from `main` after step 2, and both edit the *same*
   `background-color` line in `style.css`, but to different colors.
   - `feature-blue-theme` merges into `main` first, cleanly.
   - `feature-green-theme` merging into `main` next produces a **merge
     conflict** on that line (both branches changed it differently), which
     is resolved by hand and committed as a merge commit.

## Steps to reproduce locally

```bash
git checkout main
git checkout -b feature-add-footer
# edit index.html, add a <footer>
git commit -am "Add footer to homepage"
git checkout main
git merge feature-add-footer --no-ff

git checkout -b feature-blue-theme
# edit style.css: background-color: #2563eb;
git commit -am "Switch theme to blue"
git checkout main
git merge feature-blue-theme --no-ff

git checkout -b feature-green-theme
# edit style.css: background-color: #16a34a;
git commit -am "Switch theme to green"
git checkout main
git merge feature-green-theme --no-ff
# CONFLICT (content): Merge conflict in lab1/style.css
# open the file, resolve the <<<<<<< ======= >>>>>>> markers
git add lab1/style.css
git commit
```

## Useful commands

| Command | Purpose |
|---|---|
| `git branch <name>` | create a branch |
| `git checkout -b <name>` | create + switch to a branch |
| `git switch <name>` | switch branches (modern) |
| `git merge <branch>` | merge a branch into the current one |
| `git merge --no-ff <branch>` | force a merge commit even if fast-forward is possible |
| `git status` | see conflicted files |
| `git diff` | see conflict markers / changes |
| `git log --oneline --graph --all` | visualize branch/merge history |
| `git merge --abort` | bail out of a conflicted merge |

## Viewing the site

Open `lab1/index.html` directly in a browser, or serve it locally:

```bash
cd lab1 && python3 -m http.server 8000
```

Then visit `http://localhost:8000`.
