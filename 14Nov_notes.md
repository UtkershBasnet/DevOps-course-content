#### Date:14th November 
# Revision Notes on Docker and Container Technology

## Introduction to Containers

Containers are a fundamental technology in modern software engineering,
allowing developers to package applications with their dependencies into
standardized units. They provide isolated environments on a shared
operating system, ensuring consistency across development, testing, and
deployment.

## Historical Background

The idea of isolated environments is not new. A notable predecessor is
the Unix `chroot` command, introduced in the late 1960s--1970s. `chroot`
creates a jail-like filesystem environment where processes operate as if
they are in a separate system, though they still share the same kernel.

## Understanding Docker Containers

### What is a Container?

A Docker container is a lightweight, standalone, executable package that
includes everything needed to run software---code, runtime, libraries,
and tools. Unlike virtual machines, containers share the underlying OS
kernel instead of bundling an entire OS.

## Containers vs. Virtual Machines

### Weight and Performance

-   Containers are lightweight because they share the host OS kernel.
-   VMs bundle an entire OS, making them heavier.
-   Containers start faster and use fewer resources.

### Isolation

-   Both provide isolation.
-   Containers rely on Linux namespaces and cgroups.
-   VMs rely on hypervisors such as VMware, Hyper-V, or KVM.

## How Containers Work

### Namespace Isolation

Linux namespaces isolate: - Process IDs - Hostnames - Network access -
User IDs - Inter-process communication - File systems

### Control Groups (Cgroups)

Cgroups manage resource allocation (CPU, memory, etc.) ensuring fair
usage and preventing interference across processes.

## Docker's Kernel Interaction

Docker interfaces directly with the Linux kernel for container
management.

-   On Linux → Docker runs natively using the host kernel.
-   On Windows & macOS → A lightweight Linux VM is used because Docker
    relies on the Linux kernel.

## Running Containers on Different Systems

### Linux

-   Containers run natively using the host kernel.

### Windows & macOS

-   Require a small VM (like Docker Desktop's LinuxKit VM) because they
    lack the Linux kernel.

## Ephemeral Nature of Containers

Containers are ephemeral (temporary) by design: - They can be started,
stopped, or destroyed without affecting the system. - Great for scaling
and fault tolerance. - Applications must be stateless or store data
externally (volumes, databases, cloud storage).

## Port Mapping and Networking

Containers have their own isolated network stack.

Port mapping enables communication with the host:

    docker run -p <host_port>:<container_port> image

## Conclusion

Docker and container technology improve how applications are built,
shipped, and run. Their lightweight architecture, portability, and
efficient resource usage make them essential for cloud-native
development.
