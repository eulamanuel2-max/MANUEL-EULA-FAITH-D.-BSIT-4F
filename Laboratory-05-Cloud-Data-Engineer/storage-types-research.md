# Storage Types Research: Block, File, and Object Storage

**Date:** September 28, 2026
**Hands-on component:** MinIO object storage deployed with Docker

---

## 1. Overview

Cloud and on-premises systems store data in three main ways: **block**, **file**, and **object** storage. They differ in how data is organized, how it is accessed, and what workloads they suit.

| Feature | Block Storage | File Storage | Object Storage |
|---|---|---|---|
| **Data unit** | Fixed-size blocks | Files in a folder hierarchy | Objects (data + metadata + unique ID) in a flat namespace |
| **Access method** | Raw disk via SAN protocols (iSCSI, Fibre Channel, NVMe-oF) | NFS, SMB/CIFS | HTTP REST API (S3-compatible) |
| **Performance** | Highest IOPS, lowest latency | Moderate | Higher latency, very high throughput at scale |
| **Scalability** | Limited by volume/array | Limited by file system/NAS | Virtually unlimited, scales horizontally |
| **Metadata** | Minimal | Basic (name, size, permissions, dates) | Rich, customizable per object |
| **Modification** | Edit individual blocks in place | Edit files in place | Objects are replaced as a whole (immutable, versioned) |
| **Typical cost** | Highest per GB | Medium | Lowest per GB |
| **Examples** | AWS EBS, Azure Disk, SAN arrays | AWS EFS, Azure Files, NAS | AWS S3, Azure Blob, MinIO, Ceph RGW |

---

## 2. Block Storage

Data is split into equal-sized blocks, each with its own address. The operating system sees a block device as a raw disk and formats it with its own file system.

**Strengths**
- Very low latency and high IOPS
- Fine-grained, in-place updates
- Can boot an operating system

**Weaknesses**
- Attaches to one server at a time in most setups
- No built-in metadata; the application or OS manages structure
- Costly at large scale

**Best for:** databases, virtual machine disks, transactional workloads, boot volumes.

---

## 3. File Storage

Data is organized as files inside directories and shared over a network. Users and applications navigate using paths.

**Strengths**
- Familiar hierarchy that is easy to understand
- Multiple clients can share the same files
- Built-in permissions and locking

**Weaknesses**
- Performance and scale degrade with very large directory trees
- Hierarchy adds metadata overhead
- Harder to scale out than object storage

**Best for:** shared drives, home directories, content management, development environments.

---

## 4. Object Storage

Data is stored as **objects** in **buckets**. Each object bundles the data, its metadata, and a unique key, and is accessed over HTTP through an API rather than mounted as a disk.

**Strengths**
- Massive scalability with a flat structure
- Rich, custom metadata
- Low cost, built-in durability (replication or erasure coding)
- Features such as versioning, lifecycle rules, and access policies

**Weaknesses**
- Not suited to frequent small in-place edits
- Higher latency than block storage
- Not a direct replacement for a POSIX file system

**Best for:** photos and videos, backups and archives, data lakes, static website assets, log storage.

---

## 5. Choosing the Right Type

| If the workload needs... | Choose |
|---|---|
| Lowest latency, database or VM disk | Block |
| Shared files with a folder structure | File |
| Huge volume of unstructured data, cheap and durable | Object |

For this scenario (storing **client photos**), object storage fits best: photos are unstructured, written once and read many times, benefit from metadata, and need to grow without a fixed capacity limit.

---

## 6. Hands-On: Deploying MinIO Object Storage

MinIO is an S3-compatible object storage server. It was deployed as a Docker container on an Ubuntu host.

### 6.1 Deployment command

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server \
  -e "MINIO_ROOT_USER=<admin-username>" \
  -e "MINIO_ROOT_PASSWORD=<strong-password>" \
  quay.io/minio/minio:RELEASE.2026-08-07T18-34-35Z server /data --console-address ":9001"
```

| Option | Purpose |
|---|---|
| `-d` | Run the container in the background |
| `-p 9000:9000` | S3 API port |
| `-p 9001:9001` | Web console port |
| `--name minio-server` | Container name |
| `MINIO_ROOT_USER` / `MINIO_ROOT_PASSWORD` | Root credentials for the console and API |
| `server /data` | Start MinIO, storing objects in `/data` inside the container |
| `--console-address ":9001"` | Serve the web console on port 9001 |

### 6.2 Verification

`docker ps` showed the `minio-server` container **Up**, with ports 9000 and 9001 mapped to the host on all interfaces.

### 6.3 Bucket and object

Using the MinIO Object Browser (Community Edition):

| Item | Value |
|---|---|
| Bucket name | `client-photos` |
| Created | Mon, Sep 28 2026, 10:55:25 (GMT+8) |
| Access policy | **Private** |
| Uploaded object | `minio-deployed.png` (76.8 KiB) |
| Bucket totals | 1 object, 76.8 KiB |

This confirms the object storage workflow: **create bucket → upload object → browse and manage via console or S3 API**.

---

## 7. Security Notes

- Root credentials were passed as plain environment variables. In production, use Docker secrets or a secrets manager, and avoid sharing them in screenshots or documents.
- Create dedicated users with least-privilege policies instead of using the root account for applications.
- Keep buckets **private** by default (as done here) and grant access through policies or pre-signed URLs.
- Put MinIO behind TLS (HTTPS), and restrict ports 9000/9001 with a firewall.
- Mount a persistent volume for `/data` (for example `-v /mnt/minio:/data`); without one, data is lost if the container is removed.

---

## 8. Conclusion

Block storage delivers speed for databases and VMs, file storage provides shared hierarchical access, and object storage offers scalable, low-cost, metadata-rich storage for unstructured data. The MinIO deployment demonstrates a working, S3-compatible object store holding a private `client-photos` bucket, a practical fit for storing client images.
