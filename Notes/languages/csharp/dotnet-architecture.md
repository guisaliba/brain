Programas C# são executados no .NET, um sistema de execução virtual chamado CLR (Common Language Runtime) e um conjunto de bibliotecas de classes. Ele é parecido com o Node.js, um Runtime Environment de JavaScript, apesar de não possuirem as mesmas finalidades.

O código-fonte escrito em C# é compilado em uma **IL (linguagem intermediária)**.

O código IL e os recursos, como bitmaps e cadeias de caracteres, são armazenados em um assembly, normalmente com uma extensão de _.dll_. Um assembly contém um manifesto que fornece informações sobre os tipos, a versão e a cultura.

Quando o programa C# é executado, o assembly é carregado no CLR. Em seguida, o CLR executará a compilação JIT (Just-In-Time) para converter o código de IL em instruções nativas da máquina. O CLR também oferece outros serviços relacionados à coleta automática de lixo, tratamento de exceções e gerenciamento de recursos.

O código que é executado pelo CLR é, às vezes, chamado de "**código gerenciado**".

O contrário disso seria o "c**ódigo não gerenciado**", aquele codigo que é compilado em linguagem de máquina nativa e visa uma plataforma específica.

Além dos serviços de tempo de execução, o .NET também inclui bibliotecas extensas. Essas bibliotecas dão suporte a muitas cargas de trabalho diferentes. Eles são organizados em namespaces que fornecem uma ampla variedade de funcionalidades úteis.

As bibliotecas incluem desde a entrada e a saída do arquivo até a manipulação de cadeia de caracteres até a análise de XML até estruturas de aplicativos Web para controles de Windows Forms. Um aplicativo típico em C# usa bastante a biblioteca de classes para lidar com tarefas comuns de "conexão".

#csharp 