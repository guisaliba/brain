## Nível 0:

- Uma API está no Nível 0 quando ela utiliza do protocolo HTTP.
- Porém essa API utiliza o protocólo apenas para comunicação.
- Não utiliza as semânticas do HTTP.
- Exemplos de API no Nível 0 são aquelas que utilizam apenas um método como o POST por exemplo.

## Nível 1:

- Uma API que contempla o Nível 1 é aquela que utiliza as URIs de uma forma mais eficiente
- Apresenta um mapeamento bem definido para cada recurso.
- Possui mais de uma URI.
- Um exemplo seria uma API que possui um recurso de produtos: [http://localhost:3000/produtos](http://localhost:3000/produtos)
## Nível 2:

- Para uma API estar nesse nível, ela precisa além de utilizar o protocolo HTTP para comunicação, utilizá-lo com a semântica correta de seus verbos.
- Para cada uma das requisições como GET POST DELETE e PUT, a API deve utilizar o verbo correto do HTTP.
- Uma API nesse nível também utiliza os retornos do HTTP. Ao enviar uma requisição ao servidor, ele retornar algo, por exemplo um Status: 200, 300, 400 etc.
- Quando queremos buscar produtos do banco de dados por exemplo, utilizamos o GET. Se queremos salvar, utilizamos o POST. Dessa maneira, estamos utilizando a semântica dos verbos do protocolo HTTP.
- Essa seria uma API que contempla o Nível 2 de Maturidade.

## Nível 3:

- O Nível 3 é quando a API utiliza o protocolo HTTP, tem os recursos bem definidos, os verbos e retornos definidos
    
- E além de tudo isso, ela utiliza de HATEOAS.
    
- Os HATEOAS são os caminhos dentro da API que mostram a relação dos recursos.
    
    #### Por exemplo, numa API de produtos, um determinado produto listado possui um id que o identifica e um link com uma URI que possibilita acessá-lo especificamente na API.
    
- O inverso também ocorre. Ao acessar aquele específico produto, ele possui também um caminho de retorno, em que ele volta para o local que está inserido.
    

### Ao satisfazer esses 4 pilares, a API pode ser considerada [[restful-api]]