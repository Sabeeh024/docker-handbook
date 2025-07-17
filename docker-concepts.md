# Virtual Machines (VMs)

🖥️ A **Virtual Machine (VM)** is a software-based emulation of a physical computer. It behaves like a real computer, running an operating system (OS) and applications in an isolated virtual environment — all while sharing the physical resources of the underlying hardware.

Each VM runs on a **host machine** (the actual physical computer) and is managed by a **hypervisor** — a special software layer responsible for creating, running, and managing one or more VMs. Inside the VM, a separate **guest operating system** (like Windows or Linux) is installed and runs independently, as if it were on its own physical device.

---

# What is a Kernel?

🧠 The **kernel** is the core part of an operating system. It acts as a bridge between software (apps) and hardware (CPU, memory, storage, etc.).

- ⚙️ Manages hardware resources (CPU, RAM, I/O)
- 📅 Schedules tasks (decides which app runs when)
- 📞 Handles system calls (e.g., file read, memory allocation)
- 🔐 Enforces security and isolation between processes

---

# Docker Concepts

## What is Docker?

🐳 Docker is an open-source platform for building, packaging, and running applications in **containers** — lightweight, portable environments that include everything your app needs to run.\
Unlike virtual machines, containers share the host OS kernel, making them much faster and more resource-efficient.

## 🖼️ Image

A read-only template with everything your app needs: code, runtime, libraries, etc. Built from a `Dockerfile`.

## 📦 Container

A running instance of an image. A container is essentially a packaged runtime environment for your application, sharing the host OS kernel but running in its own isolated space.

---

## Docker Image & Container Layers

### 🔹 Image Layers (Read-Only)

- Each instruction in a Dockerfile creates a **new immutable/read-only layer**.
- Layers are:
  - 📚 **Stacked** during build
  - 🔒 **Immutable**
  - ♻️ **Shared** across containers/images
- All containers from the same image share these layers.

### 🔹 Container Layer (Writable)

- 🕒 Created at **runtime** when a container starts.
- ✏️ Captures all **filesystem changes**: create, modify, delete.
- 🗑️ Exists only for the **lifetime of the container**.
- 🔐 **Isolated per container**.

### 📁 Filesystem Layer Structure

```
Image Layers (read-only)
├── Base Image (e.g., node:alpine)
├── App dependencies
├── App source
├── Build output
└── [Container Layer] (read-write)
```

---

## Docker Layer Caching

🧠 Docker’s build process uses a layer cache to speed up rebuilds by avoiding unnecessary work.

### 🔹 Caching Behavior

- 🧱 Docker caches each **build instruction (layer)** to speed up future builds.
- 📂 If an instruction and its **context** (files, env) haven’t changed, Docker **reuses** the cached layer.
- ❌ Once a layer is **invalidated**, all **subsequent layers are rebuilt**.

#### 🧪 Example

```
FROM node:alpine
WORKDIR /app
COPY package.json .        # Cached if package.json unchanged
RUN yarn install           # Reused if package.json unchanged
COPY . .                   # Invalidate cache if any source file changes
```

---

### 🔹 Build Time

- 🔨 Happens during `docker build`
- 📄 Uses a `Dockerfile` to create an image
- 📦 Build time commands define how the image is created. ex: `FROM`, `COPY`, `RUN`.
- 🧊 Creates **read-only image layers**
- 🔧 Can use build arguments via `--build-arg`

### 🔹 Run Time

- 🚀 Happens during `docker run`
- 🏃 Starts a container from an image
- ✍️ Adds a **writable container layer**
- ⚙️ Run time commands define how the container runs from that image. ex: `CMD`, `ENTRYPOINT`, Options/flags used when starting a container like -e, -v, --entrypoint.
- 🌍 Can use environment variables via `-e`, mount volumes etc.

---

## Docker Storage Types

| Type           | Deleted with Container? | Persistent? | Managed by Docker |
| -------------- | ----------------------- | ----------- | ----------------- |
| **Bind Mount** | ❌ No                    | ✅ Yes       | ❌ No              |
| **Volume**     | ❌ No (unless pruned)    | ✅ Yes       | ✅ Yes             |

---

## Docker Volumes

### 🔹 What Are Volumes?

💾 Volumes are persistent storage mechanisms **managed by Docker**.\
They store data **independent of the container lifecycle**, allowing durability and portability.

### 🔸 Types of Volumes

| Type              | Description                                                                 |
| ----------------- | --------------------------------------------------------------------------- |
| **Named Volumes** | Docker-managed volumes identified by name. Docker manages storage location. |
| **Bind Mounts**   | Maps a **host path** into the container. Not managed by Docker.             |

---

## Docker Multi-Stage Builds

### 🔹 What Are Multi-Stage Builds?

🧰 Multi-stage builds help separate build-time dependencies (like compilers, bundlers) from the final runtime image.

### ✅ Benefits

- 📦 Produces **smaller, cleaner images**
- 🧹 Keeps **build dependencies** out of production
- 🔐 Improves **security** and **performance**
- 🗂️ Makes Dockerfiles easier to **organize and maintain**

#### 🧪 Example

```
# Stage 1: Build
FROM node:18-alpine AS builder
WORKDIR /app
COPY . .
RUN yarn build

# Stage 2: Serve
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
```

