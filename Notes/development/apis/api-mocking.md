# subject: [[api]]
# topics: #web-development #backend
--- 
Muitas vezes durante desenvolvimento iremos nos deparar com a seguinte situação: o frontend está sendo feito, ou quase pronto porém o backend do produto ainda não está preparado para ser consumido no front.

Isso significa que, nosso frontend não tem de onde puxar dados ou fazer requests, tratar erros etc, tudo que ele pode fazer é trabalhar com dados estáticos, o que não é de muita ajuda.

O que podemos fazer nesse tipo de situação é mockar uma API.

## O que isso quer dizer?

Quer dizer que podemos criar uma fake API para que nosso frontend possa dar continuidade ao desenvolvimento. A palavra “mockar” é uma expressão que se traduz em “fingir”.

Existem inúmeras formas de se fazer isso e até mesmo ferramentas ou bibliotecas. MirageJS, json-server, etc. são todos exemplos dessas.

## E como fazer isso?

Simples. Instalamos uma ferramenta ou biblioteca, e em seguida, usando os métodos e funções da ferramenta instalada, começamos a construir nossa fake API no próprio frontend.

Suponha que estamos escrevendo uma aplicação em React, podemos fazer uso de uma biblioteca chamada MirageJS por exemplo e construir um endpoint qualquer que nos retorne alguns dados essenciais da nossa aplicação.

Um exemplo de código com o Mirage:

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

## E como o frontend consome essa fake API?
Podemos utilizar um cliente HTTP como o Axios por exemplo, se estivermos utilizando um frontend JavaScript como o React para simular requests na nossa fake API. Implementá-lo no código é simples:

```tsx
// /services/api

import axios from 'axios'

export const api = axios.create({
    baseURL: '<http://localhost/3000/api/>'
})
```

A partir disso podemos utilizar quaisquer dados retornados por essa request e consumi-los em nosso frontend.