Como é escrever em HTML? O que cada elemento escrito em tela quer nos dizer e o que representam? Para visualizar e responder melhor essa pergunta, vamos usar uma simples metáfora de um presente.

Imagine que temos um presente já pronto, embalado e enfeitado. Esse presente é composto por diversas partes e elementos que só formam o presente quando estão em conjunto:

### 1. O papel-presente

O papel-presente está em volta de todo o presente, porém, se falarmos ao computador que nosso presente está envolto por um papel presente, ele vai pensar que esse papel é infinito. O computador/browser não sabe definir o limite e tamanho das coisas.

Por isso, precisamos começar nosso papel-presente e terminá-lo.

```html
<wrapping-paper></wrapping-paper>
```

Representamos o papel através de **[tags HTML**.](https://www.notion.so/Tags-HTML-e-Sintaxe-a0d433b009504e1ca67db433d5a1b8ba?pvs=21) A primeira tag diz ao computador: aqui começa o papel-presente. A segunda tag diz aonde esse papel acaba.

### 2. A caixa

Dentro do papel, temos uma caixa. Essa caixa é nosso presente de fato, o papel está apenas envolvendo a caixa. Representamos a caixa da mesma forma que fizemos para representar o papel:

```html
<wrapping-paper>
	<box>
	</box>
</wrapping-paper>
```

É possível notar que a caixa está DENTRO do papel, pois ela faz parte do presente assim como o papel, que por sua vez está em volta de todo o presente e consequentemente da caixa também.

### 3. O brinquedo

E dentro dessa caixa, temos nosso brinquedo, que nesse exemplo iremos dizer que é um tremzinho. O brinquedo é composto por uma locomotiva e três vagões. Dentro de cada um desses vagões teremos algumas pessoas (bonequinhos).

```html
<box>
	<train>
		<locomotive>
			<car>
				<people>
			</car>
			<car>
				<people>
			</car>
			<car>
				<people>
			</car>
		</locomotive>
	</train>
</box>
```

**E assim seria nosso presente se ele fosse um código HTML:**

```html
<wrapping-paper>
	<box>
		<train>
			<locomotive>
				<car>
					<people>
				</car>
				<car>
					<people>
				</car>
				<car>
					<people>
				</car>
			</locomotive>
		</train>
	</box>
</wrapping-paper>
```

É claro que, essas tags não existem no HTML, elas são apenas representações analógicas de como é a estrutura do HTML. Existem muitas tags HTML, e cada uma possui seu próprio propósito.