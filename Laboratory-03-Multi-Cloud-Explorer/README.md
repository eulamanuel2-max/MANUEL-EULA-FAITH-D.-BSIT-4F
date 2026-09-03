# Linux Investigation

## Environment
KillerCoda Playground (Linux VM)

## System Information

### Operating System
Command used: `cat /etc/os-release` (or `uname -a`)

```
[paste your terminal output here]
```

### CPU Information
Command used: `lscpu` (or `cat /proc/cpuinfo`)

```
[paste your terminal output here]
```

### Memory
Command used: `free -h`

```
[paste your terminal output here]
```

### Disk Space
Command used: `df -h`

```
[paste your terminal output here]
```

*(Insert screenshots of the terminal output for each command above.)*

## Reflection Question

**If this Linux server were migrated to the cloud, which AWS, Azure, and GCP services could host it?**

This Linux server's workload maps cleanly onto each provider's core virtual machine (IaaS) offering, since it's a general-purpose compute instance rather than a managed or serverless workload:

- **AWS** – Amazon **EC2** (Elastic Compute Cloud) would host the server directly. The instance type would be chosen to match the CPU/memory profile identified above (e.g., a `t3`/`t4g` instance for lightweight workloads, or an `m5`/`m6i` instance if more compute or memory is needed). EBS would provide the persistent disk storage.
- **Azure** – **Azure Virtual Machines** is the equivalent service, with a comparable VM size series (e.g., B-series for burstable/lightweight workloads, or D-series for general purpose) selected to match the same specs, backed by Azure Managed Disks for storage.
- **GCP** – **Compute Engine** would serve the same role, using an E2 (cost-optimized) or N2 (general purpose) machine type sized to the observed CPU and memory, with Persistent Disk for storage.

In all three cases, the migration would essentially be a "lift-and-shift": provision a VM with equivalent specs, attach comparable disk storage, and configure networking/security groups to match the current environment.
