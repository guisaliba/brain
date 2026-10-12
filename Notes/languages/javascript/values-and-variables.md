Um valor em JavaScript é basicamente a menor unidade de informação que podemos ter na linguagem. O nome "Guilherme" pode ser um valor bem como o número 23 ou os booleanos true/false, todos eles podem ser chamados de valores no JavaScript.

Guardamos esses valores dentro de variáveis. Variáveis são espaços na memória da maquina que guardam/recebem valores, sendo que, quanto maior ou mais complexo o valor sendo guardado nela, maior o espaço ocupado por essa variável na memória. Podemos pensar em variáveis como caixas que guardam itens, e podemos pensar nesses itens sendo os valores.

``` js
// variável = valor
let firstName = "Guilherme";
let age = 21;

console.log(firstName, number);
```

Variáveis são extremamente importantes em JavaScript, e por isso, existem convenções para nomenclaturas de variáveis, para que elas não tenham nomes aleatórios ou despadronizados.

A convenção mais utilizada para nomenclatura de variáveis em JavaScript é a chamada **camelCase**, é bem comum ver códigos em que variáveis estejam escritas dessa forma, e isso porque é uma convenção de nomenclatura da linguagem.

Além disso, existem algumas regras a serem seguidas na hora de nomear uma variável, essas regras são específicas da linguagem e quando desobedecidas criam um erro no código:

- Variáveis não podem começar com um número:
	 let 3years = 3;
- Variáveis não podem conter símbolos além de cifrão ($) e underscore ( _ ):
	 let me&you = "us";
-  Variáveis não podem ser nomeadas com palavras reservadas da linguagem:
	  let function = "Function";

Fora essas, existem outras convenções a respeito de palavras reservadas da linguagem que são seguidas. Por exemplo, deve-se evitar nomear uma variável com a primeira letra maiúscula, pois essa nomenclatura é utilizada em Orientação a Objetos.

Nomear uma variável da forma correta é extremamente importante, e o nome de uma variável deve ser bem claro e objetivo. Uma variável deve "explicar" de maneira simples e objetiva o valor que ela está recebendo. No exemplo abaixo, temos bons exemplos de nomenclatura de variáveis e exemplos ruins também:

``` js
// Bom
let myFirstJob = "Programmer";
let myCurrentJob = "Engineer";

// Ruim
let job1 = "Programmer";
let job2 = "Engineer";
```

### camelCase:

`myFirstName` —> camelCase
`myCurrentJob` —> camelCase
