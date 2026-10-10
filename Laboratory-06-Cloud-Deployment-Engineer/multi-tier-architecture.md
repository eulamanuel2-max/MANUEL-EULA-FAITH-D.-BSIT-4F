# Multi-Tier Architecture

## What Is a Two-Tier Architecture?

A **two-tier architecture** splits an application into two layers that each have one main job and talk to each other over a network: a **web/application tier** that users interact with, and a **database tier** that stores the data. In this mission, the Nextcloud container is the first tier and the MariaDB container is the second.

```
 User (Browser)
      │  HTTP (port 8080 → 80)
      ▼
┌───────────────────────┐
│  Web/Application Tier │   nextcloud
│  (Nextcloud + Apache) │
└───────────┬───────────┘
            │  MYSQL_HOST=database (port 3306)
            ▼
┌───────────────────────┐
│     Database Tier     │   mariadb:10.6
│       (MariaDB)       │
└───────────────────────┘
```

## The Web/Application Tier

The web/application tier is the part of the system that users reach directly. In this lab it is the **Nextcloud** container, which runs Apache and the Nextcloud application code. Its role is to:

- Serve the user interface (login page, file manager, setup screen).
- Receive and handle HTTP requests from the browser.
- Run the application logic, such as creating users and managing files.
- Query the database tier whenever it needs to read or save data.

It is the only tier exposed to the outside, through port `8080` on the host mapped to port `80` in the container.

## The Database Tier

The database tier is responsible for **persistent data storage**. In this lab it is the **MariaDB 10.6** container. Its role is to:

- Store user accounts and credentials.
- Store file metadata and application settings.
- Answer queries sent by the application tier.

It is not published to the outside; only the application container needs to reach it, using the service name `database`.

## Why Separate Them?

Keeping the web server and the database in two separate containers lets each be updated, restarted, or scaled on its own, so a change to Nextcloud does not force downtime or risk to the database. It is also more secure, because only the web tier is exposed while the database stays internal, and each container stays simple, with one job and one image. Troubleshooting is also easier since logs and failures are isolated to a single tier.
