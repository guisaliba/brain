Tipar variáveis é bem simples, como demonstrado no exemplo abaixo basta que você adicione `:tipo` depois de uma variável.

```tsx
let date: number
date = 3

let myName: string
myName = 'John Doe'

let isTrue: boolean
isTrue = false
```

Para começar, podemos usar o exemplo tradicional da soma que sem a tipagem do TypeScript aceitaria duas strings como valores e quando a função de soma fosse executada, concatenaria as strings obtendo um resultado inesperado:

```tsx
function sum(a: number, b: number){
	return (a + b)
}

sum(4,2)
// 6

sum("4","2")
// Argument of type 'string' is not assignable to parameter of type 'number'.
```

Nesse exemplo da soma, tipamos as variáveis **`a , b`** utilizando os `:` após as variáveis. Como cada uma delas recebeu uma tipagem do tipo `:number`, ambas só podem ser numbers dentro da função. Caso a função `sum()` seja chamada e as variáveis sejam strings `sum("4","2")` o TypeScript identificaria um erro e não deixaria o código ser compilado nem executado.

É possível também tiparmos funções, dando segurança no tipo de retorno daquela função:

```tsx
function resposta(): string {
  return 'Sim!';
}
```

Se colocássemos `return 4` por exemplo, ou qualquer outro valor que não fosse uma string, o TypeScript retornaria um erro, pois a função `resposta()` só pode retornar string (`: string`).