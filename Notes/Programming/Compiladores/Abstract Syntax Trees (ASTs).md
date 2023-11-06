### Como uma linguagem consegue reconhecer e saber exatamente o que um determinado método ou variável escrita em outra linguagem quer dizer no seu próprio vocabulário?

Isso é possível graças as **Abstracts Syntax Tree (AST)** ou Árvores de Sintaxe Abstratas.
As ASTs nada mais são que a representação de um determinado código em uma determinada linguagem na forma de uma estrutura de dados (uma árvore). Por serem uma estrutura de dados, elas podem ser representadas em diversos formatos, comumente representadas por um JSON.

No momento em que a conversão do código-fonte para uma AST ocorre, apenas o conteúdo estrutural do código é preservado, qualquer outra informação adicional é descartada. Isso significa que ao final, temos apenas uma árvore contendo as partes estruturais do código escrito naquela linguagem, dessa forma, temos a "base" da linguagem.

A partir dela é possível então implementar em outra linguagem, um agente ou entidade capaz de ler essa estrutura de dados e interpretar as informações ali presentes para seu próprio vocabulário, métodos e ações.

Nas ASTs, cada nó da árvore representa um **construct**, uma característica do código-fonte (da linguagem original) e nesses nós podemos encontrar métodos ou representações pertencentes àquele construct.

**Uma AST pode ser utilizada por um compilador ou por um interpretador, para traduzir (transpilar) o conteúdo estrutural do código fonte para uma outra linguagem.** Dessa forma, podemos compilar ou interpretar qualquer linguagem de programação para outra. 

[[Parsing and lexing]].