# Lab 1 — What Was Done

A log of the actual work performed in this lab, in order, with the real
commit hashes from this repo (run `git log --oneline --all --graph` to see
them yourself).

| Step | Action | Branch | Commit |
|---|---|---|---|
| 1 | Created the initial site: `index.html` + `style.css` (title, tagline, dark theme) | `main` | `e543fa5` |
| 2 | Branched off to add a footer | `feature-add-footer` | `d944137` |
| 3 | Merged the footer branch back into `main` — **clean merge** (no overlap) | `main` | `f2d7289` |
| 4 | Branched off `main` to change the background to blue | `feature-blue-theme` | `2620891` |
| 5 | Merged the blue-theme branch into `main` — **clean merge** | `main` | `bd4b579` |
| 6 | Branched off the *pre-blue* commit (`d944137`) to change the background to green — same line as step 4, on purpose | `feature-green-theme` | `dadc5ba` |
| 7 | Attempted to merge the green-theme branch into `main` — **merge conflict** on the `background-color` line in `lab1/style.css` (blue vs. green) | `main` | conflict, not committed yet |
| 8 | Opened `lab1/style.css`, resolved the `<<<<<<<` / `=======` / `>>>>>>>` markers by keeping the green value, staged the file, and completed the merge commit | `main` | `b8e2987` |

## Why the conflict happened

Steps 4 and 6 both branched off points where `background-color` was the
original dark value, and both changed that *same line* to a *different*
value (blue vs. green) before either was merged. Git can auto-merge changes
to different lines/files, but when the same line is touched differently on
both sides, it stops and asks a human to decide — that's the conflict in
step 7.

## Result

- `main` now has a footer and a green theme.
- Full branch structure (`feature-add-footer`, `feature-blue-theme`,
  `feature-green-theme`) is preserved and pushed to GitHub so the merges
  and the conflict can be inspected directly (e.g. `git show b8e2987`,
  `git log --graph --all`).
