# Virtualization vs. Containers

## Overview

Virtual machines (VMs) and containers are both technologies used to isolate applications and their dependencies from the underlying hardware, but they achieve this in fundamentally different ways.

## Virtual Machines

- A VM virtualizes an entire physical machine, including hardware, using a **hypervisor** (e.g., VMware, VirtualBox, Hyper-V, KVM).
- Each VM runs its own full **guest operating system** on top of the virtualized hardware.
- VMs are isolated at the hardware level, which provides strong security boundaries but comes with significant overhead.
- Startup time is typically measured in **minutes**, since a full OS has to boot.
- Resource usage (CPU, RAM, disk) is higher because each VM duplicates an entire OS stack.

## Containers

- Containers virtualize the **operating system** rather than the hardware, sharing the host machine's OS kernel.
- Each container packages an application with just its required libraries and dependencies, not a full OS.
- Isolation is achieved through OS-level features such as **namespaces** and **cgroups** (on Linux).
- Startup time is typically measured in **seconds or less**, since there's no OS to boot.
- Containers are lightweight, using far less disk space and memory than VMs, and many containers can run on a single host.
- Docker is the most widely used container platform, using images (like the `nginx` image) to create and run containers.

## Key Differences

| Aspect | Virtual Machines | Containers |
|---|---|---|
| Virtualizes | Hardware | Operating system |
| OS per instance | Full guest OS | Shares host kernel |
| Startup time | Minutes | Seconds |
| Resource footprint | Heavy | Lightweight |
| Isolation level | Strong (hardware-level) | Process-level |
| Portability | Less portable (larger images) | Highly portable |
| Typical use case | Running different OSes, strong isolation needs | Microservices, fast deployment, scaling |

## Why Containers for This Exercise

In this lab, Docker was used to pull and run an `nginx` container. Because containers share the host kernel and don't require booting a separate OS, the `nginx` image could be pulled, started, and serving traffic on port 8080 within seconds — something that would take considerably longer with a full VM running the same web server.
