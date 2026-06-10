---
title: "second-brain-template-dev — Change Log"
aliases: []
tags: []
created: 2026-06-09T14:22:00Z
updated: 2026-06-10T16:32:00Z
type: "literature-note"
id: "202606091422"
source: ""
---

# second-brain-template-dev — Change Log

> All mutations to this vault are logged here.

---

## 2026-06-10

### 16:32 — add .gitkeep to empty wiki folders

- Problem → `wiki/1.project/` and `wiki/4.archive/` are empty, git doesn't track empty directories so they don't appear on GitHub
- Fix → added `.gitkeep` to both folders, updated index.md tree
- Why → all four PARA folders must be visible on GitHub for template completeness

### 16:30 — ingest obsidian-worklog from inbox

- Problem → inbox/obsidian-worklog.md had incorrect command (`obsidian daily` instead of `obsidian daily:path`), missing table formats and gotchas
- Fix → wrote `wiki/3.resource/command/obsidian.md` using command.md template, corrected the command, added Work Log/Log table formats, gotchas section. Deleted from inbox
- Why → obsidian CLI commands are reference material for the daily note workflow

### 16:27 — fix index.md to match actual disk

- Problem → `index.md` still had old vault name `note-2/`, listed fake projects (BuddhismZen, LeetCode, NoteBookZen, etc.) that don't exist on disk, missing `.opencode/` and `assets/`
- Fix → rewrote entire index.md to reflect actual file system state: `1.project/` empty, `4.archive/` empty, correct counts, correct structure
- Why → index.md must match reality — template repo has no projects yet

### 16:26 — created wiki/4.archive/

- Problem → `wiki/4.archive/` was referenced in AGENTS.md vault tree but didn't exist on disk
- Fix → created the directory
- Why → PARA structure needs all four categories present from the start

### 16:25 — fix vault name in AGENTS.md

- Problem → AGENTS.md vault tree still said `note-2/` instead of `second-brain-template-dev/`
- Fix → updated the root folder name in §1 Vault Overview
- Why → template repo was renamed

### 16:24 — update AGENTS.md: build artifacts + prototype flow

- Problem → no rules for where built files (HTML, web projects, prototypes) should live
- Fix → added Phase 2 (Build Artifacts) to classification, build artifacts rule in §6 DO, §6.11 Prototype & Quick Build Flow
- Why → user wants all project files in one folder per project inside `1.project/`, with ask-first before every build
