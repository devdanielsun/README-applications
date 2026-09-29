# Docker

## Install on Ubuntu (WSL)

[https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)

## Quick CLI-Cheatsheet

| Action                      | Command                                   |
| --------------------------- | ----------------------------------------- |
| Run interactively           | `docker run -it <image> bash`             |
| Detached + map ports        | `docker run -d -p <host>:<cont> <image>`  |
| Show running / all          | `docker ps` / `docker ps -a`              |
| View logs                   | `docker logs <naam>`                      |
| Open a shell in container   | `docker exec -it <naam> bash`             |
| Stop / remove               | `docker stop <naam>` / `docker rm <naam>` |
| Build an image              | `docker build -t <naam>:<tag> .`          |
| List images                 | `docker images`                           |

## Docker Building Blocks

| Component | What it is | What it's for |
| --- | --- | --- |
| **Image** | A read-only, layered template containing an application, its dependencies, and metadata. Built from a Dockerfile. | Packaging software once and shipping it identically to any machine. |
| **Container** | A running (or stopped) instance of an image, with a thin writable layer on top. | Executing your application in an isolated, reproducible runtime. |
| **Dockerfile** | A text file with build instructions (`FROM`, `COPY`, `RUN`, `ENTRYPOINT`, ...). | Defining images as code so builds are repeatable and reviewable. |
| **Layer** | An immutable filesystem diff produced by each Dockerfile instruction. | Caching and sharing — unchanged layers are reused, making builds and pulls fast. |
| **Registry** | A server storing and distributing images (Docker Hub, Azure Container Registry, ghcr.io). | Sharing images between developers, CI pipelines, and production clusters. |
| **Tag** | A human-readable label on an image, e.g. `myapp:1.2.0`. | Versioning images and pointing deployments at a specific build. |
| **Volume** | Docker-managed persistent storage mounted into a container. | Keeping data (databases, uploads) alive when a container is recreated. |
| **Bind mount** | A host directory mapped directly into a container. | Live-editing source code during development without rebuilding. |
| **Network** | A virtual network that containers attach to; containers resolve each other by name. | Letting services talk to each other while staying isolated from the outside. |
| **Port mapping** | `-p host:container` forwarding from the host into a container. | Exposing a containerised service to your machine or the internet. |
| **Environment variables** | Key/value config injected at run time (`-e`, `--env-file`). | Configuring the same image differently per environment (dev/test/prod). |
| **Compose** | A `compose.yaml` file describing multiple services, networks, and volumes. | Running a whole multi-container application with one `docker compose up`. |
| **Healthcheck** | A command Docker runs periodically to test container health. | Letting orchestrators restart or delay traffic to unhealthy containers. |
| **Multi-stage build** | A Dockerfile with several `FROM` stages; only the last one ships. | Building with the SDK but shipping a small runtime-only image. |
| **BuildKit** | The modern Docker build engine. | Faster, parallel builds with better caching and build secrets. |
| **Context** | The set of files sent to the daemon at build time (filtered by `.dockerignore`). | Keeping builds fast and preventing secrets from leaking into images. |

**Mental model:** a *Dockerfile* builds an *image*, an image is stored in a *registry*, and running it creates a *container* — which gets its data from a *volume*, talks to other containers over a *network*, and is configured with *environment variables*. *Compose* wires all of that together for a complete application.
