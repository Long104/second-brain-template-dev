---
title: "Kubernetes Commands"
aliases:
  - "kubectl commands"
tags:
  - para/resource
  - topic/kubernetes
  - status/active
created: 2026-06-09T14:36:00Z
updated: 2026-06-09T14:36:00Z
type: "command"
id: "202606091436"
source: ""
---

# Kubernetes Commands

> Quick reference for kubectl and K8s CLI tools.

---

## Basic

| Command                       | Description                  | Example                         |
| ----------------------------- | ---------------------------- | ------------------------------- |
| `kubectl get pods`            | List pods                    | `kubectl get pods -n <ns>`      |
| `kubectl get services`        | List services                | `kubectl get svc`               |
| `kubectl get nodes`           | List nodes                   | `kubectl get nodes -o wide`     |
| `kubectl get all`             | Show everything in namespace | `kubectl get all -n default`    |
| `kubectl describe <resource>` | Detailed info                | `kubectl describe pod <name>`   |
| `kubectl logs <pod>`          | View pod logs                | `kubectl logs -f <pod>`         |
| `kubectl apply -f <file>`     | Create/update from file      | `kubectl apply -f deploy.yaml`  |
| `kubectl delete -f <file>`    | Delete from file             | `kubectl delete -f deploy.yaml` |

---

## Intermediate

| Command                | Flags         | Description               | Example                                       |
| ---------------------- | ------------- | ------------------------- | --------------------------------------------- |
| `kubectl port-forward` | —             | Forward local port to pod | `kubectl port-forward svc/myapp 8080:80`      |
| `kubectl exec`         | `-it`         | Run command in pod        | `kubectl exec -it <pod> -- sh`                |
| `kubectl top`          | —             | Resource usage            | `kubectl top pods`                            |
| `kubectl rollout`      | `status/undo` | Manage deployments        | `kubectl rollout status deploy/<name>`        |
| `kubectl set image`    | —             | Update image              | `kubectl set image deploy/myapp app=myapp:v2` |
| `kubectl config`       | `use-context` | Switch clusters           | `kubectl config use-context prod`             |
| `helm install`         | —             | Install Helm chart        | `helm install myapp ./chart`                  |
| `k9s`                  | —             | TUI dashboard             | just run `k9s`                                |

---

## Common Workflows

```
  APPLY ──► ROLLOUT ──► LOGS ──► PORT-FORWARD
```

| Step   | Command                                  | Purpose                 |
| ------ | ---------------------------------------- | ----------------------- |
| Deploy | `kubectl apply -f deploy.yaml`           | Create/update resources |
| Check  | `kubectl rollout status deploy/myapp`    | Wait for rollout        |
| Debug  | `kubectl logs -f deploy/myapp`           | Follow logs             |
| Access | `kubectl port-forward svc/myapp 8080:80` | Local access            |

---

## Gotchas

| Issue            | Cause                        | Fix                                  |
| ---------------- | ---------------------------- | ------------------------------------ |
| Pod pending      | No resources / PVC not bound | `kubectl describe pod <name>`        |
| ImagePullBackOff | Wrong image / no pull secret | Check image tag + registry auth      |
| CrashLoopBackOff | App crashes on start         | `kubectl logs <pod>` — check startup |
| Context wrong    | Wrong cluster selected       | `kubectl config current-context`     |

---

## References

- [kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
