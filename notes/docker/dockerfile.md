it all starts with the Dockerfile. docker builds images by reading instructions from a Dockerfile, it is a text file containing instructions for building the source code. using the default name Dockerfile allows to run `docker build` command without having to specify any additional command flags.

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
	return "Hello World!"
```

for that application to be deployed without docker, the developer would need to ensure many things such as: ensuring the required runtimes and dependencies are installed on the server, the python code gets uploaded to the server's filesystem, and the server correctly starts the application using the correct necessary parameters.

the following Dockerfile solves all of that:
```Dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:22.04

# install app dependencies
RUN apt-get update & &apt-get install -y python3 python3-pip
RUN pip install flask==3.0.*

# install app
COPY hello.py /

# final configuration
ENV FLASK_APP=hello
EXPOSE 8000
CMD flask run --host 0.0.0.0 --port 8000
```

the first line is optional. it instructs the docker builder what syntax to use when parsing the Dockerfile. parser directives must appear before any other comment, whitespace or instruction in the Dockerfile.

the `FROM` instruction defines what base image to use. in this case, it sets the base image to the 22.04 release of Ubuntu. everything that follows in the Dockerfile is executed in this base image. so, if the `FROM` instruction was to set the base image to Node.js for example, every following instruction would run in the specified Node runtime.

there are many public images a developer can leverage in their projects, importing them into their build steps using the `FROM` instruction in the Dockerfile.

the `RUN` instructions, as it intuitively defines, executes commands. in this case, it executes a shell in Ubuntu (the base image set) to update and install the app dependencies. as one can notice, the second `RUN` instruction uses `pip` to install Flask, so `pip` must be already installed by the time the Dockerfile tries to run `pip install flask==3.0.*` in the shell. that's why the **first** `RUN` instruction installs `python3-pip`.

that's the importance of layers and how they work. since layers are stacked and one layer is the delta (diff) from the result of the previous layer, the second `RUN` instruction will apply the described commands (delta) into an environment where `python3` and `python3-pip` area already installed.

the `COPY` instruction **copies content from the local build context into the root directory of the image.** in this case, it is copying a file `hello.py` that exists in the build context  into the Ubuntu image. a build context is the set of files that one can access in Dockerfile with instructions such as `COPY` and `ADD`.

`ENV` is used to set environment variables in the Docker build. `ENV FLASK_APP=hello` sets an environment variable in the Ubuntu image. Flask, the framework will use this variable to start the application. without it, Flask wouldn't know where to find the application to be able to run it.

the `EXPOSE` instruction marks that the final image has a service listening port in `8000`. although it isn't required it is good practice to help tools and teams understand what the application is doing.

finally, `CMD` instruction sets the command that is run when the user starts a container based on this image. in other words, when a container is about to host this image, it runs `flask run --host 0.0.0.0 --port 8000`. there are two ways to set `CMD` instructions: **shell and exec**, see difference [here](https://docs.docker.com/reference/dockerfile/#shell-and-exec-form).

to build a **container image** using the Dockerfile example, the `docker build` command can be used:

``` bash
docker build -t dockering:latest .
```

the `-t test:latest` option specifies the name and the tag of the image. the single `.` at the end sets the build context to the current directory. this means that the build expects to find `hello.py` to run the `COPY` instruction in the directory where the build command is invoked. if it is not there, the build will fail.

after an image is built, `docker run` runs it, specifying the image name:

``` bash
docker run -p 127.0.0.1:8000:8000 dockering:latest
```

this publishes the container's port `8000` with the `dockering:latest` image to `localhost:8000` on the docker host.