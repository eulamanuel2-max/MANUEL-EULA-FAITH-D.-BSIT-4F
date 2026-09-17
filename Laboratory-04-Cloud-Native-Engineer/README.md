# Laboratory 04 - Cloud-Native Engineer

## Mission Overview

This laboratory activity focuses on understanding the difference between
traditional Virtual Machines (VMs) and containers and applying
containerization using Docker. The activity uses the KillerCoda Ubuntu
playground to deploy and manage an Nginx web server in a Docker
container.

## Objectives

-   Differentiate between traditional Virtual Machines (VMs) and
    Containers.
-   Access a Docker-enabled cloud environment using KillerCoda.
-   Execute fundamental Docker CLI commands.
-   Pull, run, manage, and terminate an Nginx container.
-   Document container operations using Markdown.
-   Continue developing a well-organized GitHub Cloud Computing
    Portfolio.

## Docker Commands Executed

### Checkpoint 3 - Verify Docker

``` bash
docker --version
docker info
```

`docker --version` displays the installed Docker version, while
`docker info` displays information about the Docker environment.

### Checkpoint 4 - Deploy Nginx

``` bash
docker pull nginx
docker run -d -p 8080:80 --name nginx-server nginx
curl http://localhost:8080
```

`docker pull nginx` downloads the Nginx image.\
`docker run -d -p 8080:80 --name nginx-server nginx` creates and runs
the Nginx container in detached mode and maps port 8080 on the host to
port 80 inside the container.\
`curl http://localhost:8080` sends a local HTTP request to verify that
the Nginx web server is running.

### Checkpoint 5 - Container Lifecycle

``` bash
docker ps
docker stop nginx-server
docker ps
docker rm nginx-server
docker ps -a
```

`docker ps` lists currently running containers.\
`docker stop nginx-server` stops the Nginx container.\
The second `docker ps` verifies that the container is no longer
running.\
`docker rm nginx-server` removes the stopped Nginx container.\
`docker ps -a` verifies that the removed container is no longer listed.

## Skills Learned

-   Using the Docker command-line interface (CLI)
-   Checking the Docker environment
-   Pulling Docker images
-   Running containers in detached mode
-   Mapping host and container ports
-   Testing a containerized web server with `curl`
-   Managing the container lifecycle
-   Creating technical documentation using Markdown
-   Organizing evidence for a GitHub Cloud Computing Portfolio

## Challenges Encountered

One challenge during the activity was becoming familiar with the Docker
commands and understanding the different stages of the container
lifecycle. The terminal output helped verify whether Docker was working,
whether the Nginx container was running, and whether the container had
been stopped and removed successfully.

## Screenshots

### Docker Version and Environment

![Docker version and environment](screenshots/docker-version.png)

### Nginx Running

![Nginx running](screenshots/nginx-running.png)

### Container Lifecycle

![Container lifecycle](screenshots/container-lifecycle.png)
