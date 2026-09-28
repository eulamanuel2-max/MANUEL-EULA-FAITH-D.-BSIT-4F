# MinIO Deployment

## Deployment

The laboratory environment could not pull the `minio/minio:latest` image, so MinIO was built from source and packaged into a local Docker image named `minio-local`.

### Clone the MinIO Source

```bash
cd ~
git clone https://github.com/minio/minio.git
cd ~/minio
```

### Build the MinIO Server

The MinIO server was compiled using Go:

```bash
go build -o minio-server
```

### Local Dockerfile

```dockerfile
FROM ubuntu:24.04
COPY minio-server /usr/local/bin/minio
RUN chmod +x /usr/local/bin/minio
EXPOSE 9000 9001
ENTRYPOINT ["/usr/local/bin/minio"]
```

The Docker image was built with:

```bash
docker build -t minio-local -f Dockerfile.local .
```

## Docker Command Used

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server -e "MINIO_ROOT_USER=cloudadmin" -e "MINIO_ROOT_PASSWORD=CloudNova2026!" minio-local server /data --console-address ":9001"
```

The container was verified using:

```bash
docker ps
```

The container showed a running status and ports `9000` and `9001` mapped to the host.

## Web Console Port

The MinIO Web Console uses:

```text
9001
```

The API uses:

```text
9000
```

## Environment Variables

The `-e` flags define environment variables inside the container.

- `MINIO_ROOT_USER=cloudadmin` sets the administrator username.
- `MINIO_ROOT_PASSWORD=CloudNova2026!` sets the administrator password.

## Bucket

The required bucket name is:

```text
client-photos
```

The bucket is used to store the application's uploaded image objects.

## Note

The laboratory handout specifies `minio/minio` as the Docker image. Because that image could not be pulled in the lab environment, the actual deployment used a locally built MinIO image from the cloned source code. This file documents the method actually used.
