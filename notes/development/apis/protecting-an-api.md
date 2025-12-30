# subject: [[api]]
# topics: #web-development #security
---
Se um programa ou aplicativo possui uma API, clientes externos podem solicitar serviços dela.

A segurança das APIs é o processo de proteção das APIs contra ataques. Assim como aplicativos, redes e servidores podem estar sujeitos a ataques, as APIs podem ser vítimas de várias ameaças diferentes.

A segurança de APIs é um componente essencial da segurança de aplicativos web.

A maioria dos aplicativos web modernos depende de APIs para funcionar e as APIs apresentam riscos adicionais a um aplicativo, permitindo que terceiros o acessem.

Uma comparação é uma empresa que abre seu escritório ao público: ter mais pessoas nas instalações, algumas das quais podem ser desconhecidas (podendo obter acessos e recursos delicados sobre o escritório), apresenta maior risco.

Da mesma forma, uma API permite que pessoas de fora usem um programa, introduzindo mais riscos à infraestrutura do serviço de API.

## Quais são alguns riscos comuns de segurança de APIs?

### 1. Explorações de vulnerabilidade:

Uma exploração de vulnerabilidade ocorre quando um invasor envia dados especialmente criados para um alvo, que se aproveitam de uma falha na construção do alvo.

Essas falhas, conhecidas como "vulnerabilidades", podem dar ao invasor várias formas de acesso não intencional a uma API ou seu aplicativo correspondente. O Open Web Application Security Project ([OWASP](https://www.cloudflare.com/learning/security/threats/owasp-top-10)) mantém uma [lista](https://owasp.org/www-project-api-security/) das [10 principais vulnerabilidades de API](https://www.cloudflare.com/learning/security/api/owasp-api-security-top-10/), como [injeção de SQL](https://www.cloudflare.com/learning/security/threats/sql-injection), configuração incorreta de segurança e outras.

Se o invasor utilizar de uma vulnerabilidade anteriormente desconhecida, a exploração é chamada de [ameaça de dia zero](https://www.cloudflare.com/learning/security/threats/zero-day-exploit). São ameaças extremamente difíceis de deter.

### 2. Ataques baseados em autenticação:

Os clientes precisam se autenticar antes de fazer solicitações de API para que o servidor de API não aceite solicitações de fontes desconhecidas ou ilegítimas. Existem várias maneiras de fazer isso, mas cada maneira está sujeita a comprometimento.

Por exemplo, um invasor pode obter as credenciais de um cliente legítimo, por meio de engenharia social ou hacking, roubar uma chave de API ou interceptar e usar um token de autenticação.

### 3. Erros de autorização:

A autorização determina o nível de acesso que cada usuário tem. Se a autorização não for gerenciada com cuidado, um cliente de API pode ter acesso a dados que não deveriam estar disponíveis para ele, aumentando a chance de [violação de dados](https://www.cloudflare.com/pt-br/learning/security/what-is-a-data-breach/).

### 4. Ataques DoS e DDoS:

Muitas solicitações direcionadas a uma API podem retardar ou interromper o serviço para outros clientes. Alguns invasores direcionarão um excesso de solicitações para uma API de propósito em um ataque de [negação de serviço (DoS)](https://www.cloudflare.com/learning/ddos/glossary/denial-of-service) ou de [negação de serviço distribuída (DDoS)](https://www.cloudflare.com/learning/ddos/what-is-a-ddos-attack/).

## E como proteger uma API desses exploits?

Todas as APIs devem ser protegidas por meio de autenticação e monitoramento adequados. As duas principais maneiras de proteger APIs REST incluem:

### 1. Tokens de autenticação

Eles são usados para autorizar os usuários a fazer a chamada de API. Os tokens de autenticação verificam se os usuários são quem afirmam ser e se têm direitos de acesso para aquela chamada de API específica. Por exemplo, quando você faz login em seu servidor de e-mail, seu cliente de e-mail usa tokens de autenticação para acesso seguro.

### 2. Chaves de API

As chaves de API verificam o programa ou a aplicação que faz a chamada de API. Elas identificam a aplicação e garantem que ela tenha os direitos de acesso necessários para fazer a chamada de API específica.

As chaves de API não são tão seguras quanto os tokens, mas permitem o monitoramento da API para coletar dados sobre o uso. Você pode ter notado uma longa sequência de caracteres e números no URL do seu navegador ao visitar diferentes sites. Essa string é uma chave de API que o site usa para fazer chamadas de API internas.

### Referências:

[https://www.cloudflare.com/pt-br/learning/security/api/what-is-api-security/](https://www.cloudflare.com/pt-br/learning/security/api/what-is-api-security/)
[https://aws.amazon.com/pt/what-is/api/#seo-faq-pairs#how-to-secure-a-rest-api](https://aws.amazon.com/pt/what-is/api/#seo-faq-pairs#how-to-secure-a-rest-api)