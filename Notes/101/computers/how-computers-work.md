### Computadores podem ser explicados usando pura lógica:

Imagine um cenário de um circuito elétrico com dois interruptores (A e B). Esse circuito possui uma lâmpada, que será acesa uma vez que a corrente possa fluir por esses dois interruptores e chegar até ela. Esse é um simples exemplo em que estamos testando duas condições:

1.  **Primeira condição:** A primeira condição a ser testada nesse exemplo é se o interruptor A está fechado ou aberto. Faça essa pergunta: O interruptor A está fechado? Ou ele está aberto? Se o interruptor A estiver aberto, podemos concluir, por lógica, que a corrente não fluirá através dele, fazendo com que a lâmpada não possa ser acesa.
2.  **Segunda condição:** A segunda condição desse exemplo é a mesma que a primeira. O interruptor B está fechado? Ou está aberto? Se o interruptor B estiver aberto, concluimos também por lógica, que a corrente não fluirá por ele, fazendo a lâmpada permanecer apagada.

Como a condição para que a lâmpada seja acesa é a de que a corrente precisa fluir pelos dois interruptores, isso significa que ambos precisam estar fechados. Em outras palavras, estamos testando se A ou B estão fechados ou não.

Podemos chegar a uma conclusão de que, se A estiver fechado mas B não, a corrente não fluirá. O mesmo pode ser concluido se B estiver fechado mas A não, e também podemos inferir que se ambos não estiverem fechados, a corrente não fluirá também.

O único caso que atende a condição para a lâmpada ser acesa é se **A e B estiverem fechados.**

Se representássemos esse caso com uma tabela, usando **0** para o interruptor estar aberto e **1** para o interruptor está fechado, teríamos algo assim:

![[1.png]]

Quando ambos interruptores estão **fechados (1**), a corrente fluirá através deles e como resposta teremos a lâmpada acendida, que está sendo representada pelo **Output** de valor 1

Essa tabela é chamada de tabela da verdade. Como nesse exemplo o Output só pode ser 1 quando tanto A ****e**** B forem 1 também, chamamos esse operador lógico de ******&****** (ou AND).

**Agora,** imaginemos um circuito diferente com apenas um interruptor, que quando aberto faz a corrente passar pela lâmpada e ser acendida. E quando fechado, cria um caminho mais fácil para a corrente passar fazendo com que a lâmpada se apague.

O que acontece nesse exemplo é que estamos invertendo a lógica do exemplo anterior. Aqui, quando o interruptor possuir o valor de 1 (fechado), a lâmpada não acenderá e sim será apagada. Chamamos esse operador lógico de ****!**** (ou NOT).

![[2 2.png]]
#### Os interruptores dos computadores são nada menos que transistors.

Se usarmos o segundo exemplo novamente, mas dessa vez com um transistor no lugar de um interruptor, poderíamos recriá-lo dessa maneira:
![[3 2.png]]
Nesse primeiro momento, o “interruptor” está aberto, o que faz com que a corrente passe pelo caminho da lâmpada, o que faz com que ela ser acendida.

Porém, se colocássemos uma fonte de energia nesse transistor, a corrente encontraria através dele um caminho mais fácil para percorrer, passando por ele. Nesse momento, ele agiria como um interruptor fechado, fazendo com que a lâmpada se apague.

![[4 1.png]]
#cs #logic