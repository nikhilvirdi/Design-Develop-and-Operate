## Virtualization

Virtualization is a software technology that abstracts physical hardware to create multiple simulated computing environments called Virtual Machines (VMs). It enables a single physical machine to run multiple operating systems and applications simultaneously, improving resource utilization and reducing infrastructure costs.

* Creates multiple virtual systems on one physical machine
* Each VM behaves like an independent computer
* Managed using a hypervisor
* Supports multiple operating systems simultaneously
* Improves scalability and hardware efficiency
* Provides isolation between environments
* Widely used in cloud computing and data centers


## Containerization

Containerization is a lightweight virtualization technology that packages an application along with its dependencies, libraries, and runtime into isolated environments called containers. It enables applications to run consistently across different computing environments while sharing the host operating system kernel.

* Packages applications and dependencies together
* Ensures consistent execution across environments
* Containers share the host OS kernel
* Lightweight and faster than Virtual Machines (VMs)
* Provides process-level isolation
* Improves portability and scalability
* Widely used in DevOps, microservices, and cloud-native applications

**Examples**

* Docker
* Podman

---

# Docker

Docker is an open platform used for developing, shipping, and running applications inside containers. Instead of depending on the software installed on a machine, Docker packages the application along with all its dependencies, libraries, configuration files, and runtime into a single isolated unit called a container. This ensures that the application behaves the same way across development, testing, and production environments.

Docker solves one of the biggest problems in software development: environment inconsistency. Traditionally, applications often failed when moved between systems because of differences in operating systems, runtime versions, or installed dependencies. Docker eliminates this issue by creating standardized and portable environments that can run consistently on any system where Docker is installed.

Unlike Virtual Machines, Docker containers do not require a separate guest operating system for each instance. Containers share the host operating system kernel, making them lightweight, fast, and resource-efficient. This allows multiple containers to run simultaneously on the same machine with very low overhead.

---

## Lifecycle

Docker provides tools and a platform to manage the complete lifecycle of containers, starting from development all the way to production deployment.

### Development

Developers can build and run applications inside containers during local development. Since every developer uses the same containerized environment, issues caused by inconsistent system configurations are greatly reduced. This standardization improves collaboration and ensures predictable application behavior.

### Distribution and Testing

Containers become the standard unit for distributing and testing applications. Developers can easily share container images with teammates or deploy them into staging environments for automated and manual testing. Since the same container is used throughout the workflow, testing becomes more reliable and reproducible.

### Deployment

Once testing is complete, the same container can be deployed directly into production environments. Docker containers can run consistently across local machines, physical servers, Virtual Machines, cloud providers, or hybrid infrastructures. This portability simplifies deployment pipelines and reduces infrastructure-specific issues.

---

## What can I use Docker for?

### Fast and Consistent Application Delivery

Docker streamlines the software development lifecycle by providing standardized container environments. Developers can write code locally, package the application into containers, test it in staging environments, and deploy it into production using the exact same environment throughout the process.

Containers integrate naturally with Continuous Integration and Continuous Delivery (CI/CD) workflows because applications can be built, tested, validated, and deployed using the same environment at every stage. Bug fixes, updates, and new features can be tested and deployed rapidly without worrying about compatibility issues between environments.

### Responsive Deployment and Scaling

Docker containers are highly portable and can run across multiple platforms, including local laptops, on-premise servers, Virtual Machines, and cloud environments. Because containers are lightweight and start quickly, applications can scale up or down in near real time depending on workload demands. This makes Docker ideal for modern scalable architectures and microservices-based systems.

### Better Hardware Utilization

Docker containers consume fewer resources compared to hypervisor-based Virtual Machines because they share the host operating system kernel. This allows more workloads to run on the same hardware while maintaining performance and isolation. Due to their lightweight nature, containers start quickly, use less memory, and provide higher container density on servers, making Docker a cost-effective solution for high-density deployments and modern cloud-native infrastructure.

---

## The Docker platform

