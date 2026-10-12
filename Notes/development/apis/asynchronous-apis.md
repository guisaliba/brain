# subject: [[api]]
# topics: #web-development #backend
---
Uma API síncrona é aquela API em que cada uma das operações enviadas pelo cliente ao servidor é completada em ordem, antes que a próxima operação seja executada.

### Exemplo:

```js
console.log('First');
console.log('Second');

// First
// Second
```

O oposto disso seria uma API assíncrona. Uma API assíncrona é aquela em que a API fará uma operação e retornará seu valor imediatamente (antes que a operação seja completa). Uma vez que a operação termina, a API usa um mecanismo para realizar operações adicionais.

### Exemplo:

```js
setTimeout(() => {
      console.log('First');
    }, 300);
console.log('Second');

// Second
// First
```

Nesse exemplo, o console printaria “Second” e depois “First”, isso porque mesmo que a operação que printa a palavra “First” seja chamada primeiro, ela leva um tempo (300ms) até ser concluída.

Utilizar APIs assíncronas no Node é essencial. O Node é **single-threaded event-driven.**

“Single threaded” significa que todas as requisições para o servidor ocorrem em uma mesma thread.

Uma das maneiras de fazer sua API notificar ao app que a operação terminou é registrando uma callback function, que como seu próprio nome diz, é uma função que será chamada uma vez que a operação termine.