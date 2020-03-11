---
title: Docker
date: 2020-03-10 19:16:07
tags: ["Docker"]
categories: ["Develop","Docker"]
---

Docker is a set of platform as a service products that isolates OS-level virtualization to deliver software in packages called containers.

<!-- more -->

### What is Container?
Container completely isolates the process using Cgroup and Namespace as like Kernel function, creating an isolated environment and running it.

- Cgroup (Control Group)
 - The Kernel function which isolate CPU time in system, system memory, network.

- Namespace
  - The function which isolate with another process and make resource look like the process's dedicated recourse.

### About Docker

- After 10 years from LXC
- Made by Google's Go language
- Immutable, Stateless, Scalable
- Community Edition and Enterprise Edition($1000 per year)
- __Linux Base__
- 64-bit OS only

### Docker Terms
- Docker Image and Container
- Docker Engine (Docker Daemon, Core)
- Docker Client
  - If use docker at Window, the Window OS is Docker Client.
- Docker Host OS
  - If use docker at Window, the Window OS is Host OS.
- Docker Machine
- Docker compose
  - Use lot of docker containers
- Docker Registry, Hub, Swarm
  - Make image to Docker and share and operator lots of server.

### Docker Container
Logical Area in OS
- Process, Network, FS
- Share Directory, Library and IP Shared

### Docker Image
Container based on Docker image App, Lib, Middleware, OS, NW, etc.
Ex) MySQL image, Ubuntu image.

Image Build (Make): Docker file.

Image Ship (Share)
