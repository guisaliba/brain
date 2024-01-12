Container e Imagem são dois conceitos no Docker que estão extremamente interligados. Entender o funcionamento de um é fundamental para entender o funcionamento do outro, e vice-versa.

Em poucas palavras, uma Imagem é um ambiente em que se rodará um Container. É a partir da Imagem que o Container executa aquilo que ele precisa executar. Sem uma Imagem, um Container não pode existir.

É por isso que, quando tentamos rodar um container através do Docker Client no terminal, se a imagem para aquele container não existir, ele tentará puxá-la do Docker Hub e criá-la antes de subir o container.

O Docker Hub é um repositório de Imagens, como se fosse um GitHub porém de imagens Docker.

Podemos fazer uma analogia sobre Container e Imagem utilizando o JavaScript:

```jsx
class Imagem {
	programas
	variaveis_de_ambiente
	aplicacao
	etc
}

const container = new Imagem(); 
```

Assim como no JavaScript uma variável é uma caixa, um espaço que recebe algum dado, no Docker, o Container é um espaço aonde será recebido algo e posteriormente executado.

A variável container nessa analogia está recebendo uma função que executa a classe Imagem.

E a partir de uma imagem, é possível iniciar VÁRIOS containers. Na analogia, teríamos algo assim:

```jsx
class Imagem {
	programas
	variaveis_de_ambiente
	aplicacao
	etc
}

const container = new Imagem();
const container2 = new Imagem();
const container3 = new Imagem();
const container4 = new Imagem(); 
```

Um **Container** pode ser definido também como um **processo**. Ele é um processo rodando dentro da Imagem, que engana o Container e o faz achar que ele está rodando dentro de um OS próprio.

Porém, o que acontece quando se sobe um Container é que ele está sendo executado dentro daquela Imagem, e ele está sendo executado em alguma **porta** nessa Imagem.

Esse comportamento faz com que o OS da máquina principal (host) não tenha acesso à essa porta em que o Container está conectado e executando, **a máquina host não possui conhecimento desse processo rodando naquela porta**, uma vez que ela não existe dentro do host.

Para contornar essa situação, precisamos fazer um **binding de portas**.

Em outras palavras, é necessário **apontar** uma porta da máquina host para a porta em que o Container está sendo executado. Por exemplo, se nosso container está rodando na porta **80**, precisamos apontar uma porta da máquina host para essa porta do container.

```bash
$ docker run -p 8000:80 nginx:1.19.10-alpine
```

O que esse comando está fazendo é exatamente o binding de portas. Ele está indicando à maquina host que a **porta 8000** deve apontar para **a porta 80** do Docker, aonde rodará o processo nginx.