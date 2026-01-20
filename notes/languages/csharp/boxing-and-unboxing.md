O sistema de tipos do C# é unificado, de modo que um valor de qualquer tipo pode ser tratado como um `object`. Cada tipo no C#, direta ou indiretamente, deriva do tipo de classe `object`, e `object` é a classe base definitiva de todos os tipos. Os valores de tipos de referência são tratados como objetos simplesmente exibindo os valores como tipo `object`. Os valores de tipos de valor são tratados como objetos, executando _conversão boxing_ e _operações de conversão unboxing_. No exemplo a seguir, um valor `int` é convertido em `object` e volta novamente ao `int`.

```csharp
int i = 123;
object o = i;    // Boxing
int j = (int)o;  // Unboxing

```

Quando um valor de um tipo de valor é atribuído a uma referência `object`, uma "caixa" é alocada para conter o valor. Essa caixa é uma instância de um tipo de referência e o valor é copiado nessa caixa. Por outro lado, quando uma referência `object` é lançada em um tipo de valor, `object` é feita uma verificação de que o referenciado é uma caixa do tipo de valor correto. Se a verificação for bem-sucedida, o valor na caixa será copiado para o tipo de valor.

#csharp #oop 