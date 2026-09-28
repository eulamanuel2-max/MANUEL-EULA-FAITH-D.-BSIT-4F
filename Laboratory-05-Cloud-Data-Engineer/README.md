# MinIO Object Storage Lab

A short project exploring storage types and deploying **MinIO**, an S3-compatible object storage server, with Docker on Ubuntu. The deployment stores client photos in a private bucket.

## Project Structure

```
.
├── README.md                    # Project overview (this file)
├── storage-types-research.md    # Block vs. file vs. object storage
├── minio-deployment.md          # Step-by-step MinIO deployment record
└── reflection.md                # What was learned and what to improve
```

## Summary

| Item | Detail |
|---|---|
| Date | September 28, 2026 |
| Platform | Ubuntu with Docker |
| Software | MinIO Object Store (Community Edition) |
| S3 API port | 9000 |
| Web console port | 9001 |
| Container name | `minio-server` |
| Bucket | `client-photos` (private) |
| Test object | `minio-deployed.png` (76.8 KiB) |

## Quick Start

Replace the placeholder credentials with your own strong values:

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server \
  -e "MINIO_ROOT_USER=<admin-username>" \
  -e "MINIO_ROOT_PASSWORD=<strong-password>" \
  quay.io/minio/minio:RELEASE.2026-08-07T18-34-35Z server /data --console-address ":9001"
```

Verify it is running:

```bash
docker ps
```

Then open `http://<server-ip>:9001`, sign in, create the `client-photos` bucket, and upload a file.

## Documents

1. **[storage-types-research.md](storage-types-research.md)** compares block, file, and object storage and explains why object storage suits client photos.
2. **[minio-deployment.md](minio-deployment.md)** documents the deployment, bucket creation, upload, hardening, and troubleshooting.
3. **[reflection.md](reflection.md)** summarizes lessons learned, challenges, and next steps.

## Security Notes

- Never commit or share real credentials. Use placeholders in documentation and screenshots.
- Mount a volume for `/data` (e.g. `-v /mnt/minio-data:/data`) so objects survive container removal.
- Use least-privilege users instead of the root account, enable TLS, and firewall ports 9000 and 9001.
- Keep buckets private and share objects through policies or pre-signed URLs.

## Cleanup

```bash
docker rm -f minio-server
```

This removes the container. Data is deleted with it unless a volume was mounted.
