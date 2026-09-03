# Cloud Infrastructure Exploration — Ubuntu Playground (Killercoda)

## Overview

This mini-lab explores the underlying infrastructure of a browser-based Ubuntu sandbox provisioned through [Killercoda](https://killercoda.com/playgrounds/scenario/ubuntu). Using standard Linux commands, the OS, CPU, memory, and storage of the provisioned environment were inspected and documented, then compared conceptually against major public cloud providers.

## Environment Snapshot

| Item | Value |
|---|---|
| Platform | Killercoda — Ubuntu Playground |
| OS | Ubuntu 24.04.4 LTS (Noble Numbat) |
| Kernel | 6.8.0-136-generic |
| vCPU | 1 |
| RAM | 1.9 GiB (+ 1.0 GiB swap) |
| Disk | 20 GB ext4 root volume (30% used) |
| Hostname | ubuntu |

## Commands Used

```bash
cat /etc/os-release   # OS identity and version
uname -r              # Kernel version
nproc                 # Number of CPU cores
free -h                # Memory and swap usage
df -TH                 # Disk/filesystem usage
hostname                # Instance hostname
```

## Files in This Report

| File | Contents |
|---|---|
| `infrastructure-report.md` | Detailed, command-by-command breakdown of the environment's OS, CPU, memory, storage, and networking |
| `cloud-components.md` | Maps what was observed to core cloud computing building blocks (compute, storage, memory, networking, virtualization, orchestration) |
| `cloud-provider-comparison.md` | Compares this sandbox against AWS, Azure, and GCP |
| `reflection.md` | Personal reflection on the exercise and what it demonstrated about cloud infrastructure |

## How to Reproduce

1. Go to `killercoda.com/playgrounds/scenario/ubuntu`.
2. Wait for the terminal session to initialize (session is time-limited, ~60 minutes).
3. Run the commands listed above in order.
4. Record the output for your own report — actual figures (memory used, disk usage %) may vary slightly between sessions since each session provisions a fresh instance.
