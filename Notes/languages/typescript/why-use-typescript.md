## O TypeScript é um superset do JavaScript.
Um superset é basicamente adicionar novas features dentro da linguagem, nesse caso, adicionar novas features ao JavaScript.

## O que são essas features?
Basicamente, tipagem estática. O TypeScript oferece tipagem estática ao JS, que é uma linguagem de tipagem dinâmica.

## E o que é tipagem estática?
Tipagem estática é quando definimos os tipos das nossas variáveis, tipos de retorno etc. antes mesmo do código ser compilado para JS.

Escrever em TypeScript é adicionar essa tipagem estática ao código e ele mesmo compila esse código para JavaScript por baixo dos panos.

**O TypeScript permite adoção gradual (arquivos .ts com .js).**

## Então, o TS é linguagem ou não é?
Na verdade tanto faz, definir como linguagem ou superset não muda muita coisa. A Microsoft criadora do TypeScript o define como linguagem. Livre para interpretação.

## 1. O TypeScript evita resultados inesperados:
Como o JavaScript é dinâmico (podemos atribuir variáveis de um tipo ou de outro dentro do mesmo código) ele acaba retornando resultados nem sempre esperados.

**Exemplo:**

```tsx
function sum(a,b) {
	return a + b
}

sum(1 + 2)
// 3

sum(1, 2)
// 12
```

Nesse exemplo, as váriaveis a & b podem receber qualquer tipo (typeof), e a função que faz a soma a + b vai realizar essa soma também com qualquer tipo de valor.

Por isso, quando somamos 1 + 2 o resultado é 3.
E quando somamos “1” + “2” o resultado é 12 (concatenação de strings).
No TypeScript, esse tipo de problema não ocorreria.

## 2. O TypeScript avisa se você estiver fazendo algo de errado:

```tsx
console.log(4 / [])
// Error
```

Aqui nesse exemplo, o TypeScript avisaria como erro que não se pode dividir um **number (4**) por um **array.** Essa operação só poderia ser realizada com um number, bigint, etc.
## 3. O TS funciona como uma espécie de documentação inicial:

```tsx
type Platform = 'Windows' | 'Mac OS' | 'Linux'
type Feature = 'Single Player' | 'Co-op'

interface GameDetails {
    id: string
    title: string
    description: string
    platforms: Platform[]
    features: Feature[]
}
```

O exemplo acima nos diz nos detalhes do jogo que as plataformas aceitas são um array de plataformas `Platform[]` e nesse caso, anteriormente tipadas são três plataformas: Windows ou Mac OS ou Linux.

Isso é de muita utilidade para por exemplo, um novo desenvolvedor começar a trabalhar no jogo, já ter uma noção de quais são as plataformas aceitas pelo jogo, as features, etc.
## 4. Deixa sua IDE extremamente poderosa:

```tsx
let message: string

message.
// Todos os métodos da string message serão mostrados pela IDE.
```

## E as desvantagens do TS?
O TypeScript possuim sim algumas desvantagens:

1. Necessita ser compilado para JavaScript.
2. Aprendizado inicial dos tipos e boas práticas.
3. Os erros nem sempre são muito claros. Ou então são **ENORMES**!

Tirando isso, o TS é bem simples. Se você sabe JavaScript você vai saber TypeScript. **A diferença é que você vai escrever mais**.