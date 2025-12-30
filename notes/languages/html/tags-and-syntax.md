Toda tag precisa ser aberta e fechada. Algumas possuem uma tag de abertura e outra de fechamento, e algumas tags se abrem e se fecham sozinhas (self-closing tags).

**Uma tag de abertura e fechamento se parecem com isso:**

```html
<h1>Hello world!</h1>
```

Esse é um exemplo de **starting tag e closing tag**. Porém, existem também tags mais simples que chamamos de **self-closing tag**. Uma self-closing tag se parece com isso:

```html
<img src="cat.gif" alt="cute cat gif" />
```

Nesse exemplo, essa tag possui um **atributo**. Nesse caso o atributo “source” escrito por src, que diz ao código qual é a fonte daquela imagem.Também nessa mesma tag, temos outro atributo, o alt (texto alternativo). Atributos vão **SEMPRE** na tag de abertura (starting tag).

**Existem dois tipos de display dessas tags:**

- **Block (newline):** Uma tag de tipo **block** toma todo o **espaço** (ou o espaço determinado). Isso significa que ao inserir uma tag block, o browser criará um espaço completamente específico para ela ser mostrada em tela.

**Exemplos de tags display block: h1, h2, h3, p, div, etc.**

- **Inline:** Tags inline tomam apenas o espaço que ela precisa tomar, por causa disso, o browser não cria um novo espaço único para ela e sim a insere aonde ela deve ser inserida com o tamanho desejado da mesma.

💡 A tag **`<p></p>` (paragraph) só aceita elementos inline, ou seja, você nunca deve colocar outra tag `<p></p>` ou outro elemento com display block dentro de um paragraph.

