Docker Engine is an open source containerization technology for building and containerizing your applications. Docker Engine acts as a client-server application with:

1. a server wit a long-running daemon process `dockerd`;
2. APIs to expose calls that programs can use to talk and instruct the Docker daemon;
3. a CLI client `docker`

the daemon creates and manages Docker objects, such as images, containers, networks, and volumes. Docker has a set of APIs of its own to allow the CLI client (`docker`) control or interact with the Docker daemon.

since Docker uses a client-server architecture, the Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing Docker containers.

the client and the daemon can run on the same system, or they can run separately. you can connect a Docker client to a remote Docker daemon. they can communicate using a REST API, over UNIX sockets or a network interface.

**the Docker daemon**, `dockerd` acts as the server, listening to Docker API requests, managing Docker objects, images, containers, networks and volumes. one daemon can also communicate to other daemons to manage Docker services.

**the Docker client**, `docker` is the entry point of many Docker users to interact with Docker. running a `docker run` command sends a request through the Docker API to `dockerd`, which carries them out.