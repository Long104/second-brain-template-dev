---
title: "Docker Snippets"
aliases:
  - "dockerfile patterns"
tags:
  - para/resource
  - topic/docker
  - status/active
created: 2026-06-09T14:38:00Z
updated: 2026-06-09T14:38:00Z
type: "snippet"
id: "202606091438"
source: ""
---

# Docker Snippets

> Reusable Dockerfile and Compose patterns.

---

## Basics

### Snippet: Node.js Dockerfile

| Field        | Value                             |
| ------------ | --------------------------------- |
| Description  | Multi-stage build for Node.js app |
| When to use  | Any Node.js/TypeScript project    |
| Dependencies | Node.js, npm/pnpm                 |

```dockerfile
# Build stage
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN corepack enable && pnpm install
COPY . .
RUN pnpm build

# Production stage
FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package.json .
EXPOSE 3000
USER node
CMD ["node", "dist/index.js"]
```

### Snippet: Python Dockerfile

| Field       | Value                                  |
| ----------- | -------------------------------------- |
| Description | Multi-stage for Python app             |
| When to use | FastAPI, Django, or any Python project |

```dockerfile
FROM python:3.12-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --user -r requirements.txt

FROM python:3.12-slim
WORKDIR /app
COPY --from=builder /root/.local /root/.local
COPY . .
ENV PATH=/root/.local/bin:$PATH
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Snippet: Docker Compose (Postgres + Redis + App)

```yaml
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      DATABASE_URL: postgres://user:pass@db:5432/mydb
      REDIS_URL: redis://redis:6379
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started

  db:
    image: postgres:16-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user"]
      interval: 5s

  redis:
    image: redis:7-alpine
    volumes:
      - redisdata:/data

volumes:
  pgdata:
  redisdata:
```

---

## Patterns

### Pattern: .dockerignore

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Description | Ignore files in Docker build context       |
| When to use | Every project (reduces build context size) |

```
node_modules
.git
.env
*.md
dist
.cache
coverage
```

### Pattern: Health Check

```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget --no-verbose --tries=1 --spider http://localhost:3000/health || exit 1
```

---

## Gotchas

| Issue                 | Cause                           | Fix                                         |
| --------------------- | ------------------------------- | ------------------------------------------- |
| Large image size      | No multi-stage / fat base       | Use `-alpine` or `-slim`, multi-stage build |
| Cache miss            | COPY order wrong                | Put `COPY package.json` before source code  |
| Permission denied     | Root user in container          | Add `USER node` or `USER nobody`            |
| .dockerignore missing | Secrets / node_modules in image | Always include `.dockerignore`              |

---

## References

- [Docker best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
