
## SPA e SSR são Rendering Patterns, métodos de renderização dos conteúdos numa página.

### SSR (Server Side Rendering)

SSR é o método tradicional de renderização, funciona em um fluxo de comunicação browser-servidor aonde toda requisição feita pelo browser (cliente) chega até o servidor, para que ele possa gerar/criar todo o HTML, CSS, JS e devolver ao cliente.

É comum em sites que utilizam SSR ver uma tela branca enquanto a página carrega. Isso acontece pois o servidor está carregando o conteúdo da página no momento em que o usuário fez a requisição.

### SPA (Single-Page Application)

No modelo de renderização SPA, o fluxo é diferente. Temos duas aplicações divididas: quando o browser (cliente) faz a requisição de alguma rota, o servidor (back-end) não fica mais encarregado pela construção do HTML, CSS, JS, ou seja, a construção visual da tela.

O servidor retorna apenas as informações que estão sendo requisitadas em forma de um JSON (JavaScript Object Notation), que é uma estrutura de dados universal para carregar/transportar dados. Com esse JSON, uma segunda aplicação entra em cena: o Front-end.

O Front-end fica responsável por obter esses dados fornecidos pelo JSON e convertê-los naquilo que é visual e interativo (em HTML, CSS e JS). Isso abre um leque de várias tecnologias para construção do Front-end, uma vez que o JSON pode ser entendido por todas elas.

Uma aplicação SPA pode utilizar um Back-end (servidor) que alimenta JSON para seu Front-end React para aplicações web ou React Native para aplicações mobile, por exemplo.

#patterns