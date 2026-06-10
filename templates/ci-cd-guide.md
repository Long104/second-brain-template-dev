---
title: "{{title}} — CI/CD Guide"
aliases:
  - "{{alias}}"
tags:
  - para/resource
  - topic/ci-cd
  - topic/devops
  - status/active
created: {{datetime}}Z
updated: {{datetime}}Z
type: "resource"
id: "{{id}}"
source: ""
---

# {{title}} — CI/CD Guide

> Pipeline patterns, GitHub Actions workflows, deployment strategies, and CI/CD best practices.

---

## Overview

```
  ┌──────────────────────────────────────────────┐
  │              CI/CD GUIDE PROFILE               │
  ├──────────────┬───────────────────────────────┤
  │  PLATFORM    │ {{platform}}                   │
  │  TOOL        │ {{tool}}                       │
  │  STRATEGY    │ {{strategy}}                   │
  └──────────────┴──────────────────────────────┘
```

---

## Pipeline Stages

```
  ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
  │  LINT    │──►│   TEST   │──►│  BUILD   │──►│ DEPLOY   │
  │           │   │          │   │          │   │          │
  └──────────┘   └──────────┘   └──────────┘   └──────────┘
```

| Stage  | Purpose             | Tools / Actions              |
| ------ | ------------------- | ---------------------------- |
| Lint   | Code quality        | ESLint, Prettier, ShellCheck |
| Test   | Verify correctness  | pytest, jest, go test        |
| Build  | Compile / package   | Docker build, npm build      |
| Deploy | Ship to environment | kubectl apply, AWS deploy    |

---

## GitHub Actions Patterns

### Basic Workflow

```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: "20"
      - run: npm ci
      - run: npm test
```

### Deployment Workflow

```yaml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: ./deploy.sh
```

---

## Deployment Strategies

| Strategy   | Description                  | Downtime | Rollback  |
| ---------- | ---------------------------- | -------- | --------- |
| Blue/Green | Two identical environments   | None     | Instant   |
| Canary     | Gradual traffic shift        | None     | Automatic |
| Rolling    | Replace instances one by one | None     | Automatic |
| Big Bang   | Replace all at once          | Yes      | Manual    |

---

## Secrets Management

| Tool           | Where              | How                   |
| -------------- | ------------------ | --------------------- |
| GitHub Secrets | CI/CD pipelines    | `secrets.REPO_SECRET` |
| Vault          | Production secrets | HashiCorp Vault       |
| SSM            | AWS secrets        | AWS Systems Manager   |

---

## Gotchas

| Issue | Cause | Fix |
| ----- | ----- | --- |
|       |       |     |

---

## References

- [[linked-note]]
