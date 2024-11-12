Muitas vezes durante desenvolvimento iremos nos deparar com a seguinte situação: o frontend está sendo feito, ou quase pronto porém o backend do produto ainda não está preparado para ser consumido no front.

Isso significa que, nosso frontend não tem de onde puxar dados ou fazer requests, tratar erros etc, tudo que ele pode fazer é trabalhar com dados estáticos, o que não é de muita ajuda.

O que podemos fazer nesse tipo de situação é mockar uma API.

## O que isso quer dizer?

Quer dizer que podemos criar uma fake API para que nosso frontend possa dar continuidade ao desenvolvimento. A palavra “mockar” é uma expressão que se traduz em “fingir”.

Existem inúmeras formas de se fazer isso e até mesmo ferramentas ou bibliotecas. MirageJS, json-server, etc. são todos exemplos dessas.

## E como fazer isso?

Simples. Instalamos uma ferramenta ou biblioteca, e em seguida, usando os métodos e funções da ferramenta instalada, começamos a construir nossa fake API no próprio frontend.

Na root da nossa aplicação (ou no index) aonde estamos renderizando tudo, podemos usar uma função do MirageJS por exemplo para já construir nossa API ali mesmo.

```tsx
createServer({
  routes() {
    this.namespace = 'api'

    this.get('/transactions', () => {
      return [
        {
          id: 1,
          title: 'transaction 1',
          amount: 400,
          type: 'withdraw',
          category: 'Food',
          createdAt: new Date(),
        },
      ]
    })
  },
})
```

## O que esse pedaço de código está dizendo?

A função createServer() está mockando um servidor para receber requests HTTP do nosso frontend. Dentro dela, podemos definir as rotas em que queremos receber essas chamadas.

A função routes() é a responsável aqui por definir as rotas, quando escrevemos this.namespace = ‘api’ estamos dizendo ao servidor que nossas rotas virão do endpoint [https://app/api](https://app/api). Assim, toda rota definida partirá desse endpoint.

O this.get() é nada mais nada menos que nossa request, nesse caso do tipo GET. Ela está sendo feita no endpoint /api/transactions e retornando um objeto com várias informações.

## E como o frontend consome essa fake API?

Podemos utilizar um cliente HTTP como o Axios para simular requests na nossa fake API. Implementá-lo no código é simples:

```tsx
// /services/api

import axios from 'axios'

export const api = axios.create({
    baseURL: '<http://localhost/3000/api/>'
})
```

No nosso código, aonde quisermos fazer uso dessa request, como por exemplo em um componente aonde o useEffect() vai observar qualquer alteração nessas requests, escrevemos:

```tsx
import { api } from ./services/api

useEffect(() => {
    api.get('transactions')
      .then((response) => console.log(response.data))
  }, [])
```

## O que esse pedaço de código está dizendo?

O useEffect() é o responsável por observar no React quando o valor de uma variável é alterado, e ser executado novamente a cada mudança.

Nossa const api é uma função do Axios que cria um cliente HTTP para nossa API do MirageJS. O baseURL define de qual endereço as requests serão feitas. Nesse exemplo a request é do tipo GET, então `api.get('transactions')` está fazendo uma request para o endpoint /transactions.