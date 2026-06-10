---
title: "{{title}} — Git Workflow Guide"
aliases:
  - "{{alias}}"
tags:
  - para/resource
  - topic/git
  - status/active
created: {{datetime}}Z
updated: {{datetime}}Z
type: "command"
id: "{{id}}"
source: ""
---

# {{title}} — Git Workflow Guide

> Branching strategies, commit conventions, PR flow, hooks, and daily Git operations.

---

## Overview

```
  ┌──────────────────────────────────────────────┐
  │              GIT WORKFLOW PROFILE               │
  ├──────────────┬───────────────────────────────┤
  │  STRATEGY    │ {{strategy}}                   │
  │  CONVENTION  | {{convention}}                 │
  │  PROTECTED   │ main / main + hotfix            │
  └──────────────┴──────────────────────────────┘
```

---

## Branching Strategy

```
  main
    │
    ├── feature/short-description
    ├── fix/short-description
    └── hotfix/critical-fix
```

| Branch Type | Prefix     | Merges To | Lifecycle           |
| ----------- | ---------- | --------- | ------------------- |
| Feature     | `feature/` | main      | Deleted after merge |
| Bug fix     | `fix/`     | main      | Deleted after merge |
| Hotfix      | `hotfix/`  | main      | Deleted after merge |

---

## Commit Convention

```
<type>(<scope>): <description>

type: feat | fix | docs | refactor | test | chore
scope: affected module or component
description: imperative, lowercase, no period at end
```

| Type       | Purpose                                 |
| ---------- | --------------------------------------- |
| `feat`     | New feature                             |
| `fix`      | Bug fix                                 |
| `docs`     | Documentation only                      |
| `refactor` | Code change that neither fixes nor adds |
| `test`     | Adding or updating tests                |
| `chore`    | Maintenance, config, tooling changes    |

---

## Daily Commands

| Command                 | Description             | Example |
| ----------------------- | ----------------------- | ------- |
| `git status`            | Check working tree      |         |
| `git add -A`            | Stage all changes       |         |
| `git commit`            | Commit staged           |         |
| `git push`              | Push to remote          |         |
| `git log --oneline -10` | Recent commits          |         |
| `git diff --stat`       | Changed files           |         |
| `git stash`             | Temporarily shelve work |         |

## PR Workflow

```
  1. Create branch      git checkout -b feature/short-desc
  2. Make changes       edit, commit with conventional style
  3. Push               git push -u origin feature/short-desc
  4. Open PR             gh pr create --fill --base main
  5. Review + merge       Code review, approve, squash merge
  6. Cleanup             git branch -d feature/short-desc
```

---

## Hooks

| Hook       | File                    | Purpose                          |
| ---------- | ----------------------- | -------------------------------- |
| pre-commit | `.git/hooks/pre-commit` | Lint, format check before commit |
| pre-push   | `.git/hooks/pre-push`   | Prevent push to protected branch |
| commit-msg | `.git/hooks/commit-msg` | Enforce commit convention        |

---

## Gotchas

| Issue | Cause | Fix |
| ----- | ----- | --- |
|       |       |     |

---

## References

- [[linked-note]]
