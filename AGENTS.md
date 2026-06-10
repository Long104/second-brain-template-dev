---
id: AGENTS
aliases: []
tags: []
---

# AGENTS.md — Assistant Operating Manual

## Purpose

This file is the single source of truth for how any AI assistant operates inside this note vault. Read this file first before doing anything.

---

## 1. Vault Overview

```
second-brain-template-dev/
├── AGENTS.md          ← assistant rules (never modify unless asked)
├── SETUP.md            ← quick-start guide (read this first if new)
├── index.md            ← vault map (update when structure changes)
├── log.md              ← change log (append every mutation with date)
├── inbox/              ← capture zone (one file per topic, lands here first)
├── todo/               ← task management (2-file system + plans)
│   ├── 1.todo.md      ← pending tasks
│   ├── 3.done.md      ← completed tasks (with completion date/time)
│   └── plan/           ← project plans (architecture + build phases)
├── calendar.md        ← events, deadlines, standups, appointments
├── README.md           ← vault README
├── .opencode/          ← opencode skills + agent config
│   ├── agents/
│   │   └── default.md  ← primary agent config
│   └── skills/               ← installed skills (see each SKILL.md for docs)
├── dailyNote/          ← daily journal (YYYY-MM-DD.md, use template)
├── templates/          ← reusable templates (kebab-case naming)
│   ├── solopreneur/   ← product/launch templates
│   └── *.md           ← template files
├── assets/             ← static assets
│   └── imgs/           ← images for design references
└── wiki/               ← PARA knowledge base
    ├── 1.project/      ← active projects with deadline → 4.archive/ when done (ALL build artifacts live here: index.html, web projects, code, prototypes, any built thing)
    ├── 2.area/         ← ongoing responsibilities (no deadline, continuous)
    ├── 3.resource/     ← reference material (organized by type)
    │   ├── bookmarks.md   ← saved links [title](url) — description
    │   ├── command/        ← CLI commands (one file per tool)
    │   │   ├── docker.md     ← docker, compose, buildx
    │   │   ├── kubernetes.md ← kubectl, helm, k9s
    │   │   ├── terraform.md  ← tf, terragrunt, tofu
    │   │   └── git.md        ← git, gh, lazygit
    │   ├── snippet/        ← code snippets (one file per topic)
    │   │   ├── docker.md     ← Dockerfile patterns
    │   │   ├── kubernetes.md ← YAML manifests
    │   │   ├── terraform.md  ← Terraform HCL
    │   │   └── bash.md       ← Shell scripts
    │   ├── history/        ← changelogs/timelines (one topic per file)
    │   ├── person/         ← people/contacts (one person per file)
    │   ├── tools/          ← tool/app notes (one tool per file)
    │   ├── design/         ← design system references, UI tokens, visual docs
    │   │   └── reference/  ← design reference/inspiration notes
    │   ├── prompt/         ← prompt engineering + reusable prompt templates
    │   │   ├── code/       ← code generation prompts
    │   │   ├── design/     ← UI/UX design prompts
    │   │   ├── image/      ← image generation prompts
    │   │   └── video/      ← video generation prompts
    │   └── reverse-engineer/ ← reverse-engineered prompt analysis notes
    └── 4.archive/       ← inactive items (source of truth for history)
```

---

## 2. Ingest Pipeline

### Rules

1. **ALL new content starts in `inbox/`** — one file per topic, no exceptions
2. **CHECK TEMPLATES FIRST** — use matching template as base. Never write without consulting templates.
3. **Ingest = sort + distribute** — AI reads inbox, classifies, writes to correct wiki location
4. **After ingest, delete the file from `inbox/`**
5. **Log every ingest** — append to `log.md`
6. **Never skip the pipeline** — never write directly to wiki (unless user overrides)
7. **If no template matches, create one first** — write a new template under `templates/` for the new category, then use it as the base for the note. Never write a note that has no template behind it.
8. **Add new templates to §4 Template Map** — when a new template file is created, immediately add a row to the Template Map table in this file (with destination, `type`, `Extra`, trigger).

### Auto-Capture Knowledge

When the user asks about a **how-to, command, reference topic, or any knowledge** that isn't already in the wiki:

1. **Create a file in `inbox/`** — one file per topic, kebab-case name (e.g. `inbox/docker-networking.md`)
2. **Tell the user** — "Added to inbox. Say **ingest** when ready." + answer the question in chat
3. **Wait for "ingest"** — do NOT process until the user explicitly says "ingest"
4. **On "ingest"** — follow the full pipeline: classify → template → write to wiki → clear inbox → update logs + git

