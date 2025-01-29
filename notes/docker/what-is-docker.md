docker solves the "works on my machine" problem. it enables one developer to ship to a server the exact same environment as they are developing, through an image that lives in a container.

the container, as you can already imagine, contains the image but it cannot live and exist out of nowhere, it has to run inside an OS because it is kind of a process, and as every process, it needs resources such as CPU, RAM etc.

docker builds images by reading instructions from a Dockerfile, it is a text file containing instructions for building the source code. using the default name Dockerfile allows to run `docker build` command without having to specify any additional command flags.

docker images consist of layers, where each layer is the result of a build instruction in the **Dockerfile**. layers are stacked sequentially and each one is a **delta representing the changes applied to the previous layer**.

a Dockerfile describes how an image is going to be built. more on what a [[Dockerfile]] is.

each layer has a SHA (hash) that depends on the hash of the base image. if the hash of the base image doesn't change, the other layers get **cached** meaning that they're only getting built on sequential runs if they didn't exist before.

e.g.:
```Dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:22.04

# install app dependencies
RUN apt-get update & &apt-get install -y python3 python3-pip
RUN pip install flask==3.0.*
```

after building and running this image the first time, if the hash of the base image doesn't change on sequential runs, the two layers of those `RUN` commands will not be rebuilt unless they change. any new layers added to this Dockerfile will be built the first time they run.

docker has three building steps.
1. **build**: the building step consists on building from ground up what an image needs to exist, and it all starts with the Dockerfile. 
2. **ship**: after they're built, images can be published to a hub such as Dockerhub where they'll be host and can be pulled from. by default, images are published in **privately**.
3. **run**: running an image leverages the Docker Engine to orchestrate the dependencies to run that image. the Docker Engine acts as a client-server application for building and containerizing applications.

