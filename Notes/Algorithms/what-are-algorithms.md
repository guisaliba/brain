Algoritmos são um conjunto de instruções ou regras que são seguidas para realizar uma tarefa ou resolver um problema. São fundamentais para a computação, pois possibilitam que computadores executem operações complexas de maneira eficiente.

Os algoritmos são usados na computação para realizar tarefas específicas, como busca e classificação de dados. Eles também são usados para ajudar a executar as instruções necessárias para executar um programa.

Em computação, um algoritmo é uma sequência de etapas a serem tomadas a partir de um **Input,** para que se obtenha um **Output**. Definimos **Input** como **ENTRADA** e **Output** como **SAÍDA**.

Mas isso não significa que para cada Input exista somente um algoritmo que leve à um Output. E nem que existe somente um Output para cada Input.

Algoritmos são desenvolvidos para qualquer tipo de problema, e tem como função resolver o problema para o qual ele foi desenvolvido, mesmo que esse problema possa variar inúmeras vezes.

Em resumo:
-   Um algoritmo é uma função, que dado um Input aponta para um Output. Esperamos que esse Output seja uma resposta correta para o problema.
-   Para provar que a resposta de um algoritmo está correta, muito provavelmente utilizamos loops, recursões e condições. Chamamos isso de **PROVA POR INDUÇÃO**.
-   Algoritmos devem sempre ser eficientes, e medimos a eficiência de um algoritmo não pelo tempo que ele gasta para ser executado mas sim pela quantidade de operações que ele precisa performar para solucionar o problema.

Um exemplo de algoritmo capaz de solucionar um problema aleatório é o algoritmo de busca binária. Ele é usado para localizar um elemento específico em um conjunto de dados organizados. O algoritmo funciona dividindo a lista ao meio, comparando o elemento de meio com o elemento alvo e, em seguida, decide se o elemento alvo está no primeiro ou segundo conjunto de dados.

O processo se repete até que o elemento alvo seja encontrado.

Uma representação desse algoritmo em JavaScript poderia ser assim:

```jsx
function binarySearch(array, target) {
  let left = 0;
  let right = array.length - 1;

  while (left <= right) {
    let middle = Math.floor((left + right) / 2);
    let value = array[middle];

    if (value === target) {
      return middle;
    } else if (value < target) {
      left = middle + 1;
    } else {
      right = middle - 1;
    }
  }

  return -1;
}
```

A função `binarySearch` é o algoritmo de busca binária em si.

As variáveis `left` e `right` são usadas para definir os limites do intervalo de busca. `left` começa em 0 pois é a primeira posição do array, o `index 0`, comumente chamado de posição inicial.A variável `right` é definida como o último índice do array, ou seja, `array.length - 1`, pois o índice começa em 0. Como o índice começa em 0, o último índice é `array.length - 1`.

Num array de 6 números (1 a 6) por exemplo, o primeiro índice seria o 0, que teria como valor correspondente o número 1. O último indíce seria o 5, que teria como valor o número 6.

O `while` loop é usado para percorrer o intervalo até que o elemento alvo seja encontrado ou até que não haja mais elementos para serem verificados.

O `middle` é usado para definir a posição da metade do intervalo.

A variável `value` é usada para armazenar o valor da posição atual do intervalo.

Se o valor for igual ao elemento alvo, o algoritmo retorna o índice do elemento alvo. Se o valor for menor que o elemento alvo, o algoritmo avança para a próxima metade do intervalo.

Se o valor for maior do que o elemento alvo, o algoritmo retrocede para a metade anterior do intervalo. Se o elemento não for encontrado, o algoritmo retorna -1.

#alg 