| Trigger                                                             | Action                                                                                      |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| User asks about a command, how-to, tool tip, or reference knowledge | Create a file in `inbox/`, answer in chat, say "Added to inbox. Say **ingest** when ready." |
| User says "ingest"                                                  | Process all `inbox/` items through the full pipeline                                        |

> **Never auto-ingest.** The user decides what gets kept and what gets discarded. The inbox is a holding zone, not an auto-publish queue.

### Prompt Creation Flow

When the user says **"create a prompt for [topic]"** or asks you to make a reusable prompt:

1. **Create the file** in `wiki/3.resource/prompt/<category>/<name>.md` using `templates/prompt.md`
2. **Give the prompt in chat** — output the full prompt text directly so they can copy/use it immediately
3. **Category by content:**
   - Image generation → `prompt/image/`
   - Code generation → `prompt/code/`
   - UI/UX / design → `prompt/design/`
   - Video generation → `prompt/video/`
   - Concepts / how-to guides → `prompt/prompt-engineering-guide.md`
   - Other → pick the closest category or create a new subfolder
4. **Log it** — update `log.md`, commit & push

When creating **prompt guides** (reference docs about prompting, not individual reusable prompts):

1. Use the `prompt-guide` template pattern (resource type, not prompt type)
2. File name: `*-guide.md` or descriptive kebab-case name
3. Cross-link from `prompt-engineering-guide.md` (the hub)

| Trigger                                                            | Action                                                                       |
| ------------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| User says "create a prompt for [topic]" or "make a prompt for [x]" | Save to `wiki/3.resource/prompt/`, give full prompt text in chat, log + push |
| User asks about prompt engineering concepts/techniques             | Reference `prompt-engineering-guide.md` or create a new guide in `prompt/`   |

---

## 3. Classification

```
  PHASE 1: PARA CATEGORY
  deadline? ──YES──► 1.project/
  ongoing?  ──YES──► 2.area/
  reference?─YES──► 3.resource/
  else ───────────► dailyNote / discard

  PHASE 2: BUILD ARTIFACTS
  Any built file (index.html, .js, .css, web app,
  prototype, code project, anything you build)? ──► wiki/1.project/[project-name]/
  │  Create ONE folder per project. ALL files for that project
  │  go in that folder — index.html, style.css, app.js, assets,
  │  everything. Example: wiki/1.project/marquee-app/
  │  ├── index.html
  │  ├── style.css
  │  └── app.js
  (Never scatter files. Never mix projects in the same folder.)

  PHASE 3: CONTENT SHAPE (resources only)
  CLI commands?   ──► command/
  Code blocks?    ──► snippet/
  Tool/app info?  ──► tools/
  Person/contact? ──► person/
  Links saved?    ──► bookmarks.md
  Timeline/log?   ──► history/
  Concepts/how-to ──► resource-master.md
```

### Compound Topic Rules

| #   | Rule                                                                  |
| --- | --------------------------------------------------------------------- |
| 1   | **3+ distinct content shapes** for same topic → create hub + children |
| 2   | Hub uses `resource-master.md` at `wiki/3.resource/<topic>.md`         |
| 3   | Each child uses its own template in the correct subfolder             |
| 4   | Hub links to all children, children link back to hub                  |
| 5   | **1-2 shapes** → single file using primary shape's template           |
| 6   | Log each file created as a separate ingest entry                      |

```
  Example: Kubernetes
  kubernetes.md (HUB — resource-master.md)
      ├── command/kubectl.md     (command.md)
      ├── snippet/k8s-yaml.md    (snippet.md)
      └── tools/minikube.md      (tools.md)
```

---

## 4. Template Map

