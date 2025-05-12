# subject: [[api]]
# topics: #web-development #backend 
---

Uma API é quem permite a comunicação entre sistemas, tanto internamente quanto externamente. É uma aplicação client-server que permite a interoperabilidade entre sistemas.

Seguir as melhores práticas e padrões para se construir uma API é muito importante.

Um dos padrões mais famosos atualmente na web para se fazer uma API é o padrão, o conceito arquitetural chamado **REST.**

## E o que é uma API REST?

- É uma aplicação client-server que utiliza do protocolo HTTP para se comunicar, e também do padrão JSON ou XML para criar essa comunicação.
- A principal característica da API REST é a ausência de estado. A ausência de estado significa que os servidores não salvam dados do cliente entre as solicitações.
- As solicitações do cliente ao servidor são semelhantes aos URLs que você digita no navegador para visitar um site.
- A resposta do servidor corresponde a dados simples, sem a renderização gráfica típica de uma página da Web.

## E qual a diferença entre REST e RESTful?

- REST é um conceito arquitetural para implementar APIs, garantido boas práticas na hora do desenvolvimento ou na hora que o usuário vá consumir essa API.
- RESTful é a implementação do conceito REST em uma determinada API.
- Quando aplicamos os conceitos arquiteturais REST numa API, podemos chamá-la de API RESTful.

## E como sabemos se uma API é RESTful?

- Podemos identificar uma API RESTful através da Maturidade de Richardson.
- O modelo de [[richardson-maturity]] são 4 pilares que, caso seguidos ao construir uma API, ela possa ser considerada uma API RESTful.

## **Quais são os benefícios das APIs RESTful?**

As APIs RESTful oferecem quatro principais benefícios:

### 1. Integração

As APIs são usadas para integrar novas aplicações com sistemas de software existentes. Isso aumenta a velocidade de desenvolvimento porque cada funcionalidade não precisa ser escrita do zero. Você pode usar APIs para aproveitar o código existente.

Exemplo: Seu código precisa implementar um sistema de pagamento dentro do app. Você não precisa escrever tudo isso do zero no código, basta utilizar uma API de algum serviço de pagamento e implementá-la no seu código já feito.

### 2. Inovação

Setores inteiros podem mudar com a chegada de uma nova aplicação. As empresas precisam responder rapidamente e oferecer suporte à rápida implantação de serviços inovadores. Elas podem fazer isso fazendo alterações no nível da API sem precisar reescrever todo o código.

### 3. Expansão

As APIs apresentam uma oportunidade única para as empresas atenderem às necessidades de seus clientes em diferentes plataformas. Por exemplo, a API de mapas permite a integração de informações de mapas por meio de sites, Android, iOS etc. Qualquer empresa pode fornecer acesso semelhante aos seus respectivos bancos de dados internos usando APIs gratuitas ou pagas.

### 4. Facilidade de manutenção

A API atua como um gateway (ponte de comunicação) entre dois sistemas. Cada sistema é obrigado a fazer alterações internas para que a API não seja afetada. Dessa forma, qualquer alteração futura de código feita por uma parte não afetará a outra parte.