Docker provides a platform for packaging, distributing, and running applications inside lightweight isolated environments called containers. Containers include everything required to run an application — the code, dependencies, libraries, runtime, and configuration files — ensuring applications behave consistently across development, testing, and production systems.

Docker containers are lightweight because they share the host operating system kernel instead of running a complete guest operating system like Virtual Machines. This allows multiple containers to run simultaneously on the same machine with low resource overhead while still maintaining isolation and security between applications.

Docker also provides tools for managing the complete lifecycle of containers. Developers can build applications using containers, distribute them for testing and collaboration, and deploy the same containers directly into production environments. Since containers remain consistent across environments, deployment becomes simpler and more reliable whether the infrastructure is a local data center, cloud platform, or hybrid environment.

---

## Docker architecture

Docker uses a client-server architecture where different components work together to build, manage, and run containers. The Docker Client acts as the interface through which users interact with Docker. It communicates with the Docker Daemon, which performs the actual work of building images, creating containers, managing networks, and handling storage. Communication happens through the Docker API using UNIX sockets or network interfaces. The Docker Client and Docker Daemon can run on the same machine or on different remote systems.

<img width="700" alt="docker-architecture" src="https://github.com/user-attachments/assets/90ab1d94-7dae-488e-ada4-1a345d326cf7" />

### Daemon

The Docker Daemon (`dockerd`) is the background service responsible for managing Docker objects such as images, containers, networks, and volumes. It listens for Docker API requests from the Docker Client and executes them, performing the heavy lifting of pulling images, creating containers, starting applications, and managing Docker services.

### Client

The Docker Client (`docker`) is the primary interface users interact with. When a user runs a command such as `docker run nginx`, the client sends the request to the Docker Daemon, which then performs the operation. The client communicates using the Docker API and can connect to both local and remote Docker daemons. Common commands include:

```bash
docker run
docker build
docker pull
```

### Desktop

Docker Desktop is a desktop application for Windows, macOS, and Linux that provides a complete Docker development environment. It simplifies containerized application development by providing an easy-to-install local Docker environment that bundles all the core components:

- Docker Daemon
- Docker Client
- Docker Compose
- Kubernetes support
- Credential management tools

### Registries

A Docker Registry is a storage and distribution system for Docker images. Images can be uploaded to registries and later downloaded whenever required. Docker Hub is the default public Docker registry. Organizations can also create private registries to securely manage internal container images. Common registry operations include:

```bash
docker pull nginx
docker push myapp:v1
```

---

## Docker Objects

Docker works using different objects such as images, containers, networks, and volumes.

### Image

A Docker Image is a read-only template used to create containers. It contains everything required to run an application, including the application code, dependencies, libraries, runtime environment, configuration files, and system tools. Images act as blueprints from which containers are created.

Images are usually built using a `Dockerfile`, where each instruction defines a step in the image creation process. Each instruction creates a separate read-only layer. Docker caches these layers during the build process — if only one layer changes, Docker rebuilds only that specific layer and reuses unchanged cached layers, making image creation fast and efficient. Since images are immutable, they do not change once built. Instead, new versions are created whenever modifications are required.

Images are often built on top of other base images. For example, a Node.js application image may be built using an Ubuntu base image with Node.js and application files added on top. Layers also reduce storage usage because multiple images can share common base layers instead of storing duplicate copies.

### Container

A container is a runnable instance of an image. Once an image is executed, it becomes a container with its own isolated runtime environment. Containers provide process-level isolation while sharing the host operating system kernel. Each container has its own filesystem, network interfaces, processes, and configurations, making it behave like an independent system.

Containers are lightweight and start quickly because they do not require a full guest operating system like Virtual Machines. Multiple containers can run simultaneously on the same machine with minimal resource overhead. Containers are also ephemeral by default — changes made inside a container are temporary unless persistent storage volumes are attached.

Containers can be created, started, stopped, restarted, and deleted. They are isolated from each other and from the host system, although Docker allows controlled sharing of networking, storage, and resources when required.

