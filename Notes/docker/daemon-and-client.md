# subject: [[docker]]
# topics: #docker 
---
when we use docker on our machine, it consists of two agents:
- **docker daemon**: the docker daemon is like a server. this server runs continuously on our machine, and it's responsible for managing the containers and images of the application.
- **docker client**: the docker client is what communicates with the docker daemon (the server) through the command lines that the user types.

this parallel can be imagined as if it were a REST API. there is a client and a server, the client is responsible for making calls to the server. in this case, client and server are client and daemon respectively.

when we execute a docker command in the terminal, the docker client communicates with the daemon going through several steps until it can execute what the command requests:

```bash
$ docker run hello-world
```

this client command tells the daemon to start a container called hello-world. if this container doesn't exist, the server (daemon) will identify this absence and automatically pull the corresponding **image** from docker hub, creating the container afterward.

```bash
$ docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete
Digest: sha256:aa0cc8055b82dc2509bed2e19b275c8f463506616377219d9642221ab53cf9fe
Status: Downloaded newer image for hello-world:latest
Hello from Docker!
```

this whole process occurred following a series of steps:
1. the docker client contacted the docker daemon.
2. the docker daemon pulled the "hello-world" image directly from docker hub.
3. the docker daemon created a new container from this image, which runs the executable that produced the message "Hello from Docker!" (in this context).
4. the docker daemon transmitted this response to the docker client, which in turn, sent it to the terminal.