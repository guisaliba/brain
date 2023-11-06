Um [[ConsoleApp]] é uma simples aplicação do .NET que roda num console (como o próprio nome indica). Assim como todos os outros tipos de aplicações .NET, exceto Class Library, o ConsoleApp possui um ponto de saída que é justamente o arquivo ou código que rodará em sua execução.

Iremos entender passo a passo como funciona um ConsoleApp no .NET:

```bash
$ dotnet new console -o MyApp
```

Podemos criar uma aplicação .NET através da sua CLI com esse comando. Vamos entendê-lo:

-   **dotnet new →** cria um novo app .NET usando a CLI;
-   **console →** especifica ao .NET qual tipo de aplicação queremos criar aqui;
-   **************-o →************** flag que especifica em qual diretório o app será criado, se essa flag não for passada, o .NET sempre criará o projeto no diretório atual em que o terminal estiver rodando;
-   **MyApp →** o nome do diretório aonde o app será criado, esse nome acompanha a flag -o.

Agora, com a aplicação criada, podemos navegar até o diretório e abri-la no editor ou IDE:

```bash
$ cd MyApp
$ code .
```

Esse comando navegará até o diretório MyApp, aonde o projeto se encontra e abrí-lo no VSCode.

Dentro do VSCode, podemos ver duas pastas e dois arquivos. Antes de entendermos o que cada um representa, precisamos estar atentos à notificação que irá aparecer no canto da tela e selecionarmos a opção **Yes**. Essa notificação sempre aparecerá no VSCode ao abrir um projeto C#.

Ao aceitarmos a notificação, uma nova pasta nominada **.vscode** será adicionada ao nosso projeto.

Agora, no explorador, veremos algo parecido com isso:

![[Images/Csharp/Estrutura de um ConsoleApp em Csharp/1.png]]

*A pasta .vscode possui alguns arquivos de configuração JSON e não nos importa muito nesse momento, apesar de serem arquivos importantes para a execução do projeto.

O primeiro arquivo que iremos olhar e entender é o arquivo **MyApp.csproj**.

Um arquivo como esse com a extensão **.csproj** existirá em todo projeto .NET, ele é o arquivo que especifica as configurações do projeto ao .NET. Além disso, esse arquivo precisa sempre ter o mesmo nome do diretório do projeto.

Dentro dele podemos ver algo assim:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
```

O que está escrito dentro desse arquivos são códigos XML, e eles estão dizendo ao .NET as configurações e especificações do projeto, tais como a SDK do projeto, o arquivo de saída, o framework .NET do projeto, etc.

```xml
<OutputType>Exe</OutputType>
```

Essa linha por exemplo, especifica qual será o tipo de arquivo de saída do projeto. No caso de um projeto ConsoleApp (e de todos os projetos .NET exceto Class Library) o arquivo final que será executado é um arquivo ********.exe******** em uma máquina Windows ou ********.dll******** em máquinas Linux e Mac.

Já a linha seguinte especifica qual framework o .NET está utilizando nesse projeto, ou seja, em qual framework o projeto será executado. Isso é uma informação extremamente importante pois, o framework utilizado precisa sempre estar de acordo com o **************.NET Standard**************, que é a API que roda por baixo de todo o .NET para garantir que a aplicação rodará em diferentes versões do .NET.

```xml
<TargetFramework>net7.0</TargetFramework>
```

O arquivo **Program.cs** é o arquivo de saída do projeto. Em outras palavras, quando o .NET executar a aplicação ele irá procurar pelo arquivo de saída, pois ele é o arquivo que contém as instruções do que a aplicação irá fazer quando o .NET tentar subí-la.

Nesse projeto, entro do nosso ********************Program.cs******************** podemos ver algo assim:

```csharp
Console.WriteLine("Hello, World!");
```

Quando o .NET rodar a aplicação, a mensagem “Hello, World!” mostrará no console.

A pasta **bin** e a pasta **obj** possuem vários arquivos de configurações e debugging, tais como JSONs, cache, target e props. É recomendado não mexer nessas pastas, por possuírem arquivos de configurações já criados e configurados pelo próprio .NET quando criamos nosso app.

#csharp