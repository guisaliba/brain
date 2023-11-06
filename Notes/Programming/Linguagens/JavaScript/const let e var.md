## Diferenças entre var, let e const.

O grande problema em utilizar **var** para atribuir valor a uma variável é que você pode facilmente acabar alterando o valor dela ao decorrer do seu código, o que pode acabar gerando problemas num programa maior. Para evitar esse problema, podemos usar **le**t ou **const** para atribuirmos valor a uma variável qualquer.

Utilizando let, criamos uma espécie de variável de nome único, fazendo que dessa forma outra variável de mesmo nome não possa ser declarada em nenhuma parte do código, nunca alterando assim o seu valor por engano.

```js
let camper = "James";
let camper = "David";

// Cannot redeclare block-scoped variable 'camper'.
```

No exemplo acima, o console mostraria um erro (variável camper de escopo de bloco não pode ser redeclarada) pois o valor da variável foi atribuído duas vezes.

A função da variável *let* é exatamente essa: criar uma variável de escopo de bloco.

Se nesse mesmo exemplo, tivéssemos criado variáveis utilizando a keyword **var,** o JavaScript não reconheceria nenhum erro, uma vez que var permite que a mesma variável seja atribuída mais de uma vez.

```js
var camper = "James";
var camper = "David";

// nenhum erro no console.
```

Isso pode ser perigoso pois acabar redefinindo o valor de uma variável num código muito grande vai acabar causando muita dor de cabeça e erros não desejados.

Utilizando **const**, temos uma variável fixa declarada. O valor atribuido a uma const pode até ser alterado, porém ela não pode ser redeclarada. O JS a reconhece como uma variável read-only.

```js
const FAV_PET = "dog";
FAV_PET = "bird";
const FAV_PET = "cat";

// Cannot redeclare block-scoped variable 'FAV_PET'.
```

O console mostraria um erro pois a const FAV_PET foi redeclarada.

O caso de uso de uma const é quando queremos ter uma variável fixa, que nunca deve ser redeclarada nem ter seu valor mudado ao longo do nosso programa.

Além disso, o comportamento da **********const********** nos impede de declararmos ela e não darmos nenhum valor à ela, diferente do var e let. Se fizermos algo assim, obteriamos um erro:

```js
const myName;
// SyntaxError: const declarations must be initialized.
```

*OBS: É comum utilizar letras maiúsculas em todo o nome da variável para declarar consts.*

## Em resumo:

Na linguagem JavaScript, existem três maneiras de declarar uma variável: utilizando as palavras **let, const, var**. "let e const" são maneiras mais atuais de declarar variáveis, implementadas recentemente na linguagem.

De maneira básica, usamos let quando queremos declarar uma variável cujo valor pode ser alterado no futuro. Por exemplo, let age = 21; a variável "age" guarda um valor que, por se tratar do número da idade de alguém, pode ser alterado futuramente. Chamamos o evento de alterar o valor de uma variável de **mutação**. Além disso, outra característica fundamental da palavra *let* é que ao declarar uma variável com essa palavra, a variável recebe um escopo de bloco.

Ao contrário do let, utilizamos a palavra const quando pretendemos declarar variáveis cujos valores não serão alterados em nenhum momento, sendo valores **constantes** como o próprio nome da palavra sugere. Por exemplo, const independenceDay = "7 de Setembro"; e assim como variáveis declaradas com a palavra let, elas também possuem escopos de bloco.

Escopos de bloco em variáveis significa que, essas variáveis só podem ser acessadas dentro do bloco de código em que elas foram declaradas e nos filhos desse bloco.

Por fim, declarar variáveis com a palavra var significa criar variáveis com escopo de função. Essas variáveis podem ser acessadas dentro da função em que foram declaradas, e mesmo que tenham sido declaradas dentro de um bloco filho dessa função, elas ainda poderão ser acessadas fora desse bloco no restante do corpo da função.