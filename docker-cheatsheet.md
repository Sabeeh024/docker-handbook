# Docker CLI Cheat Sheet

## 🐳 Container Management

### List running containers

```bash
docker ps
```

### List all containers (including stopped)

```bash
docker ps -a
```

### View container logs

```bash
docker logs <container_id or name>
```

### Start a stopped container

```bash
docker start <container_id or name>
```

### Stop a running container

```bash
docker stop <container_id or name>
```

### Restart a container

```bash
docker restart <container_id or name>
```

### Delete a container

```bash
docker rm <container_id or name>
```

### Run a container

```bash
docker run [OPTIONS] <image-name>
```

#### Common `docker run` options

| Option      | Description                                  | Example                                            |
| ----------- | -------------------------------------------- | ---------------------------------------------------|
| `-d`        | Run container in background (detached mode)  | `-d`                                               |
| `-p`        | Publish a container port to the host         | `-p 3000:3000`                                     |
| `--name`    | Assign a name to the container               | `--name my-app`                                    |
| `-v`        | Mount a volume (Named Volume)                | `-v <volume-name>:<container-mount-path> <image>`  |
| `-v`        | Mount a volume (Bind Volume)                 | `-v <host-path>:<container-mount-path> <image>`    |
| `--rm`      | Automatically remove container when it exits | `--rm`                                             |
| `-it`       | Run with interactive terminal                | `-it`                                              |

---

## 🛠️ Image Management

### List all images

```bash
docker images
```

### Build an image

```bash
docker build -t <image-name> <build-context>
```

#### Common `docker build` options

| Option          | Description                                  | Example                                   |
| --------------- | -------------------------------------------- | ----------------------------------------- |
| `-t` / `--tag`  | Name and optionally tag the image            | `-t my-app:latest`                        |
| `.` (context)   | Build context directory                      | `.`                                       |
| `-f` / `--file` | Specify Dockerfile path                      | `-f ./Dockerfile.dev`                     |
| `--build-arg`   | Pass build-time variables                    | `--build-arg NODE_ENV=production`         |
| `--secret`      | Mount secrets using BuildKit                 | `--secret id=envfile,src=.env.production` |

---

## 💾 Volume Management

### List all volumes

```bash
docker volume ls
```

### Inspect a volume

```bash
docker volume inspect <volume-name>
```

### Remove a volume

```bash
docker volume rm <volume-name>
```

### Prune (remove) all unused volumes

```bash
docker volume prune
```

---

## 🧹 System Cleanup

### Remove unused containers, networks, images, and build cache

```bash
docker system prune
```

### Remove **everything** unused (volumes included)

```bash
docker system prune -a --volumes
```

---

## 📦 Image Push & Pull

### Push image to Docker Hub

```bash
docker push <username>/<repo>:<tag>
```

### Pull image from Docker Hub

```bash
docker pull <username>/<repo>:<tag>
```

---

## 🐳 Miscellaneous

### Show container stats

```bash
docker stats
```

### Exec into running container

```bash
docker exec -it <container_id or name> /bin/sh
```

---
