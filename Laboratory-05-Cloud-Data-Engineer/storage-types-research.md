# Storage Types Research

| Storage Type | Description | Primary Use Case | Cloud Provider Example |
|---|---|---|---|
| Block Storage | Stores data in fixed-size blocks that can be managed like a disk. | Virtual machines, databases, and applications that need fast disk access. | AWS EBS |
| File Storage | Stores data as files organized in folders and directories. | Shared files and data that need to be accessed by multiple systems. | AWS EFS |
| Object Storage | Stores data as objects together with metadata and a unique identifier. | Large amounts of unstructured data such as images, videos, and backups. | AWS S3 |

## Why Object Storage is Suitable for the Client

Object Storage is well suited for the client's user-uploaded images because it is designed for large amounts of unstructured data such as photos. It provides scalable storage for large numbers of images while allowing applications to access the stored objects when needed.
