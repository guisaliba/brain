on a Dockerfile, the `FROM` command that specifies the base image fetches an image from somewhere. usually, this image gets fetched from Dockerhub but there are many places that host images and leverages pulling these images to your applications.

when a base image gets pulled from a hub (or host) for the first time, running that Dockerfile image again won't pull that base image again, since the SHA (hash) of the base image didn't change. that saves a lot of resources and build time.

the same happens for the layers of an image, where each instruction ran represents a layer that will only be executed again if the SHA of the base image changes.

usually an image is a service that will run in a _kind of a VM_ (but it's not actually a VM, it's a process with limited resources borrowed from the host machine). running `docker container ls` lists the running images on the current machine and where they are living. `ps aux | grep <image>` will display the process information (PID and other stuff) running the image you're searching for.

an image is a read-only template with instructions to create a Docker container. often, an image is based on another image (e.g.: your image needs the Ubuntu 22.04 image for your application to actually work) with some additional customization.

you might create your own images or you might use existing images published in a registry. sometimes all you need for your simple application to exist is the Node.js runtime, in order to execute your JavaScript code. so you only have to `FROM node` to serve as your base image. from there on, you're good to go running all the other necessary instructions for your code to work.

to build your own image you create a [[Dockerfile]] defining the steps needed to create the image and run it.