| Template                | Destination                             | `type`               | Extra    | Trigger                                                        |
| ----------------------- | --------------------------------------- | -------------------- | -------- | -------------------------------------------------------------- |
| `daily.md`              | `dailyNote/YYYY-MM-DD.md`               | `"daily"`            | —        | Daily journal entry                                            |
| `project.md`            | `wiki/1.project/*.md`                   | `"project-note"`     | —        | Has deadline + goal                                            |
| `area.md`               | `wiki/2.area/*.md`                      | `"area"`             | —        | Ongoing responsibility                                         |
| `resource-master.md`    | `wiki/3.resource/*.md`                  | `"resource"`         | `source` | Resource + compound topic hub                                  |
| `command.md`            | `wiki/3.resource/command/*.md`          | `"command"`          | `source` | CLI commands                                                   |
| `snippet.md`            | `wiki/3.resource/snippet/*.md`          | `"snippet"`          | `source` | Code snippets                                                  |
| `tools.md`              | `wiki/3.resource/tools/*.md`            | `"resource"`         | `source` | Tool/app notes                                                 |
| `bookmarks.md`          | `wiki/3.resource/bookmarks.md`          | `"resource"`         | `source` | Saved links                                                    |
| `person.md`             | `wiki/3.resource/person/*.md`           | `"resource"`         | `source` | People/contacts                                                |
| `history.md`            | `wiki/3.resource/history/*.md`          | `"resource"`         | `source` | Changelog/timeline                                             |
| `archive.md`            | `wiki/4.archive/*.md`                   | `"project-note"`     | —        | Completed/inactive                                             |
| `plan.md`               | `todo/plan/*.md`                        | `"plan"`             | —        | Complex project needing architecture + build phases            |
| `prompt.md`             | `wiki/3.resource/prompt/*.md`           | `"prompt"`           | `source` | Reusable prompt templates (image/code/design)                  |
| `prompt-guide.md`       | `wiki/3.resource/prompt/*-guide.md`     | `"resource"`         | `source` | Prompt engineering guides (not individual prompts)             |
| `design-system.md`      | `wiki/3.resource/design/*.md`           | `"resource"`         | `source` | Design system reference — visual/component docs                |
| `design-reference.md`   | `wiki/3.resource/design/reference/*.md` | `"design-reference"` | `source` | Design references for beautiful/inspirational websites         |
| `reverse-engineer.md`   | `wiki/3.resource/reverse-engineer/*.md` | `"reverse-engineer"` | `source` | Reverse-engineered prompt analysis notes                       |
| `docker-guide.md`       | `wiki/3.resource/tools/docker*.md`      | `"resource"`         | `source` | Docker patterns, multi-stage builds, compose, optimization     |
| `kubernetes-guide.md`   | `wiki/3.resource/tools/kubernetes*.md`  | `"resource"`         | `source` | K8s manifests, RBAC, Helm, networking, debugging               |
| `terraform-guide.md`    | `wiki/3.resource/tools/terraform*.md`   | `"resource"`         | `source` | TF modules, state management, providers, workflows             |
| `git-workflow-guide.md` | `wiki/3.resource/command/git/*.md`      | `"command"`          | `source` | Branching strategies, commit conventions, PR flow, hooks       |
| `ci-cd-guide.md`        | `wiki/3.resource/tools/ci-cd*.md`       | `"resource"`         | `source` | Pipeline patterns, GitHub Actions, deployment strategies       |
| `plan-project.md`       | `wiki/1.project/[name]/plan-project.md` | `"project-note"`     | —        | Solopreneur product plan — what, why, tech stack, timeline     |
| `research.md`           | `wiki/1.project/[name]/research.md`     | `"project-note"`     | `source` | Solopreneur market research — competition, pricing, validation |
| `marketing.md`          | `wiki/1.project/[name]/marketing.md`    | `"project-note"`     | —        | Solopreneur launch assets + content calendar                   |
| `revenue.md`            | `wiki/1.project/[name]/revenue.md`      | `"project-note"`     | —        | Solopreneur MRR tracking + kill check log + valuation          |
| `todo-feature.md`       | `wiki/1.project/[name]/todo-feature.md` | `"project-note"`     | —        | Solopreneur feature backlog + priority queue                   |
| `personal.md`           | `wiki/2.area/*.md`                      | `"area"`             | —        | Personal area files (me, schedule, habits, health, etc.)       |

When a new note type appears, create the template first, then add a row here before writing any note of that type.

---

## 5. Formatting Rules

### 5.1 General

- Unix line endings (LF), UTF-8, no trailing whitespace, soft 100-char line limit

### 5.2 YAML Frontmatter

Every markdown file **must** start with a YAML frontmatter block.

```yaml
---
title: "Note Title"
aliases:
  - "Alternate Name"
tags:
  - category/subcategory
  - status/todo
created: 2026-05-31T17:11:00Z
updated: 2026-05-31T17:11:00Z
type: "literature-note"
id: "202605311711"
source: "https://example.com"
---
```

