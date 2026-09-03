# Infrastructure Report

## 1. Environment Overview

| Item | Detail |
|---|---|
| Platform | Killercoda Playground — Ubuntu scenario (`killercoda.com/playgrounds/scenario/ubuntu`) |
| Access method | Browser-based terminal (Chrome), no local installation required |
| Session type | Time-limited sandbox (60-minute session timer shown in the UI) |
| Hostname | `ubuntu` |
| Date observed | August 13, 2026 |

Killercoda provisions a temporary, disposable Linux container/VM per session. The environment resets once the session timer expires, which is characteristic of a cloud-hosted, on-demand compute sandbox rather than a persistent server.

## 2. Operating System

Command used: `cat /etc/os-release`

| Field | Value |
|---|---|
| Name | Ubuntu |
| Pretty Name | Ubuntu 24.04.4 LTS |
| Version | 24.04.4 LTS (Noble Numbat) |
| Version ID | 24.04 |
| Codename | noble |
| ID_LIKE | debian |

Command used: `uname -r`

| Field | Value |
|---|---|
| Kernel version | 6.8.0-136-generic |

## 3. Compute Resources

Command used: `nproc`

| Resource | Value |
|---|---|
| CPU core(s) allocated | 1 vCPU |

This confirms the instance is a minimal/free-tier-style allocation, typical of sandbox or trial cloud environments rather than a production-grade VM.

## 4. Memory

Command used: `free -h`

| Type | Total | Used | Free | Shared | Buff/Cache | Available |
|---|---|---|---|---|---|---|
| Memory (RAM) | 1.9 Gi | 461 Mi | 794 Mi | 1.1 Mi | 815 Mi | 1.4 Gi |
| Swap | 1.0 Gi | 0 B | — | — | — | — |

Observations:
- The instance has roughly **2 GB of RAM**, with a matching **1 GB swap** partition configured as overflow.
- At the time of inspection, memory usage was light (~461 Mi used), leaving 1.4 Gi readily available.
- No swap was in use, indicating the workload was not memory-constrained during testing.

## 5. Storage

Command used: `df -TH`

| Filesystem | Type | Size | Used | Avail | Use% | Mounted on |
|---|---|---|---|---|---|---|
| tmpfs | tmpfs | 200M | 1.1M | 199M | 1% | /run |
| /dev/vda1 | ext4 | 20G | 5.8G | 14G | 30% | / |
| tmpfs | tmpfs | 998M | 87k | 998M | 1% | /dev/shm |
| tmpfs | tmpfs | 5.3M | 0 | 5.3M | 0% | /run/lock |
| /dev/vda16 | ext4 | 924M | 123M | 737M | 15% | /boot |
| /dev/vda15 | vfat | 110M | 6.4M | 103M | 6% | /boot/efi |

Observations:
- The root filesystem (`/dev/vda1`) is a **20 GB ext4 disk**, 30% utilized at the time of inspection — plenty of headroom remains.
- The `/dev/vda*` naming convention indicates a **virtio block device**, standard for KVM/QEMU-based virtualization — consistent with how most cloud providers (and container/VM sandboxes like Killercoda) present virtual disks to a guest OS.
- Separate `/boot` and `/boot/efi` partitions confirm the VM boots via UEFI with GRUB, a standard cloud VM boot configuration.
- tmpfs mounts (`/run`, `/dev/shm`, `/run/lock`) are RAM-backed and reset on reboot, as expected for an ephemeral sandbox.

## 6. Networking / Identity

Command used: `hostname`

| Field | Value |
|---|---|
| Hostname | ubuntu |

Note: `hostname -H` was attempted but is not a valid flag on this system's `hostname` implementation (usage/help output was returned instead). No further network-specific commands (`ip a`, `hostname -I`) were captured in this session.

## 7. Summary

This is a single-vCPU, ~2 GB RAM, 20 GB disk Ubuntu 24.04.4 LTS virtual machine, provisioned on demand through the Killercoda browser-based playground. Its specs are consistent with a lightweight, disposable cloud sandbox intended for short training/demo sessions rather than a production workload.
