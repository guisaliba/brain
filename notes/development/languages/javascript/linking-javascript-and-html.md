JavaScript é uma linguagem de programação de alto nível multi-paradigmas, é largamente utilizada para construções de interfaces web, trabalhando lado a lado com o HTML e o CSS.

Na estrutura de arquivos para a construção de um website por exemplo, devemos ter pelo menos um arquivo .html, responsável por renderizar os elementos html na tela. Junto à ele, podemos ter um arquivo .js, que será responsável pela lógica JavaScript do website. Assim, para *linkarmos* os elementos html com a lógica do JavaScript, adicionamos uma tag html *<script></script> ao final do <body>*do html.



``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>JavaScript Fundamentos - 1</h1>

    <script src="main.js"></script>
  </body>
</html>
```

Neste exemplo, na estrutura do repositório, temos um arquivo html (chamado de index.html) e outro arquivo JavaScript chamado main.js. Este arquivo por sua vez está sendo conectado ou linkado ao html por meio da tag <script></script> como mencionado anteriormente, ao final do elemento <body> no html.
