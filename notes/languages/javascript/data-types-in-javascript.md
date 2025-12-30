---
id: "4e6bf149-a5d4-40d6-8a3a-eaea3c8409c7"
title: "Tipos de dados em JavaScript"
source: ""
aliases: ["Tipos de dados em JavaScript"]
---
Na linguagem JavaScript, todo valor é **ou um object, ou primitivo**. Quando o valor não é um object, então ele é primitivo. Por agora, falaremos dos tipos de dados primitivos da linguagem:

Ao todo, existem 7 tipos de dados primitivos em JavaScript:

1. Number: Qualquer número. -> let age = 23;
2. String: Sequência de caracteres, utilizada para texto. -> let firstName = "Jonas";
3. Boolean: Tipo de dado lógico, pode ser *true* ou *false*. -> let isEmpty = true;
4. Undefined: Valor dado a uma variável que ainda não teve um valor definido ("valor vazio"). -> let myName;
5. Null: Também significa "valor vazio", com uma pequena diferença.
6. Symbol (ES2015): Valor único que não pode ser mudado.
7. BigInt (ES2020): Númeors inteiros maiores que o tipo Number permite.

Se um valor não for de qualquer um desses tipos, então ele automaticamente é um valor do tipo **object**.

Um fator fundamental sobre tipos de dados em JavaScript é que essa é uma linguagem **dinamicamente tipada** ou de **tipagem dinâmica**, isso significa que não precisamos manualmente definir o tipo do valor guardado em uma variável. Isso é feito automaticamente pela linguagem uma vez que o valor é dado à ela.

``` js
let javascriptIsFun = true;
// O tipo do valor dessa variável é automaticamente definido como Boolean.
```
Além disso, é importante saber que: **o tipo de dado é de um valor, não de uma variável**. Variáveis apenas guardam valores de todos os tipos.

É comum que, ao longo do código surja alguma dúvida em relação ao tipo do valor de uma variável. Por exemplo, podemos confundir o valor "23" com 23, em que o primeiro é do tipo de dado String e o segundo é do tipo de dado Number. O JavaScript permite checarmos o tipo de um valor com um operador especial da linguagem chamado de **typeof**.

``` js
let myNumber = 23;
let myString = "23";

console.log(typeof myNumber);
```
Nesse exemplo, o console printaria "number" pois a variável myNumber guarda o valor 23, que é um valor do tipo number. O mesmo vale para a variável myString, quando colocada dentro do console.log(), o console printaria "string".

E, vamos dizer que queremos mudar o valor da variável myNumber, podemos fazer isso somente escrevendo o nome da variável e assignando um novo valor à ela, sem a necessidade de usar a palavra *let* novamente.

``` js
let myNumber = 23;
console.log(typeof myNumber);
myNumber = "23";
console.log(typeof myNumber);
```

Perceba que, ao mudarmos o valor da variável myNumber, acabamos por mudar também o tipo desse valor. O que era antes um number agora passou a ser uma string, e como JavaScript é uma linguagem dinamicamente tipada, ela permite que isso aconteça. Então, o primeiro console.log() printaria *number* e o segundo *string*, mesmo que ele esteja checando pelo tipo do valor da mesma variável.


