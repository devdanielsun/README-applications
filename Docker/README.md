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
