# Reflection

**Date:** September 28, 2026
**Topic:** Storage types and deploying MinIO object storage

---

## What I Did

I researched the three main storage types (block, file, and object) and then deployed MinIO, an S3-compatible object storage server, in a Docker container on Ubuntu. I created a private bucket called `client-photos` and uploaded a test image to confirm it worked.

## What I Learned

- **Each storage type has a clear purpose.** Block storage is for speed and databases, file storage is for shared folders, and object storage is for large amounts of unstructured data like photos and backups.
- **Object storage works differently from a disk.** Data lives in buckets as objects with metadata and is reached through an HTTP API instead of being mounted like a drive.
- **Docker makes deployment fast.** One `docker run` command started a working storage server, and `docker ps` confirmed it was running.
- **Port mapping matters.** Port 9000 serves the API and 9001 serves the console, and both had to be exposed to reach the service.

## Challenges

- Understanding what each part of the long `docker run` command does, especially the environment variables and the `--console-address` flag.
- Realizing that data stored in the container is lost if the container is removed unless a volume is mounted.
- Recognizing that credentials typed into a command or shown in a screenshot are exposed, which is a security risk.

## Why Object Storage Fits Client Photos

Photos are unstructured, written once and read many times, and the collection keeps growing. Object storage scales without a fixed capacity, costs less per GB, supports metadata, and lets me keep the bucket private and share files through controlled access.

## What I Would Improve Next Time

1. Mount a persistent volume for `/data`.
2. Create a dedicated user with limited permissions instead of using the root account.
3. Enable HTTPS and restrict the ports with a firewall.
4. Store credentials in a secrets manager or environment file rather than typing them in the command.
5. Try versioning and lifecycle rules on the bucket.

## Conclusion

This exercise connected the theory of storage types to a real deployment. I now understand when to choose object storage and how to set up and verify a basic MinIO instance, along with the security and persistence steps needed to make it production-ready.
