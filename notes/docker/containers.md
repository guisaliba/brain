a container is a runnable instance of a Docker image. you can create, start, stop, move or delete a container using the Docker API or CLI. see more on [[images]].

by default a container is relatively well isolated from other containers and its host machine. you can control how isolated a container's network, storage, or other underlying subsystems are from other containers or from the host machine.

any configuration provided to a container when you create or start it will be passed into it. deleting a container means that any changes to its state that aren't stored in persistent storage also disappears.

```bash
 docker run -i -t ubuntu /bin/bash
```

when you run the command above, the following happens:
1. if the `ubuntu` image is not found locally, it gets pulled from the configured registry.
2. Docker creates a new container.
3. Docker allocates a read-write filesystem to the container. this allows a running container to create or modify files and directories in its local filesystem.
4. creates a network interface to connect the container to the default network. this includes assigning an IP address to the container. by default, containers can connect to external networks using the host machine's network connection.
5. Docker starts the container and runs the command `/bin/bash`.
6. when the command `exit` is run to terminate the `/bin/bash` command, the container stops but doesn't get deleted. you can start it again or remove it.

pretend you're developing an awesome web app consisting of three components: a React **frontend**, a Python API for the **backend** and a PostgreSQL **database**. each of these can be run (and should be) in a different, isolated and self-contained **container**.

each one of them runs in their own isolated environment, completely isolated from everything else in your machine. they can talk to each other leveraging networking, since each gets an IP address assigned, exposing a port on one of them creates a network path that can be reached by the other containers using the network.

![[aN4kQ.webp|683]]

a container must not get confused with a Virtual Machine. a VM is an entire operating system with its own kernel, hardware drivers, programs and applications. a container is simply an isolated process running whatever image it is defined to run, with all of the files it needs to run.

if you run multiple containers, they all share the same kernel.