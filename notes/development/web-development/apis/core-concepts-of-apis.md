# subject: [[api]]
# topics: #web-development
---
## O que é um endpoint de uma API e por que ele é importante?

Os endpoints da API são os pontos de contato finais no sistema de comunicação da API. Estes incluem URLs de servidores, serviços e outros locais digitais específicos de onde as informações são enviadas e recebidas entre sistemas.

Em outras palavras, são os pontos em que uma API se conecta com o software/programa. Esses pontos especificam quando e aonde a API pode acessar recursos e ajudam a garantir o funcionamento do(s) programa(s) conectado(s) à ela.

Os endpoints da API são fundamentais para as empresas por dois motivos principais:

### 1. Segurança

Os endpoints da API tornam o sistema vulnerável a ataques. O monitoramento da API é crucial para impedir o uso indevido.

### 2. Performance

Os endpoints da API, especialmente os de alto tráfego, podem causar gargalos e afetar a performance do sistema.

Programas de software geralmente possuem múltiplas APIs incorporadas e em funcionamento. O Instagram, por exemplo, possui diversos endpoints e um desses endpoints é responsável por mostrar o número de interações de uma postagem ao dono dela, outro é responsável por permitir a moderação dos comentários e respostas da postagem, etc.

## Como os endpoints funcionam?

Sistemas que se comunicam por meio de APIs são chamados de sistemas integrados. O lado que **envia** informações para a API é chamado de **servidor (sever)****. O outro lado, quem faz as requisições dessa informações e manipula a API, é chamado de **cliente (client)**.

O ponto (a parte) do servidor que fornece essas informações é o ****************endpoint**************** da API.

Para uma requisição ser processada com sucesso pelo endpoint, o cliente precisa fornecer uma URL, um método, uma lista de headers e um body na requisição.

### Headers

Os headers são responsáveis por provêr metadados de uma requisição. 

### Body
O body é o responsável por armazenar os dados enviados pelo cliente ao servidor.

Endpoints trabalham em conjunto com métodos de APIs. Na maioria das vezes, um endpoint funciona em virtude de um (ou mais) método(s). Um exemplo claro disso seria um endpoint fictício da Série A de futebol brasileiro, que seria responsável por listar todos os times da competição:

`GET https://brasileirao.com.br/serieA/teams`

O método **GET** antes do endpoint significa que está sendo feita uma requisição do tipo GET (obter informações) no endpoint **seriea/teams.** Nesse exemplo, o servidor poderia estar requisitando as informações sobre esses times ao Amazon DynamoDB Service, do lado do servidor a requisição seria lida como *[https://dynamodb.us-west-2.amazonaws.com](https://dynamodb.us-west-2.amazonaws.com)*

A arquitetura de uma API geralmente é explicada em termos de cliente e servidor. A aplicação que envia a solicitação é chamada de cliente e a aplicação que envia a resposta é chamada de servidor.

Existem quatro maneiras diferentes pelas quais as APIs podem funcionar, dependendo de quando e por que elas foram criadas:

### APIs SOAP
Essas APIs usam o Simple Object Access Protocol (Protocolo de Acesso a Objetos Simples). Cliente e servidor trocam mensagens usando XML. Esta é uma API menos flexível que era mais popular no passado.

### APIs RPC
Essas APIs são conhecidas como Remote Procedure Calls (Chamadas de Procedimento Remoto). O cliente conclui uma função (ou um procedimento) no servidor e o servidor envia a saída de volta ao cliente.

### APIs WebSocket
A API de WebSocket é outro desenvolvimento de API da Web moderno que usa objetos JSON para transmitir dados. Uma API WebSocket oferece suporte à comunicação bidirecional entre aplicativos cliente e o servidor. O servidor pode enviar mensagens de retorno de chamada a clientes conectados, tornando-o mais eficiente que a API REST.

### APIs REST
Essas são as APIs mais populares e flexíveis encontradas na Web atualmente. O cliente envia solicitações ao servidor como dados. O servidor usa essa entrada do cliente para iniciar funções internas e retorna os dados de saída ao cliente. Ver anotação sobre [API REST](https://www.notion.so/API-RESTful-50353d44db6c406090b0644dc70866c5?pvs=21).