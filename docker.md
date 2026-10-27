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
Think of it like email: a Docker Registry is the concept of an email server, while Docker Hub is Gmail.## basic cmds
- `docker run`, `docker ps`, `docker stop`, `docker rm`, `docker image rm`
- Interactive mode: `-it` flag
- Detached mode: `-d` flag
- Port mapping: `-p host:container`
- Naming: `--name`
- Logs: `docker logs`
- Exec into container: `docker exec`
- Image history: `docker image history`
- Create without starting: `docker create`
- Follow logs: `docker logs -f`
- Inspect: `docker inspect`
- Cleanup: `docker system df`, `docker system prune`
- Build: `docker build -t name:tag .`
- Volumes: `docker volume create`, `-v volume_name:/path`
- Bind mount: `-v /host/path:/container/path`
- Networking: `docker network create`, `--network`
- Ping: `docker exec container1 ping container2`
`docker compose up`(creates and runs containers), `docker compose down`(stops and removes containers)

## detached mode (-d)
Running a Docker container in detached mode differs from running it normally (foreground mode) based on how the container connects to your terminal session.By default, when you execute docker run, the container starts in foreground mode. Your terminal attaches directly to the container’s standard input, output, and error streams (stdin, stdout, stderr)


## common instructions in a Dockerfile include:

- `FROM` — base image
- `WORKDIR` — set working directory
- `COPY` — copy files from host to image
- `RUN` — execute commands during build
ENV <name> <value> - this instruction sets an environment variable that a running container will use.
- `EXPOSE` — document the port
USER <user-or-uid> - this instruction sets the default user for all subsequent instructions.
- `CMD` — default command
- `RUN` — execute commands during build


## cmd vs entrypoint
The most powerful pattern in Docker development is combining ENTRYPOINT and CMD together. When paired, ENTRYPOINT defines the fixed executable, while CMD acts as the default arguments passed to that executable.

## Layering
Layer order matters in a Dockerfile because Docker builds images sequentially from top to bottom and uses a cache mechanism that breaks down the moment a single layer changes


Containers are ephemeral — they lose data when removed. And by default, containers can't easily talk to each other.

## named volumes vs bind mount
The primary difference between a named volume and a bind mount is who manages the storage location on the host machine. A named volume is completely managed by Docker and abstracted away from the host's direct file structure, whereas a bind mount is a direct link to a specific, absolute path that you define on your host machine.
 If you mount an empty named volume into a container directory that already contains files (like a new MySQL database folder), Docker will automatically copy those initial files into your volume so the application functions properly.
 Developers use bind mounts to link their local source code directory to the container. You can edit code in an IDE on your machine, and the containerized app updates instantly without needing a rebuild.

 ## Why does custom networking allow name-based communication but the default bridge doesn't?
 Custom networks enable name-based communication because Docker runs an embedded DNS server (at IP 127.0.0.11) on user-defined networks, whereas the default bridge network lacks this built-in DNS capability for backward compatibility.
 # • Embedded DNS: Docker runs an internal DNS server for every user-defined network.
    • Automatic Registration: When you start a container on a custom network with a name or alias, Docker registers that name in the internal DNS.
    • Query Resolution: When one container tries to reach another by name (e.g., pinging backend), the container queries 127.0.0.11, which translates the name to the target container's IP address.
 # • No Automatic DNS: The default bridge network (named docker0) predates Docker's embedded DNS feature.
    • Backward Compatibility: Docker keeps the default bridge unchanged so older scripts and legacy workflows that rely strictly on raw IP addresses or deprecated --link flags do not break.
    • IP-Only Communication: Containers on the default bridge can still talk to each other, but they must use their hardcoded, dynamic internal IP addresses (like 172.17.0.3), which change when containers restart.

## dockerfile vs docker compose
A Dockerfile builds a single Docker image, while Docker Compose runs and connects one or more containers. They are not competing tools; rather, they work together to manage different stages of the container lifecycle.


## restart: always vs restart: on-failure vs restart: unless-stopped
The core difference between restart: always and restart: on-failure lies in how they handle successful, intentional shutdowns (Exit Code 0) and host reboots.
# restart: always
If your script finishes its job successfully and exits with a 0 code, Docker ignores the success and restarts it anyway, putting it into an infinite loop. If the host machine reboots or the Docker service restarts, Docker will automatically spin this container back up—even if you had manually stopped it before the reboot.
# restart: on-failure
If the process completes successfully (Exit Code 0), Docker leaves it alone. The container transitions nicely to a Stopped status.It will not boot up with the Docker daemon unless it was actively in a failing/crashing state right before the daemon went down.
# restart: unless-stopped
If you like always but hate that it turns back on after a system reboot even though you manually typed docker stop, use restart: unless-stopped. It acts exactly like always, but respects your manual docker stop commands during system restarts.