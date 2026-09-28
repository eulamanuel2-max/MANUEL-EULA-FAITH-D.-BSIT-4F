# MinIO Deployment

**Date:** September 28, 2026
**Environment:** Ubuntu host, Docker
**Purpose:** Deploy an S3-compatible object storage server and store client photos in a private bucket.

---

## 1. Prerequisites

- Ubuntu host with root or sudo access
- Docker installed and running
- Ports **9000** (S3 API) and **9001** (web console) free and reachable

Check Docker:

```bash
docker --version
```

---

## 2. Deploy the Container

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server \
  -e "MINIO_ROOT_USER=<admin-username>" \
  -e "MINIO_ROOT_PASSWORD=<strong-password>" \
  quay.io/minio/minio:RELEASE.2026-08-07T18-34-35Z server /data --console-address ":9001"
```

| Option | Purpose |
|---|---|
| `-d` | Run in the background (detached) |
| `-p 9000:9000` | Expose the S3 API |
| `-p 9001:9001` | Expose the web console |
| `--name minio-server` | Name the container |
| `MINIO_ROOT_USER`, `MINIO_ROOT_PASSWORD` | Root credentials |
| `server /data` | Store objects under `/data` in the container |
| `--console-address ":9001"` | Serve the console on port 9001 |

Docker printed the new container ID (`4bd8a3137a36...`), confirming the container was created.

---

## 3. Verify the Container

```bash
docker ps
```

Result: container `minio-server` with status **Up**, mapping `0.0.0.0:9000-9001` and `[::]:9000-9001` to the container's ports 9000-9001.

---

## 4. Access the Web Console

Open `http://<server-ip>:9001` in a browser and sign in with the root credentials. The MinIO Object Store (Community Edition) Object Browser loads.

---

## 5. Create the Bucket

1. In the console, select **Create Bucket**.
2. Name it `client-photos`.
3. Create it.

Result:

| Property | Value |
|---|---|
| Name | `client-photos` |
| Created | Mon, Sep 28 2026, 10:55:25 (GMT+8) |
| Access | **Private** |

---

## 6. Upload an Object

1. Open the `client-photos` bucket.
2. Select **Upload** and choose a file.
3. Confirm it appears in the list.

Result:

| Object | Size | Last Modified |
|---|---|---|
| `minio-deployed.png` | 76.8 KiB | Today, 10:55 |

The bucket summary shows **1 object, 76.8 KiB**.

---

## 7. Useful Management Commands

```bash
docker logs minio-server        # view server logs
docker stop minio-server        # stop the server
docker start minio-server       # start it again
docker rm -f minio-server       # remove the container
```

> Objects live inside the container's `/data` directory. Without a volume mount, removing the container deletes the data.

---

## 8. Recommended Hardening

| Item | Recommendation |
|---|---|
| Persistence | Add `-v /mnt/minio-data:/data` to keep data outside the container |
| Credentials | Use a strong, unique root password stored in a secrets manager; do not reuse it or share it in screenshots |
| Users | Create least-privilege users and access keys for applications instead of using root |
| Transport | Enable TLS (HTTPS) or place MinIO behind a reverse proxy |
| Network | Firewall ports 9000 and 9001 to trusted IPs only |
| Access | Keep buckets private; use policies or pre-signed URLs to share objects |

---

## 9. Troubleshooting

| Symptom | Check |
|---|---|
| Console not loading | Confirm `docker ps` shows the container Up and port 9001 is open in the firewall |
| Port already in use | Stop the conflicting service or map different host ports (e.g. `-p 9100:9001`) |
| Login fails | Verify `MINIO_ROOT_USER` / `MINIO_ROOT_PASSWORD` values; password must be at least 8 characters |
| Container exits immediately | Run `docker logs minio-server` for the error |
