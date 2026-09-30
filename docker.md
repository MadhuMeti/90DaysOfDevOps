## Containers vs Virtual Machines — what's the real difference?
virtual machines (VMs) virtualize physical hardware to run an entire separate operating system, while containers virtualize the operating system to share a single host kernel.

## daemon, client, images, containers, registry
The Docker Client is the primary interface you use to interact with Docker. When you type a command in your terminal (like docker run or docker build), you are talking to the client.

The Docker Daemon (dockerd) is a persistent background service running on your host operating system.

A Docker Image is a read-only template containing the application code, libraries, dependencies, and environment configurations needed to run an application.

A Docker Container is a running, isolated instance of a Docker Image.

A Docker Registry is a centralized storage system used to share, distribute, and track versions of Docker images.

## Docker Registry and Docker Hub
a Docker Registry is a general concept or technology specification, whereas Docker Hub is a specific, cloud-based implementation of a registry owned and operated by Docker, Inc.
Think of it like email: a Docker Registry is the concept of an email server, while Docker Hub is Gmail.