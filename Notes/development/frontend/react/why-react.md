## 1. O React é “composable”:

O conceito de composable significa componentizável, em outras palavras, o React é uma biblioteca JavaScript que permite escrever o código em componentes. Isso é, juntar pequenas peças (cada uma em seu propósito e tamanho) para obter o produto maior, a peça final.

E isso pode ser feito sem perdermos a essência do HTML, pois os componentes são nada mais nada menos que HTML sendo escrito em uma função ou classe JavaScript.

### Um “React component” (como são chamados os componentes em React) são escritos geralmente dessa forma:

```jsx
function MainContent() {
    return (
	    <h1>
		    I'm learning React!
	    </h1>
	    <p>
		   It is an awesome JavaScript library
	   </p>
		)
}
```

Assim, estamos separando nosso código em pequenos chunks para mais tarde juntarmos todos no nosso ReactDOM.render() que é o método responsável por de fato renderizar nosso código em tela.

```jsx
ReactDOM.render(
    <div>
        <Navbar />
        <MainContent />
	</div>,
	
	document.getElementById("root")
)
```

## 2. O React é declarativo:

E o que significa ser declarativo?

Significa escrever de forma declarativa, ou seja, exatamente oposta da forma imperativa de se programar. E o React trabalha de forma declarativa.

Quando escrevemos um código de forma imperativa, precisamos dizer literalmente tudo, passo a passo, de como o computador deve executar aquele código, ou no nosso caso, o browser (html).

Dessa forma, pra renderizar um simples elemento h1 no código JavaScript de forma imperativa, precisariamos escrever algo assim:

```jsx
const h1 = document.createElement("h1");
h1.textContent = "This is an imperative way to program";
h1.className = "header";
document.getElementById("root").append(h1);
```

Primeiro precisamos declarar uma const h1, então dizer o que ela faz, colocar um conteúdo nela, e só então linkar ela à nossa div root, com o método .append

Com o React, estamos programando de forma declarativa ou seja, ele se vira com as coisas que não estão explicitamente descritas e descobre o que ele tem que fazer com aquilo. Assim, o mesmo código escrito acima pode ser escrito assim com React:

```jsx
ReactDOM.render(
	<h1>This is a declarative way to program</h1>,
	document.getElementById("root")
)
```

Como estamos escrevendo nosso HTML no JavaScript, isso significa que podemos implementar toda a lógica pertencente da linguagem ao HTML, sem sequer sair do JavaScript. Assim, o React sabe o que fazer com nosso HTML e como renderizá-lo em tela mesmo estando no código JS.