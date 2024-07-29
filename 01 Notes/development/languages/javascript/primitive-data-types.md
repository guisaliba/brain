### Os tipos de dados primitivos do JavaScript.

1. **Number:** Utilizado para números decimais e inteiros, um número decimal é chamado de “floating point number” (25.1) e todo número inteiro escrito em JavaScript é também um floating point number. No caso de 25, o JavaScript o entende como 25.0
    
    ```js
let myNumber = 39;
    ```
    
2. **String:** Strings são sequências de caracteres, textos. Deve sempre estar entre aspas simples ou duplas (’" ou "") para que seja compreendido como string pelo JavaScript.
    
    ```js
let myName = "Guilherme";
    ```
    
3. **Boolean:** Tipo de dado lógico que assume apenas dois valores: true or false. Utilizado para cálculos lógicos, decisões lógicas e condições.
    
	```js
let hasDriverLicense = false;
	```
    
4. **Undefined:** Valor assumido por uma variável quando essa variável ainda não teve um valor definido. Podemos dizer que undefined significa valor vazio (**empty value**).
    
``` js
let randomVariable;
console.log("randomVariable");

// undefined
```
    
5. **Null:** O JavaScript enxerga o null como um objeto, ele é muito parecido e facilmente confundido com o undefined porém é a representação de “sem valor” ao invés de valor vazio. O próprio JS reconhece que ambos possuem o mesmo significado porém não são o mesmo tipo de dado.
    
 ```js
let testNull = null;

console.log("testNull"); // null
console.log(typeof testNull); // object
 ```
    
 ```js
 // Podemos provar a diferenca entre null e undefined
  
console.log(null === undefined); // false (not same type)
console.log(null == undefined); // true (empty value)
 ```
    
6. **Symbol** (ES2015): Valor único que não pode ser mudado.
    
7. **BigInt** (ES2020): Números inteiros muito grande que ultrapassam o limite que os Numbers conseguem armazenar.
    

### Variáveis possuem valores, mas não possuem tipos de dados.

São os valores quem possuem tipos de dados, as variáveis só existem para armazenar esses valores.