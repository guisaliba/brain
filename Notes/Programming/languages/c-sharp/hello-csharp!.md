O programa "Hello, World!" é usado tradicionalmente para introduzir uma linguagem de programação. Este é um Hello World para C#:

```csharp
using System;

class Hello
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

O programa "Hello, World" começa com uma diretiva `using` que faz referência ao namespace `System`. Namespaces fornecem um meio hierárquico de organizar bibliotecas e programas em C#. Os namespaces contêm tipos e outros namespaces — por exemplo, o namespace `System`contém uma quantidade de tipos, como a classe `Console` referenciada no programa e diversos outros namespaces, como `IO`e `Collections`.

A diretiva `using`que faz referência a um determinado namespace permite o uso dos tipos que são membros desse namespace.

Devido à diretiva `using`, o programa pode usar `Console.WriteLine`como um atalho para `System.Console.WriteLine`.

```csharp
class Hello
{
	//
}
```

A classe `Hello` declarada pelo programa "Hello, World" tem um único membro, o método chamado `Main`. O método `Main` é declarado com o modificador `static`.

Por convenção e padrão, um método estático denominado `Main` serve como ponto de entrada de um programa C#. A saída do programa é produzida pelo método `WriteLine`da classe `Console`no namespace `System`. Essa classe é fornecida pelas bibliotecas de classe padrão, que, por padrão, são referenciadas automaticamente pelo compilador.

#csharp 