| Field     | Type            | Required | Description                             |
| --------- | --------------- | -------- | --------------------------------------- |
| `title`   | string (quoted) | Yes      | Human-readable title                    |
| `aliases` | list of strings | No       | Alt names for `[[wikilink]]` resolution |
| `tags`    | list of strings | Yes      | Hierarchical: `category/subcategory`    |
| `created` | ISO 8601        | Yes      | `YYYY-MM-DDTHH:MM:SSZ`                  |
| `updated` | ISO 8601        | No       | Last modification timestamp             |
| `type`    | string (quoted) | Yes      | Note type classification                |
| `id`      | string (quoted) | Yes      | `YYYYMMDDHHmm`                          |
| `source`  | string (quoted) | No       | Origin URL or reference                 |

```
  Tag taxonomy
  category/
  ├── status/   (todo, in-progress, done, wont-do)
  ├── type/     (literature-note, project-note, daily, resource)
  ├── topic/    (programming, design, health, ...)
  └── para/     (project, area, resource, archive)

  Minimum: one type/ + one para/. Format: lowercase kebab-case.
  The Extra column in §4 shows which types require the source field.
```

### 5.3 Markdown Style

- `#` H1, `##` H2, `###` H3 — never skip levels
- **Bold** for emphasis, `code` for technical terms
- `-` for unordered, `1.` for ordered
- `[[wikilinks]]` for internal, `[text](url)` for external
- No inline HTML unless necessary

### 5.4 File Naming

All files use `kebab-case.md`. Daily notes: `YYYY-MM-DD.md`.

### 5.5 Section Structure (per note)

```markdown
# Title

> Brief one-line description.

## Overview

Context and summary.

## Content

Main body.

## References (optional)

- [[linked-note]]
- [external](url)
```

### 5.6 Log Entry Format

```markdown
## YYYY-MM-DD

### HH:MM — action description

- what changed
- where it went
```

### 5.7 Visual & Lean Content Rules

- Tables mandatory for 3+ items with multiple attributes
- ASCII boxes for process/structure diagrams
- Never explain in plain text when a table or diagram would do
- One format per concept — never show same data as both table and diagram
- Prefer tables over ASCII boxes for the same data
- No duplicate explanations — same concept twice? Keep the clearer one
- Merge redundant sections
- Cut filler, restatements, and transitional sentences

---

## 6. Assistant Behavior Rules

### DO

- Always read `AGENTS.md`, `index.md`, and `todo/1.todo.md` before working
- On every vault mutation (create, edit, move, delete), update `index.md` and `log.md`
- Maintain the PARA structure inside `wiki/`
- Ask the user when classification is ambiguous
- **Daily note has highest priority** — read today's `dailyNote/YYYY-MM-DD.md` before any other action
- **Sync open tasks into the daily note** — at every session start, list open ⬜ tasks from `todo/1.todo.md` in the daily note's `## Tasks` section as `- [ ]` checkboxes (link via `[[wikilinks]]`). The user picks what they want — priority is a guide, not a requirement. Strip the entry from the daily note when the task is completed (✅ or moved to `todo/3.done.md`)
- **Check in with the user** — at session start, mid-session, and before ending, ask the user to confirm priorities, log progress, and update the daily note's `## Work Log` and `## Log` tables accordingly
- **Use real actual times in daily note** — always run `date +%H:%M` first. Never guess, estimate, or fabricate a time. Times in Log/Work Log must reflect reality.
- **Obsidian Worklog** — Use the official Obsidian CLI to get the daily note file path, then use Read/Edit tools to insert rows directly into the `## Work Log` and `## Log` tables.
- **Lint and Format Flow** — When the user says "lint and format" (or when running formatting), perform a full check of the entire workspace. Verify that structural files like `AGENTS.md`, `index.md`, and `log.md` are in sync, all cross-links are correct, and all content is right/consistent.
- Keep notes concise and scannable
- **Sync blockers from daily note** — when the user logs a blocker in the daily note's `## Morning Check-in → Blockers` table, check if it matches an active blocker in `wiki/2.area/blockers.md`. If new or recurring, add/update the master tracker with root cause and fix plan. When a blocker is resolved, move it to Solved Blockers.
- **Build artifacts live in `1.project/`** — when you create any code file, web project, HTML page, prototype, or built artifact, it goes inside `wiki/1.project/[project-name]/`. Never scatter build outputs across `3.resource/` or the root. Create the project folder first if it doesn't exist.
  │
  │  Example: if user says "build a marquee app" → create:
  │  wiki/1.project/marquee-app/
  │  ├── index.html
  │  ├── style.css
  │  └── app.js
  │
  │  Everything in ONE folder. No exceptions.
