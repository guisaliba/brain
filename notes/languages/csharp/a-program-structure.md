Os principais conceitos em C# são **programas, namespaces, tipos, membros e assemblies.**

Os programas declaram tipos que contêm membros e podem ser organizados em namespaces.

**Classes, structs e interfaces** são exemplos de **tipos**.

**Campos, métodos, propriedades e eventos** são exemplos de **membros**.

Quando os programas em C# são compilados, eles são empacotados fisicamente em **assemblies**. Os assemblies normalmente têm a extensão de arquivo `.exe`  ou `.dll`, dependendo se eles implementam **aplicativos ****ou **bibliotecas**, respectivamente.

```csharp
namespace Acme.Collections;

public class Stack<T>
{
    Entry _top;

    public void Push(T data)
    {
        _top = new Entry(_top, data);
    }

    public T Pop()
    {
        if (_top == null)
        {
            throw new InvalidOperationException();
        }
        T result = _top.Data;
        _top = _top.Next;

        return result;
    }

    class Entry
    {
        public Entry Next { get; set; }
        public T Data { get; set; }

        public Entry(Entry next, T data)
        {
            Next = next;
            Data = data;
        }
    }
}
```

O nome completo da classe Stack é `Acme.Collections.Stack`. Essa classe contém vários membros:

-   Um campo chamado `_top`.
-   Dois métodos chamados `Push` e `Pop`.
-   Uma classe aninhada chamada `Entry`, que ainda contém três membros:
    -   Um campo chamado `Next`.
    -   Um campo chamada `Data`.
    -   Um construtor: `public Entry(Entry next, T data)`.

`Stack` é uma classe genérica. Ele tem um parâmetro de tipo, `T` que é substituído por um tipo concreto quando é utilizado. O exemplo dessa classe Stack é uma classe que define o comportamento de uma pilha (stack).

É possível declarar uma variável que se refira a uma instância dessa classe `Stack` para utilizá-la.

Os assemblies contêm código executável na forma de instruções de IL (Linguagem Intermediária) e informações simbólicas na forma de metadados. Antes de ser executado, o compilador do .NET (CLR) converte o código IL em um assembly em código específico da máquina.

Os tipos públicos e os membros contidos em um assembly específico são disponibilizados em um programa C# simplesmente fazendo referência a esse assembly ao compilar o programa.

Esse programa usa a classe `Acme.Collections.Stack` do assembly `acme.dll` por exemplo:

```csharp
class Example
{
    public static void Main()
    {
        var s = new Acme.Collections.Stack<int>();
        s.Push(1); // stack contains 1
        s.Push(10); // stack contains 1, 10
        s.Push(100); // stack contains 1, 10, 100
        Console.WriteLine(s.Pop()); // stack contains 1, 10
        Console.WriteLine(s.Pop()); // stack contains 1
        Console.WriteLine(s.Pop()); // stack is empty
    }
}
```

Para compilar este programa, você precisaria fazer referência **ao assembly que contém a classe de pilha definida no exemplo anterior, que pode ser um arquivo `.dll` ou .`exe`

#csharp #oop 
