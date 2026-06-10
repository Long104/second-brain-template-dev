---
title: "Terraform Commands"
aliases:
  - "terraform cli"
tags:
  - para/resource
  - topic/terraform
  - status/active
created: 2026-06-09T14:37:00Z
updated: 2026-06-09T14:37:00Z
type: "command"
id: "202606091437"
source: ""
---

# Terraform Commands

> Quick reference for Terraform CLI.

---

## Basic

| Command                | Description             | Example                      |
| ---------------------- | ----------------------- | ---------------------------- |
| `terraform init`       | Init working directory  | `terraform init`             |
| `terraform plan`       | Preview changes         | `terraform plan -out=tfplan` |
| `terraform apply`      | Apply changes           | `terraform apply tfplan`     |
| `terraform destroy`    | Destroy resources       | `terraform destroy`          |
| `terraform fmt`        | Format code             | `terraform fmt -recursive`   |
| `terraform validate`   | Validate configs        | `terraform validate`         |
| `terraform output`     | Show outputs            | `terraform output`           |
| `terraform state list` | List resources in state | `terraform state list`       |

---

## Intermediate

| Command               | Flags             | Description                     | Example                                    |
| --------------------- | ----------------- | ------------------------------- | ------------------------------------------ |
| `terraform workspace` | `new/select/list` | Manage workspaces               | `terraform workspace new prod`             |
| `terraform state mv`  | —                 | Move resource in state          | `terraform state mv module.old module.new` |
| `terraform state rm`  | —                 | Remove from state (not destroy) | `terraform state rm <address>`             |
| `terraform import`    | —                 | Import existing resource        | `terraform import aws_bucket.b my-bucket`  |
| `terraform taint`     | —                 | Mark for recreation             | `terraform taint <address>`                |
| `terraform plan`      | `-destroy`        | Preview destroy                 | `terraform plan -destroy`                  |
| `terraform apply`     | `-auto-approve`   | Skip confirmation               | `terraform apply -auto-approve`            |
| `tofu`                | same flags        | OpenTofu drop-in                | `tofu plan` (same as terraform)            |

---

## Common Workflows

```
  CODE ──► INIT ──► PLAN ──► APPLY ──► VERIFY
```

| Step    | Command                      | Purpose              |
| ------- | ---------------------------- | -------------------- |
| Init    | `terraform init`             | Install providers    |
| Preview | `terraform plan -out=tfplan` | Check changes        |
| Apply   | `terraform apply tfplan`     | Execute changes      |
| Verify  | `terraform output`           | Check outputs        |
| Clean   | `terraform destroy`          | Tear down (dev only) |

```
  STATE RECOVERY (when state is corrupt or lost)
```

| Step    | Command                        | Purpose            |
| ------- | ------------------------------ | ------------------ |
| List    | `terraform state list`         | See what's tracked |
| Inspect | `terraform state show <addr>`  | See details        |
| Import  | `terraform import <addr> <id>` | Re-import          |
| Fix     | `terraform state rm <addr>`    | Remove bad entry   |

---

## Gotchas

| Issue               | Cause                   | Fix                                              |
| ------------------- | ----------------------- | ------------------------------------------------ |
| State locked        | Another process running | `terraform force-unlock <lock-id>`               |
| Provider not found  | Not initialized         | Run `terraform init`                             |
| Drift detected      | Manual changes to infra | `terraform plan` catches it, apply to reconcile  |
| Sensitive in output | Values marked sensitive | Use `terraform output -json` or `nonsensitive()` |

---

## References

- [Terraform CLI docs](https://developer.hashicorp.com/terraform/cli/commands)
