# Laboratory 06 – The Cloud Deployment Engineer

**Course:** CCM101 – Cloud Computing
**Platform:** KillerCoda Ubuntu 24.04 Playground

## Mission Overview

CloudNova Technologies has a client, a university, that wants to replace Google Drive with its own private cloud storage. The chosen solution is **Nextcloud**, which needs a database to store user accounts and file metadata. In this mission I deployed a proof-of-concept **two-tier architecture** (a Nextcloud web container and a MariaDB database container) using **Docker Compose**, moving from typing individual `docker run` commands to **Infrastructure as Code (IaC)** with a single YAML file.

## Objectives

- Explain the concept of a multi-tier application architecture.
- Understand the purpose and structure of a `docker-compose.yml` file.
- Use the Linux text editor `nano` to create configuration files.
- Deploy a multi-container application (Nextcloud + MariaDB) using Docker Compose.
- Document deployment procedures and IaC principles using Markdown.
- Continue expanding my GitHub Cloud Computing Portfolio.

## Commands Executed

```bash
# Create the project directory and move into it
mkdir nextcloud-deployment
cd nextcloud-deployment

# Create the Compose file (YAML pasted into the editor, then saved)
nano docker-compose.yml

# Deploy the whole stack in the background
docker-compose up -d

# Verify both containers are running
docker-compose ps

# Tear the whole stack down (containers and network removed)
docker-compose down
```

| Command | Purpose |
|---|---|
| `mkdir nextcloud-deployment` | Creates a folder for the project |
| `cd nextcloud-deployment` | Moves into the project folder |
| `nano docker-compose.yml` | Opens the text editor to write the Compose file |
| `docker-compose up -d` | Pulls images, creates the network, and starts all services in detached mode |
| `docker-compose ps` | Lists the containers of the stack, their state, and ports |
| `docker-compose down` | Stops and removes the containers and the network |

## Evidence

**1. Successful deployment and running containers**

![Compose deployment](screenshots/compose-deployment.png)

**2. Nextcloud setup page accessed through port 8080**

![Nextcloud web](screenshots/nextcloud-web.png)

**3. Teardown of the stack**

![Compose teardown](screenshots/compose-teardown.png)

## Skills Learned

- Describing a two-tier architecture and the role of each tier.
- Writing a valid, indentation-sensitive `docker-compose.yml`.
- Using `nano` to create and save files from the terminal.
- Deploying and removing a multi-container stack with one command each.
- Linking containers through Compose service names (`MYSQL_HOST=database`).
- Exposing a container port (`8080:80`) and reaching the app from a browser.
- Documenting infrastructure in Markdown and keeping it in a GitHub repository.

## Files in This Laboratory

- [multi-tier-architecture.md](multi-tier-architecture.md)
- [docker-compose-guide.md](docker-compose-guide.md)
- [reflection.md](reflection.md)
- [screenshots/](screenshots/)
