O Express é um framework do Node.js para construção de diversas aplicações. Uma das possibilidades de criação com o Express é de poder criar uma API, com endpoints, métodos HTTP (GET, POST, PUT...) e poder realizar comunicações request e response, como todo servidor http faz.

Dito isso, é bem simples inicializar um servidor http utilizando o Express. Como toda biblioteca ou framework, ele é uma dependência e pode ser instalada utilizando tanto npm como yarn. Nessa anotação, utilizei o npm para inicialização do package.json no projeto e para instalação do Express no projeto também.

1. No repositório do projeto, abra o terminal e inicialize o arquivo package.json utilizando npm:
	``` bash
	npm init -y
	```
Agora, podemos instalar o Express no nosso projeto como dependência através do npm.

2.  Novamente no terminal, digite o comando:
	``` bash
	npm install express
	```
Isso instalará o Express como dependência do projeto, e todos seus métodos, propriedades e também suas dependências estarão disponíveis para serem importadas em qualquer arquivo.

3. Importe o Express no arquivo desejado e crie uma instanciação dele.
	``` javascript
	const express = require('express');
	const app = express();
	```
O que essas duas linhas fazem é importar o framework Express no arquivo, e em seguida instanciá-lo em outra variável para que os métodos e propriedades do framework possam ser utilizados.

4. Agora podemos criar a primeira rota do nosso servidor, e subí-lo em alguma porta.
``` javascript
	const express = require('express');
	const app = express();

	app.get('/', (req, res) => {
		res.send('Hello World!');
	});

	app.listen(3000, () => console.log('Server running at http://localhost:3000'));
	```

Simples assim, num único arquivo, criamos um servidor http utilizando o Express, subimos ele na porta 3000 da nossa máquina e definimos um método **GET** para a rota **/** que ao receber uma request retorna a string Hello World! como response.

#node 