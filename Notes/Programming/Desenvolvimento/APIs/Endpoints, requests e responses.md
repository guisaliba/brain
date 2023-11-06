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

Os headers são responsáveis por provêr metadados da requisição

### Body

O body é o responsável por armazenar os dados enviados pelo cliente ao servidor.

Endpoints trabalham em conjunto com métodos de APIs. Na maioria das vezes, um endpoint funciona em virtude de um (ou mais) método(s). Um exemplo claro disso seria um endpoint fictício da Série A de futebol brasileiro, que seria responsável por listar todos os times da competição:

`GET https://brasileirao.com.br/serieA/teams`

O método **GET** antes do endpoint significa que está sendo feita uma requisição do tipo GET (obter informações) no endpoint **seriea/teams.** Nesse exemplo, o servidor poderia estar requisitando as informações sobre esses times ao Amazon DynamoDB Service, do lado do servidor a requisição seria lida como *[https://dynamodb.us-west-2.amazonaws.com](https://dynamodb.us-west-2.amazonaws.com)*