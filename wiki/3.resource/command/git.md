---
title: "Git Commands"
aliases:
  - "git cli"
tags:
  - para/resource
  - topic/git
  - status/active
created: 2026-06-09T14:36:00Z
updated: 2026-06-09T14:36:00Z
type: "command"
id: "202606091436"
source: ""
---

# Git Commands

> Quick reference for Git CLI.

---

## Basic

| Command               | Description       | Example                                  |
| --------------------- | ----------------- | ---------------------------------------- |
| `git init`            | Init repo         | `git init`                               |
| `git clone <url>`     | Clone repo        | `git clone git@github.com:user/repo.git` |
| `git add <file>`      | Stage changes     | `git add .` (all), `git add -A`          |
| `git commit -m "msg"` | Commit staged     | `git commit -m "fix: typo"`              |
| `git status`          | Show working tree | `git status -s` (short)                  |
| `git log`             | Show history      | `git log --oneline -10`                  |
| `git push`            | Push to remote    | `git push origin main`                   |
| `git pull`            | Pull from remote  | `git pull origin main`                   |

---

## Intermediate

| Command               | Flags      | Description            | Example                                |
| --------------------- | ---------- | ---------------------- | -------------------------------------- |
| `git branch`          | `-a`       | List branches          | `git branch -a`                        |
| `git checkout`        | `-b`       | Switch / create branch | `git checkout -b feat/foo`             |
| `git merge <branch>`  | —          | Merge branch           | `git merge feat/foo`                   |
| `git rebase <branch>` | `-i`       | Rebase / interactive   | `git rebase -i HEAD~3` (squash last 3) |
| `git stash`           | `pop`      | Save / restore WIP     | `git stash && git stash pop`           |
| `git diff`            | `--staged` | Show changes           | `git diff HEAD`                        |
| `git remote`          | `-v`       | Show remotes           | `git remote add origin <url>`          |
| `git fetch`           | —          | Fetch without merge    | `git fetch origin`                     |

---

## Common Workflows

```
  FEATURE BRANCH
  main ──► feat/foo ──► commit ──► push ──► PR ──► merge
```

| Step    | Command                                   | Purpose               |
| ------- | ----------------------------------------- | --------------------- |
| Start   | `git checkout -b feat/foo`                | Create feature branch |
| Save    | `git add -A && git commit -m "feat: foo"` | Commit work           |
| Push    | `git push -u origin feat/foo`             | Push + track          |
| Sync    | `git checkout main && git pull`           | Get latest            |
| Cleanup | `git branch -d feat/foo`                  | Delete local branch   |

```
  FIX A MISTAKE
```

| Situation                       | Command                               |
| ------------------------------- | ------------------------------------- |
| Undo last commit (keep changes) | `git reset --soft HEAD~1`             |
| Undo last commit (discard)      | `git reset --hard HEAD~1`             |
| Fix last commit message         | `git commit --amend -m "new message"` |
| Unstage a file                  | `git restore --staged <file>`         |
| Discard working changes         | `git restore <file>`                  |

---

## Gotchas

| Issue             | Cause                            | Fix                                     |
| ----------------- | -------------------------------- | --------------------------------------- |
| Merge conflict    | Same file changed both sides     | Fix manually → `git add` → `git commit` |
| Permission denied | Wrong SSH key / auth             | `ssh -T git@github.com` to test         |
| Diverged branches | Local vs remote out of sync      | `git pull --rebase`                     |
| Detached HEAD     | Checked out a commit, not branch | `git switch -c temp-branch`             |

---

## References

- [Git docs](https://git-scm.com/doc)
