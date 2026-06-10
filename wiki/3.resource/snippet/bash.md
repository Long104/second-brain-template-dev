---
title: "Bash Snippets"
aliases:
  - "shell scripts"
tags:
  - para/resource
  - topic/bash
  - status/active
created: 2026-06-09T14:39:00Z
updated: 2026-06-09T14:39:00Z
type: "snippet"
id: "202606091439"
source: ""
---

# Bash Snippets

> Reusable shell script patterns.

---

## Basics

### Snippet: Script Template

| Field       | Value                   |
| ----------- | ----------------------- |
| Description | Safe bash script header |
| When to use | Every new script        |

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

# Script name
SCRIPT_NAME=$(basename "$0")

# Colors
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

log_info()  { echo -e "${GREEN}[INFO]${NC}  $1"; }
log_warn()  { echo -e "${YELLOW}[WARN]${NC}  $1"; }
log_error() { echo -e "${RED}[ERROR]${NC} $1"; }

# Usage
usage() {
    echo "Usage: $SCRIPT_NAME [options]"
    echo "  -h    Show help"
    exit 1
}

while getopts "h" opt; do
    case $opt in
        h) usage ;;
        *) usage ;;
    esac
done
```

### Snippet: Loop Through Files

```bash
# Find and process markdown files
for file in wiki/**/*.md; do
    [ -f "$file" ] || continue
    echo "Processing: $file"
    # do something
done
```

---

## Patterns

### Pattern: Git Auto-Commit

```bash
#!/usr/bin/env bash
set -euo pipefail

BRANCH=$(git rev-parse --abbrev-ref HEAD)
MESSAGE="${1:-auto: update}"

git add -A
git commit -m "$(date +%H:%M) — $MESSAGE" || true
git push 2>/dev/null || echo "No remote configured"
```

### Pattern: Check Dependencies

```bash
# Check required CLIs are installed
check_deps() {
    local deps=("docker" "kubectl" "terraform")
    local missing=()

    for cmd in "${deps[@]}"; do
        if ! command -v "$cmd" &>/dev/null; then
            missing+=("$cmd")
        fi
    done

    if [ ${#missing[@]} -gt 0 ]; then
        log_error "Missing: ${missing[*]}"
        exit 1
    fi
    log_info "All dependencies found"
}
```

### Pattern: JSON API Call

```bash
# Fetch data from API with error handling
fetch_json() {
    local url="$1"
    local token="${API_TOKEN:-}"

    response=$(curl -s -w "\n%{http_code}" \
        -H "Authorization: Bearer $token" \
        "$url")

    http_code=$(echo "$response" | tail -1)
    body=$(echo "$response" | sed '$d')

    if [ "$http_code" -ne 200 ]; then
        log_error "API returned $http_code"
        echo "$body"
        return 1
    fi

    echo "$body"
}
```

---

## Utilities

### Utility: Backup a File

| Field       | Value                    |
| ----------- | ------------------------ |
| Description | Copy file with timestamp |
| Input       | File path                |
| Output      | `original.20260609.bak`  |

```bash
backup() {
    local file="$1"
    local ts
    ts=$(date +%Y%m%d)
    cp "$file" "${file}.${ts}.bak"
    log_info "Backed up to ${file}.${ts}.bak"
}
```

### Utility: Find Large Files

```bash
# Show top 10 largest files in current dir
find . -type f -not -path './.git/*' -exec ls -lh {} \; \
    | awk '{print $5, $NF}' \
    | sort -rh \
    | head -10
```

---

## Gotchas

| Issue                    | Cause                    | Fix                                                |
| ------------------------ | ------------------------ | -------------------------------------------------- | --- | --------------- | --- | ---------------- |
| `set -e` unexpected exit | Command returns non-zero | Use `                                              |     | true`or`command |     | log_error "msg"` |
| Variable unbound error   | `set -u` + undefined var | Use `${VAR:-default}` for optional vars            |
| IFS splitting spaces     | Word splitting on spaces | Set `IFS=$'\n\t'` at top                           |
| `rm -rf` disaster        | Empty variable in path   | Always check: `[[ -n "$DIR" ]] && rm -rf "$DIR"/*` |

---

## References

- [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html)
