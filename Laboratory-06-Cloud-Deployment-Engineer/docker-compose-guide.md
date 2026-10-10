# Docker Compose Deployment Guide

This guide documents the Infrastructure as Code (IaC) configuration used to deploy the Nextcloud and MariaDB multi-container stack[cite: 4].

---

## Key Configuration Concepts

### 1. What does the `services:` block do?
The `services:` block in a `docker-compose.yml` file defines the individual containers (services) that make up your application stack[cite: 4]. Each service specifies the container image to use, environment variables, port mappings, and networking rules, allowing Docker Compose to build and run them as a cohesive unit[cite: 4].

### 2. How did the Nextcloud app container find the database container?
The Nextcloud application container located the database container using Docker's built-in automatic service discovery and networking[cite: 4]. By setting the environment variable `MYSQL_HOST=database`, the Nextcloud container resolved the hostname `database` directly to the MariaDB service defined within the same Docker Compose network[cite: 4].

### 3. Difference between `docker run` and `docker-compose up -d`
* **`docker run`:** Used in manual deployments (such as Mission 4)[cite: 4]. It requires executing long, complex commands with multiple flags for ports, environment variables, and network configurations one container at a time[cite: 4].
* **`docker-compose up -d`:** An Infrastructure as Code (IaC) approach that reads a declarative YAML configuration file and deploys the entire multi-container stack simultaneously in the background (`-d`) with a single command[cite: 4].
