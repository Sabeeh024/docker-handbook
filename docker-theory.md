# Problems Before Virtualization

Before virtualization, physical servers had several major drawbacks:

- **Low Resource Utilization**  
  - Most servers used less than 20% of their capacity.  
  - → Wasted hardware and higher operating costs.

- **High Hardware Costs**  
  - Each app needed a separate physical machine.  
  - → Increased spending on hardware, power, and maintenance.

- **Inflexible and Hard to Scale**  
  - Adding environments required new hardware setups.  
  - → Slow provisioning and expensive scaling.

- **Poor Isolation**  
  - Multiple apps on one OS often caused version or dependency conflicts.  
  - → One crash could affect the whole system.

- **Difficult Disaster Recovery**  
  - Full machine backups and restores were slow and complex.  
  - → Higher risk of downtime and data loss.

- **Development & Testing Issues**  
  - Developers shared systems with inconsistent setups.  
  - → “Works on my machine” bugs in production.

---

# Virtual Machines (VMs)

A **Virtual Machine (VM)** is a software-based emulation of a physical computer. It behaves like a real computer, running an operating system (OS) and applications in an isolated virtual environment — all while sharing the physical resources of the underlying hardware.

Each VM runs on a **host machine** (the actual physical computer) and is managed by a **hypervisor** — a special software layer responsible for creating, running, and managing one or more VMs. Inside the VM, a separate **guest operating system** (like Windows or Linux) is installed and runs independently, as if it were on its own physical device.

**Hypervisors come in two main types:**

- **Type 1: Bare-Metal**  
  Runs directly on physical hardware (no host OS). Offers high performance and is commonly used in servers and data centers.

- **Type 2: Hosted**  
  Runs on top of an existing operating system. Easier to set up for personal use or testing, but slightly slower due to the extra OS layer.

---

## Advantages of Virtual Machines

- **Isolation**: Each VM runs independently — issues in one don't affect others.
- **Security**: VMs are sandboxed; one VM can’t easily interfere with another.
- **Resource Control**: Allocate specific CPU, memory, and storage to each VM.
- **Snapshot & Restore**: Save VM state and revert when needed.

---

## Disadvantages of Virtual Machines

- **Overhead**: Uses more CPU, memory, and disk compared to lighter alternatives like containers.
- **Performance**: Slower than running directly on hardware or using containers.
- **Boot Time**: Takes longer to start up than containers.

---

# Problems with Virtual Machines

While VMs are powerful, they come with several limitations:

- **Performance Overhead**: Each VM runs a full OS, consuming more CPU, memory, and storage than necessary.

- **Slow Boot Time**: VMs take longer to start because they load an entire operating system.

- **Storage-Heavy**: Every VM includes a full OS image, quickly using up disk space.

- **Fixed Resource Allocation**: Resources are pre-allocated and can’t be easily shared between idle and active VMs.

- **Complex Management**: Managing updates, patches, and configurations across many VMs is time-consuming.

- **Misconfiguration Risks**: Poor security setups can lead to vulnerabilities like VM escape attacks.

- **Not Ideal for Microservices**: VMs are too heavy for fast-scaling, cloud-native workloads—containers are preferred.

- **Licensing Costs**: Each VM may require its own OS license, increasing overall cost.

- **Hardware Requirements**: Efficient virtualization needs hardware support like Intel VT-x or AMD-V.

- **Limited Portability**: VM images are large and often tied to specific platforms, making migration harder.

--- 

# What is a Kernel?
The **kernel** is the core part of an operating system. It acts as a bridge between software (apps) and hardware (CPU, memory, storage, etc.).

- Manages hardware resources (CPU, RAM, I/O)
- Schedules tasks (decides which app runs when)
- Handles system calls (e.g., file read, memory allocation)
- Enforces security and isolation between processes

# What is Docker?

Docker is an open-source platform that lets you build, package, and run applications in containers — lightweight, portable environments that keep everything your app needs in one place.

Each container includes your app, along with its dependencies like libraries, runtimes(the software that knows how to run your code), and config files, so it works the same across all environments — from development to production.

Unlike virtual machines, Docker containers share the host system’s operating system kernel, making them faster and more efficient.

A high-level view of how Docker transforms your app code into a running container:

```
[Your App Code]
       ↓
[Dockerfile] ← instructions to build the image
       ↓
[Docker Image] ← frozen blueprint of your app
       ↓
[Docker Container] ← live, running instance of the image
```
---

## Core Docker Concepts

- **Image**  
  A read-only template with everything your app needs: code, runtime, libraries, etc. Built from a `Dockerfile`.

- **Container**  
  A running instance of an image. A container is essentially a packaged runtime environment for your application, sharing the host OS kernel but running in its own isolated space.

- **Dockerfile**  
  A script that defines how to build an image step-by-step (install packages, copy files, etc.).

- **Layer**  
  Each Dockerfile instruction adds a layer to the image. Layers are cached and reused to speed up builds.

- **Volume**  
  Persistent storage that lives outside the container — useful for storing data that shouldn't be lost.

- **Network**  
  Virtual network allowing containers to communicate with each other or with the host.

- **Docker Engine**  
  The Docker runtime responsible for building, running, and managing containers on your machine.

- **Registry**  
  A storage and distribution system for Docker images (e.g., Docker Hub, private registry).

- **Build Context**  
  The files and folders sent to Docker when building an image — typically the contents of your project directory.

- **Port Mapping**  
  Define which internal container ports are made available to the host machine or other containers.

---

## Features of Docker

- **Containerization**  
  Packages applications and their dependencies into isolated environments that run consistently across platforms.

- **Docker Images**  
  Immutable, lightweight templates used to create containers. Built from `Dockerfile`s and support versioning and reuse.

- **Portability**  
  Containers run the same on any system with Docker — local machine, server, or cloud.

- **Layered Filesystem**  
  Each image is made of layers that are cached and reused, making builds efficient and faster.

- **Isolation**  
  Containers run independently, preventing conflicts between applications and environments.

- **Volume Management**  
  Use volumes to persist data outside the container’s lifecycle (e.g., for databases or file uploads).

- **Built-in Networking**  
  Docker provides networking that allows containers to talk to each other and expose ports to your host machine.

- **Docker Hub / Registry**  
  Share and store images in public or private registries like Docker Hub, GitHub Container Registry, or your own.

- **Fast Boot Times**  
  Containers start in seconds, enabling faster development, testing, and scaling.

