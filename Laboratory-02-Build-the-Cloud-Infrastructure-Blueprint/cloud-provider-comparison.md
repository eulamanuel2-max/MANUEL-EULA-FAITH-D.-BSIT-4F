# Cloud Provider Comparison

This document compares the platform used in this exercise (Killercoda) against the three major public cloud providers, to give context on where a browser-based sandbox fits relative to production cloud infrastructure.

## 1. Overview

| Provider | Type | Primary Use Case |
|---|---|---|
| **Killercoda** | Browser-based Linux sandbox / learning platform | Training, tutorials, quick experimentation |
| **Amazon Web Services (AWS)** | Full public cloud (IaaS/PaaS/SaaS) | Production workloads at any scale |
| **Microsoft Azure** | Full public cloud (IaaS/PaaS/SaaS) | Production workloads, strong enterprise/Windows integration |
| **Google Cloud Platform (GCP)** | Full public cloud (IaaS/PaaS/SaaS) | Production workloads, strong data/AI tooling |

## 2. Feature Comparison

| Feature | Killercoda | AWS | Azure | GCP |
|---|---|---|---|---|
| Setup required | None — opens instantly in browser | Account, billing, region/VPC setup | Account, billing, resource group setup | Account, billing, project setup |
| Persistence | Ephemeral (session expires, ~1 hour) | Persistent until terminated | Persistent until terminated | Persistent until terminated |
| Cost | Free | Pay-as-you-go (free tier available) | Pay-as-you-go (free tier available) | Pay-as-you-go (free tier available) |
| Scalability | None (fixed 1 vCPU / ~2 GB RAM sandbox) | Elastic (auto-scaling, thousands of instance types) | Elastic (auto-scaling, VM scale sets) | Elastic (auto-scaling, managed instance groups) |
| Networking control | None — managed automatically | Full (VPC, subnets, security groups, load balancers) | Full (VNet, NSGs, load balancers) | Full (VPC, firewall rules, load balancers) |
| Storage options | Single ephemeral disk (~20 GB) | EBS, S3, EFS, and more | Managed Disks, Blob Storage, Files | Persistent Disk, Cloud Storage, Filestore |
| Identity/access management | Not applicable (single-user sandbox) | IAM | Azure AD / Entra ID | Cloud IAM |
| Intended audience | Students, trainers, quick demos | Businesses, developers, enterprises | Businesses, developers, enterprises (esp. Windows/.NET shops) | Businesses, developers, data/ML-focused teams |
| Region/data-center choice | None | 30+ regions worldwide | 60+ regions worldwide | 40+ regions worldwide |

## 3. Key Takeaways

- **Killercoda is not a cloud provider in the commercial sense** — it's a *learning sandbox* that provisions temporary containers/VMs (likely on top of a real cloud backend) so users can practice Linux and DevOps skills without any setup, cost, or risk to real infrastructure.
- **AWS, Azure, and GCP** are full-scale public cloud platforms offering elastic compute, persistent storage, global networking, identity management, and hundreds of managed services (databases, AI/ML, containers, serverless, etc.) — the kind of infrastructure the Killercoda sandbox is *simulating a small piece of*.
- The specs observed in this exercise (1 vCPU, ~2 GB RAM, 20 GB disk) are comparable in size to the **smallest/free-tier instance types** on each major provider (e.g., AWS `t2.micro`/`t3.micro`, Azure `B1s`, GCP `e2-micro`), which is intentional — sandbox environments are typically sized to be "just enough" for a single learner's session.
- Real cloud providers add layers this sandbox does not need to expose: billing, IAM/security policy, region selection, auto-scaling, load balancing, and persistent storage lifecycle management.

## 4. Conclusion

Killercoda is best understood as a **disposable teaching front-end** for cloud/Linux concepts, while AWS, Azure, and GCP are the **actual infrastructure providers** businesses use to run production systems. The exercise in this environment (inspecting OS, CPU, memory, and disk via terminal commands) reflects the same fundamental building blocks — compute, memory, storage, and OS — that underpin any VM on any of the three major cloud platforms.
