Quando utilizamos o Docker em nossa máquina, ele é composto de dois agentes:

- **Docker Daemon**
    
    O Docker Daemon é como se fosse um servidor. Esse servidor fica rodando o tempo inteiro em nossa máquina, e ele é o responsável por administrar os containers e imagens da aplicação.
    
- **Docker Client**
    
    O Docker Client é quem se comunica com o Docker Daemon (o servidor) através das linhas de comando que o usuário digita.
    

Esse paralelo pode ser imaginado como se fosse uma API REST. Existe um client e um servidor, o client é o responsável por fazer chamadas ao servidor. Nesse caso, client e servidor são Client e Daemon respectivamente.

Quando executamos um comando docker no terminal, o Docker Client se comunica com o Daemon passando por algumas etapas até conseguir executar aquilo que o comando pede:

```bash
$ docker run hello-world
```

Esse comando do Client diz ao Daemon para que ele inicie um Container chamado hello-world. Caso esse container não exista, o servidor (Daemon) identificará essa ausência e automaticamente puxará da Docker Hub a **image** correspondente, criando o Container em seguida.

```bash
$ docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete
Digest: sha256:aa0cc8055b82dc2509bed2e19b275c8f463506616377219d9642221ab53cf9fe
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
```

Esse processo todo ocorreu seguindo uma série de etapas:

1. O Docker Client entrou em contato com o Docker Daemon.
2. O Docker Daemon puxou a image "hello-world" direto do Docker Hub.
3. O Docker Daemon criou um novo container a partir dessa imagem, que roda o executável que produziu a mensagem “Hello from Docker!” (nesse contexto).
4. O Docker Daemon transmitiu essa resposta ao Docker Client, que por sua vez, a enviou para o terminal.