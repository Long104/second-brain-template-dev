---
title: "Obsidian Worklog"
aliases:
  - "Obsidian Worklog"
tags:
  - para/resource
  - topic/tools
  - status/active
created: 2026-06-10T07:56:05Z
updated: 2026-06-10T07:56:05Z
type: "command"
id: "202606100756"
source: ""
---

# Obsidian Worklog

> Guide on using the official Obsidian CLI to get the daily note file path and insert rows directly into the Work Log and Log tables.

---

## Overview

```
  ┌──────────────────────────────────────────────┐
  │              COMMAND REFERENCE                │
  ├──────────────┬───────────────────────────────┤
  │  TOOL        │ Obsidian CLI                  │
  │  CATEGORY    │ cli / productivity            │
  │  DIFFICULTY  │ intermediate                  │
  └──────────────┴───────────────────────────────┘
```

---

## Commands

### Get Daily Note File Path

Use the Obsidian CLI to retrieve the absolute path of today's daily note.

```bash
obsidian daily
```

---

## Workflows

### Inserting Rows to Work Log and Log Tables

1. Retrieve the daily note path using `obsidian daily`.
2. Open the file at that path.
3. Parse the Markdown tables for `## Work Log` and `## Log`.
4. Insert new rows matching the activity details and save.

---

## References

- [[index]]