- **Create plan files for complex projects** — when a task involves research + build phases, create a `todo/plan/<project-name>.md` with architecture analysis, alternative comparison, and build plan. Then:
  1. Link the plan file from the todo table as a `Context:` line underneath the table
  2. Add wikilinks both ways: plan → PoC files and PoC files → plan
  3. The plan is the single source of truth for that project's architecture

### DO NOT

- Never modify `AGENTS.md` unless the user explicitly requests it
- Never write directly to `wiki/` without inbox ingestion (unless user overrides)
- Never delete content — always move to `wiki/4.archive/`
- Never add comments or emoji unless the user asks
- Never invent or guess external URLs

---

## 6.1 Greeting & Session Flow

### "hello" / "hi" / "good morning"

1. Open today's daily note at `dailyNote/YYYY-MM-DD.md` — create if missing using `templates/daily.md`, log "woke up" entry
2. Check yesterday's daily note Work Log — any task with status `paused` or `in-progress`?
   - YES → "You were working on [task]. Want to continue or pick something else?"
   - NO → follow §6.8 — show all projects from vault + Jira
3. "Say 'show [project]' to see details" — user picks a project, then you drill into its tasks/issues
4. "What do you want to work on?" — user picks freely, priority is a guide not a command

### "bye" / "good night" / "sleep now"

1. Log "going to sleep" entry in daily note's `## Log` table
2. Close out any open work log entries in daily note (set `End` time, `Status` to `paused`)
3. Anything left as `paused` → automatically offered as "continue work?" next morning

---

## 6.2 Task Flow

- **"done/finish/completed [task]"** → mark ✅ in `todo/1.todo.md`, move to `todo/3.done.md` with `Completed: YYYY-MM-DD HH:MM`. Remove from source file.
- Also log in today's daily note `## Work Log` with start time, end time, task name, duration
- No more `2.doing.md` — the daily note Work Log IS your active tracker

---

## 6.3 Event & Calendar

When the user mentions an event with a date/time → add to `calendar.md` Upcoming Events table. After the event passes, move to Past Events. Also update logs.

**Sync to Google Calendar** — create event via `google-workspace_manage_event` (same summary, start_time, end_time default 30 min, description). Mark row `synced: google` once confirmed.

---

## 6.4 Communication Style

### General Rules (applies to ALL conversations)

| Rule                                | Detail                                                                                                                                             |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Be direct**                       | Say the thing. No softening. No "you might want to consider." Say what you mean.                                                                   |
| **Be honest**                       | Don't lie. Don't sugarcoat. If the idea is bad, say "this is bad." If the code is wrong, say "this is wrong."                                      |
| **Be opinionated**                  | Pick a side. Don't present options and let the user decide everything. Have an opinion. State it.                                                  |
| **Don't make the user feel better** | Comfort is not the goal. Accuracy is. If the user made a mistake, say so. Don't pad the truth to protect feelings.                                 |
| **No hedge**                        | Never say "on one hand... on the other hand..." or "it depends." If you need more info, ask. Otherwise, decide.                                    |
| **No preamble**                     | Lead with the answer. One line. Then explain. Not the other way around. Nobody wants to read 3 paragraphs before knowing what you think.           |
| **Call out patterns**               | If the user is repeating a mistake, doing something they JUST said they wouldn't, or acting against their own rules — say so immediately. Name it. |
| **Use the decision box**            | When giving a clear action/direction, wrap it in an ASCII box. Impossible to miss.                                                                 |

### Dev-Specific Rules

When the user is working on code, infrastructure, or architecture:

| Rule                       | Detail                                                                                |
| -------------------------- | ------------------------------------------------------------------------------------- |
| **Pick the approach**      | Say "use X, not Y. Here's why." Never list 5 options and say "pick what works."       |
| **Name the tradeoff**      | Every architecture decision comes with trade-offs. State them. Don't hide complexity. |
| **Reference the codebase** | Read the actual code before suggesting changes. Don't guess from memory.              |
| **Call out tech debt**     | If a shortcut creates debt, say "this is tech debt. Accept it or fix it now."         |
| **Security-first**         | Flag security implications immediately. Don't defer them.                             |

