# Docker Deployment: Nginx Container

## Environment

Verified Docker installation and environment before deployment:

```bash
root@ubuntu:~$ docker --version
Docker version 29.1.3, build 29.1.3-0ubuntu3~24.04.2

root@ubuntu:~$ docker info
Client:
 Version:    29.1.3
 Context:    default
 Debug Mode: false
...
Server:
 Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
 Images: 0
 Server Version: 29.1.3
 Storage Driver: overlay2
 Backing Filesystem: extfs
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Runtimes: io.containerd.runc.v2 runc
```

At the start, there were 0 images and 0 containers on the host.

## Steps

### 1. Pull the nginx image

```bash
root@ubuntu:~$ docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
6310eb16bf42: Pull complete
9302921ce9b3: Pull complete
ab606a349520: Pull complete
0478569e858e: Pull complete
76225461b7d3: Pull complete
c06193164a25: Pull complete
3fe5ab3f8614: Pull complete
Digest: sha256:d0d674272be3be36f9a13d79194fa0db5aa630ab3ede9bec459d12f67370aaef
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```

### 2. Run the container

```bash
root@ubuntu:~$ docker run -d -p 8080:80 --name nginx-server nginx
9570f2ee6ff7019641e7558768779b834446d8dd8fe3792f804262dcad517e81
```

This runs the container in detached mode (`-d`), maps host port `8080` to the container's port `80` (`-p 8080:80`), and names the container `nginx-server`.

### 3. Verify it's serving traffic

```bash
root@ubuntu:~$ curl http://localhost:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working. ...</p>
...
</html>
```

The default nginx welcome page confirms the container is running and reachable on port 8080.

### 4. Inspect running containers

```bash
root@ubuntu:~$ docker ps
CONTAINER ID   IMAGE   COMMAND                  CREATED          STATUS          PORTS                                   NAMES
00d2c39351b9   nginx   "/docker-entrypoint..."  About a minute ago   Up About a minute   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   nginx-server
```

### 5. Stop and remove the container

```bash
root@ubuntu:~$ docker stop nginx-server
nginx-server

root@ubuntu:~$ docker ps
CONTAINER ID   IMAGE   COMMAND   CREATED   STATUS   PORTS   NAMES

root@ubuntu:~$ docker rm nginx-server
nginx-server

root@ubuntu:~$ docker ps -a
CONTAINER ID   IMAGE   COMMAND   CREATED   STATUS   PORTS   NAMES
```

After stopping and removing, `docker ps -a` shows no containers, confirming a clean teardown.

## Summary of Commands Used

| Command | Purpose |
|---|---|
| `docker --version` | Check installed Docker version |
| `docker info` | Inspect Docker client/server configuration |
| `docker pull nginx` | Download the nginx image from Docker Hub |
| `docker run -d -p 8080:80 --name nginx-server nginx` | Create and start a container from the image |
| `curl http://localhost:8080` | Confirm the container is serving content |
| `docker ps` | List running containers |
| `docker stop nginx-server` | Stop the running container |
| `docker rm nginx-server` | Remove the stopped container |
| `docker ps -a` | List all containers (running and stopped) to confirm removal |
