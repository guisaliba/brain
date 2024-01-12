### Visão geral do HTTP

**HTTP** é um **protocolo** que permite a obtenção de recursos, como documentos HTML. É a **base** de qualquer troca de dados na Web e um protocolo **cliente-servidor**, o que significa que as requisições são iniciadas pelo destinatário, geralmente um navegador da Web.

Clientes e servidores se comunicam trocando mensagens individuais (ao contrário de um fluxo de dados). As mensagens enviadas pelo cliente, geralmente um navegador da Web, são chamadas de **solicitações** (requests), ou também **requisições**, e as mensagens enviadas pelo servidor como resposta são chamadas de **respostas** (responses).

O HTTP é um protocolo **cliente-servidor**: as requisições são enviados por uma entidade, o agente-usuário (ou um _proxy_ em nome dele). A maior parte do tempo, o agente-usuário é um navegador da Web, mas pode ser qualquer coisa, como por exemplo um robô que varre a Web para preencher e manter um índice de mecanismo de pesquisa e coletar informações.

Cada requisição individual é enviada para um servidor, que irá lidar com isso e fornecer um resultado, chamado de **resposta**. Entre a solicitação e a resposta existem várias entidades, designadas coletivamente como [proxies](https://developer.mozilla.org/pt-BR/docs/Glossary/Proxy_server), que executam operações diferentes e atuam como **gateways** (intermediários) ou [caches](https://developer.mozilla.org/pt-BR/docs/Glossary/Cache), por exemplo.

Na realidade, existem muitos outros computadores entre o navegador e o servidor que está tratando a requisição: existem roteadores, modems e muito mais. Graças ao modelo de camadas da Web, essas funcionalidades estão escondidas nas camadas de rede e transporte, respectivamente.

![[images/Programming concepts/HTTP/1.png]]

O agente-usuário, predominantemente chamado de **cliente**, é qualquer ferramenta que age em nome do **usuário**. Na maioria dos casos, é o **navegador Web** (o browser).

O navegador é ************sempre************ a entidade que inicia as requisições ao servidor.

Para mostrar uma página na web por exemplo, o navegador envia uma **requisição** ao servidor pedindo o documento **HTML** daquela página. Ele então realiza uma análise do arquivo e todos seus componentes, bem como recursos adicionais como o CSS ou scripts.

Depois disso, o navegador **interpreta** tudo que foi buscado e mostra em **tela** ao usuário.

### O servidor (de páginas Web):

Do outro lado do canal de comunicação está o servidor que serve o documento requisitado pelo usuário. Um servidor se apresenta virtualmente apenas como uma máquina: isto porque o servidor pode ser uma coleção de servidores dividindo a carga.

Um servidor não é necessáriamente apenas uma máquina, mas vários servidores podem estar hospedados na mesma máquina.

### Proxies (ou representantes):

Entre o navegador Web e o servidor, vários computadores e máquinas transmitem as mensagens HTTP. Devido a estrutura em camadas da pilha Web, a maioria dessas máquinas operam em alguma das camadas: de transporte, de rede ou física, sendo transparente na camada da aplicação HTTP, e potencialmente exercendo um grande impacto na performance.

Essas máquinas que operam na camada de aplicação são normalmente conhecidas como *******_**proxies**_ (ou representantes, ou procuradores, etc).

Eles podem ser transparentes ou não (alterações nas requisições não passam por eles), e podem desempenhar várias funções:

-   **cacheamento** (o _cache_ pode ser público ou privado, como o _cache_ dos navegadores)
-   **filtragem** (como um _scanner_ de antivírus, controle de acesso, etc)
-   **balanceamento de carga** (para permitir que vários servidores possam responder a diferentes requisições)
-   **autenticação** (para controlar quem tem acesso aos recursos)
-   **autorização** (para controlar quem tem acesso a determinada informação)
-   **registro de informação** (permite o armazenamento de informações de histórico)

## O fluxo HTTP

Quando o cliente quer comunicar com um servidor, este sendo um servidor final ou um _proxy_, ele realiza os seguintes passos:

1.  Abre uma conexão TCP: A conexão TCP será usada para enviar uma requisição, ou várias, e receber uma resposta. O cliente pode abrir uma nova conexão, reusar uma conexão existente, ou abrir várias conexões aos servidores.
    
2.  Envia uma mensagem HTTP: mensagens HTTP antigas (1.1 ou anteriores) são legíveis às pessoas. Isso foi completamente mudado a partir do HTTP/2.0.
    
    ```json
    GET / HTTP/1.1
    Host: developer.mozilla.org
    Accept-Language: fr
    ```
    
3.  Lê a resposta do servidor:
    
    ```json
    HTTP/1.1 200 OK
    Date: Sat, 09 Oct 2010 14:28:02 GMT
    Server: Apache
    Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
    ETag: "51142bc1-7449-479b075b2891b"
    Accept-Ranges: bytes
    Content-Length: 29769
    Content-Type: text/html
    
    <!DOCTYPE html... (here comes the 29769 bytes of the requested web page)
    ```
    
4.  Fecha ou reutiliza a conexão para requisições futuras.

### Mensagens HTTP

HTTP/1.1 e mensagens mais antigas HTTP são legíveis às pessoas.

No HTTP/2.0, essas mensagens são embutidas numa nova estrutura binária, um quadro, permitindo otimizações como compressão de cabeçalhos e multiplexação.

### Requisições

Exemplo de uma requisição HTTP:

![[images/Programming concepts/HTTP/2.png]]

As requisições consistem dos seguintes elementos:

-   Um método HTTP, geralmente é um verbo como [GET](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/GET>), [POST](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/POST>), [DELETE](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/DELETE>), [PUT](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/PUT>), etc. ou um substantivo como [OPTIONS](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/OPTIONS>) ou [HEAD](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/HEAD>) que define qual operação o cliente quer fazer. Tipicamente, um cliente quer **pegar um recurso** (usando [GET](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/GET>)) ou **publicar dados** de um formulário HTML (usando [POST](<https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods/POST>)).
-   O **caminho** do recurso a ser buscado:  URL do recurso sem os elementos que são de contexto, por exemplo sem o protocolo, o domínio ou a porta.
-   A **versão** do protocolo HTTP.
-   **Cabeçalhos** (headers) opcionais que contém informações adicionais para os servidores.
-   Ou um corpo de dados, para alguns métodos como `POST`, similares aos corpos das respostas, que contém o recurso requisitado.

### Respostas

Exemplo de resposta HTTP:

![[images/Programming concepts/HTTP/3.png]]

Respostas consistem dos seguintes elementos:

-   A **versão** do protocolo HTTP que elas seguem.
-   Um **código de status**, indicando se a requisição foi bem sucedida, ou não, e por quê.
-   Uma **mensagem de status**, uma pequena descrição informal sobre o código de status.
-   Cabeçalhos HTTP, como aqueles das requisições.
-   Opcionalmente, um corpo com dados do recurso requisitado.

## Aspectos básicos do HTTP

### HTTP não tem estado, mas tem sessões

HTTP é sem estado: não existe uma relação entre duas requisições sendo feitas através da mesma conexão. Isso traz um problema imediato para usuários que interagem com algumas páginas de forma coerente, por exemplo, usando um carrinho de compras de _e-commerces_.

Mas como o fundamento básico do HTTP é não manter estados, _cookies_ HTTP permitem que as sessões tenham estados. Usando a extensibilidade dos cabeçalhos, os _cookies_ são adicionados ao fluxo do HTTP, permitindo que a criação de sessão em cada requisição HTTP compartilhem o mesmo contexto, ou o mesmo estado.

 💡 O problema do carrinho de compras de _e-commerces_ e o protocolo HTTP: como o protocolo HTTP não guarda o estado das requisições e respostas, é **impossível** fazer com que um site guarde as informações de um carrinho de compras **somente através do HTTP**. Por exemplo, imagine que você irá comprar um computador novo e um jogo de xícaras de chá. Para que esses dados possam ser mantidos enquanto você navega no site do _e-commerce_ olhando mais produtos (cada página visitada gera um novo par de requisição/resposta), duas estratégias podem ser usadas, já que o HTTP por si só, não permitiria isso:

1.  Você possui um cadastro no _e-commerce_ e um programa escrito no servidor é responsável por armazenar suas informações do carrinho; ou
2.  Um programa escrito em linguagem cliente (como JavaScript), gerencia essas informações através dos _cookies_ e de bancos de dados que os próprios navegadores disponibilizam para as aplicações, para armazenamento **temporário** dessas informações de carrinho. 

### HTTP e conexões

Uma conexão é controlada na camada de transporte, e portanto fundamentalmente **fora** do controle do HTTP. Entretanto o HTTP não requer que o protocolo de transporte utilizado seja baseado em conexões, só requer que seja **confiável** ou **não perca** mensagens.

Dentre os dois protocolos de transporte mais comuns na internet, o **TCP é confiável** e o UDP não. Portanto, o **HTTP utiliza o padrão TCP,** que é baseado em conexão, mesmo que nem sempre seja obrigatório o uso de uma conexão.

### O que pode ser controlado pelo HTTP?

-   **Cache:** O servidor pode instruir _proxies_ e clientes, sobre o que cachear e por quanto tempo.
-   **Relaxamento das restrições na origem:** Para prevenir bisbilhoteiros e outros invasores de privacidade, os navegadores reforçam estritamente a separação dos sites Web. Somente páginas de **mesma origem** podem acessar todas as informações de uma página Web.
-   **Autenticação:** Algumas páginas podem ser protegidas para que apenas usuários específicos possam acessá-la. Autenticação básica pode ser fornecida pelo HTTP, usando tanto o cabeçalho `WWW-Authenticate` e similares, quanto configurando uma sessão específica usando cookies HTTP.
-   **Proxy e tunelamento:** **Servidores e/ou clientes estão frequentemente localizados em _intranets_ e escondem seu verdadeiro endereço IP aos outros. Requisições HTTP recorrem aos _proxies_ para contornar essa barreira na rede.
-   **Sessões:** Usando os _cookies_ HTTP, permite você vincular requisições com o estado do servidor. Isso cria as sessões, apesar do protocolo HTTP básico não manter estado.

#web #redes