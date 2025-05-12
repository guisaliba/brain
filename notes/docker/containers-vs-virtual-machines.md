# subject: [[docker]]
# topics: #containers #vm 

the keyword for understanding Docker is **containers.** understanding what containers are is fundamental to understanding how Docker works. and to understand containers, we need to understand the concept of **virtual machines.**

a virtual machine is an environment that runs within another Operating System (**OS**). it emulates an entire Operating System, from the kernel to all configurations of the chosen OS. this causes the user to have a resource **overhead**.

and what does resource overhead mean? it means that when a virtual machine is initialized, it will mandatorily hijack resources from the machine on which it is hosted. that is, CPU processing and available memory. the more virtual machines initialized, or rather, the more environments sequestering resources, the heavier the entire process becomes.

these machines could be used, for example, in a scalable application that grows increasingly in size, demanding more and more virtual machines to be raised. from this, a light, simple, and conducive environment becomes necessary: **containers.**

### the concept of virtual machines:
first we need to understand what VMs are. virtual machines (VMs) are virtual machines with their own OS that run in isolation within the host (main OS).

this makes it possible to separate program executions from the host. a VM has its own kernel, its own binaries and libs, and each of the things running on it will also have its own separate OS. this way, changing each one will not affect the others.

VMs are heavy and not very optimized, requiring a lot of processing from the host.

a better alternative then emerges, Linux containers.

### containers:
containers are like VMs but they run on the same kernel as the host (the base machine), without creating a new one for each new program executed, making them lighter and more efficient.

this mechanism is called a container engine. Docker is a container engine, responsible for managing the containers we're working with.

an **image** is a package that contains the files and configurations needed to create a container. once the container is started, it inherits the image's configurations and executes the code specified in the image.

and we can download these environments and packages from the internet, just like npm (node package manager) through **Dockerhub**. images enable much greater portability for Docker (for containers) compared to VMs.