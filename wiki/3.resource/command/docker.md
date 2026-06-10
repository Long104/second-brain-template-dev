---
title: "Docker Commands"
aliases:
  - "docker cli"
tags:
  - para/resource
  - topic/docker
  - status/active
created: 2026-06-09T14:35:00Z
updated: 2026-06-09T14:35:00Z
type: "command"
id: "202606091435"
source: ""
---

# Docker Commands

> Quick reference for Docker CLI.

---

## Basic

| Command               | Description             | Example                          |
| --------------------- | ----------------------- | -------------------------------- |
| `docker ps`           | List running containers | `docker ps -a` (all)             |
| `docker images`       | List images             | `docker images -a`               |
| `docker pull <image>` | Download an image       | `docker pull nginx:alpine`       |
| `docker run <image>`  | Run a container         | `docker run -d -p 8080:80 nginx` |
| `docker stop <id>`    | Stop a container        | `docker stop $(docker ps -q)`    |
| `docker rm <id>`      | Remove a container      | `docker rm -f <id>`              |
| `docker rmi <image>`  | Remove an image         | `docker rmi <id>`                |
| `docker logs <id>`    | View logs               | `docker logs -f <id>` (follow)   |

---

## Intermediate

| Command               | Flags          | Description                      | Example                          |
| --------------------- | -------------- | -------------------------------- | -------------------------------- |
| `docker exec`         | `-it`          | Run command in running container | `docker exec -it <id> sh`        |
| `docker build`        | `-t`           | Build image from Dockerfile      | `docker build -t myapp:latest .` |
| `docker compose up`   | `-d`           | Start services from compose file | `docker compose up -d`           |
| `docker compose down` | `-v`           | Stop + remove volumes            | `docker compose down -v`         |
| `docker cp`           | —              | Copy files to/from container     | `docker cp <id>:/app/logs ./`    |
| `docker stats`        | —              | Live resource usage              | `docker stats`                   |
| `docker system prune` | `-a --volumes` | Clean unused data                | `docker system prune -af`        |

---

## Common Workflows

```
  BUILD ──► TAG ──► PUSH ──► DEPLOY
```

| Step  | Command                               | Purpose          |
| ----- | ------------------------------------- | ---------------- |
| Build | `docker build -t myapp:1.0 .`         | Build image      |
| Tag   | `docker tag myapp:1.0 user/myapp:1.0` | Tag for registry |
| Push  | `docker push user/myapp:1.0`          | Push to registry |
| Run   | `docker compose up -d`                | Deploy locally   |

---

## Gotchas

| Issue                       | Cause                 | Fix                                             |
| --------------------------- | --------------------- | ----------------------------------------------- |
| Permission denied           | docker socket         | `sudo usermod -aG docker $USER` (then re-login) |
| Disk full                   | unused images/volumes | `docker system prune -af --volumes`             |
| Container exits immediately | process ends          | Use `-it` or `CMD` that stays alive             |
| Compose command not found   | old Docker            | `docker compose` (v2) vs `docker-compose` (v1)  |

---

## References

- [Docker CLI docs](https://docs.docker.com/engine/reference/commandline/cli/)
