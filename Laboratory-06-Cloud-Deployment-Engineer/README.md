# Laboratory-06: The Cloud Deployment Engineer

## Mission Overview
Transitioning from manual single-container deployments to Infrastructure as Code (IaC) using Docker Compose to deploy an enterprise-grade private cloud storage solution (Nextcloud and MariaDB) for CloudNova Technologies[cite: 4].

---

## Objectives
* Explain the concept of a multi-tier application architecture[cite: 4].
* Understand the purpose and structure of a `docker-compose.yml` file[cite: 4].
* Use a Linux command-line text editor (`nano`) to create configuration files[cite: 4].
* Deploy and manage a multi-container application stack using Docker Compose[cite: 4].
* Document deployment procedures and Infrastructure as Code principles using Markdown[cite: 4].

---

## Commands Executed
```bash
# Create and enter project directory
mkdir nextcloud-deployment
cd nextcloud-deployment

# Create and edit configuration file
nano docker-compose.yml

# Deploy the multi-container stack in the background[cite: 1]
docker-compose up -d

# Verify running containers[cite: 1]
docker-compose ps

# Gracefully stop and remove the container stack[cite: 2]
docker-compose down
