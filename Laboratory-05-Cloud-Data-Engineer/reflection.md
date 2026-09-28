# Mission Reflection

Object storage is well suited for storing millions of photos because photos are unstructured data and can be stored as individual objects. Object storage organizes these objects into buckets and is designed to handle large amounts of data, making it suitable for a photo-sharing application.

Docker made it easier to deploy the MinIO storage server because the server could run in an isolated container with its ports and environment variables configured when the container was started. During this activity, I also learned how to troubleshoot an unavailable Docker image, build MinIO from source, create a local Docker image, and run the service in a container.

A bucket is a logical container used to organize objects in object storage. In this activity, the required bucket is named `client-photos`, which is intended to contain uploaded images.

Large enterprise companies can help protect object storage data from physical server failures through redundancy, replication, backups, and multiple storage locations. Keeping additional copies of data can help make the information available even when hardware fails.

My confidence in navigating the Linux command line is growing because this activity required me to use commands for cloning a repository, checking software versions, installing tools, building software, creating a Docker image, and running and checking a Docker container. I also became more comfortable reading error messages and using them to troubleshoot problems.
