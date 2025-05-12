# subject: [[docker]]
# topics: #docker #containers #vm

## understanding docker through containers

the keyword for understanding docker is **containers.** understanding what containers are is fundamental to understanding how docker works. and to understand containers, we need to understand the concept of **virtual machines.**

a virtual machine is an environment that runs within another Operating System (**OS**). it emulates an entire Operating System, from the kernel to all configurations of the chosen OS. this causes the user to have a resource **overhead**.

and what does resource overhead mean? it means that when a virtual machine is initialized, it will mandatorily hijack resources from the machine on which it is hosted. that is, CPU processing and available memory. the more virtual machines initialized, or rather, the more environments sequestering resources, the heavier the entire process becomes.

these machines could be used, for example, in a scalable application that grows increasingly in size, demanding more and more virtual machines to be raised. from this, a light, simple, and conducive environment becomes necessary: **containers.**

## containers:

instead of virtualizing an entire machine to create a new environment, containers are just a process in the OS that is **tricked** into thinking it has an entire Operating System at its disposal. in the end, it is just a process, much simpler, efficient, and cheaper.

this is the idea of **docker**. creating containers to build applications inside them. the main advantage of containers is that, unlike virtual machines, they share resources with the main OS, and also share among themselves (in the case of multiple containers running on the machine).