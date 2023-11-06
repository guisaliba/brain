# Enunciado
Fazer um interpretador ou compilador que rode em uma máquina com 2 núcleos e 2G de RAM.
Seu interpretador ou compilador deve trabalhar com uma AST em JSON. Essa AST será gerada pelos próprios desafiadores. Sua tarefa é receber o JSON dessa AST e em seguida, interpretar ou compilar o programa de acordo com as informações recebidas desse arquivo.

Simplificando:
1. Receber um JSON contendo uma AST.
2. Implementar um interpretador ou compilador que leia esse JSON.
3. Obter sucesso nessa leitura.

## Executando
O projeto **deve** conter um `Dockerfile` para que os desafiadores consigam executá-los. Para executar testes se seu interpretador ou compilador está funcionando corretamente é possível usar o arquivo `files/fib.rinha` ou `files/fib.json` sendo o segundo um arquivo já em formato JSON.

A linguagem terá que rodar com base em algum arquivo, que é o JSON da AST da rinha especificado [aqui](https://github.com/aripiprazole/rinha-de-compiler/blob/main/SPECS.md). O papel do interpretador ou compilador é rodar esse JSON com sucesso.

1. O arquivo terá que ser lido de `/var/rinha/source.rinha.json`
2. Poderá também ser lido de `/var/rinha/source.rinha`, se você quiser ler a AST na mão.

A linguagem do compilador ou do interpretador é qualquer linguagem de programação dinâmica, como JavaScript, Ruby, etc. ficando a próprio critério.

## Enviando
Para enviar sua participação será preciso fazer uma PR alterando o arquivo  [PARTICIPANTS.md](https://github.com/aripiprazole/rinha-de-compiler/blob/main/PARTICIPANTS.md) com uma nova linha contendo seu nome e seu repositório do interpretador ou compilador implementado. Seu repositório deve ter uma imagem na root.

O prazo para envio é até dia 23/09, depois disso não serão aceitas mais PRs.

## Especificação
A especificação completa da linguagem `rinha` pode ser encontrada [aqui](https://github.com/aripiprazole/rinha-de-compiler/blob/main/SPECS.md). Esse arquivo contém a especificação da AST da linguagem, com todos os tipos, termos, operadores, implementações, funções e expressões implementadas pela linguagem.

## Como fazer
Como especificado anteriormente, a implementação do interpretador ou compilador pode ser em qualquer linguagem dinâmica como JavaScript, TypeScript Kotlin, C# (qualquer linguagem de programação de alto nível) só que quer escrever em .rinha e gerar o JSON para testar o teu interpretador. Para isso tu pode fazer o seguinte: