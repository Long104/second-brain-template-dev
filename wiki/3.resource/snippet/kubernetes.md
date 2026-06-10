---
title: "Kubernetes Snippets"
aliases:
  - "k8s manifests"
tags:
  - para/resource
  - topic/kubernetes
  - status/active
created: 2026-06-09T14:38:00Z
updated: 2026-06-09T14:38:00Z
type: "snippet"
id: "202606091438"
source: ""
---

# Kubernetes Snippets

> Reusable K8s manifest patterns.

---

## Basics

### Snippet: Deployment

| Field       | Value                          |
| ----------- | ------------------------------ |
| Description | Stateless app deployment       |
| When to use | Web apps, API servers, workers |

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: app
          image: myapp:latest
          ports:
            - containerPort: 3000
          resources:
            requests:
              cpu: 100m
              memory: 128Mi
            limits:
              cpu: 500m
              memory: 256Mi
          livenessProbe:
            httpGet:
              path: /health
              port: 3000
            initialDelaySeconds: 10
          readinessProbe:
            httpGet:
              path: /ready
              port: 3000
```

### Snippet: Service (ClusterIP)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 3000
  type: ClusterIP
```

### Snippet: Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  ingressClassName: nginx
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: myapp
                port:
                  number: 80
  tls:
    - hosts:
        - myapp.example.com
      secretName: myapp-tls
```

---

## Patterns

### Pattern: ConfigMap (env vars)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  NODE_ENV: production
  LOG_LEVEL: info
---
apiVersion: apps/v1
kind: Deployment
spec:
  template:
    spec:
      containers:
        - name: app
          envFrom:
            - configMapRef:
                name: app-config
```

### Pattern: PersistentVolumeClaim

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: data-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: standard
```

### Pattern: HorizontalPodAutoscaler

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
```

---

## Gotchas

| Issue                 | Cause                      | Fix                               |
| --------------------- | -------------------------- | --------------------------------- |
| Pod not starting      | Missing ConfigMap / Secret | Check `describe pod` for events   |
| Service not reachable | Selector mismatch          | Labels on pod must match selector |
| Ingress 404           | Wrong ingressClassName     | Check cluster ingress controller  |
| HPA not scaling       | Missing metrics server     | Install metrics-server            |

---

## References

- [K8s manifests reference](https://kubernetes.io/docs/concepts/)
