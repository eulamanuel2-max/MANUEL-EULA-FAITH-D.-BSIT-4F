# Reflection

## What I Did

In this exercise, I worked through the full lifecycle of a Docker container: checking the Docker installation and environment, pulling an official `nginx` image from Docker Hub, running it as a detached container mapped to port 8080, verifying it was serving traffic with `curl`, and finally stopping and removing the container to clean up.

## What I Learned

- **Docker images vs. containers**: An image is a static, read-only template (like `nginx`), while a container is a running instance created from that image. Pulling the image and running it are two distinct steps.
- **Port mapping**: The `-p 8080:80` flag maps a port on the host machine to a port inside the container, which is what let me reach the containerized nginx server via `localhost:8080` instead of the container's internal port 80.
- **Container lifecycle**: Containers move through clear states — created, running, stopped, removed. `docker ps` only shows running containers, while `docker ps -a` shows all containers regardless of state, which was useful for confirming the container was fully removed at the end.
- **Speed and lightweight nature of containers**: Compared to spinning up a full virtual machine, pulling an image and getting a working web server took only a few seconds, which highlighted why containers are so popular for fast, repeatable deployments.
- **Clean teardown matters**: Stopping a container with `docker stop` doesn't delete it — it still shows up in `docker ps -a` until `docker rm` is run. This distinction between "stopped" and "removed" wasn't something I'd thought about before.

## Challenges

Keeping track of the exact sequence of commands (and what state the container was in at each point) took some care, especially the difference between `docker ps` and `docker ps -a` when trying to confirm the container was truly gone.

## Next Steps

I'd like to build on this by trying:
- Persisting data with Docker volumes so content survives a container being removed.
- Writing a `Dockerfile` to build a custom image instead of using the stock `nginx` image.
- Running multiple containers together with `docker-compose`.
