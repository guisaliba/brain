# div e span

“Div” são uma abreviação para division. Elas são elementos html para construir conteúdos, servem como se fossem caixas, que ajudam a agrupar e separar esses conteúdos.

Uma div é por padrão um elemento block-level. Em outras palavras, por padrão, divs irão ocupar todo o espaço daquela linha sem dividir com outros elementos.

Devido à esse comportamento, elas se empilham uma em cima da outra.

```html
<div>
	<p>
		i am inside a div!
	</p>
</div>
```

```css
div {  width: 490px;  background-color: red }
```

Aqui temos um parágrafo dentro de uma div. Esse parágrafo estará ocupando o espaço que a div tiver, ou seja, se determinarmos um certo tamanho e largura para essa div, o parágrafo deve caber ali dentro.

Já o span funciona de maneira diferente, por padrão, ele não é um elemento block-level. Ele não precisa ocupar todo o espaço daquela linha. Um span ocupa apenas o espaço que ele precisa ocupar.

```html
<div>
	<p>
		<span>
			Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet.
			<!--spans are not block-level elements like divs. -->
		</span>
  </p> 
</div>
```

```css
div {  width: 490px;  background-color: red;}span {    color: yellow;}
```

Nesse exemplo, a div continua se comportando como block-element, tomando o espaço de toda a linha por 490px.

Porém, o span dentro do parágrafo pode ter a cor amarela sem quebrar a linha ou criar outro espaço para ele próprio.