on a Dockerfile, the `FROM` command that specifies the base image fetches an image from somewhere. usually, this image gets fetched from Dockerhub but there are many places that host images and leverages pulling these images to your applications.

when a base image gets pulled from a hub (or host) for the first time, running that Dockerfile image again won't pull that base image again, since it's already cached in your machine. that saves a lot of resources and build time.

usually an image is a service that will run in a kind of VM (but it's not actually a VM, it's a process with limited resources borrowed from the host machine). running `docker container ls` lists the running images and where they are living. `ps aux | grep <image>` will display the process information (PID and other stuff) that runs the image you're searching for.

an image is a read-only template with instructions to create a Docker container. often, an image is based on another image (e.g.: your image needs the Ubuntu 22.04 image for your application to actually work) with some additional customization.

you might create your own images or you might use existing images published in a registry. to build your own image you create a [[Dockerfile]] defining the steps needed to create the image and run it.