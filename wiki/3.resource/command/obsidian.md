---
title: "Obsidian Commands"
aliases:
  - "Obsidian CLI"
tags:
  - para/resource
  - topic/tools
  - status/active
created: 2026-06-10T16:30:00Z
updated: 2026-06-10T16:30:00Z
type: "command"
id: "202606101630"
source: ""
---

# Obsidian Commands

> Quick reference for Obsidian CLI commands.

---

## Overview

```
  ┌──────────────────────────────────────────────┐
  │              COMMAND REFERENCE                │
  ├──────────────┬───────────────────────────────┤
  │  TOOL        │ Obsidian CLI                   │
  │  CATEGORY    │ cli / productivity             │
  │  DIFFICULTY  │ beginner                       │
  └──────────────┴───────────────────────────────┘
```

---

## Basic Commands

| Command                | Description                          | Example                                    |
| ---------------------- | ------------------------------------ | ------------------------------------------ |
| `obsidian daily:path` | Get absolute path of today's daily note | `obsidian daily:path`                   |
| `obsidian daily:path vault=<name>` | Get daily note path for specific vault | `obsidian daily:path vault=second-brain` |

---

## Common Workflows

### Insert Rows into Daily Note Work Log

```
  ┌───────────┐     ┌───────────┐     ┌───────────┐
  │  GET PATH │────►│  READ FILE│────►│INSERT ROW │
  │           │     │           │     │           │
  └───────────┘     └───────────┘     └───────────┘
```

| Step | Command / Action              | Purpose                                          |
| ---- | ----------------------------- | ------------------------------------------------ |
| 1    | `obsidian daily:path`         | Get the absolute file path of today's daily note |
| 2    | Read the file at that path    | Parse `## Work Log` and `## Log` tables         |
| 3    | Insert row into Work Log      | `\| task \| doing \| HH:MM \| — \| — \|`        |
| 4    | Insert row into Log           | `\| HH:MM \| Started: task description \|`      |

#### Work Log table format

```
| Task        | Status | Start | End   | Duration |
|-------------|--------|-------|-------|----------|
| Build thing | doing  | 16:30 | —     | —        |
```

#### Log table format

```
| Time  | Activity                    |
|-------|-----------------------------|
| 16:30 | Started: Build thing        |
```

---

## Gotchas

| Issue                          | Cause                                   | Fix                                               |
| ------------------------------ | --------------------------------------- | ------------------------------------------------- |
| Wrong daily note returned      | Multiple vaults open                    | Add `vault=<name>` to specify which vault        |
| Tables not found in file       | Daily note created without template    | Recreate daily note using `templates/daily.md`   |
| Time inserted incorrectly      | Estimated/guessed instead of real time | Always run `date +%H:%M` first — never guess      |

---

## References

- [[daily-note-workflow]]
- [[AGENTS]] — §6 Obsidian Worklog rules
