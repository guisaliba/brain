# subject: [[docker]]
# topics: #containers #vm 

the keyword for understanding docker is **containers.** understanding what containers are is fundamental to understanding how docker works. and to understand containers, we need to understand the concept of **virtual machines.**

a virtual machine is an environment that runs within another Operating System (**OS**). it emulates an entire Operating System, from the kernel to all configurations of the chosen OS. this causes the user to have a resource **overhead**.

and what does resource overhead mean? it means that when a virtual machine is initialized, it will mandatorily hijack resources from the machine on which it is hosted. that is, CPU processing and available memory. the more virtual machines initialized, or rather, the more environments sequestering resources, the heavier the entire process becomes.

these machines could be used, for example, in a scalable application that grows increasingly in size, demanding more and more virtual machines to be raised. from this, a light, simple, and conducive environment becomes necessary: **containers.**
### O conceito de Máquinas Virtuais:

Primeiro precisamos entender o que são VM’s. Virtual Machines (VM’s) são Máquinas Virtuais com OS próprio que executam de forma isolada dentro do Host (OS principal).

Com isso é possível separar as execuções de programas do Host. Uma VM tem seu próprio kernel, seus próprios binários e libs e cada uma das coisas executadas nela terão também seu próprio OS separado. Dessa forma, mexer em cada um deles não afetará mais os outros.

VM’s são pesadas e não muito optimizadas, requerem muito processamento do Host.

Uma melhor alternativa surge então, os Linux Containers.

### Containers:

Os Containers são como as VM’s porém eles são executados no mesmo kernel do Host (da máquina base), sem criar um novo para cada novo programa executado, tornando-se mais leve e eficiente.

Esse mecanismo é chamado de Container Engine. O Docker é um Container Engine, ele é responsável por administrar os containers nos quais estamos mexendo.

Uma **Imagem** é um pacote que contém os arquivos e as configurações necessárias para criar um container. Uma vez que o container é iniciado, ele herda as configurações da imagem e executa o código especificado na imagem.

E podemos baixar esses ambientes e pacotes da internet, assim como o npm (Node Package Manager) através do **Dockerhub**. As Imagens possibilitam uma portabilidade muito maior ao Docker (aos containers) em relação as VM’s.

### Daemon e Client:

O Docker possui um daemon e um cliente. O Daemon é responsável por executar os containers e gerenciar seus recursos. O cliente é usado para criar e gerenciar containers.