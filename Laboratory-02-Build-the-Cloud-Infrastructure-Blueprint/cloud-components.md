# Cloud Components

This document identifies the core cloud computing components present (or represented) in the Killercoda Ubuntu playground environment used for this exercise, and briefly explains what each one does.

## 1. Compute
**What it is:** The processing capacity (CPU/vCPU) allocated to run the operating system and workloads.

**Observed in this environment:**
- 1 vCPU (`nproc` = 1)
- Ubuntu 24.04.4 LTS running as the guest OS
- Kernel 6.8.0-136-generic, `/dev/vda*` device naming — indicating a KVM/virtio-based virtual machine

This is the equivalent of an EC2 instance (AWS), a Compute Engine VM (GCP), or an Azure VM — a small, single-core sandbox instance.

## 2. Memory (RAM)
**What it is:** Volatile, high-speed working storage used while processes run.

**Observed in this environment:**
- 1.9 GiB total RAM
- 1.0 GiB swap configured as overflow when RAM is exhausted
- 461 MiB used, 1.4 GiB available at time of inspection

## 3. Storage
**What it is:** Persistent (or semi-persistent) disk space for the OS, applications, and data.

**Observed in this environment:**
- `/dev/vda1` — 20 GB ext4 root volume (main OS + data disk)
- `/dev/vda16` — dedicated `/boot` partition
- `/dev/vda15` — vfat `/boot/efi` partition (UEFI boot files)
- tmpfs mounts for `/run`, `/dev/shm`, `/run/lock` — RAM-backed, non-persistent

This mirrors how cloud providers separate boot/system volumes from data volumes (e.g., AWS EBS root + boot volumes).

## 4. Networking
**What it is:** Connectivity that lets the instance communicate internally and with the outside world.

**Observed in this environment:**
- Hostname `ubuntu` assigned to the instance
- Access delivered entirely through a browser-based terminal (no SSH key or local client needed), meaning Killercoda handles the network tunneling/proxying behind the scenes
- A session identity/URL (`killercoda.com/playgrounds/scenario/ubuntu`) that routes the user's browser session to the correct backend container/VM

## 5. Virtualization Layer
**What it is:** The layer that allows a single physical host to run many isolated guest systems.

**Observed in this environment:**
- Device naming (`vda`, `vda1`, `vda15`, `vda16`) is characteristic of **virtio** block devices used in **KVM/QEMU** virtualization — the same underlying technology used by most public cloud providers.

## 6. Operating System / Platform Layer
**What it is:** The software layer the user actually interacts with.

**Observed in this environment:**
- Ubuntu 24.04.4 LTS "Noble Numbat", kernel 6.8.0-136-generic — a standard long-term-support Linux distribution commonly offered as a base image across cloud providers.

## 7. Sandbox / Session Management (Killercoda-specific)
**What it is:** The orchestration layer that provisions, times out, and tears down the environment.

**Observed in this environment:**
- A visible countdown timer (54–60 minutes) in the Killercoda UI, confirming the instance is ephemeral and will be reclaimed automatically
- "Editor", "Scenarios", and "Ask/Help" panels alongside the terminal, indicating this is a managed learning environment layered on top of the raw VM

## Summary Table

| Component | Cloud Concept | Evidence in this Environment |
|---|---|---|
| Compute | vCPU / instance | `nproc` → 1 |
| Memory | RAM + swap | `free -h` → 1.9Gi RAM, 1.0Gi swap |
| Storage | Block/root volume | `df -TH` → 20G ext4 on `/dev/vda1` |
| Networking | Hostname/routing | `hostname` → ubuntu |
| Virtualization | Hypervisor | virtio `vda` device naming |
| OS/Platform | Guest OS image | Ubuntu 24.04.4 LTS |
| Orchestration | Session lifecycle | Killercoda timed playground session |
