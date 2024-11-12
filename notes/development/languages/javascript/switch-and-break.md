O switch é uma forma de testar valores, testar condições com valores fixos.

Ele só atende números inteiros ou strings.

Diferente do if e do else, ele não é muito bom para testar intervalos.

O switch é útil quando se precisa testar dados pontuais.

Eles são mais limitados que os **if elses**, portanto sua utilidade também é limitada. A estrutura de um switch para testar números relacionados aos dias da semana por exemplo seria assim:

```js
var date = new Date(); // Função do JavaScript para datas
var dayWeek = date.getDay();

switch (dayWeek) {
    case 0:
        console.log('Domingo');
        break
    case 1:
        console.log('Segunda-feira');
        break
    case 2:
        console.log('Terça-feira');
        break
    case 3:
        console.log('Quarta-feira');
        break
    ...
}
```

Os breaks são obrigatórios depois de cada caso. Sem eles, o programa continuará verificando os próximos casos antes de pular para o próximo bloco do código.

Se esse código utilizasse o dia atual em que essa anotação foi escrita (Segunda-feira) ele executaria o case 1, e satisfeito, pararia e pularia para o próximo bloco de código.

#logic 