**Example — `docker run`:**

```bash
docker run -it ubuntu /bin/bash
```

When this command executes:

1. Docker checks whether the Ubuntu image exists locally.
2. If unavailable, Docker pulls it from a registry.
3. Docker creates a new container from the image.
4. A writable filesystem layer is attached.
5. Networking is configured automatically.
6. The `/bin/bash` process starts inside the container.

Because interactive flags (`-i` and `-t`) are used, the terminal attaches directly to the container shell. When the shell exits, the container stops but still exists unless explicitly removed.

### Volume

A Docker Volume is a persistent storage mechanism used to store data independently from containers. Normally, data inside a container is lost when the container is removed because containers are ephemeral by default. Volumes solve this problem by storing data outside the container filesystem while still allowing containers to access it.

This is especially important for stateful services such as databases, Redis caches, uploaded files, and application logs. Even if a container crashes, restarts, or gets deleted, the data stored inside volumes remains intact. Volumes also improve portability and make backup, migration, and data sharing between containers easier.

### Network

Docker Networks enable communication between containers, host machines, and external systems. By default, containers are isolated, so networking is required for services to interact with each other. Docker automatically creates network interfaces and assigns IP addresses to containers. Containers connected to the same Docker network can communicate directly using container names instead of manually configuring IP addresses.

Networking is essential in multi-container applications where services such as backend APIs, databases, Redis, and message brokers need to communicate securely and efficiently. Docker supports multiple networking modes such as bridge networks, host networks, and overlay networks depending on deployment requirements.

---

## Other Core Terminologies

### Layer

Docker images are built using layers. Every instruction inside a `Dockerfile` — such as `RUN`, `COPY`, and `ADD` — creates a separate read-only layer. Docker caches these layers during the build process. If only one layer changes, Docker rebuilds only that specific layer and reuses the unchanged cached layers, significantly improving build speed and efficiency.

Layers also reduce storage usage because multiple images can share common layers. For example, several Node.js application images may reuse the same Ubuntu base image layer instead of storing duplicate copies. This layered architecture is one of the main reasons Docker images are lightweight, efficient, and fast to distribute.

### Registry

A Docker Registry is a storage and distribution system for Docker images. Registries allow developers and organizations to upload, store, version, and share container images. Docker pulls images from registries whenever they are not available locally, and custom-built images can be pushed to registries for collaboration and deployment.

Common Docker registries include:

- Docker Hub
- Amazon Elastic Container Registry (ECR)
- GitHub Container Registry

Registries can be public or private depending on organizational requirements.

---

## Why Docker ?

### Eliminates Environment Inconsistency

Docker packages the application together with its dependencies, libraries, configuration files, and runtime environment inside a container. This ensures the application behaves the same way on every system regardless of the host machine configuration, permanently eliminating the classic "works on my machine" problem.

### No Environment Drift Across Stages

Docker uses the same container image across all environments — development, testing, CI/CD pipelines, staging, and production. Since the exact same environment is used everywhere, configuration mismatches and environment drift are eliminated entirely.

### Isolated and Conflict-Free Services

Each container runs in an isolated environment with its own dependencies and configurations. Different services can use different runtime versions or libraries without interfering with each other, preventing dependency conflicts between services running on the same host.

---

## Underlying Technology

Docker is written in the Go programming language and uses several Linux kernel features to implement containers efficiently. Instead of creating full Virtual Machines, Docker relies on operating-system-level virtualization to provide lightweight isolated environments.

### Namespaces

Linux Namespaces are one of the core technologies behind Docker containers. Namespaces provide isolation by separating system resources for each container, making containers behave like independent systems even though they share the same host operating system kernel.

Docker creates separate namespaces for processes, networking, filesystems, users, and hostnames. Because of this isolation, containers cannot directly see processes running in other containers, each container can have its own network interfaces and IP addresses, and applications inside containers behave as if they are running on independent machines. This namespace-based isolation is what makes containers lightweight, fast, and efficient compared to traditional Virtual Machines.

---

