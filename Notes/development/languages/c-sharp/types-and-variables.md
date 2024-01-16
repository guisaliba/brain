Um **tipo** define a estrutura e o comportamento de qualquer dado em C#. A declaração de um tipo pode incluir seus membros, tipo base, interfaces implementadas e operações permitidas para esse tipo. Uma **variável** é um rótulo que se refere a uma instância de um tipo específico.

Há dois tipos em C#: **tipos de referência** e _**tipos de valor.**_ Variáveis de tipos de **valor** contêm diretamente seus dados. Variáveis de tipos de **referência** armazenam referências a seus dados, o último sendo conhecido como objetos.

Com tipos de referência, é possível que duas variáveis referenciem o mesmo objeto e, portanto, é possível que operações em uma variável afetem o objeto referenciado por outra variável.

Com tipos de valor, cada variável tem sua própria cópia dos dados e não é possível que operações em uma variável afetem a outra (exceto em variáveis de parâmetros `ref` e `out`).

Um **identificador** é um nome de variável. Um identificador é uma sequência de caracteres unicode sem nenhum espaço em branco.

Um identificador pode ser uma palavra reservada em C#, se for prefixado por `@`. Usar uma palavra reservada como identificador pode ser útil ao interagir com outros idiomas.

Os tipos de **valor** do C# são divididos em **tipos simples**, **tipos de enumeração**, _**tipos struct**_ e **tipos de valor anulável** e __tipos de valor de tupla_._** Os tipos de **referência** do C# são divididos em **tipos de classe**, **tipos de interface**, **tipos de matriz** e **tipos delegados**.

A estrutura de tópicos a seguir fornece uma visão geral do sistema de tipos do C#.

### Tipos de valor

**São armazenados diretamente na memória:**

-   Tipos simples
    -   Integral com sinal:: `sbyte`, `short`, `int`, `long`.
    -   Integral sem sinal:: `byte`, `ushort`, `uint`, `ulong`.
    -   Caracteres Unicode: `char`, que representa uma unidade de código UTF-16.
    -   Ponto flutuante binário de IEEE: `float`, `double`.
    -   Ponto flutuante decimal de alta precisão: `decimal`.
    -   Booliano: `bool`, que representa valores boolianos — valores que são `true` ou `false`.
-   Tipos enum
    -   Tipos definidos pelo usuário do formulário `enum E {...}`. Um tipo `enum` é um tipo distinto com constantes nomeadas. Cada tipo `enum` tem um tipo subjacente, que deve ser um dos oito tipos integrais. O conjunto de valores de um tipo `enum` é o mesmo que o conjunto de valores do tipo subjacente.
-   Tipos struct
    -   Tipos definidos pelo usuário do formulário `struct S {...}`.
-   Tipos de valor anuláveis
    -   Extensões de todos os outros tipos de valor com um valor `null`.
-   Tipos de valor de tupla
    -   Tipos definidos pelo usuário do formulário `(T1, T2, ...)`.

### Tipos de referência

**São armazenados na memória do heap, e o endereço de memória é armazenado na pilha.**

**Todos os tipos de referência são herdados da classe base `System.Object`.**

-   Tipos de class
    -   Classe base definitiva de todos os outros tipos: `object`.
    -   Cadeias de caracteres Unicode: `string`, que representa uma sequência de unidades de código UTF-16.
    -   Tipos definidos pelo usuário do formulário `class C {...}`.
-   Tipos de interface
    -   Tipos definidos pelo usuário do formulário `interface I {...}`.
-   Tipos de matriz
    -   Unidimensional, multidimensional e irregular. Por exemplo: `int[]`, `int[,]` e `int[][]`.
-   Tipos delegados
    -   Tipos definidos pelo usuário do formulário `delegate int D(...)`.
-   Array: são coleções de elementos do mesmo tipo, com tamanho fixo.

Tipos anuláveis não exigem uma definição separada. Para cada tipo não nulo `T` há um tipo anulável correspondente `T?`, que pode conter um valor adicional, `null`.

Por exemplo, `int?`é um tipo que pode conter qualquer inteiro de 32 bits ou o valor `null`e `string?`é um tipo que pode conter qualquer `string`ou o valor `null`.

#csharp #oop