---
title: "{{title}} — Terraform Guide"
aliases:
  - "{{alias}}"
tags:
  - para/resource
  - topic/terraform
  - topic/infrastructure-as-code
  - status/active
created: {{datetime}}Z
updated: {{datetime}}Z
type: "resource"
id: "{{id}}"
source: ""
---

# {{title}} — Terraform Guide

> Terraform modules, state management, providers, workflows, and IaC best practices.

---

## Overview

```
  ┌──────────────────────────────────────────────┐
  │           TERRAFORM GUIDE PROFILE             │
  ├──────────────┬───────────────────────────────┤
  │  TOPIC       │ {{title}}                     │
  │  CATEGORY    │ modules / state / providers / tfcloud │
  │  DIFFICULTY  │ beginner / intermediate / advanced  │
  └──────────────┴───────────────────────────────┘
```

---

## Core Concepts

| Concept | Description |
| ------- | ----------- |
|         |             |

---

## Module Structure

```
modules/
└── {{module-name}}/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    ├── versions.tf
    └── README.md
```

### Variables

```hcl
variable "{{name}}" {
  description = ""
  type        = string
  default     = ""
}
```

### Outputs

```hcl
output "{{name}}" {
  description = ""
  value       = module.{{module}}.{{output}}
}
```

---

## State Management

| Method          | Backend           | When to Use          |
| --------------- | ----------------- | -------------------- |
| Local           | local state file  | Local dev only       |
| S3              | AWS S3 + DynamoDB | Production (AWS)     |
| GCS             | GCS + bucket      | Production (GCP)     |
| Terraform Cloud | TF Cloud backend  | Teams / shared state |

---

## Providers

| Provider | Version | Purpose |
| -------- | ------- | ------- |
|          |         |         |

---

## Workflow

```
  terraform init ───► terraform plan ───► terraform apply
       │                 │                    │
       ▼                 ▼                    ▼
  Download deps    Preview changes     Apply to infra
```

---

## Gotchas

| Issue              | Cause | Fix                                    |
| ------------------ | ----- | -------------------------------------- |
| State lock         |       | `terraform force-unlock` (last resort) |
| Drift detection    |       | Review plan, apply with `-target`      |
| Destroy protection |       | Add `lifecycle { prevent_destroy }`    |

---

## References

- [[linked-note]]
