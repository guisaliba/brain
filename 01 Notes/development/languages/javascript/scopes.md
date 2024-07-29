Escopos no JavaScript moderno (ES6) são como limitações ou blocos que existem em nosso código.

Esses blocos tem como função por exemplo, determinar se uma variável estará disponível no nosso código inteiro, de forma **global, ou se ela só estará disponível para ser utilizada dentro de algum pedaço de código, como uma função.**

Podemos dar um exemplo de uma variável em escopo global assim:

```js
var animal = 'dog'
var sound = 'auau'

console.log(animal);
console.log(sound);

// dog
// auau
```

Essas duas variáveis, animal e sound, estão definidas no código, sem estarem dentro de uma função, classe ou objeto. Portanto, podemos classificá-las como variáveis globais, que estão definidas no escopo global do JavaScript.

Isso permite com que possamos acessá-las de qualquer lugar do nosso código, dentro de qualquer função ou classe. Agora imagine outro cenário, em que essas variáveis existam somente na função:

```js
function sayAnimal() {
	var animal = 'dog'
  console.log(animal);
}

sayAnimal();
console.log(animal);

// dog
// undefined
```

Agora, a variável `animal` existe somente no escopo da função `sayAnimal()`, e pode ser chamada ou utilizada DENTRO dela. Por isso, o `console.log()` dentro da função realmente loga o valor dessa variável ao chamarmos a função. Porém, quando tentamos fazer o mesmo log ********FORA******** da função, o retorno já não é o correto.

Isso acontece porque a variável animal não está em escopo global, ou seja, não está visível para o JS fora daquela função. Ele só consegue enxergá-la dentro da função, por isso o `console.log()` dentro dela printa o valor correto e o log fora dela não.

```js
var animal;

function sayAnimal() {
	animal = 'dog'
  console.log(animal);
}

sayAnimal();
console.log(animal);

// dog
// dog
```

Agora, nesse exemplo, corrigimos o problema do escopo da variável ao inicializarmos ela fora do bloco da função. A variável animal está em escopo global, e pode ser acessada de qualquer lugar do código. Dentro da função, estamos apenas atribuindo um valor à uma variável já existente fora do escopo da função, nesse caso, a variável animal.