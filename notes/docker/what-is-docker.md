docker solves the "works on my machine" problem. it enables one developer to ship to a server the exact same environment as they are developing, through an image that lives in a container.

the container, as you can already imagine, contains the image but it cannot live and exist out of nowhere, it has to run inside an OS because it is kind of a process, and as every process, it needs resources such as CPU, RAM etc.

docker builds images by reading instructions from a Dockerfile, it is a text file containing instructions for building the source code. using the default name Dockerfile allows to run `docker build` command without having to specify any additional command flags.

docker images consist of layers, where each layer is the result of a build instruction in the Dockerfile. layers are stacked sequentially and each one is a **delta  representing the changes applied to the previous layer**.

more on what a [[dockerfile]] is.

docker has three building steps.
1. **build**: the building step consists on building from ground up what an image needs to exist, and it all starts with the **Dockerfile**. 
2. **ship**:
3. **run**:


some common types of Dockerfile instructions:

|[`FROM <image>`](https://docs.docker.com/reference/dockerfile/#from): defines a base for your image.
|[`RUN <command>`](https://docs.docker.com/reference/dockerfile/#run): executes any commands in a new layer on top of the current image and commits the result. `RUN` also has a shell form for running commands.
|[`WORKDIR <directory>`](https://docs.docker.com/reference/dockerfile/#workdir): sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it in the Dockerfile.
|[`COPY <src> <dest>`](https://docs.docker.com/reference/dockerfile/#copy): copies new files or directories from `<src>` and adds them to the filesystem of the container at the path `<dest>`.|
|[`CMD <command>`](https://docs.docker.com/reference/dockerfile/#cmd): lets you define the default program that is run once you start the container based on this image. each Dockerfile only has one `CMD`, and only the last `CMD` instance is respected when multiple exist.