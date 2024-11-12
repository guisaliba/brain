
## Conversões

Conversões de tipos de valores no JavaScript acontecem frequentemente, e muitas vezes, por baixo dos panos sem sequer percebermos.

Dois tipos de valores diferentes não podem operar, ou seja, não irão funcionar como esperado sem que façamos a conversão de um ou outro para o mesmo tipo de dado antes.

### Exemplo:

``` js
const inputYear = "1991";
console.log(inputYear + 18);
```

 Essa operação iria retornar o valor 199118 em vez de retornar o esperado 2009, isso acontece porque uma _string_ e um _number_ são dois tipos de dados diferentes, e não irão operar junto numa adição que requer dois números.

Para convertermos algum valor em número, podemos simplesmente utilizar a função Number(valor).

### Exemplo:

``` js
const inputYear = "2000";
console.log(Number(inputYear));
```

Esse console iria retornar o número 1991 em vez da string 1991. E claro, podemos fazer o contrário, converter um número para uma string com a função String(valor).

### Exemplo:

``` js
const age = 42;
console.log(String(age));
```

O console vai retornar a string 42 em vez do número 42.

Conversões só podem ser feitas para uma _string_, para um _number_ ou para um _boolean_. Não podemos converter algo para _undefined_ ou _NaN_.

## Coerções

Coerções de tipos acontecem quando estamos lidando com dois valores diferentes na mesma operação automaticamente.

### Exemplo:

``` js
console.log('I am ' + 23 + ' years old');
// I am 23 years old
```

Aqui, o código converteu automaticamente o número 23 para uma string devido ao operador “+”. Por termos um valor não idêntico aos outros entre os operadores +, ele fez a conversão do _number_ para _string_ automaticamente.

E o inverso ocorre com o operador de menos (-).

### Exemplo:

```js
console.log('23' - '10' - 3);
// 10
```

Nesse caso o operador “-” converteu os valores _string_ para o valor _number_ automaticamente.