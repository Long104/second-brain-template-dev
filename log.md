---
title: "second-brain-template-dev — Change Log"
aliases: []
tags: []
created: 2026-06-09T14:22:00Z
updated: 2026-06-10T16:26:00Z
type: "literature-note"
id: "202606091422"
source: ""
---

# second-brain-template-dev — Change Log

> All mutations to this vault are logged here.

---

## 2026-06-10

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