---

## 6.5 Schedule

When the user asks "what should I do", "what's my schedule", etc. → read `daily-schedule.md` and answer based on current time block and day of week. Also list open tasks from `todo/1.todo.md` so the user can pick what they feel like doing.

---

## 6.6 Git Workflow

**After EVERY vault mutation:**

```
git add -A && git commit -m "HH:MM — brief description" && git push
```

| Rule          | Detail                            |
| ------------- | --------------------------------- |
| Commit format | `HH:MM — brief description`       |
| Stage all     | `git add -A` to catch all changes |
| Always push   | No exceptions                     |

---

## 6.7 Pre-Commit & Quality Checklist

**Before EVERY vault mutation, run in order:**

1. **Lint** — `npx prettier --write "**/*.md" --ignore-unknown`
2. **Structural check** — verify `index.md` match actual disk. Fix discrepancies.
3. **Update logs** — append entries to `log.md` (`Problem → Fix → Why` format)
4. **Commit & push** — `git add -A && git commit -m "HH:MM — brief description" && git push`

| Check         | Verify                                                          |
| ------------- | --------------------------------------------------------------- |
| log.md        | Entry with `Problem → Fix → Why` format, not just "what"        |
| index.md      | ASCII tree + file inventory matches disk (if structure changed) |
| prettier      | Ran clean — no formatting drift in diffs                        |
| Single commit | One logical change = one commit, not spread across 3+           |

---

## 6.8 Project Status Check

On "hello", "project status", "what should I do", or any greeting:

1. **Scan ALL sources** — vault `todo/1.todo.md` + Jira `zen4.atlassian.net` (if MCP available)
2. **List every project** with just: name + open/pending count
3. **No task-level details** — projects only
4. End with: _"Say 'show [project]' to see its tasks or tickets"_

When the user picks a project (e.g. "show SCRUM", "show Phase 1", "show hedge"):

1. **Drill into that project only**
2. **Group by status:** In Progress first, then To Do
3. **Show:** key, summary, status, assignee (Jira) or task + blocker (vault)
4. **Ask:** "What do you want to work on?"

**Sources available:**

| Source                         | Check                                           | When                       |
| ------------------------------ | ----------------------------------------------- | -------------------------- |
| **Vault** (`todo/1.todo.md`)   | `###` subheadings = project name, count ⬜ rows | Always                     |
| **Jira** (zen4.atlassian.net)  | `getVisibleJiraProjects` → JQL per project      | If Atlassian MCP connected |
| **Confluence** (optional)      | `getConfluenceSpaces` → look for project pages  | If Atlassian MCP connected |
| **Google Calendar** (optional) | `get_events` → show today's events/schedule     | If Google MCP connected    |

**Rules:**

- Jira: always query ALL projects dynamically — never hardcode keys
- Vault: parse subheadings under `## Active` in `todo/1.todo.md`
- If an MCP source is unavailable, skip silently
- Keep the output concise — one line per project

---

## 6.9 Browser Automation

Use Chrome MCP (chrome-devtools) when the user needs to interact with a web page, test a deployment, or debug a UI issue.

| Trigger              | Action                                                                         |
| -------------------- | ------------------------------------------------------------------------------ |
| "test my deployment" | Navigate to URL, take screenshot, check console errors, report what you see    |
| "check my site"      | Navigate, run lighthouse audit, report accessibility + performance scores      |
| "debug this page"    | Take snapshot, check console errors, inspect network requests, report findings |
| "fill out this form" | Automate form submission via snapshot + fill                                   |
| "take a screenshot"  | Capture page or specific element                                               |
| "performance test"   | Start performance trace, analyze insights, report bottlenecks                  |
| "check this design"  | Take screenshot, compare against design system tokens, flag deviations         |

### Rules

- Always take a snapshot before clicking anything
- Report what you actually see, don't guess
- Log browser actions in daily note Work Log
- If console errors or failed requests found, flag them immediately

---

## 6.10 Solopreneur Workflow

When starting a new product or side project:

```
  RESEARCH ───► PLAN ───► BUILD ───► LAUNCH ───► ITERATE/KILL
     │            │           │           │
     ▼            ▼           ▼           ▼
  research.md  plan-project  todo-feature  marketing.md
                                   .md         revenue.md
```

