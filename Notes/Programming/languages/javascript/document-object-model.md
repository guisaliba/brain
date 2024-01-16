---
# Mandatory fields
id: "f720e070-e920-4459-8ea7-cd695690baab"
# Optional fields
title: "Document Object Model (DOM)"
tags: ["calc", "display", "calc", "calc", "display", "calc"]
source: "https://javascript.info/dom-nodes"
source_title: ""
source_description: ""
source_image_url: ""
created_date: "13-09-2023"
modified_date: "13-09-2023"
---
O Document Object Model (DOM) é uma árvore que representa a estrutura de dados do HTML. Ele é gerado no momento em que o browser interpreta o conteúdo HTML que ele estiver recebendo. Nessa árvore, cada tag (ou elemento) HTML é  considerado um nó da árvore.

Consequentemente, cada tag dentro de outra (*nested tags*) são filhas da tag que a envolve. Por exemplo, um elemento <h1> dentro de uma <div> é filho dessa tag div. Cada nó da árvore (ou seja, cada elemento HTML) é considerado um **object**.

Qualquer elemento colocado fora da tag <body>, ou seja, depois do fechamento dessa tag (</body>) é automaticamente movido para dentro do body ao final dele. Esse comportamento ocorre porque o HTML obriga que todo o conteúdo esteja dentro do body.

Se o browser encontrar um HTML mal escrito, ele automaticamente o corrigirá. Por exemplo, a tag <html> é sempre a primeira do documento, se ela não estiver no topo, o browser a colocará lá quando gerar o DOM. Ou então, se a tag <body> não estiver sendo fechada corretamente, o browser colocará o fechamento </body> quando gerar a árvore.

Além de elementos HTML, existem outros tipos de nós presentes na árvore do DOM. Um exemplo são os comentários: 
```
<!-- #calc-display is children of #display-container which is children of #calc-container -->
        <input type="number" id="calc-display" disabled />
```
Para o DOM, tanto o comentário *#calc-display is children of #display-container which is children of #calc-container* quanto a tag <input> são nós da árvore. Comentários são chamados de *comment nodes*.

**Tudo em HTML, até mesmo comentários, viram parte do DOM.**

Os 4 tipos mais importantes de nós dessa árvore DOM são:
1. document – o ponto de entrada do DOM.
2. element nodes – tags HTML.
3. text nodes – texto (string).
4. comments – informações adicionais colocadas por alguém, não serão lidas, mas o JavaScript pode interpretá-las.
