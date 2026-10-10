# Docker Compose Guide

This guide explains the `docker-compose.yml` file used to deploy Nextcloud and MariaDB, so another engineer can understand it.

## The Compose File

```yaml
version: '3'

services:
  database:
    image: mariadb:10.6
    environment:
      - MYSQL_ROOT_PASSWORD=cloudnova_root
      - MYSQL_PASSWORD=cloudnova_pass
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud_user
  app:
    image: nextcloud
    ports:
      - 8080:80
    environment:
      - MYSQL_PASSWORD=cloudnova_pass
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud_user
      - MYSQL_HOST=database
```

## Line-by-Line Overview

| Key | Meaning |
|---|---|
| `version: '3'` | The Compose file format version. |
| `services:` | The list of containers that make up the application. |
| `database:` | A service named `database`, the database tier. |
| `image: mariadb:10.6` | Uses the MariaDB image, version 10.6. |
| `app:` | A service named `app`, the web/application tier. |
| `image: nextcloud` | Uses the official Nextcloud image (`latest` by default). |
| `ports: - 8080:80` | Maps host port 8080 to container port 80. |
| `environment:` | Sets environment variables inside the container. |
| `MYSQL_ROOT_PASSWORD` | Root password for MariaDB (database service only). |
| `MYSQL_DATABASE` / `MYSQL_USER` / `MYSQL_PASSWORD` | Database name and user that MariaDB creates; the app uses the same values to connect. |
| `MYSQL_HOST=database` | Tells Nextcloud where the database is. |

## What Does the `services:` Block Do?

The `services:` block defines every container in the application. Each entry under it (here `database` and `app`) is one service, with its own image, ports, and environment variables. When I run `docker-compose up -d`, Compose reads this block and creates one container per service, so the whole stack is described in a single place instead of in separate commands. The terminal output showed the containers created as `nextcloud-deployment_database_1` and `nextcloud-deployment_app_1`.

## How Did the Nextcloud Container Find the Database?

It found it through the `MYSQL_HOST=database` environment variable. Compose automatically puts all services of a project on a shared default network (in my run, `nextcloud-deployment_default`) and registers each service name as a hostname on it. Because the database service is named `database`, the Nextcloud container can reach it at the hostname `database`, and Docker's built-in DNS resolves that name to the database container's IP address. This is also why the Nextcloud setup page showed "Autoconfig file detected": the `MYSQL_*` variables pre-filled the database settings, so no manual entry was needed.

## `docker run` vs `docker-compose up -d`

| | `docker run` | `docker-compose up -d` |
|---|---|---|
| Scope | Starts **one** container per command | Starts **all** services defined in the YAML file |
| Configuration | Options typed as flags each time (`-p`, `-e`, `--name`, ...) | Stored in a reusable `docker-compose.yml` file |
| Networking | Containers must be linked or put on a network manually | A shared network is created automatically |
| Repeatability | Easy to make typing mistakes or forget a flag | The same file gives the same result every time |
| Version control | Commands are scattered or in shell history | The file can be committed to Git (Infrastructure as Code) |
| Cleanup | Stop and remove each container by hand | `docker-compose down` removes containers and network together |

## Note on Credentials

The passwords in this file are plain text because this is a proof-of-concept lab environment. In a real deployment, secrets should be kept out of the Compose file (for example in an `.env` file excluded from Git, or in Docker secrets).
