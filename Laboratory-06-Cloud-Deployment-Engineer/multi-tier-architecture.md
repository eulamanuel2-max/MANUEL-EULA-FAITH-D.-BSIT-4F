# Multi-Tier Architecture Overview

## What is a Two-Tier Architecture?
A **Two-Tier Architecture** is a software design pattern where an application is split into two distinct, communicating logical tiers or layers: the **Web/Application Tier** and the **Database Tier**. In a containerized environment, each tier runs within its own dedicated container, communicating over a shared Docker network.

---

## The Tiers

### 1. The Web/Application Tier
* **Role:** This tier serves as the front-end user interface and handles incoming HTTP/HTTPS requests from clients. 
* **Nextcloud Implementation:** In our deployment, the Nextcloud container processes user interactions, renders the web dashboard, and manages file uploads and web traffic.

### 2. The Database Tier
* **Role:** This tier is responsible for secure, persistent data storage, managing relational data, user credentials, configurations, and file metadata[cite: 4].
* **MariaDB Implementation:** The MariaDB container acts as the backend data store, ensuring that data persists even if the application container restarts or is updated[cite: 4].

---

## Why Separate Them?
Separating the web server and the database into two distinct containers rather than packing them into a single monolithic container provides modularity, scalability, and enhanced security[cite: 4]. If the web application encounters high traffic or crashes, the database remains unaffected and secure[cite: 4]. Furthermore, independent scaling and easier maintenance allow administrators to update the application frontend or the database engine separately without disrupting the entire system[cite: 4].
