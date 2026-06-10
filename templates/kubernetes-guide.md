---
title: "{{title}} — Kubernetes Guide"
aliases:
  - "{{alias}}"
tags:
  - para/resource
  - topic/kubernetes
  - status/active
created: {{datetime}}Z
updated: {{datetime}}Z
type: "resource"
id: "{{id}}"
source: ""
---

# {{title}} — Kubernetes Guide

> Kubernetes manifests, RBAC, Helm charts, networking, debugging, and production patterns.

---

## Overview

```
  ┌──────────────────────────────────────────────┐
  │           KUBERNETES GUIDE PROFILE           │
  ├──────────────┬───────────────────────────────┤
  │  TOPIC       │ {{title}}                     │
  │  CATEGORY    │ manifests / rbac / helm / networking │
  │  DIFFICULTY  │ beginner / intermediate / advanced  │
  └──────────────┴───────────────────────────────┘
```

---

## Core Concepts

| Concept | Description |
| ------- | ----------- |
|         |             |

---

## Manifest Patterns

### Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name:
spec:
```

### Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name:
spec:
```

### Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name:
spec:
```

---

## RBAC

| Role | Resources | Verbs | Users |
| ---- | --------- | ----- | ----- |
|      |           |       |       |

---

## Helm Charts

| Chart | Repo | Purpose |
| ----- | ---- | ------- |
|       |      |         |

---

## Debugging

| Tool    | Command | Purpose |
| ------- | ------- | ------- |
| kubectl |         |         |
| k9s     |         |         |
| stern   |         |         |
| logs    |         |         |

---

## Gotchas

| Issue | Cause | Fix |
| ----- | ----- | --- |
|       |       |     |

---

## References

- [[linked-note]]