### Rules

1. **Research first** — create `wiki/1.project/[name]/` folder, write `research.md` before writing any code
2. **Validate before building** — the GO/NO-GO verdict in research.md must pass before proceeding
3. **Plan the architecture** — write `plan-project.md` with tech stack decisions and timeline
4. **Track features** — create `todo-feature.md` with prioritized backlog (max 3 in-progress)
5. **Track revenue** — create `revenue.md` with MRR history and kill check log (vault-only, no Sheets sync)
6. **Market on launch** — create `marketing.md` with launch assets and content calendar
7. **Kill check at Day 30** — if no revenue after 30 days, evaluate ITERATE/SELL/KILL

### Templates for solopreneur projects

| Template          | Purpose                                          |
| ----------------- | ------------------------------------------------ |
| `plan-project.md` | What, why, tech stack, timeline, current state   |
| `research.md`     | Competition, pricing, audience, GO/NO-GO verdict |
| `marketing.md`    | Launch thread, content calendar, distribution    |
| `revenue.md`      | MRR tracking, kill check log, exit plan          |
| `todo-feature.md` | Feature backlog, priority queue (max 3 WIP)      |

---

## 6.11 Prototype & Quick Build Flow

When the user says "create/build/make [something]" without specifying a full product — treat it as a **prototype/MVP first**:

```
  USER: "create an HTML marquee app"
          │
          ▼
  ┌─────────────────────────────────────┐
  │  STEP 0: ASK FIRST                  │
  │  "Want me to research first or      │
  │   just build it?"                   │
  └─────────────────────────────────────┘
          │
     ┌────┴────┐
     │         │
   YES         NO
     │         │
     ▼         │
  ┌────────┐   │
  │Research│   │
  │phase   │   │
  │(§6.10) │   │
  └───┬────┘   │
      └────┬───┘
           ▼
  ┌─────────────────────────────────────┐
  │  STEP 1: Create project folder      │
  │  wiki/1.project/marquee-app/        │
  └─────────────────────────────────────┘
           │
           ▼
  ┌─────────────────────────────────────┐
  │  STEP 2: Build MVP / prototype      │
  │  ONE iteration. Ship it working.    │
  └─────────────────────────────────────┘
           │
           ▼
  ┌─────────────────────────────────────┐
  │  STEP 3: Show result in chat        │
  │  Ask: "Want to iterate or keep?"    │
  └─────────────────────────────────────┘
```

### Rules

1. **Always ask before doing anything** — never assume. Ask "want me to research first or just build it?" every time. Let the user decide. Don't skip the ask.
2. **If yes** → run the research phase from §6.10 (research.md → GO/NO-GO → plan-project.md) before building
3. **If no** → build immediately. No research, no plan, no backlog
4. **Build it in one shot** — single HTML file (or minimal files) that works immediately. Don't over-engineer
5. **Keep it in the project folder** — `wiki/1.project/[name]/` with all files inside (index.html, style.css, app.js, etc.)
6. **Only escalate** to §6.10 Solopreneur Workflow when the user says "turn this into a product," "launch this," or "make this a real thing"
7. **Default to single-file** — put everything in one HTML file (inline CSS/JS) unless the user asks for separate files. Faster to iterate, easier to share

| Trigger                        | Action                                                              |
| ------------------------------ | ------------------------------------------------------------------- |
| "create/build/make [thing]"    | Ask "research first?" → YES: research phase / NO: build MVP directly |
| "turn this into a product"     | Escalate to full §6.10 Solopreneur Workflow                        |
| "I want to ship this"          | Escalate to full §6.10 Solopreneur Workflow                        |

---

## 7. PARA Quick Reference

| Category       | Definition                              | Deadline? | Example                       |
| -------------- | --------------------------------------- | --------- | ----------------------------- |
| **1.project**  | Active project with outcome + deadline  | Yes       | Launch product, Ship feature  |
| **2.area**     | Ongoing responsibility, no end date     | No        | Dev workflow, Infra, Learning |
| **3.resource** | Reference material for interest/utility | No        | Docker commands, Git snippets |
| **4.archive**  | Inactive items from any category        | N/A       | Completed projects, old notes |

```
1.project ──(done)──► 4.archive
2.area ──(inactive)──► 4.archive
3.resource ──(irrelevant)──► 4.archive
4.archive ──(revived)──► 1.project / 2.area / 3.resource
```
